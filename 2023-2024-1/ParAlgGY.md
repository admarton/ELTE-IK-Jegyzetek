# Párhuzamos algoritmusok és adatszerkezetek

# 1.GY

Párhuzamos adatszerkezetek lesznek a gyakon
Van több processzorom
- Distributed - mindenki csinálja a saját dolgát és a végén egyeztetnek
- Párhuzamos - egy közös memórián dolgoznak - ez nehezebb
	- Hogy oldjuk meg az írás helyességét
	- Olvasás általában könnyebb

Egyre több nyelvi könyvtárban van ilyen adatszerkezetre implementáció, de tudni kell, hogy melyiket kell használni és ha nincs akkor meg tudjuk írni.

Burcsi Péter - Tegeződünk

## Jegyszerzés

- Egy jegy van
- Beadandó
- A nyelvre nincs meghatározás
- Adatszerkezet implementáció, vagy valami amin dolgozik
- Január végéig lehet megírni

## Láncolt lista

- Sávszélesség növelése
- Helyes viselkedés megőrzése
	- Kérdés hogy mi a helyes
- Versengés az amikor egyszerre módosítják
- Zárak
	- Lezár, beír, felold
	- Ez biztos, de elveszi a párhuzamosítás lényegét
- Meglepő dolgok is párhuzamosíthatók - pl verem
- Alap trükk
	- Ha különböző helyen dolgozik két szál akkor nem kell közbe avatkozni

### Coarse-Grain Synchronization

- Minden metódus lezár és kölcsönös kizárás van
- Lehet hogy lassabb lesz

### Fine-Grain Sync

- Nem egy nagy lock egy memóriarészre
- Az objektum külön részeire külön zár 
- Tudnak egyszerre dolgozni külön részeken

### Optimistic Sync

- Olvasás - pl bent van-e az elem
	- Lehet többen egyszerre
- Írás - pl beszúrás és törlés
	- Ezek konfliktust okozhatnak
- Keresés lock nélkül és a helyre beszúrni már lock-olt
	- De lehet hogy közben valaki módosít

### Lazy Sync

- Takarítási és adminisztratív munkákat elhalasztunk
- Logikai és fizikai törlés elválasztása

### Lock-Free Sync

- Zárak nélküli működés
- Hardver adja a compare-and-set műveletet
	- Atomi típusokon
	- Feltétel és helyes ág utasítása egyben történik
- Komplex és néha lehet rosszabb eredmény

### List-Based set

#### Node
- T item
- int key
- Node next

#### Szabályok

- Eleje és vége egy-egy kamu node
- Az elemeke kulcs szerint növekvőek
- Invariánst tartja
	- add, remove, contains
- **Linearizációs pont** van egy trükkös lépés
	- Ez a legfontosabb lépése egy folyamatnak
- Mellékhatásoktól óvakodni kell

Lock spórlás
- Beszúrásnál kétszer is berakom ha egyszerre csinálják
	- De ilyenkor ki kell törölni mindkettőt
- Valahol meg kell fizetni az árat

#### Course Grain Lock

- Lezárom az egész listát és dolgozom
- A többiek addig várnak
- Nem hatékony
- De általában megvalósítható
#### Fine Grain

- Node-okat lehet zárolni
	- Párosával kell zárolni
- Csak akkor kell várni ha két zárat nem tudom megkapni
- Törlés linearizációs pontja amikor az előző node mutatóját átrakom a következőre
	- Ami előtte és utána volt nem olyan fontos
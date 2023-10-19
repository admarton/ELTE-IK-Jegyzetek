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

# 3.GY

## Verem
- Push, Pop
- FILO

### Push
- Létrehozás, beállítás és CompareAndSet a befűzés

### Pop
- Egy pointer átállítása a szinkronizációs pont
- Azt kell csak egy szálnak tudni
- ComapreAndSet

### Lock Free
- Nincs lock-olás
- De a CompareAndSet hardver igényes
- Egy pointer-t akar állítani mindenki
	- Nincsen sok aszinkronitás
	- Egyszerre csak egy ember tud berakni vagy kivenni

### GC nélkül ABA
- Sok node-ot kell létrehozni és törölni
- Újra lehet használni a node-okat
	- Node pool
- ABA probléma
	- A-t berakom, kiveszem, berakom a B-t, kiveszem és berakom az A-t
	- Pointer megmarad, de a tartalma megváltozik
		- Zavart okozhat
	- Időbélyegzővel lehet ezt elkerülni ezt az ütközést

## Elimination-Backoff Stack / Kihátráló-Várakozó Verem
- Exponential-backoff
	- 20-an írnák ugyanazt, egynek sikerül, de ha mindenki újrapróbálja akkor megint nagy terhelés
		- Ezért lehet kihátrálni - kicsit várni és utána próbálkozni
			- Véletlenszerű időt várni
- Valaki berakna - valaki kivenne
	- A stack nem változik
	- Tehát egyből átadhatnák egymásnak a node-ot
- Plusz párosítási tömb a verem mellett
- Ha nem tud a verembe rakni, akkor az Elimination array-be rakja
	- Aki ki akar venni, akkor a párosítási tömbből szedi ki, ha nincs ott semmi akkor vesz csak a veremből
- Kérdések:
	- Mekkora legyen a tömb?
		- Ha kicsi akkor ott is versengés
		- Ha nagy akkor kevés találat
		- Ha gyakran nem tudok berakni a verembe, akkor nagyobb tömb kell mert nagy a versengés
- Most már nem egy ponton, hanem egy tömbön versengünk

Ne adjuk fel a párhuzamosítást, több dolgot lehet párhuzamosítani mint gondolnánk...

# EA - 2023.10.18

## Osztott számláló - Shared counter

Feladat pool, szálak amik dolgoznak, kiveszik az aktuális feladatokat és megcsinálják.  
Ezek sorszámot húzhatnak.
A feladatokat el kell osztani minél optimálisabban.

### Balancer

2-2 - Bemeneti huzalok és kimeneti huzalok.  
A bemeneten jön a feladat és a kiegyensúlyozó elosztja a kimenti huzalok között.  

### Smoothing Network

2 hatvány huzal.  
Párosával kötjük a szálakat. 

```
--#-----#--#--
  #     #  #
--#--#-----#--
     #  #
--#--#-----#--
  #     #  #
--#-----#--#--
```

## Counting Network

- Kicsi a versengés
	- 2-2 szál van egy balancer-ben
- Magas átviteli sebesség
- Bitonic\[k\] nem linearizálható
	- Később jövő feladat lehet, hogy hamarabb végig megy
	- Ütemező melyik balancer-t futtatja
- Bitonic\[2k\]
	- Két Bitonic\[k\] és ezekre egy Merger\[2k\]
		- Felváltva vannak bekötve
	- Merger\[2k\]
		- Fent is lent is kiegyensúlyozott, de egymáshoz képest nem
		- Ezt oldja fel
		- Két Merger\[k\]-ból áll
		- Kimenetnél felváltva jön a fentiből meg a lentiből
- Garantálja a kimenet egyenlőségét
- log^2

### Rendező hálózatok

Hasonló elv alapján lehet rendező hálózatot csinálni.  
Balancer helyett két szám összehasonlítása és a kimenetnél jó sorrendben adja ki.  
Ugyan az a hálózat rendezetten adja ki az eredményt.

```
2 rendezés - 4 összerendezése \
2 rendezés /                   \
2 rendezés \                   /- 8 összerendezése
2 rendezés - 4 összerendezése /
```

n * log(n) lépés lesz mindig, legjobb, legrosszabb és átlagos esetben is.  
Ha van n processzorom n elemhez akkor log(n) lesz a rendezési idő.  

### Teljesítmény

Akkor éri meg leginkább amikor telített.  
Ha alul telített, akkor nincs kihasználva teljesen.  
Ha túl van terhelve, akkor versengések vannak a balancer-ekben, ez lassít.

### Lehet számolni is

Nagyon sok processzor akar hozzáadni egy értékhez.
Nagyon sok szálnál a lock nem elég hatékony.
De csak -1 vagy +1 lehet. **Combining Tree** tud több számot összeadni.  
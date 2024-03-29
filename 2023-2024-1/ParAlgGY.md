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

# 10.25 GYAK

## Beadandó

- Órai adatszerkezet
- Saját probléma
- Kapott probléma

## Kombináló fa

- Előző órán volt Bitonic
	- Csak számolni tud
- Combining tree tud összeadni, egynél nagyobb számmal növelni
- Bináris fában vannak a szálak és a gyökérben vannak az eredmények
- Két szál a közös pontjukon egyesítik az eredményeiket, majd ez feljebb gyűrűzik a fában.
- Az ördög a részletekben rejlik
	- Mi van ha nem egyszerre érnek oda a szálak?
		- Aki előbb odaér, az vár
		- Párhuzamos várakozás, multi-phase
		- Csúcs státusz: 
			- IDLE - vár
			- FIRST - első lett
			- SECOND - második lett
			- DONE - feljutott a szülőben
			- ROOT - gyökér lett
		- Ezeket a státuszokat is szinkronizálni kell
		- Az első feljebb is néz és ott is eldönti, hogy első lesz-e
			- Ez lesz a párhuzamos várakozás
		- Második szál lock-olja a node-ot és beírja az értékét
			- Az első szál is beírja és a közös értéket viszi tovább
		- A fában visszafelé is jelezni kell mindenkinek, hogy mi történt
- Kellően nagy de nem túl nagy terhelésnél log(n) időben feljutnak az eredmények
- Balszerencsés esetben mindenki zár a n * log(n) lesz
- RMW típusú műveletek közül sokra tud működni

## Queue

- enq(x), y = deq()
- A két végén dolgoznak
- Ha csak egy berak és egy kivesz, akkor jól párhuzamosítható

### Bounded Queue

- Láncolt lista szerű megoldás
- Számláló ami nézi a sor hosszát
- A számláló használata indokolhatja a combining tree használatát

### Lock menetes sor

- Compare And Set
- Időbélyegzők az ABA problémához

# GYAK - 11.08

Halmaz ábrázolások
Konkurens halmazok
- Fák, Piros-fekete, AVL
- A kiegyensúlyozás globális módosítás, emiatt le kell zárni nagy részt, ami párhuzamosan nem jó
- Nem determinisztikus megoldások

## Probabilisztikus adatszerkezetek - Skip List

- Várható értékben logaritmikus
- Fa szerű
- Láncolt lista, rövidítésekkel
- Pointer-eknek szintjei
	- Magasabb szint messzebb mutat
	- Első szint a következő node-ra
	- Várhatóan a következő szinten kétszer akkora ugrás
- Log N magas az első node
- Nem egzakt, szimmetrikus rendszer, inkább véletlen szerű
- Node magassága véletlen, de nem egyenletes, nagyon magas nem jó
- Beszúrás
	- Megkeressük
	- Elkérjük a lock-okat
		- Mindent ami majd oda mutat
	- Befűzzük
	- Feloldjuk a zárakat
	- Az összes link beállítása a linearizációs pont
- Törlés
	- Keresni az összes oda mutatót
	- Bitben jelöljük, hogy törölt
	- Lock-oljuk az oda mutatókat
	- Átállítjuk a link-eket
	- Feloldjuk a zárakat
	- A bit beállítása a linearizációs pont
- Keresés
	- Akkor van bent ha 
		- Nincs törlésre jelölve
		- És teljesen beszúrt bit is be van jelölve
- Optimista, lusta, finomszemcsés
- Keresés, beszúrás, törlés logaritmikus lehet

# GYAK 11.15

## Beadandó ötletek

### Logikai játék

- n×m kocka az asztalon
- Mindegyiken van valami -> közösen kirajzolódik egy ábra
- Összekeverték
	- Egy sor vagy egy oszlop forgatva van 90 fokkal a tengelye körül
- Feladat
	- Összekevert állapotból jussunk egy kirakott állapotba
	- Minimális lépésszámmal
- Egy kocka forgatása
	- sor_i -> oszlop_j -> sor_i^-1 -> oszlop_j^-1
- Szélességi keresés
	- Párhuzamosítani
	- Gráf az egyes állapotai a játéknak
	- Élek a lépések
- Óriási a gráf
	- Nehéz eltárolni

### Burrows Wheeler trafó

- String algoritmus
- Tömörítésre is használják
- Egy szó egy hosszú érték sorozat
	- Ez később jól tömöríthető
	- Elég csak a jel és a darabszám a tömör verzióban
- String összes ciklikus eltolása -> rendezés -> utolsó oszlop lesz az eredmény
- BANANA$ -> BNN$AAA

# GYAK - 11.29

-  Nem mindig ragaszkodunk a linearizálhatósághoz
- De lehet hogy, vannak fázisok amikor meg kell állni

## Barrier Sync

- Sorompóknál megállunk
- Pl.:
	- GPU magok a kép különböző részeit render-elik, de be kell várniuk egymást, hogy egységes képet adjanak ki
	- Streaming, buffer-ben tudunk várni kieső dolgokra
- Phase
- Ne csináljuk túl hamar, de ne is szabadítsuk fel az erőforrásokat túl hamar
- Barrier - nem mehetünk tovább amíg nem végez mindenki
	- A fázison belül nem számít a sorrend, de a fázisok szigorúan egymás után vannak
- Nagy numerikus számolásokban is használják
- Duálisa a mutex-nek
	- Nem az, hogy más ne csinálja amit én
	- Hanem az, hogy mindenki azt csinálja mint én
- Parallel prefix
	- [a,b,c,d] -> [a,a+b,a+b+c,a+b+c+d]
	- Minden elemre egy szál
	- Hozzáadják a számuk a következőhöz (1,2,4,8,...)
	- log_2 N körben lehet megcsinálni
	- De addig nem lehet a következő körre menni amíg egy kör be nem fejeződött
- Barrier megvalósítás
	- Ha egy változó amit mindenki ír
		- Az minden cache-be be lesz másolva és minding szinkronizálni kell
		- Ez drága
	- `AtomicInteger` a fenti okokból nem jó
	- **Combining Tree** Barrier
		- Két két szál kell csak veszekedjen
		- Bottleneck szétosztása több helyre, ha ez volt a baj akkor segíthet
	- **Tournament Tree** Barrier
		- Ha csak egy bitet kell állítani, akkor statikusan el lehet dönteni dolgokat
	- **Dissemination** Barrier
	- Static binary tree a legjobb ha előre tudjuk az architektúrát

# Adatbázisok 2 EA - 2021.09.07

inf.elte.hu/

## Ismétlés
1. Adatbázis-kezelő rendszerek - Fontos
2. A relációs adatmodell - Fontos
3. Az SQL nyelv részei
4. Adatmodellezés

## Adatbázis kezelés
- Háttértáron rögzített nagy mennyiségű adat kezelése
- Adatmodell támogatás
- Adatbázis kezelő nyelvek
- Több felhasználó kezelése
- Tranzakció-kezelés *
- Helyreállíthatóság *
- Ügyfél-kiszolgáló felépítés
- Adatvédelem, adatbiztonság

## Adatmodellek
- Hálós, hierarchikus adatmodell (apa-fiú kapcsolat gráfja)
- Relációs adatmodell (tábla szerű kezelés)
- Objektum-orientált adatmodell (háttérben relációk is lehetnek)
- Logikai modell (tények és szabályok, tény + szabály -> új tény)
- Félig strukturált (XML, gráfos)

## Adatbázis-kezelő nyelvek
- DDL - adatdefiniáló nyelv (sémák...)
- DML - Adatkezelő nyelv (beszúrás, törlés,...)
- QL  - lekérdező nyelv
    - Deklaratív (SQL, kalkulus)
    - Procedurális (relációs algebra)
- PL/SQL - programozási szerkezetek + SQL
- Programozási nyelv beágyazás
- 4GL nyelvek

## Több felhasználó
- Felhasználói csoportok
- DBA - ab rendszergazda
- Jogosultságok (írás, olvasás, jogok továbbadása, visszavonása)
- Jogok tárolása is táblákban (lekérdezhető)

## Tranzakció-kezelés
- **Tranzakció**: adatkezelő műveletekből álló sorozat
- **Cél**: tranzakció párhuzamos végrehajtása
    - Műveleteket össze kell fésülni
    - Egyik fél se várakozzon
    - Az eredménynek olyannak kell lennie mintha sorosan lenne végrehajtva
- Tranzakció kezelő biztosítja:
    - Atomosság (egységben lefut vagy sem, ne maradjon félállapotban) Atomiciti
    - Következetesség (nem rontja el az adatbázist) Consistenci
    - Elkülönítés (mintha egyedül kezelné az AB-t) 
    - Tartósság (commit után megmarad az állapot, hiba esetén is)

### Zárolások (Lock, Unlock)
Egymásra várnak a tranzakciók.

### Kétfázisú protokoll

### Tranzakció érvényesítés

### Ütemező
Végrahajtás sorrendjét adja meg.

### Szerializálhatóság
Ekvivalens tranzakciók egymás utáni végrehajtása.

## Helyreállíthatóság
- Szoftver vagy hardver hiba esetén utolsó jó pont visszaállítása
- Rendszeres mentések
    - Statikus adatb (nem gyakori)
    - Dinam (gyakori)

## Ügyf. - Kisz.
- **Kiszolgáló**:
    - Nagy tárhely, gyors
    - Optimalizált párhuzamos végrehajtás
- **Ügyfél**:
    - Formázás
    - Kérés küldése

## Adatvédelem
- Jogok kezelése (grant, revoke)
- Nézettáblákra is
- Titkosítani lehet az adatokat vagy a hálózati kapcsolatot

## AB-kezelő felépítése
- Lekérdezés feldolgozó
    - Szintaktika ellenőrzés
    - Táblák léteznek
    - Jogok ellenőrzése
    - Lek. opt. átértelmezése
    - Végrehajtási tervek készítése
    - Legjobb költségű kiválasztása
- Tranzakció-kezelő
    - Párhuzamos végrahajtást biztosít
    - (ACID)
- Tárkezelő
    - memóriába töltés
    - előre létrehozott indexek, nézettáblák,...
    - bonyolultabb lekérdezések gyorsítása

## Adatb-kezelő felépítése
```
Alkalmazás  Lekérdezés              Sémaleírás
        \       /                       |
    Lekérdezés-feldolg.             Sémafordító
                    \               /
                Adatb-kezelő motor
                        |
                Állománykezelő
```
## Szintek
- Sémák és előfordulások
- Fizikai, logikai, alkalmazások
  
- Fizikai adatfüggetlenség
    - A réteg módosítása ne látszódjon a felsőbb rétegekben

- Logikai függetlenség
    - Logikai bővítésnél az alkalmazásokat nem kell újraírni

## Relációs adatmodell
### Edgar Frank Codd 12 szabálya
1. Egységes megjelenésű információ - táblázatokban
2. Garantált lokalizálhatóság szabálya - adatmodellnek megfelelően kell hivatkozni az adatra, Tábla,Sor,Oszlop egyértelműen meghatároz
3. A NULL értékek egységes kezelése - típusfüggetlen
4. A relációs modell alapján aktív online katalógust kell üzemben tartani - rendszertáblák is megvannak, SQL-el olvashatóak
5. A teljes körű "adatnyelv" szabálya - interaktív, appba építve, kül. a lekérd. és az adatmódosító műv., lehessen tranzakció
6. A nézet frissítésének szabálya - nézettáblák használata, automatikus frissítés
7. Magas szintű beszúrás, törlés, módosítás
8. Fizikai adatfüggetlenség
9. Logikai adatfüggetlenség
10. Jóság (integritás) függetlensége - constraintek definiálása, ellenőrzése
11. Elosztástól való függetlenség - alkalmazói szinten nem látszik, hogy elosztott az adatbázis, redundancia
12. Megkerülhetetlenség szabálya - ne hessen közvetlenől belenyúlni, csak a kezelővel lehessen módosítani

## Relációs adatmodell
- Relációséma: R(A1,A2,...,An)
    - R - relációnév
    - Ai - attr.-, tul.-, oszlop név
    - Dom(Ai) - lehetséges értékek halmaza
**!!??????????????????!!**

- Jelölések:
    - t ∈ r esetén t sor (angolul: tuple - n-es)
    **!!??????????????????!!**

## SQL lekérdezés módosítása
Structured Query Language  
Összetett lekérdezés felbontása, és külön optimalizálás.
- Egyszerű SQL
    - Kiválasztás
    - Több tábla
    - Halmazművelet
    - Átnevezés
    - 

## Relalg műveletek
1. UNIÓ, R ⋃ S, R,S azonos sáma, sorok halmaza
2. KÜLÖNBSÉG, R - S,  
3. DIREKT SZORZÁS, R × S, két tábla sémája nem egyezhet meg, átneveződik, nincs kétszer ugyanaz az oszlop
4. PROJEKCIÓ, SELECT, Πₐ(R), SELECT a FROM R
5. KIVÁLASZTÁSOK, SZŰRÉS, oszlop összehasonlítása, σₕ(R), SELECT * FROM R WHERE h  
    - σ_A∧B(R) ⩳ σ_A(σ_B(R))
    - σ_A∨B(R) ⩳ σ_A(R) ∪ σ_B(R)
6. ÁTNEVEZÉS, ρ_S(A,B)(R) az R át lesz nevezve S-re és az oszlopai is

Részkifejezésekből nézettáblák -> azokon lekérdezése = összetett lekérdezés felépítése  
```SQL
 CRATE VIEW T1 AS SELECT ... FROM ... WHERE ...;
 ```

Ilyen műveletek sorozata a relációs algebra.

Él táblából Út tábla. Tranzitív lezárt.  
Nem triviális rekurzió.  
**Tétel:** Nem lehet relációs algebrával megoldani.  
*Teljes nyelv* ha mindent tud amit a relációs algebra. 

## Származtatott műveletek
- Metszet
- Összekapcsolások
    - Téta : |X|_A=B  
        A szabály alapján kell összekapcsolódni
    - Természetes : |X|  
        Közös oszlop alapján összekapcsolás
    - Félig-összekapcsolás: |X  
        Az elsőből csak azok kellenek amihez van a másodikban
    - Külső összekapcsolás : |X|^O (Outter)  
        Mindent szeretnénk látni, ezért NULL párokkal bekerülnek a hiányzó dolgok (nem teljesen relációs művelet)


    - séma egyezés r|X|s=r∩s
    - séma nem egyezik r|X|s=r×s
- Osztás, hányados
- Monotonitás - sorok hozzáadásával növekedni fog.

# AB2 EA 2021.09.14

## Algebrai optimalizálás
**Cél:**
Lekérdezések gyorsítása, a tábla specifikus paraméterek, statisztikák ismeretében, heurisztikák használatával.

## Lekérdezés optimalizálása
- SQL lekérdezés
1. elemzés
- Elemző fa
2. Átalakítás
- Logikai lekérdező terv
3. Szabályok alkalmazása
    - algebrai optimalizáció
- Javított logikai lekérdező terv
4. Várható méretek becslése
5. Fizikai tervek készítése
- 
6. Költségek becslése
- Terv, költség párok : **{(FT1,KI),(FT2,K2)...}**


## Példa:
```SQL
SELECT B,D
FROM R,S
WHERE R.A = 'c'
AND S.E = 2 AND R.C=S.C;
```
????

- Két tábla direkt szorzata és abból a megfelelő sorok, majd vetítés.
    - A direkt szorzatnak nagy eredménye lesz.
    - Oracle-ban: NESTED LOOP
    - Költséges
    - Π_(B,D)[σ_(felt)](R×S)

- Relációs algebrát ábrázolhatjuk fával
    - A levelek a táblák
    - Belső csúcsok műveletek

- Kiválasztások hamarabb, utána összekapcsolás.
    - Két vélhetően kisebb tábla lesz összerakva.
    - Π_(B,D)[(σ(R))|X|(σ(S))]
1. Keresést lehet gyorsítani pl indexekkel
2. Összekapcsolás is gyorsítható indexel
3. S-re szűrés
4. Összekapcsolás közben lehet ellenőrizni a vetítést

## Példa 2:
```SQL
SELECT TITLE
FROM StarsIn
WHERE starName IN (
    SELECT name
    FROM MovieStar
    WHERE birthdate LIKE '%1960'
);
```
1. Elemzőfa, Parse Tree
    - \<Query>, \<SFW>, 
2. Rendszertáblákból ellenőrizve vannak, hogy léteznek-e a táblák, megfelelő típusok vannak, megvannak a jogosultságok, stb..
3. Elemzőfából lehet REL-ALG fát csinálni
    - '\<tuple> IN \<query>' ezt még át kell alakítani
    - \<table> × \<query> majd σ_('x in y' -> 'x = y.x')
    - lehet theta joint a szorzás helyett
4. Ezeket a műveleteket végrehajtási szinten is lehet optimalizálni

## Algebrai optimalizálás
- **Cél:** gyorsabb kiszámítás
- **Költségmodell:** költség arányos a méretekkel, lehetne bonyolultabb költségeket is kiszámolni (miénk alapszintű)
- **Módszer:** műveletei tula. alapján ekviv. átalakítás
- **Az eljárás heurisztikus**, nem valódi méretekkel számol
- **Az eredmény nem egyértelmű:** Az átalakítások sorrendje nem determinisztikus, de általában jobb költségű
- **Megj.:** Az SQL sokkal bővebb, de most klassic. alg. kif. lesznek.

- kifejezést gráffal ábrázoljuk
- **Kifejezésfa:**
    - nem levélcsúcs
        - unáris műveletek
        - bináris műveletek
    - levelek: konstans relációk vagy reláció változók

## Példa 3:
- kv(s,i,kc) //könyv(sors., író, k.cím)
- kő(a,n,lc) //kölcsönző(azon., név, l.cím)
- ks(s,a,d)  //kölcsönzés(sors., azon., dátum)
- Milyen című könyvet kölcsönöztek ki 2007-től kezdve?
    - Π_kc(σ_(d>='2007.01.01')(kv |X| kő |X| ks))
    - ha minden infó kell, akkor az összekapcsolás szükséges - materializált nézet
    - Kölcsönző adataira nincs szükség, de lehet van materializált nézetünk

## 11 szabály csoport
1. Kommutativitás
    - X × Y ⩳ Y × X
2. Asszociativitás
    - A × B × C ≂ A × (B × C)
3. Vetítések összevonása, bővítés
    - A ⊆ B ⊆ E
    - Π_A(Π_B(E)) ⩳ Π_A(E)
4. Kiválasztások felcserélhetősége, felbontása
    - σ_(F1 ∧ F2)(E) ⩳ σ_(F1)(σ_(F2)(E))
5. Kiválasztás és vetítés felcserélhetősége
6. Kiválasztás és szorzás felcserélhetősége
7. Kiválasztás és egyesítés felcs.
8. Kiválasztás és kivonás felcs.
9. Kiválasztás és természetes összekapcsolás felcs.
10. Vetítés és szorzás felcs.
11. Vetítés és egyesítés felcs.
- Nem minden cserélhető pl: Vetítés és kivonás nem cserélhető fel

## Heurisztikus elvek
1. Minél hamarabb szelektáljuk
2. Összekapcsolások jobbak mint a szorzások
3. Unáris műveletek összevonása
4. Keressünk közös rész kifejezéseket

## Optimalizáló algoritmus
1. A kiválasztásokat bontsuk fel (4)
2. A kiválasztást mélyebbre visszük (4-9)
3. A vetítések is mélyre (3,5,10,11)
4. Műveletek összevonása (3-5)
5. Bináris műveletek csoportosítása, egy-egy művelte egy csoportban.
6. A fát kiértékeljük


## Példa 3:
- kv(s,i,kc) //könyv(sors., író, k.cím)
- kő(a,n,lc) //kölcsönző(azon., név, l.cím)
- ks(s,a,d)  //kölcsönzés(sors., azon., dátum)
- Milyen című könyvet kölcsönöztek ki 2007-től kezdve?
    - Π_kc(σ_(d>='2007.01.01')(kv |X| kő |X| ks))
    - Π_kc(σ_(kv.s=ks.s)((Π_(kv.s, kc)(kv))×Π_ks.a(σ_(kő.a=ks.a)(Π_kő.a(kő)×Π_(ks-s,ks.s)(σ_2007(ks))))))
    - Részgráfok képzése


# EA 2021.09.21

## Fizikai tervek
- Eddig logikai terv volt
- SQL lekérdezésből lesz egy terv
- "Explain Plan" ablak
- Műveletek közül próbál jobb költségűeket keres (nem a legjobbat, csak kb)
- blokk műveletek száma a mértékegység
- minden műveletre ki kell számolni a költségeket
    - jobb költségű sorozatot kell választani
    - műveletsorozat
        - kövi művelet költsége az előzőtől függ
- Méreteket és futási időkkel kell összehasonlítani

## Sorrend:
- SQL
    - elemzés
- Elemző fa
    - átalakítás
- Logikai lekérdező terv - fix pont
    - szabályok alkalmazása
- Javított logikai terv
    - Végrehajtás megbecslése
- Fizikai tervek
    - Költségek becslése
- "Legjobb kiválasztása"
    - Végrehajtás
- Eredmény

## Miért jó?
- Ez egy általános módszer
- Mi lehet tudunk speckó infókat amivel jobb végrehajtást tudunk adni
- Ha megértettük, akkor lehet javítani

## Indexelés
- Célok:
    - gyors lekérdezés
    - gyors adatmódosítás
    - minél kisebb tárhely
    - (hálózati forgalom optimalizálás, stb)
- Nincs általános legjobb optimalizáció. A célok egymás ellen dolgoznak
- Adatbázis lehet
    - statikus (ritkán módosul, komplex lekérdezések) - pl.: adattárház
    - dinamikus (sok módosítás, egyszerű lekérdezések) - pl.: bank felhasználói rendszere
- Hogyan mérjük költségeket?
- Memória műveletek gyorsabbak mint a háttértár műveletek
- Blokkokat ír,olvas, blokkokban számolunk
    - Írnia kell az eszköz dobozán a blokk sebességet, azzal kell felszorozni az aktuális hardveren
    - blokkméretet fixnek tekintjük (pl OP rendszer is meghatároz, író/olvasó fej is meghatároz ilyet, adatbázis is meghatároz)
- Feltesszük, hogy beolvasás és kiírás költsége arányos a háttértár és memória között mozgatott blokkokkal (memória beli műveletek arányosan nagyon kicsik, eltekintünk tőlük)
- Adatbázist is blokkokba szervezzük
- Feltesszük, hogy állandó hosszúak a rekordok
- blokkok tartalmaznak:
    - leíró fejlécet (hol vannak rekordok, üres helyek, egyéb infókat)
    - rekordokat
    - üres helyeket
- Költségek méréséhez paramétereket használunk
    - l - (length) rekord méret (bájtban)
    - b - blokkméret (bájtban)
    - T - (Tuple) rekordok száma
    - B - a fájl mérete blokkban
    - bf - blokkolási faktor (mennyi rekord fér el egy blokkban = bf = ⌊ b / l ⌋ - alsó egészrész)
    - B = ⌈ T / bf ⌉ - felső egészrész
    - M - memória mérete blokkban
    - Példa: R×S mérete
        - l(R×S) = l(R)+l(S)
        - T(R×S) = T(R)*T(S)
        - bf(R×S) = b / (l(R)+l(S))
        - B(R×S) = (T(R)*T(S)) * (l(R)+l(S)) / b =  
            = (T(S) * T(R) * I(R)/b) + (T(R) * T(S) * I(S)/b) =   
            = **T(S) * B(R) + T(R) * B(S)**

- Milyen lekérdezést vizsgálunk?
- Rel-alg 
    - Kiválasztás
        - Legegyszerűbb:
            - A = a (A mező, a konstans)
        - Kétféle bonyolultság
            - átlagos
            - legrosszabb
        - A=a -ból mennyi van (sok, egy)
            - ezt nem akarjuk vizsgálni, ezért feltesszük, hogy minden konstansból ugyanannyi van
            - **Egyenletességi feltétel**
            - Mennyi az annyi?
            - Különböző értékek száma I(A) - (image)
            - I(A) = |π_A(R)|
            - Egyenletességi feltétel esetén
                - T(σ_A=a(R)) = T(R) / I(A)
                - B(σ_A=a(R)) = B(R) / I(A)
            - Fejlesztési módszerek
                - Ömlesztett adatok
                - Kupac
                - Hasító index
                - Rendezett állomány
                - Elsődleges index (ritka)
                - Másodlagos (sűrű)
                - Többszintű index
                - B⁺-fa, B*-fa
            - Mi csak azt nézzük, hogy az elsőt mennyi megtalálni.  
                - A többire csak becslést adunk
            - Módosítási műveletek:
                - beszúrás
                - frissítés
                - törlés
            - Memóriában lévő adatokra is lehetne figyelni, nem kellene újra betölteni

### Kupac szervezés
- Blokk első üres helyére rakjuk, sorban
- Tárméret: B
- A=a keresési idő:
    - B (legrosszabb)
    - B/2 (átlagosan)
    - lineáris keresés
- Beszúrás
    - Utolsó blokkot kell beolvasni és beleírni: 2 művelet
- Módosítás:
    - 1 keresés + 1 írás
- Törlés:
    - 1 keresés + 1 írás (üres hely marad, vagy törlés bitet beállítjuk)
    - más is hivatkozhat erre

### Hasító szervezés
- Szekvenciális gyorsítása
- Láncok a blokkokból
- Egy blokkban hasonló dolgok
- Csak az adott kosárban kell keresni
- kosarak száma
    - fix -> statikus hasítás : K
    - adatoktól függően változik -> dinamikus hasítás
- A besorolás az indexmező értékei alapján 
- h(x)∈{1,...,K} hasító függvény
- A hasító függvény általában maradékos osztáson alapul
    - statikus esetben mod(K)
- Akkor jó a ha nem függ attól hogy melyik blokk milyen hosszú
- Adatok eloszlásához lehet állítani a hasító függvényt
- blokkláncok egyforma hosszúak legyenek, blokklánc B/K blokkból álljon
- Keresés A=a:
    - Túl nagy K sem segít
    - Túl kicsi sem biztos hogy jó
- Beszúrás
    - Blokk telítődik, akkor hozzáláncol egy újat
- Módosítás:
    - 1 keresés + 1 írás
    - ha a hasító érték módosul akkor átkerül
- Törlés:
    - Láncon előrébb lehet vinni, de felesleges lassítás lehet
- Intervallumos keresésre nem jó, egyenlőségre épül fel

- Dinamikus hasítás
    - kiterjeszthető
    - lineáris

- Kiterjeszthető hasító index:
    - kezdetben mindegyik blokk 1 rekordot tartalmaz, keresési költség: 1
    - hasító függvény:
        - rekordok várható számának logaritmusánál nagyobb k-t választunk
        - k hosszú bináris sorozatot ad
        - kosár azonosítója a bináris kód
        - prefix kód, i hosszú
        - h(x) bináris kód, annak i hosszú eleje lesz a kosarának a prefix azonosítója
        - ha betelik akkor átosztjuk a következő bit alapján a kosarakat
        - sok adatnál sok kosár jöhet létre és hosszú láncok jöhetnek létre
        - teljes fa lenne a jó, ki kell egyensúlyozni
        - virtuálisan kiegészítjük a fát
    - Kosár kódokat számon kell tartani
        - ha egyiknek nő a hossza, akkor fel kell venni az összes olyan hosszú kódszót
        - ha két külön direktori bejegyzés van, de csak egy blokk akkor ugyan arra mutatnak (csak virtuális szétbontás)

- Lineáris
    - több blokkból álló kosarak
    - komplexebb feltétel
    - telítettség alapján van szétbontva
    - pl.: kosarak átlagos mérete
    - kosarak csoportosítva a végződéseik alapján (postfix)

# AB2 EA 4 2021.09.28

## Indexelés

### Rendezett állomány
- Egy adott mező szerint sorba rendezi
- Ha a keresési mező a rendezett mező jók vagyunk
- Blokkos keresés
    - Beolvassa a középső blokkot
    - Bináris keresés
    - Vagy az adott blokkban van, vagy el tudjuk dönteni hogy melyik felében van az érték a maradék résznek
- Keresési idő: **log₂(B)** // B = blokkok száma
- Beszúrás
    - Hova kell beszúrni
    - Be kell rakni és a maradékot tologatni kell
    - Ha a blokkban nincs hely akkor az sok művelet
    - Helyeket hagyunk 
        - Nem teljesen töltjük ki
        - Kevesebb művelet a tologatás
        - pl a felét üresen hagyjuk
            - 2× akkora hely
            - Keresés: log₂(2*B) = **1 + log₂(B)**
            - Ha betelik akkor újrarendezés

    - Túlcsordulási blokkok
        - Keresés több helyen
        - G = túlcsordulási blokkok száma
        - Keresés
            - Log ker a rendezettben
            - \+ a rendezetlen rész
            - **log₂(B) + K**
            - K minél kisebb kell legyen
                - Ha nagy a K akkor újrarendezés
                    - B*log₂(B)
- Törlés
    - Keresés
    - \+ törlés bit átállítása
    - Sok törölt esetén újrarendezés

- Akkor jó ha inkább keresünk
- Több mezőre keresés
    - új indexet kell nekik létrehozni

## Indexek
- Mezők konka.-ra is lehet indexet csinálni
- Nő a tárméret
- Karban kell tartani
- Főfájl + indexek
- Ha sokszor keresünk azokra akkor van értelme
- Felépítés
    - (a,p) index és mutató
    - p Blokk mutató (pontosabb is lehet)
- Oracle
```sql
CREATE INDEX <NÉV> ON <TÁBLA> (<MEZŐNÉV>);

--ÖSSZETETT
CREATE INDEX <NÉV> ON <TÁBLA> (<MEZŐNÉV>, <MEZŐK NEVEI>) COMPUTE STATISTICS;
```
- Statisztikák
    - egy oszlopban hány féle érték stb.

### Elsődleges index - Primari
- Arra a mezőre amire rendezve van a fájl
- Csak egy mezőre lehet
- Csak egy lehet
- `Primary key` kulcsszóval rendezett lesz és lesz hozzá index
- Ritka index - nem kell minden mezőhöz
    - (sűrű - minden rekordhoz)
- bf(I)>>bf - az index sokkal kisebb mint a fájl
- B(I) = B / bf(I) << B = T / bf
- Keresés
    - Keresünk az indexben, csak fedő értéket tudunk keresni
    - Kisebbek közül a legnagyobbat
    - log₂(B(I))
    - Ha meg van a blokk akkor azt is be kell olvasni és abban is keresni
        - **1+log₂(B(I))** << log₂(B)
- Módosítás
    - Be kell szúrni a táblába és talán az indexbe is
    - Ha van még hely a blokkban akkor kevesebb művelet
    - Indexfájlban is hagyhatunk helyet

### Másodlagos index
- Több másodlagos index is lehet
- Minden rekordból lesz index - sűrű
- Nagyobb méretű
- Index alapján lehet tudni, hogy benne van-e
- bf(I) >> bf
- B(I) = T/bf(I) << B = T/bf
- Keresés
    - **1+log₂(B(I))** << log₂(B)
- Módosítás
    - Index fájlt kell módosítani mindig
    - Mindig rendezett kell legyen
    - Max üres hely lehet benne


### Indexnél több érték is lehet ugyanaz
- Nem foglalkozunk és felvesszük többször
    - Mindet ki kell szedni
- Ritka indexxel nem túl hatékony mert több irányba is lehet, hogy kell keresni
    - Javítás ha az első előfordulást tároljuk el
    - Összeláncoljuk a blokkokat
- Közös index, de több mutató hozzá
    - Nem fix hosszú rekordok
- Elsőt tároljuk
    - Összeláncoljuk a közös blokkokat
    - Sok mindent kell karbantartani
- Index mutatója egy külön helyre
    - kosarakra
    - kosarak mutatnak az adott rekordokra
    - Több mezőre keresésnél kellenek a kosarak metszetei

### Indexelés
- Klaszter (nyaláb, fürt)
    - Klaszterszervezés
        - Egyforma értékek egy blokkban vagy közeli blokkban
    - Ilyenekre lehet klaszter indexet készíteni
    - Ha két táblát gyakran össze kell kapcsolni
        - klaszterindex az összekapcsolási rekordokra
- Indextábla is tábla
    - Arra is lehet indexelni
    - Csak rendezett táblára lehet ritka index
    - Egy index már rendezett - arra indexelni már ritka lesz
    - Addig lehet csinálni amíg elég kevés érték marad a legfelső indexbe (min 1 rekord)
    - Ez már fa szerű felépítés lesz

### Többszintű index
- legfelül bináris keresés
- onnantól lefelé minden szinten csak egy blokkot kell beolvasni 
    - (blokkon belüli keresés gyors - elhanyagolható)

|                   | Főfájl | 1.szint | 2.szint | ... | t.szint |
| ----------------: | :----: | :-----: | :-----: | :-: | :-----: | 
|     blokkok száma |    B   | B/bf(I) | B/bf(I)² | ... | B/bf(I)ᵗ |
|    rekordok száma |    T   |    B    | B/bf(I) | ... | B/bf(I)ᵗ⁻¹ |
| blokkolási faktor |   bf   |  bf(I)  |  bf(I)  | ... | bf(I) |

- t = **log_(bl(I))(B)** < log₂(B)

### B⁺, B* fák
- B⁺ min 50%-ban telített
- B* min 66%-ban telített
- Legalsó szinten sűrű index
- Csúcs
    - n+1 mutató
    - n index érték
    - az index értékek intervallumokat jelentenek
- Fa magassága blokk művelet
- Beszúrásnál ha nincs hely akkor karbantartás
    - Ha nincs hely akkor kettéválasztja a blokkot és beszúrja
        - Egy szinttel feljebb is be kell kötni az új blokkot
        - Tovább gyűrűzhet
        - Magasabb lehet a fa
- Törlésnél kicsi a telítettség
    - Blokkokat kell összevonni
    - Ez is felfelé gyűrűzik
    - Kisebb lehet a fa

# EA 5 2021.10.05

## Optimalizálás
- Több féle végrehajtás
    - szevenciális, index alapú keresés
    - Primari key-ből egy van
π_name(σ_cours=AdvancedDBs((student |X|_cid takes) |X|_courseid course))
    - költségeket alulról számoljuk
    - hogyan kapcsoljuk össze?
    - K_n - összekapcsolás sebessége
    - O_n - új tábla mérete
    - az utolsó a végeredmény
    - Teljes költség:
        - ∑_i=1..n K_i + O_n
- Optimalizáscónál
    - K költségek közül választunk
    - a legkisebb költségűt választjuk
    - nem számolja ki az összeset és keresi a legjobbat
    - heurisztika alapján DP-vel keres egy jót

## Költségek
- Lemez I/O
- CPU idő (nem számoljuk)
- Hálózati kommunikáció (nem számolunk vele)
- Idő, költség és méret becslés
- SQL developerben meg lehet nézni
    - később lehet megtanuljuk hogy a felhasználó is befolyásolhatja
- Műveletek
    - σ, π, ∪, -, x, |X|, ∩
- Költésgek
    - N_R: Rekordok szám (Eddig T_R)
    - L_R: Rekordok mérete (eddig I_R)
    - F_R: blokkolási tényevő (eddig bf_R)
    - B_R: R-hez szükséges blokkok száma
    - V(A,R): A mező különböző értékeinek száma
    - SC(A,R): A mező kiválasztási számossága
            - szelektivitás - hány olyan van
        - A kulcs: SC(A,R)=1
        - 
    - HT_i: index fa, B* fa magassága

## Kiválasztás
- Lineáris 
    - nem kulcs: B_R
    - kulcs: 0.5*B_R
- Logaritmusos keresés
    - rendezett mező esetén:|log_2 B_R|+m
    - átlagos költség:
        - m további lapot kell beolvasni
        - m = ⌈SC(A,R)/F_R⌉ -1
    - (inkábbb attól függ hogy hány találat van)
- Elsődleges/cluster index
    - átlagos: 
        - egy: HT_i + 1
        - több: HT_i + ⌈SC(A,R)/F_R⌉
- Másodlagos index:
    - átlag
        - kulcs: HT_i + 1
        - nem kulcs:
            - legrosszabb: HT_i + SC(A,R)
            - lineáris keresés jobb ha sok a találat
    
## Összetett kiválasztás
- konjungciós kiválasztás
    - egyik feltételre az egyszerű költség
        - a találatokra megy a többi ellenőrzés
        - a leggyorsabb indexet kell kiválasztani
    - Több index és találtaok metszete
- diszjunkciós kiválasztás
    - indexek nem gyorsítanak
    - szekvenciális keresés és ellenőrzés

## Méretbecslés - kiválasztás
- A = a
    - Sorok száma: SC(A,R)
    - Blokkok száma: SC(A,F)/F_R
- A <> a
    - Sorok száma: N_R * (v - min(A,R)) / (max(A,R)-min(A,R))
    - Blokkok száma: Sorok száma/F_R
- θ ∧..∧ θ
    - független feltételeknél szorzat - felső becslés
    - Sorok száma: N_R * [(s_1/N_R)*..*(s_n/N_R)]
    - Blokkok száma: Sorok száma/F_R
- θ ∨..∨ θ
    - komplementere: egyik feltétel sem igaz -> hasonló a konjunkcióhoz - annak a fordítottja
    - Sorok száma: N_R * (1-[(1-s_1/N_R)*..*(1-s_n/N_R)])
    - Blokkok száma: Sorok száma/F_R
## Halmazműveletek: ∪, ∩, -
- Rendezésekre visszavezetve
- Ha minden befér a memóriába akkor ott rendezünk és kiírjuk : 2*B_R
- Ha nem fér be akkor bonyolultabb, rendezett részek
    - futamokat kőpzönk
    - bolvasunk annyit ami befér a memóriába és lerendezzük
    - kiírjuk
    - rendezett részeket összefésüléssel hosszabbakat csinálunk
    - Rendezett futam: 2*B_R
    - Hány összefésülés: log_(M-1)(B_R/M)
    - 2 * B_R + 2 * B_R * log_(M-1)(B_R/M) [- B_R]

## Vetítés
- Felesleges oszlopok kidobása
    - B_R + B_R1
- Duplikátumok elhagyása
    - Rendezés igénye

## Méretbecslés - Vetítésre
- Felső becslés: B_R
- Egy oszlopra:
    - Sorok: V(A,R)

## Unió
- felső: N_R + N_S
- duplikátumok törlése rendezéstől függ

## Szorzat
- sorok: N_R X N_S
- blokk: B_R * N_R + B_S * N_S

## Metszet
- sorok: min(N_R, N_S)
- blokk: min(B_R, B_S)

## Kivonás
- sorok: N_R
- blokk: B_R
        
## Öaazekapcsolások
- Nested-loop join - Skatulyásott ciklusos
    - B_R + B_S
    - ha csak egy blokk fér a memóriába
    - R minden sorához végig kell olvasni a másik táblát
        - N_R * B_S + B_R
```
R minden t_R rekordján
    S minden t_S rekordján
        ha (t_R t_S illeszkedik) akkor összerakás 
    vége
vége
```
- Block-nested join - Blokk skatulyázott
```
R minden X_R blokkra
    S minden X_S blokkra
        X_R minden t_XR rekordra
            X_S minden t_XS rekordra
                ha (t_R t_S illeszkedik) akkor t_R |X| t_S kiírása 
            vége
        vége
    vége
vége
```
- Index nested join - Inexelt skatulyázott
    - jobb a klaszter index
    - külsőn végigmegyünk és index alapján keresünk hozzá értéket
    - B_R + N_R * c
        - c kiválasztási költség
    - Kisebb tábla legyen a külső
- Sort-merge join
    - Ha rendezve van a tábla az jó
    - He nem akkor lerendezi
    - Két mutató mozog - mindig a kisebbet kell léptetni
- Hash join 
    - Kosarakba hasítjuk
    - Akkora kosarak, hogy beférjen kettő a memóriába
    - Ugyan azt a hasító függvényt kell használni
    - A kicsi kosarakat könnyebb kezelni
    - Az adott kosárban azonos értékű sorok vannak
    - Összekapcsolható sorok ugyanabba a kosárba kerülnek
    - Végig kell olvasni és hasítani mindkét táblát, utána már csak beolvasás és kiírás
    - 2*(B_R+B_S) + (B_R+B_S)

## Méretbecslés - összekapcsolás
- legrosszabb : direkt szorzat
- egy közös oszlop
    - N_R*N_S/V(A,S)
    - sorok:N_S*N_R / Max(V(A,R), V(A,S))
    - tARTALMAZÁSNÁL KEVESEBB

## öSSZEFOGLALÁS
- Minden költséget lehet becsülni
- Összeadjuk
- És ebből próbálunk jobbat csinálni
- Esetleg párhuzamosítás
- Tetszőleges orrend lehet sok helyen, lehet variálni

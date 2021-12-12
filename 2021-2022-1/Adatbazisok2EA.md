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
Végrehajtás sorrendjét adja meg.

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
2. Összekapcsolások jobbak, mint a szorzások
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
- Mi lehet tudunk speckó infókat amivel, jobb végrehajtást tudunk adni
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
- Memória műveletek gyorsabbak, mint a háttértár műveletek
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
    - Túl kicsi sem biztos, hogy jó
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
    - Vagy az adott blokkban van, vagy el tudjuk dönteni, hogy melyik felében van az érték a maradék résznek
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
            - Ha betelik akkor újra rendezés

    - Túlcsordulási blokkok
        - Keresés több helyen
        - G = túlcsordulási blokkok száma
        - Keresés
            - Log ker a rendezettben
            - \+ a rendezetlen rész
            - **log₂(B) + K**
            - K minél kisebb kell legyen
                - Ha nagy a K akkor újra rendezés
                    - B*log₂(B)
- Törlés
    - Keresés
    - \+ törlés bit átállítása
    - Sok törölt esetén újra rendezés

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

### Elsődleges index - Primary
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
    - Javítás, ha az első előfordulást tároljuk el
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
- Beszúrásnál, ha nincs hely akkor karbantartás
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
- Többféle végrehajtás
    - szekvenciális, index alapú keresés
    - Primari key-ből egy van
π_name(σ_cours=AdvancedDBs((student |X|_cid takes) |X|_courseid course))
    - költségeket alulról számoljuk
    - hogyan kapcsoljuk össze?
    - K_n - összekapcsolás sebessége
    - O_n - új tábla mérete
    - az utolsó a végeredmény
    - Teljes költség:
        - ∑_i=1..n K_i + O_n
- Optimalizációnál
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
    - később lehet megtanuljuk, hogy a felhasználó is befolyásolhatja
- Műveletek
    - σ, π, ∪, -, x, |X|, ∩
- Költségek
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
    - (inkább attól függ hogy hány találat van)
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
    - Több index és találatok metszete
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
    - futamokat képzünk
    - beolvasunk annyit ami befér a memóriába és lerendezzük
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
        
## Összekapcsolások
- Nested-loop join - Skatulyázott ciklusos
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
    - külsőn végig megyünk és index alapján keresünk hozzá értéket
    - B_R + N_R * c
        - c kiválasztási költség
    - Kisebb tábla legyen a külső
- Sort-merge join
    - Ha rendezve van a tábla az jó
    - He nem akkor lerendezi
    - Két mutató mozog - mindig a kisebbet kell léptetni
    - cost of sorting + B_S + B_R
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

# EA 6 2021.10.12

## Több tábla összekapcsolása 
- Több fizikai terv is lehet
- Összekapcsolások nagyon gyakoriak
- Kommutatív asszociatív, sorrendjük nem számít, de költségben lehet különbség
- Összekapcsolások végrehajtási fában ábrázolható
- Rendezéseshez nagy memória kell + lehet rendezni kell a táblát
- Zárójelezéssel mindig csak két táblát kapcsolunk össze
- Direkt szorzat nem jó nekünk, sok elem lesz
- Hány zárójelezés van?
    - T(1) = 1
    - T(n) = \sum T(i)T(n-1), T(6) = 42
    - n táblára
    - lehetne a sorrendet is változtatni, permutáció
    - 6 táblánál - 42*6!
- Csak speciális zárójelezéseket néz
    - Left-deep tree
    - Bushy tree
    - Valaminek az újra felhasználása
    - Csak a kb legjobbat keressük heurisztikával
        - pl 4 tábla legjobbját megkeressük és ahhoz hozzáveszük a következőt
            - ez nem mindig a legjobb, de általában elég jó
- Selinger Algoritmus
    - Mindig a legkisebbet nézi
    - melyik a legkisebb tábla
    - melyik a legkisebb két táblás, amiben a legkisebb tábla benne van
    - melyik a legkisebb három táblás összekapcsolás, amiben a legkisebb kettes benne van
    - így tovább addig amennyi kell

- Három tábla, kettőre van klaszterindex
    - Stratégiák
        1. balról jobbra
        2. balról jobbra, eredmény a memóriában marad
        3. középső táblához kapcsoljuk a szélsőket
    - Feltételezések
        - ugyan annyi soruk van : T
        - ugyan annyi memóriát  : B
        - ugyan annyi a gyakori : I
        - Összetartozók elférnek a memóriába
    - Számolások
        1. B + 5 * T * B / I + 4 * T^2 * B / I^2
        2. B + T * B / I + 4 * T^2 * B / I^2
        3. B + 2 * T * B / I + 3 * T^3 * B / I^2

## Oracle SQL Tuning
- Régen volt szabály alapú optimalizálások, heurisztikákkal
    - Nem volt olyan jó mint a mostani Költség alapú optimalizálás
- Egyet könnyebb megtalálni: First_rows_n(1, 10, 100, 1000), All_rows
- Session szinten ehet állítani
- Adatnak van cím része - (melyik tábla, melyik blokk, melyik sor)
- Blokkokban tárolódik, üres helyek vannak
- Index is egy fájl, blokkokban
- Lemezről blokkok beolvasása az SGA-ba (puffer memória, gyorsítótár)
- SGA-ból vannak végrehajtva a műveletek
- `Explain plan for <SQL utasítás>`
- Oracle esetek
    - Egyetlen tábla, nincs index 
        - select * from _
        - Select Statement; Table Access full _
        - where feltétel nem ad hozzá, utólag lesz leszűrve
        - order by -> SORT order by
        - ha rendezésre van index akkor azon megyünk -> INDEX full scan _index_
        - group by -> SORT group by
        - having -> filter
        - where rowid='_memóriacím_' -> TABLE ACCESS by rowid _tábla_, jó ha sokszor keressük ugyan azt
    - Egy tábla, index
        - van unique index -> INDEX unique scan _index_
        - nincs unique -> INDEX range scan _index_
        - unique index, de egyenlőtlenség -> INDEX range scan _inde_
        - összetett index - ha több feltétel van akkor jó lehet
            - ha nem az összes részére szűrünk akkor is jobb, mint a semmi
        - több index is van - az egyedire szűrtet használja
        - van amikor több stratégiát vesz és összehasonlítja
            - számít, hogy milyen távol van egymástól a több megegyező
        - több indexnél a mutatókat össze kell metszeni, mindkét indexet használja -> AND-EQUAL
        - count(*) -> INDEX fast full scan _index_ - a sűrű indexben benne van a count
    - Összekapcsolás, skatulya
        - NESTED LOOPS és két TABLE ACCESS ful
        - Ha van feltétel
        - MERGE JOIN; SORT join; full access...
        - indexelt -> nested loops, full, tableacc by rowid; INDEX range...
        - össze kell hasonlítani h melyik irány a jobb
        - hasításost találja a legjobbnak -> HASH JOIN
    - Alkérdések
        - nézetet csinál belőle
        - kioptimalizál és összekapcsol, nem lesz allekérdezés
        - or pointerek uniója -> CONCATENATE
        - metszet -> INTERSECT
        - minus -> MINUS, SORT
- Konkrét értékek lekérdezhetőek
- Beágyazott megjegyzések
    - SELECT /* +<tipp> */
    - tippek
        - full
        - index
        - ordered
        - use_nl
        - use_merge
        - use_hash
        - leading
        - first_rows, all_rows            
    - Analizáló utasítások
- BITMAP index
    - értékek helyett bitmap van
    - csak bináris értékek ha kevés dolog van az oszlopban

# EA 7 2021.10.19
- Az algoritmus nem biztos, hogy a legjobbat adja, de elég jót
- Osztott adatbázisokról nem beszéltünk
    - Ott a hálózati művelet a lassú
    - Arra kell optimalizálni

## Tranzakciókezelés
(Helyreállítás, naplózás; konkurencia)
- Tranzakció
    - Adatbázis kezelő műveletek egy sorozata
    - Beszúrási, törlési, módosítási
    - Röviden írás, olvasás
- Program jó adatbázisból jót képezzen
    - Szabályokat ne sértse meg
    - pl.: Unique oszlop maradjon az beszúrás után is.
- Több tranzakció között van probléma
- Vagy ha tranzakció közben elromlik valami
- **Konzisztencia**
    - Adott feltételek amiknek meg kell felelnie
    - Kulcs, FF(funkcionális függ), érték megszorítások
    - Adatstruktúrák karban tartása, pl indexek
    - Több rekordra szóló megszorítások (az átlag kétszeresénél nem lehet több egyik érték sem)
- **Konzisztens állapot**
    - kielégíti a feltételeket
- **Konzisztens adatbázis**
    - konzisztens állapotban van
- **Tranzakció megszorítás**
    - Ha módosítás van akkor növelni kell
    - Törlés után valami legyen
    - Törlési bit beállítás

- Megszorításokat ellenőrizni kell a tranzakcióban
- Megszorításokat előre meg kell tervezni
- Adatbázis a valóságot próbálja modellezni
    - Fontosabb adatokkal és összefüggéseikkel

- Tranzakció közben lehet nem konzisztens állapot
- Az elején és a végén kell konzisztens legyen

- Rendszerhiba miatt megállhatna, vagy más miatt is abortálhat, így megmaradna egy hibás állapotban
- Vissza kell állítani az előző konzisztens állapotba

## Naplózási és helyreállítási modul
- Biztosítja, hogy az adatbázisban mindig helyes állapot legyen
- Mit tároljunk el, hogy vissza lehessen állítani
- Atomiságot biztosítja
- Tartósságot is


## Konkurenciakezelő
- Úgy fut több tranz. egy időben mintha mindegyik külön futna
- Ütemezéssel össze is lehet fésülni a tranzakciókat


## Tranzakció feldolgozás
- Mindegyik izoláltan fut
- Mások adatait nem látja és más sem látja az övét
- Véglegesítésnél 'commit'-nál kerülnek be az adatbázisba
- Onnantól kezdve másoknak is elérhető

## ACID
- Atomosság - vagy teljesen vagy semennyire legyen végrehajtva
- Konzisztencia - konzisztensből konzisztensbe
- Elkülönítés (isolation) - minden tranzakció úgy fut mintha csak ő használná
- Tartósság ()

## Commit és Rollback
- Trigger típusú műveletek miatt
    - sima adatművelet is tranzakciószerű lesz

## Tranzakció feldolgozása
1. Naplózás
    - Nem ír ki a lemezre 
    - Pufferbe ír, oda gyűjti azt, ami kell neki
    - Majd eldönti az adatbázis, hogy mikor lesz kiírva
2. Konkurenciavezérlés
    - Több tranzakció az több művelet sorozat
    - Össze lehet fésülni őket, megfelelő sorrendbe
    - Ütemezőnek az összefésülések közül ki kell választani a jó ütemezéseket - legjobbat
    - Egymás utáni végrehajtás biztos jó lenne
        - de lehet ennél jobbat csinálni
        - gyorsabbat, másodiknak ne kelljen olyan sokat várni, stb...
    - Megoldások
        1. Zárak - tiltanak hozzáférést, zártábla
3. Holtpont
    - Egymásra várakozásba akadnak
    - Pl záraknál

## Mitől sérül a konzisztencia?
- Tranzakcióhiba
    - Hibásan megírt program
    - Ütemezési hiba
- Adatbázis-kezelési hiba
    - ABKezelő komponenese rosszul csinál valamit
- Hardverhiba
    - Sérült adat
- Adatmegosztásból származó hiba

## Helyreállítás
- Hiba modellezése
- Memória hiba
    - Megszakadt futás
- Lemezhiba
- Rossz adatbevitel
    - Tartalmi hiba: nehéz észlelni
    - Formai hiba
    - Triggerekkel ha több minden kell automatikusan
- Készülékhiba
    - Kis hiba: több bit sérül, paritás ellenőrzés, helyi javítás
    - Nagy hiba: jelentős sérülés, vannak megoldások
        1. RAID
            - elveszett lemez adatai visszaállíthatóak
        2. Archiválás
            - menet közbeni archiválás nem biztos, hogy jó állapotot tárolna el
            - napló segíthet
        3. Osztott másolat
            - költséges szinkronizálás
            - szinkronizálás közben is lehet probléma
- Katasztrofális hibák
- Rendszerhibák

## Naplózás
- Állományok jönnek létre
- Memóriában és a lemezen is van adata
- Napló állományban mindig jó állapot legyen
- Helyreállítás ezt használja
- Elérhető kell legyen

## Napló és tranzakció
- Pufferekben is kell ellenőrizni és oda írnak

## Adategység (adatbáziselem)
- Bármi lehet, rekord, táblarész

## Adatműveletek
- INPUT(X) - lemez beolvasás, X-et a pufferbe
- OUTPUT(X) - lemezre kiírás
- READ(X,t) - pufferből olvasás, X-et a t tranzakcióba  olvassa
- WRITE(X,t) - pufferbe ír

## Naplóbejegyzés
- Tranzakció kap egy számot
- Sorrendiség is van
- Ti - i-edik tranzakció
- Bejegyzések:
    - Ti kezdődik: (Ti. START)
    - Ti írja A-t: (Ti, régi érték, új érték)
    - Ti rendben befejeződött: (Ti, COMMIT)
    - Ti a hamarabb befejeződött: (Ti, ABORT)
- Napló mérete gyorsan nő
- El kell dönteni, hogy mit lehet eldobni
- Biztos lemezen kell tárolni - mindig meg legyen
- El kell dönteni, hogy mikor lehet kiírni, mikor kell

## Undo Naplózás
- Régi érték van benn
## Redo Naplózás
- Új érték van benn
## Kombinált Naplózás (Undo-Redo)
- Előző kettő kombináltja


# EA 8 2021.11.02

## Vizsga
- Írásbeli
- Weboldalon
- Elméleti anyag 
- Jelenléti formában
- Keddi napok lesznek vizsganapok
- 8:15-10:00

## Naplózás

### Undo log (Semmiségi naplózás)
- Régi értéket naplózzuk
- Azonnali kiírás, ne vesszen el a naplózás
- Ha minden rendben akkor commit üzenet a naplóba 
    - Itt a commit azt jelenti, hogy a tranzakció véget ért és minden változtatás a lemezre is került
    - Csak akkor, ha tényleg minden rendben van
- Undo naplózás szabályai:
    - U1. (T, X, régi érték) kerül a naplóban, hamarabb, mint hogy módosulna
    - U2. COMMIT csak, akkor, ha minden módosítás bekerült az adatbázisba
- Sorrend
    1. Változás naplója
    2. Változás
    3. COMMIT
- Helyreállítás
    - Olyan tranzakciókat, amiknek nincs COMMIT vagy ABORT bejegyzése
    - Végig kell menni a bejegyzésein és be kell állítani a régi értékeket
- Ellenőrző pontok képzése
    - Ellenőrző pont előtti részt el lehet dobni
    - Checkpoint megállítással
        - Megállítjuk a rendszert
        - Ha minden rendben volt addig akkor az előtte lévő részt már nem kell napló visszaállításnál vizsgálni
        - Indítjuk a rendszert
        - Utána csak a CHECKPOINT-ig kell visszamenni a helyreállításnál
    - Checkpoint megállítás nélkül
        - Hosszú idő lenne a folyamatok leállítása
        - Aktív tranzakciókat figyelembe véve készít checkpointot
        - < START CKPT(T1,..,Tk) > napló bejegyzés ha T1,..,Tk befejeződött
        - Közben indulhatnak újak
        - < END CKPT > a vége
        - Köztes rész a "piszkos" rész

### Redo logging (Helyrehozó naplózás)
- Az új értéket naplózzuk
- commit:
    - tranzakciós lépések a start és a commit között vannak
    - írások a commit után lehetnek csak
- end:
    - az írás is megtörtént
- szabályok
    - R1. Naplóbejegyzés módosítás előtt, commit után írások
- Ha nincs end csak commit 
    - újra ki kell írni az adatokat
    - commit előtti lépések újra végrehajthatóak
- Ha nincs commit
    - nem voltak írások
    - nem probléma
    - abort-áljuk
- Módosított redo napló
    - nincs end
    - commit-ot látunk, mindig végrehajtjuk
    - vizsgálat nélkül fut minden
    - abort-al is jelezhetjük a commit-ig nem eljutó tranzakciókat
- Különbség UNDO-val
    - commit mást jelent

- Ellenőrzőpont
    - < START CKPT(T2,..,Tk) > ha T2,..,Tk előttiek már befejeződtek(commit)
    - T2,..,Tk előtti tranzakciók módosításait kiírjuk
    - < END CKPT > -ig kell csak visszamenni
        - ha van end akkor előtte lezárt tranzakciók már kiíródtak
    
### Undo/Redo log (Semmiségi/helyrehozó naplózás)
- Későbbi jó állapotba lehet hozni
- Hátrányok
    - Undo-nál nagy az log mérete
    - Redo-nál buffereket kellett üríteni
- Megoldás:
    - < T,X,v,w > - v régi, w új érték
    - Bárhol lehet a COMMIT
        - Ha nem volt Commit -> Undo visszaállítás
        - Ha volt -> Redo visszaállítás
        - Mettől meddig tart a tranzakció
- Szabály:
    - UR1: naplóbejegyzés hamarabb legyen kiírva, mint a módosítása
    - WAL: Write After Log elv
- Nagyobb napló: több adat benne
- Helyreállítás:
    - UR2: A commit minél hamarabb kikerüljön a lemezre
        - későbbi állapotra állítás valószínűsége nagyobb
- Checkpoint
    - Összes piszkos puffert kiírjuk
    - Ha ki van írja akkor END CKPT
    - Startig kell visszamenni
    - Akinek volt COMMIT azt kiírjuk
    - Akinek nem azt visszaállítjuk
    - Visszaállításnál kevesebbet kell újra végrehajtani
    
# EA 9 2021.11.09

## Eszköz meghibásodás kezelés

### Lemezhiba elleni védekezés
1. Háromszoros redundancia
    - 3 másolat külön lemezen
    - Output(x) -> 3 kiírás
    - Input(x) -> 3 olvasás + szavazás
2. Checksum összegek
3. Adatbázismentés + napló
    - Aktív adatbázisnál a napló is kell
    - Napló redo bejegyzéséből naprakész állapotra lehet hozni
    - Legrégebbi aktív tranzakcíóig kell csak visszamenni és kiírni

### Mentés működés közben
1. < START DUMP >
2. REDO vagy UNDO/REDO naplózásos **ellenőrzőpont** kialakítása
3. Adatok teljes vagy növekményes mentése
4. A napló mentése
5. < END DUMP >

## Oracle naplózási és archiválási rendszere
- Helyreállítás kezelő automatizmusok indításkor
- REDO típusú log-állományt készít
- UNDO dolgoknak egy ROLLBACK segmenset csinál
- UNDO/REDO típusú naplózást tud így csinálni
- Online napló
- Archivált napló
- System Global Area - SGA
    - naplóbejegyzések ideiglenesen itt vannak
- Log Writer írja ki (LGWR)
- Több napló is online
- Ha betelik a teljes napló, akkor 
    - NOARCHIVELOG MÓD
        - az egyikből kidobja a régi dolgokat
    - ARCHIVELOG MÓD
        - kiírja, archiválja
- LogMiner naplóelemző eszközök
    - rekordok vannak, sql-el kezelhető
- Rollback szegmenseknek a SYS a tulajdonosa, ő adhat jogokat másoknak
    - Tranzakció befejezésekor, utána idővel lehet törölni
    - Teljesen törlődnek
    - Lehet bővíteni is

- Naplózást is naplózzuk
- Rolling forward és rolling back is lehetséges
- Teljes vagy részleges mentés

## Konkurenciavezérlés, sorbarendezhetőség, konfliktus-sorbarendezhetőség

- ACID tulajdonság biztosítása

### Ütemező
- szabályozza a feladatok sorrendjét

### Konkurenciavezérlő
- párhuzamos folyamatok ne rontsák el egymást
- rossz ütemezést azonosítja és kijavítja
    - (rossz = konkurens problémát okozna)
- ha nem tudja kijavítani
    - abortálhat tranzakciót
    - várakoztathat

### Lényeg
- Az összefésült ütemezés ekvivalens-e a sorok ütemezéssel
- Mindig konzisztens állapot legyen a végeredmény
- Egy tranzakció műveletei ugyanabban a sorrendben legyenek
- Konfliktusos pár:
    - Megcserélve jó-e
    - Mi nem konfliktusos
        - ezt könnyebb meghatározni
        - ha különböző adatot írnak-olvasnak
    - ugyan az a tranzakció művelete
    - ugyanazt írják

- Cserékkel el lehet jutni soros ütemezésig akkor jó
    - nem konfliktusos párokat cserélgetve lehet összefésülni

- **konfliktusekvivalens** - szomszédok nemkonfliktusos cseréjével alakítjuk

- **konfliktus-sorbarendezhető** - konfliktusekvivalens egy soros ütemezéssel

- Az ütemező jót eldobhat
    - de rosszat sose mond jónak


# EA 10 2021.11.16

## Konfliktus sorbarendezhetőség
- Elégséges a sorbarendezhetőséghez
- Konfliktusos párokat definiálunk
    - Felcserélve más eredményt kapnánk
- Nem kell egymás mellett legyenek
- T₁ megelőzi T₂-t ha egymás mellett konfliktusos pár lenne
    1. A₁ megelőzi A₂-t 
    2. A₁ és A₂ ugyanarra az adatbáziselemre vonatkozik
    3. A₁ és A₂ közül az egyik írási művelet

## Megelőzési gráf
- Csúcsa tranzakciók
- Megelőzések az élek
- Lemma:
    - S₁, S₂ konfliktusekvivalens ⇒ gráf(S₁)=gráf(S₂)
        - Indirekt, ha egy él nincs benne az egyikben de benne van a másikban akkor nem ekvivalensek
    - A Gráf megegyezése nem jelent konfliktusekvivalenciát

## Konfliktussorbarendezhetőségi teszt
- Ha megelőzési gráfban van kör, akkor nem konfliktussorbarendezhető
- topológikus sorrendbe kell rakni a tranzakciókat
    - ha van él A-ból B-be, akkor A elemei megelőzik B elemeit
    - Nem konliktusos párok cseréjével el lehet jutni a sorbarendezett ütemezésig

## Passzív módszer
- Néha megnézi a megelőzési gráfot
- Ha van kör, akkor abortál tranzakciókat
- Ha nincs, akkor örül

## Aktív módszer
- Rosszakat soha nem enged át
- Szigorúbb általában
- Lehet veszteség
- megoldások
    1. Zárak
    2. Időbélyegek
    3. Érvényesítéses

### Zárolási ütemező
#### Legszigorúgg zárolás
- lᵢ(A) - kizárólagos zárolás
- uᵢ(A) - zár elengedése
- teljesen zárolja az adott adatbáziselemet
- ezekkel biztosítja a sorbarendezhetőséget
- Tranzakció konzisztenciája
    1. Akkor írhat, olvashat valamit, ha azt már zárolta és még nem oldotta fel
    2. Ha zárolt, akkor fel is kell oldania
- Ütemezés jogszerűsége
    1. Két tranz. nem zárolhatja ugyan azt
        - ütemezében csak, akkor jöhet ugyan arra zár, ha már fel lett oldva
- Különböző típusú zárakat is fel lehet venni
#### Kétfázisú zárolás
- Minden zárfeloldást megelőz minden zárolás
- Konzisztens, kétfázisú zárolású tranz. jogszerű ütemezését át lehet alakítani konfliktusekvivalensé
#### Holtpont elkerülés
- Tranzakciók egymásra várakozása
- Várakozási gráf
    - Tranzakciók a csúcsok
    - él ha i várakozik j-re
- Ha kör van, akkor holtpont is van
- Ez a gráf dinamikus
    - Megszűnhet kör, létre jöhet
- Optimista működés
    - Hagyjuk, hogy kérjék a lock-okat
    - Ha kör lesz, akkor kilő tranz.
- Pesszimista
    - El sem indítjuk, ha nem kaphatja meg az összes zárat
    - Nem tudhatjuk előre az összes zárat
- Másik pesszimista
    - Adat elemeken sorrend
    - Zárakat sorrendben kell kiadni
#### Kiéheztetés
- Egy tranzakció sosem kapja meg a zárat
- Várakozási sor bevezetése

#### Olvasásokhoz is várakozik
- Olvasáshoz ne kelljen zár
- Gyorsabb lesz
- Csak íráshoz legyen zár
- Olvasási és írási zár bevezetése
    - Olvasás gyengébb
    - Olvasni tud több is
    - Írni csak egy, de akkor olvasni sem lehet
- Olvasási - shared - sl
- Írási - exclusive - xl
- Feloldás - u
- Olvasás előtt választhatunk, de az osztott hatékonyabb
- Két kizárólagos nem adható ki

#### Kompatibilitási mátrix
- Lehet tárolni a jogszerűséget

# EA 11 2021.11.23
...
## 8:30-tól

## Zárak
- Osztott zár erősebb, mint a kizárólagos
- Mert többet tilt
- Nem összehasonlítható is lehet

### Módosítási zár
- Olvasóból írásiba átmenetbe kerül be
- olvasásiból módosítási
- módosításiból írási

 . | S | X | U
---|---|---|---
 S | i | n | i
 X | n | n | n
 U | n | n | n

 - Csak az első kapja meg a felminősítés jogát
 - Nem lesz holtpont

## Növelési zárak
 
- Bizonyos írási-olvasási műveletek felcserélhetőek

- olvas, növel, ír = ezt tekinthetjük egy műveletnek

- ha több tranz is növelni akarja, annak a sorrendje felcserélhető

- incᵢ(x) - Tᵢ megnöveli az x elemet

- ilᵢ (x) - növelési zár
    - több ilyen lehet egyszerre
    - nem cserélhető egy tetszőleges írással, olvasással


 . | S | X | I
---|---|---|---
 S | i | n | n
 X | n | n | n
 I | n | n | i

 ## Zárási ütemező
 - Nem a programozó adja a zárakat és feloldásokat
 - SQL ütemező kér majd zárakat
 - Zár ütemező ad neki megfelelő zárakat
 - Tranzakció jön - nincs benne zárás
 - Ütemező első és második része a zártáblát használva beszúrja a zárakat
 - Ütemező I. része
    - beteszi a lehető leggyengébb zárakat
    - ha csak kizáró zár van, akkor nem kell a többi művelettel foglalkozni
    - ha többféle zár is van
        - akkor tudnia kell, hogy mire milyen zár van
- Ütememző II. része
    - Eldönti a zártábla alapján, hogy késlelteti vagy végrehajtja
    - Közben érkeznek új feladatok
    - Összefűződnek
- Zártábla
    - Adatbáziselem
    - Zárolási információ
        - Csoportos mód:
            - kiadott legerősebb zár van itt
            - csak egy ellenőrzés kell, nem kell minden kiadottra
        - Várakozik-e:
        - Lista:
            - Tranz.
            - Mód
            - Vár?
            - Tköv.
            - Köv.

## A zárfeloldás kezelése
1. Első beérkező első kiszolgálás
2. Elsőbbségadás az osztott záraknál
3. Elsőbbségadás a zárfelminősítésnél

## Adatbáziselemekből álló hierarchia
1. ...
2. Indexek adnak egy hierarchiát

### Mit lehet zárolni
- Ha b+ gyökerét zároljuk akkor ez egészhez nem férhet hozzá más
- Nagy adatok zárolása
    - kevesebb zárás kell
    - de más tovább kell várjon
- Kis elemeke
    - sok zár kell
    - sok trez. futhat egyszerre
- megenegedünk kicsi és nagy objektumok zárolását is
    - tábla, blokk, rekord
    - külön zár mehet mindegyikre
- Figyelmeztető zárak
    - S,X sima zár
    - figyelmeztető zár IS, IX
        - alacsonyabb szinten akarunk zárolni
        - addig amíg lejutunk arra a szintre ami kell nekünk


| . | IS | IX | S | X  
----|----|----|---|---  
 IS | i  | i  | i | n  
 IX | i  | i  | n | n  
  S | i  | n  | i | n  
  X | n  | n  | n | n  

# EA 12 2021.11.30

## Vizsga
https://people.inf.elte.hu/kiss/15ab2/13ab2osz.htm
- Itt van minta
- Másolás nem elég, fogalmazni kell és ábrákat rajzolni
- Esszét kell írni, példákat is kell adni, érteni kell, tudni kell
    - Mindent lehet használni

- Jövőhéten nincs ea

## Zárak
### Figyelmeztető zárak
- Nem kell a legfelső szinten zárolni, ha kisebb adatelemet akarok zárolni
- Sorrendben lehet kiadni a zárakat
    - figyelni kell a hierarchiát
    - feloldások sorrendje is fontos
- Kompatibilitási mátrix
    - Sor: ha van ilyen zár kiadva
    - Oszlop: megkaphatjuk-e ezt a zárat
    - nem minden zár hasonlítható össze
        - Mindennél erősebb **SIX**
            - olvas majd lehet, hogy ír
            - mindent tilt a mit az S vagy IX

| . | IS | IX | S |SIX| X 
----|----|----|---|---|---
 IS |*i* |*i* |*i*|*i*| n
 IX |*i* |*i* | n | n | n
  S |*i* | n  |*i*| n | n
SIX |*i* | n  | n | n | n
  X | n  | n  | n | n | n

- Csoportos mód szándékzárakon

| Szülőn ilyen zár van | A gyerek ily zárat kaphat |
| :------------------: | :------------------------ |
| IS                   | IS, S                     |
| IX                   | IS, S, IX,X, SIX          |
| S                    | S, IS                     |
| SIX                  | X, IX, SIX                |
| X                    | semmi                     |

- Szabályok
    1. A kompatibilitási mátrixnak megfelelően tegye a zárakat
    2. Először a gyökeret zárolhatja, utána megy lefelé
    3. Olvasási vagy szándékolt módba, akkor teheti, ha a szülőre már kirakta a megfelelő zárat
    4. Írási vagy szándékolt módba, akkor teheti, ha a szülőre irakta a figyelmeztető írási zárakat
    5. Kétfázisó protokollnak megfelelően kell zárolni
    6. Feloldás gyerektől szülő felé történik

### Insert, Delete esetben mi történik?
- Eddig csak update-et meg olvasást néztük
#### Insert
- Nem lehet rá zárat rakni, mert még nincs is
- Nem ismételhető olvasási problémát okozhat
    - Más eredményt ad, mert lehet pont beszúrtak egy új dolgot
- **Fantom** sorok - a még nem létező sorok
- Két tranzakció is be akar szúrni
    - Olvasási zárakat raknak, mert a létező dolgokat csak olvasni akarják
    - Beszúrás előtt a szülőt írási módba zároljuk, így a másik tranz.-nak várni kell
- B+ fa esetén a levél beszúrásához egészen a gyökérig zárolni kell, mert a szülőket is módosítani kell(het)
    - Nem kell az egészet zárolni
    - Ki lehet számolni, hogy milyen magasságig kell zárolni
    - Fa protokoll biztosítja a sorbarendezhetőséget
        - Gyökértől kezdve zárakat kell rakni
        - Elengedhetünk fentebbi záraz, ha lent rájövünk, hogy nem kell már
        - **Mászóka** módszer
            - Adott csomóponton eldöntjük, hogy az előző nem kell, elengedjük
            - Lezárjuk a kövi szintet
    - Gyerekeinek száma alapján és a kívánt művelet alapján látjuk, hogy lehet-e egyáltalán kettévágás azon a szinten


#### Fa protokoll szabályai
1. Első zárat bárhova teheti
2. Későbbiekben csak akkor rakhat egy csúcsra zárat, ha van zárja a szülőjén
3. Zárat bármikor fel lehet oldani
4. Nem lehet újrazárolni, csak akkor engedjük el ha tényleg nem kell már

## Zár nélküli ütemezés
- Időbélyeges módszer
    - beérkezés sorrendje határozza meg
    - ezzel ekvivalens ütemezést akarunk megtartani
    - időbélyegek szerint össze tudjuk hasonlítani
    - minden adatbázis elemnél nyílván kell tartani az utolsó Írás és Olvasás időbélyegzőjét
        - ha nem jó az új dolog akkor be kell avatkozni
- Érvényesítéses módszer
    - Committálás alapján van a helyes sorrend - végződés alapján sorrend
    - Ezzel ekviv. sorrendet akarunk megtartani

## Oracle konkurenciavezérlés
- Zárolásos módszert használ
    - Táblát vagy sort lehet zárolni
    - Az ütemező automat. kihelyezi a zárakat
    - Bizonyos zárakat ki lehet helyezni manuálisan
- Select vagy update esetén végig ugyan azt az adatot mutatja
- Egy teljes tranzakció összes lekérdezése az indulási állapotban látja az adatbázis
- Mód választás: sorbarendezhető, csak olvasás
- Ezek olvasási konzisztenciák
- Rollback segmenset használja ezekhez
- Blokkhoz bekerül, hogy mikor módosították utoljára, ha ez újabb, akkor a rollback-ből nézi a legújabb kisebbet
- Piszkos olvasás
- Nem ismételhető olvasás
- Fantomok olvasása
- Tranzakció elkülönítés

| . | ... |
|---| --- |
| nem olvasásbiztos |
| olvasásbiztos |
| megismételhető |
| sorbarendezhető |

`set tranzaction isolation levet serializable;`
- Ha nem túl hosszú és nem ütközik mással, akkor érdemes

`set tranzaction read only`
- ha mindenki olvas akkor nem kell konkurenciavezérlés
- pl adattárház

### Zárolások
- Tábla vagy sor zárolás
- Konkurens tranz. vagy commit vagy abort
- Ha commit-ált, akkor hibát is adhat, ha nem tudja sorbarendezni
- Kétfázisú zárat használ, felszabadítás csak a commit, abort, rollback után történik
- Zárak
    1. DML-zárak
    2. DDL-zárak is léteznek
- Időbélyegző
    - Sorszintű zárolás
    - Időbélyegzők
    - csak akkor vár két tanz. ha ugyan azt a sort módosítják
- Táblák szintjén
    1. row share - figyelmeztető olvasás
    2. row excludeive - figy. olv.
    3. share    - olvasás
    4. share row exclusive  - olvasás és alatta írás
    5. exclusive - kézzel is ki lehet rakni - olvasás
- Sima lekérdezés nem zárol semmit
- Insert, update, delete már zárol
- Felminősítés
    - Sorokra csak kizárólagos zár, nincs felminősítés
    - Táblára van felminősítés
    - Select for update - RS zár aztán lehet RX lesz belőle
- Zárak kiterjesztése
    - Sok sor zárolásánál auto. kiterjeszti az egész táblára
    - Oracle jelenleg ezt nem támogatja
        - Növeli a konkurencia szinkronizációját, holtpont veszélyt
    
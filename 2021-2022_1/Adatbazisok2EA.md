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
- Relációs adtmodell (táblaszerű kezelés)
- Objektum-orientált adatmodell (háttérben relációk is lehetnek)
- Logiakai modell (tények és szabályok, tény + szabály -> új tény)
- Félig struktúrált (XML, gráfos)

## Adatbázis-kezelő nyelvek
- DDL - adatdefiniáló nyelv (sémák...)
- DML - Adatkezelő nyelv (beszúrás, törlés,...)
- QL  - lekérdező nyelv
    - Deklaratív (SQL, kalkulus)
    - Procedurális (relációs algebra)
- PL/SQL - programozási szerkezetek + SQL
- Programozási nyelv beágyazás
- 4GL nyelvekű

## Több felhaználó
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
- Szoftver vagy hardverhiba esetén utolsó jó pont visszaállítása
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
- Titkosítani lehet az edatokat vagy a hálózati kapcsolatot

## AB-kezelő felépítése
- Lekérdezés feldolgozó
    - Szintaktika ellenőrzés
    - Táblák léteznek
    - Jogok ellenőrzése
    - Lek. opt. átértelmezése
    - Végrehajtási tervek készítése
    - Legjobb költségő kiválasztása
- Tranzakció-kezelő
    - Párhuzamos végrahajtást biztosít
    - (ACID)
- Tárkezelő
    - memóriába töltés
    - előre létrehozott indexek, nézettáblák,...
    - bonyolultabb lekérezések gyorsítása

## Adatb-kezelő felépítése
Alkalmazás  Lekérdezés              Sémaleírás
        \       /                       |
    Lekérdezés-feldolg.             Sémafordító
                    \               /
                Adatb-lezelő motor
                        |
                Állománykezelő

## Szintek
- Sémák és előfordulások
- Fizikai, logiaki, alkalmazások
  
- Fizikai adatfüggetlenség
    - A réteg módosítása ne látszódjon a felsőbb rétegekben

- Logikai függetlenség
    - Logiaki bővítésnél az alkalmazásokat nem kell újraírni

## Relációs adatmodell
### Edgar Frank Codd 12 szabálya
1. Egységes megjelenésű információ - táblázatokban
2. Garantált lokalizálhatóság szabálya - adatmodellnek megfelelően kell hivatkozni az adatra, Tábla,Sor,Oszlop egyértelműen meghatároz
3. A NULL értékek egységes kezelése - típusfüggetlen
4. A relációs modell alapján aktív online katalógust kell üzemben tartani - rendszertáblák is megvannak, SQL-el olvashatóak
5. A teljes körű "adatnyelv" szabálya - interaktív, appba élítve, kül. a lekérd. és az adatmódósító műv., lehessen tranzakció
6. A nézet frissítésének szabálya - nézettáblák használata, autómatikus frissítés
7. Mahgas szintű beszúrás, törlés, módostás
8. Fizikai adatfüggetlenség
9. Logikai adatfüggetlenség
10. Jóság (integritás) függetlensége - constraintek definiálása, ellenőrzése
11. Elosztástól való föggetlenség - alkalmazói szinten nem látszik, hogy elosztott az adatbázis, redundancia
12. Megkerülhetetlenség szabálya - ne hessen közvetlenől belenyúlni, csak a kezelővel lehessen módosítani

## Relációs adatmodell
- Relációsáma: R(A1,A2,...,An)
    - R - relációnév
    - Ai - attr.-, tul.-, oszlop név
    - Dom(Ai) - lehetséges értékek halmaza
**!!??????????????????!!**

- Jelölések:
    - t ∈ r esetén t sor (angolul: tuple - n-es)
    **!!??????????????????!!**

## SQL lekérdezés módostása
Structured Query Language  
Összetett lekérdezés felbontása, és külön optimalizálás.
- Egyzserű SQL
    - Kiválasztás
    - Többtábla
    - Halmazművelet
    - Átnevezés
    - 

## Relalg műveletek
1. ÚNIO, R ⋃ S, R,S azonos sáma, sorok halmaza
2. KÜLÖNBSÉG, R - S,  
3. DIREKT SZORZÁS, R × S, két tábla sémája nem egyezhet meg, átneveződik, nincs kétszer ugyan az az oszlop
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

## Származtatott műveltek
- Metszet
- Összekapcsolások
    - Téta : |X|_A=B  
        A szabály olapján kell összekapcsokólni
    - Természetes : |X|  
        Közös oszlop alapján összekapcsolás
    - Félig-összekapcsolás: |X  
        Az elsőből csak azok kellenek amihez van a másodikban
    - Külső összekapcsolás : |X|^O (Outter)  
        Mindent szeretnénk látni, ezért NULL párokkal bekerülnek a hiányzó dolgok (nem teljesen relációs művelet)


    - séma egyezzés r|X|s=r∩s
    - séma nem egyezzik r|X|s=r×s
- Osztás, hányados
- Monotonitás - sorok hozzáadásával növekedni fog.

# AB2 EA 2021.09.14

## Algebrai optimalizálás
**Cél:**
Legérdezések gyorsítása, a tábla specifikus paraméterek, statisztikák ismeretében, heurisztikák használatával.

## Lekérdezés optimalizálása
- SQL lekérdezés
1. elemzés
- Elemző fa
2. Átalakítás
- Logikai lekérdező terv
3. Szabályok alkalmazása
    - algebrai optimalizáció
- Javított logikai lekérdező terv
4. Várható métretek becslése
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
2. Rendszertáblákból ellenőrizve vannak, hogy léteznek-e a táblák, megfelelő típúsok vannak, meg vannak a jogosultságok, stb..
3. Elemzőfából lehet REL-ALG fát csinálni
    - '\<tuple> IN \<query>' ezt még át kell alakítani
    - \<table> × \<query> majd σ_('x in y' -> 'x = y.x')
    - lehet theta joint a szorzás helyett
4. Ezeket a műveleteket végrehajtási szinten is lehet optimalizálni

## Algebrai optimalizálás
- **Cél:** gyorsabb kiszámítás
- **Költségmodell:** költség arányos a méretekkel, lehetne bonyolultabb kölségeket is kiszámolni (mienk alap szintű)
- **Módszer:** művletei tula. alapján ekviv. átalakítás
- **Az eljárás heurisztikus**, nem valódi méretekkel számol
- **Az eredmény nem egyértelmű:** Az átalakítások sorrendje nem determinisztikus, de általában jobb költségű
- **Megj.:** Az SQL sokkal bővebb, de most klassic. alg. kif. lesznek.

- kifejezést gráffal ábrázoljuk
- **Kifejezésfa:**
    - nem levél csúcs
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
5. Kiválasztás és vetítés felcserálhetősége
6. Kiválasztás és szorzás felcserélhetősége
7. Kiválasztás és egyesítés felcs.
8. Kiválasztás és kivonás frlcs.
9. Kiválasztás és természetes összekapcsolás felcs.
10. Vetítés és szorzás felscs.
11. Vetítés és egyesítés felcs.
- Nem minden cserélhető pl: Vetítés és kivonás nem cserélhető fel

## Heurisztikus elvek
1. Minnél hamarabb szelektáljuk
2. Össszekapcsolások jobbak mint a szorzások
3. Unáris műveletek összevonása
4. Keressünk közös részkifejezéseket

## Optimalizáló algoritmus
1. A kiválasztásokat bontsuk fel (4)
2. A kiválasztást mélyebbre visszük (4-9)
3. A vetítések is mélyre (3,5,10,11)
4. Műveltek összevonása (3-5)
5. Bináris műveltek csoportosítása, egy-egy művelte egy csoportban.
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
- Eddig logiaki terv volt
- SQL lekérdezésből lesz egy terv
- "Explain Plan" ablak
- Műveletek közül próbál jobb költségűeket keres (nem a legjobbat, csak kb)
- blokk műveletek száma a mártákegység
- minden műveltre ki kell számolni a költségeket
    - jobb költségű sorozatot kell választani
    - műveletsorozat
        - kövi művelet költsége az előzőtől függ
- Méreteket és futási időkel kell összehasonlíthatni

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
    - Végrahajtás
- Eredmény

## Miért jó?
- Ez egy általános módszer
- Mi lehet tudunk speckó infókat amivel jobb végrahajtást tudunk adni
- Ha megértettük, akkor lehet javítani

## Indexelés
- Célok:
    - gyors lekérdezés
    - gyors adatmódosítás
    - minnél kisebb tárhely
    - (hálózati forgalom optimalizálás, stb)
- Nincs általános legjobb optimalizáció. A célok egymás ellen dolgoznak
- Adatbázis lehet
    - statikus (ritkán módosul, komplex lekérdezések) - pl.: adattárház
    - dinamikus (sok módosítás, egyszerű lekérdezések) - pl.: bank fálhasználói rendszere
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
            - ezt nem akarjuk viszgálni, ezért feltesszük, hogy minden konstansból ugyan annyi van
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
    - Utolsó blokkot kell beolvasnni és beleírni: 2 művelet
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
- Akkor jó a ha nem fögg attól hogy melyik blokk milyen hosszú
- Adatok eloszlásához lehet állítani a hasító függvényt
- blokkláncok egyforma hosszúak legyenek, blokklánc B/K blokkból álljon
- Keresés A=a:
    - Túl nagy K sem segít
    - Túl kicsi sem biztos hogy jó
- Beszúrás
    - Blokk telítódik, akkor hozzáláncol egy újat
- Módosítás:
    - 1 keresés + 1 írás
    - ha a hasító érték módosul akkor átkerül
- Törlés:
    - Láncon előrébb lehet vinni, de felesleges lassítás lehet
- Intervallumos keresésre nem jó, egyenlőségre épül fel

- Dinamikus hasítás
    - kiterjesztjóhető
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
        - teljes fa lenne a jó, ki kell egyensújozni
        - virtuálisan kiegészítjük a fát
    - Kosár kódokat számon kell tartani
        - ha egyiknek nő a hossza, akkor fel kell venni az összes olyan hosszú kódszót
        - ha két külön direktori bejegyzés van, de csak egy blokk akkor ugyyan arra mutatnak (csak virtuális szétbontás)

- Lineáris
    - több blokkból álló kosarak
    - komplexebb feltétel
    - telítettség alapján van szétbontva
    - pl.: kosarak átlagos mérete
    - kosarak csoportosítva a végződéseik alapjána (postfix)
    


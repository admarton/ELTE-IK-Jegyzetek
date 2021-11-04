# Mesterséges Intelligencia Konzi 2021.09.09


## Követelmény
- Aszinkron online + hibrid konzultáció
- Heti tesztek 75%-a min 75%
- Canvason
    - Kurz. info
    - Videó linkek
    - Heti teszt kvízek
    - Fórum
- Vizsga
    - oldalon van minta
    - online vizsgánál heti kvízhez hasonló

## MI és sci-fi irodalom
- Vannak hívők
- Vannak szkeptikusak - MI tagadók
- Több MI terület bemutatása
    - Heurisztikus keresések a ma is használtak
    - A többi régi dolog már nem divatos
- Isac Asimov - A fiú legjobb barátja (Robottörténetek) 1974
    - Robot kutya helyett kap egy rendes kutyát
    - Mi az MI? - Turing teszt - Kínai szoba teszt az ellentéte
    - Kit érdekel, hogy mi az MI, én szeretem! - Mondtaje a kisfiú.
- Isac Asimov - Igaz szerelem (Robottörténetek) 1977
    - Egyszerű szűrésekkel keresi az MI a barátnőt a programozónak.
- Stanislaw Lem - Elektrubadúr (Kiberiáda) 1965
- Isac Asimov - Robot álmok (Robot univerzum) 1986
    - Az álmáról kikérdezi
    - Egy ember felszabadítja a robotokat
    - (Az ember a robot aki a felszabadító)
    - Ezért lelövik


# Mesterséges Intelligencia EA 2021.09.09
### Bevezetés 1

## A mesterséges intelligencia nem részterülete az informatikának
- nem egy feladat megoldásával foglalkozik
- adatbázisok : nagy adat tárolás
- ford. prog : hogyan lehet gépi kódot csinálni
## MI inkább szemlélet
- Ha az embert jobbnak látjuk egy feladatban, akkor MI-vel próbálkozunk.
- Az if-then-else elágazás is MI projekt mentén jött létre
- OOP is MI projekt mentén jött létre
- Gondolkodási, kutatási előörs
- Megoldhatatlannak tűnő problémát próbál megoldani és ementén létrejönnek hasznos technológiát
## MI kutatók csoportjai
- Erős MI
    - Szélsőséges Redukció
        - Elemi részekre bontás
        - Azok jellemzése
        - Kapcsolataik jellemzése
        - Így minden pontosan leírható és megérthető
    - Church-Turing tézis
        - Adott folyamatot kellő pontossággal le tudunk írni, úgyhogy mindenkinek egyértelmű legyen, akkor az algoritmussal is leírható
    - Ha az emberi intelligenciát részekre tudjuk bontani és kellő pontossággal le tudjuk írni, akkor algoritmizálható
- MI szkeptikusok
    - A számítógép sohasem lesz okosabb az embernél
- Gyenge MI - Közép csoport - Technokrata, mérnök szemlélet
    - Probléma megoldásához sokszor mesterséges intelligencia szerű megoldások jönnek lére
## MI története
- 1956. Nyara - Deklarálták az MI létrejöttét
    - Kutatási irány elindult
    - Az emberi gondolkodás számítógépes reprodukálása
- Romantikus kor (60-as problémák)
    - Mindenféle problémát megpróbáltak megoldani MI-vel
    - Sakkprogramokkal mérték az MI fejlettségét
    - Mesterséges neuronhálók -\_
    - Evolúciós algoritmusok  -/ \- nem voltak a gépeken sikerek
    - Bukások:
        - Gépek gyengesége
        - Kombinatorikus robbanások
            - Nem fért be memóriába, túl sokáig tartott kiszámolni
            - Túl bonyolult problémákat próbáltak megoldani
        - Általános megoldásokat akartak
            - Nem építették bele a heurisztikát(aktuális feladat speciális dolgait)
            - angol-orosz fordító program
                - sok pénz volt
                - kudarc lett
                - konteksztust nem tudta
                - szótárak alapján dolgozott
                - túl általános lett volna
    - 1958. LISP
    - 1966. ELIZA beszélgető program
        - Nem rosszabb mint egy mai chatbot
        - Egyszerű, de mégis egész jó volt
        - Tanult a beszélgetésből
        - Próbálta fenntartani a beszélgetést
        - Fontos részei:
            - Minta-válasz párok:
                - Ha illeszkedett, akkor az alapján válaszolt!
                - Tanuló komponens kiegészítette
            - Ismétlés felismerése
                - Eltárolta az egész beszélgetést
                - "Miért ismételgeti önmagát?"
            - Folytatási szabályok
                - Ha nem tudott mit mondani
                - "igen, értem", "kérem, folytassa", stb
        - Hasonlít a pszijáterekre:
            - lett DOKTOR verziója
    - 1966. GPS(general problem solving), rezolúció(elsőrendű logiki gondolatok)
- Klasszikus kor
    - Speciális módszerek használata a speciális feladatokra
    - SHRDLU 1972
        - chatbot
        - de csak idomokról lehetett beszélgetni
        - így sikeresebb lett volna
        - 6-7 éves gyerek szintje
    - BACON
        - Fizikai szabályok keresésére használták
        - Mérési adatsorok között stabil összefüggés keresése és kifejezés létrehozása
    - AM
        - Matematikai állításokat keresett logikai állítások alapján
        - Prím számok fogalmát kereste
        - Két általános fogalmat összeéselt
        - Két szigorút szét vagyolt
        - Így keresett izgalmas szabályokat
    - DENDRAL 1969-1978, MYCIN 76
        - szakértő
        - Tünetek alapján betegség 
    - heurisztikus keresés
    - tudás reprezentáció
    - prolog
- Ipari kor
    - kilép a kutatási térből
    - bekerül az iparban
    - szakértő rendszerek
    - XCON 1982
        - pc konfig. összeállításnál használták
    - PROSPECTOR 1979
        - Bányászati keresés műhold alapján
        - próbafúrások helyét adta meg
    - Shell-ek (IDE) amivel szakértő mi-ket lehetett csinálni könnyebben
    - tudás-alapú tech.
    - nem-klasszikus következtetés
    - bizonytalanság kezelése
- MI tél
    - befektetők elfordulnak
    - sok idő a szakértő rendszer elkészítése
    - elavul a hardver amíg elkészül
    - befektetők internetre térnek át
    - kutatások leállnak
- Előkerülnek régi dolgok az új hardvereken
    - Sokkal jobban működnek
    - Mesterséges neuronhálók
    - Gépi tanulás
    - Adattudomány
    - Hibrid dolgok
    - Deep Blue 1997
        - Legyőzi a sakkvilágbajnokot
        - Nem okosabb a régieknél
        - Csak a vas erősebb alatta
    - IBM Watson 2011
        - kvízműsorban vert meg embereket
    - Megint jönnie kéne egy leszálló ágnak, de még nem látszik

# Mesterséges Intelligencia EA 2021.09.09
### Bevezetés 2
Mérő László - jó könyvek a témában

## Van-e benne MI?
1. Megoldandó feladat
    - Nehéz feladatok, még embernek is
    - Sakk, Go, kell a kövi még nehezebb
    - Orvosi diagnózis
    - Olyan terület, ami olyan problémákkal foglalkozik amit nem lehet számítógéppel megoldani
    - Számológép (60-as években cirkuszban fejszámoló)
    - Nagy a problématér
        - Utazó ügynök problémája
            - Városok bejárása
            - 5 város
            - Hamilton-kört kell találni
            - Összes megoldás feltérképezése és a legjobb választása
            - Az összes lehetséges út a **problématér**
                - ennek a mérete most n városra (n-1)! 
                - 5 város 24 út
                - 51 város 6.10⁶² //nagyon sok
        - Feladat megoldásához a problématérben keresünk egy bizonyos megoldást
    - Brute force nem ad megoldást
    - Ötlet, intuíció kell, **heurisztika**
        - Utazó ügynök
            - ugyan azok a városok között ugyan az lesz a legjobb út
            - új infók felvétele
                - megoldás halmaz helyett valami jobb szerkezet
                - szomszédos elemek felcserélése
            - könnyebb kb jó megoldást találni
        - több ötlettel is meg lehet próbálni és a legjobbat kiválasztani
2. Szoftver viselkedés
    - intelligens
    - Turing teszt
        - Független bíró
        - Ember és robot azonos interfacen keresztül kommunikál
        - Ha a bíró nem tudja megkülönböztetni az embert és a gépet, akkor átment
        - Ennek ellentéte a Kínai szoba elv
    - Intelligens szofver jellemzői
        - megszerzett ismeret tárolása
        - autómatikus következtetés
        - tanulás
        - term. nyelvű kommunikáció
        - manapság + gépi látás
    - Általános mesterséges vagy speciális feladat megoldása jól
3. Felhasznált tech.
    - sajátos tech. jellemző rájuk
    - spec. repezentáció, modellezés
    - heurisztikus algoritmusok
    - gépi tanulási módszerek

# Mesterséges Intelligencia EA 2021.09.09
### Bevezetés 3

## Modellezés és keresés bev.
- Útkeresési problémára vezetjük vissza
- Gráf reprezentáció
- Modellezési teknikák
    - Allapottér modell
    - Probléma redukció
    - Peobléma dekomp.
    - Korlátprogramozás modellje
    - Logikai reprezentációk
    - Valószínűségi hálók
- Keresések
    - Lokális keresések
    - Visszalépéses keresés
    - Gráfkersések
    - Evolúciós algoritmusok
    - Játékfa kiértékelő módszerek
    - Logikai következtetések
    - Bizonytalanság kezelés

## Modellezés fókusza
- problématér a központban
- heurisztikák beépítése
- hasznos ill. haszontalan elemek
- kiinduló elemek
- szomszédsági kapcsolatok
- adott pillanatban lehessen rangsorolni

## Útkeresési probléma
**Def.:** Útkeresési probléma az, amelynek megoldása megfeleltethető egy *élsújozott irányított gráfbeli*
    - *csúcsnak* (célcsúcs)
    - *útnak* (startcsúcsból célcsúcsba, esetleg a legolcsóbb)

Ez a gráf (δ-gráf) lehet végtelen nagy, de
- *csúcsainak kifoka véges*
- *élei súlyának van konstans globális pozitív alsó korlátja* (δ)

## Gráf fogalmak
| Fogalom               | Jelölés |
| :-----                |  :----: |
| csúcsok               | N |
| irányított élek       | A⊆N×N |
| él *n*-ből *m*-be     | (n,m) ∈ A (n,m ∈ N) |
| n utódai              | Γ(n) = { m ∈ N \| (n,m) ∈ A} |
| n szülei              | π(n) ∈ Π(n) = { m ∈ N \| (m,n) ∈ A} |
| irányított gráf       | R = (N,A) |
| véges sok kivezető él | \|Γ(n)\|<∞ (∀n∈N) |
| élköltség             | c:A→ℝ |
| δ-tulajdonság (δ∈ℝ⁺)  | c(n,m) ≥ δ > 0 (∀(n,m)∈A) |
| δ-gráf                | δ-tulajdonságú, véges sok kivezető élű, élsúlyozott irányított gráf |
| irányított út         | α = (n,n₁),(n₁,n₂),...,(nₖ₋₁,m) <br/> = <n, n₁, n₂,..., nₖ₋₁, m>
| ... út csúcshalmazba  | n ⟶^α m, n⟶m, n⟶M (M ⊆ N) |
| ... összes út halmaza | {n⟶m}, {n⟶M} (M ⊆ N) |
| út hossza             | az út éleinek száma: \|α\| |
| út költsége           | c(α)=c^α(n,m):=∑ᵢ₌₁...ₖc(nᵢ₋₁, nᵢ) |
| opt. költség          | c*(n,m):=min(c^α(n,m)) (α∈{n⟶m}) |
| opt. költségű út      | n⟶*m:=min_c{ α \| α∈{n⟶m} } | 

## ÉS/VAGY gráfok
- R = (N,A) élsúlyozott irányított hipergráfok (egy él 2-nél több csúcsot is összeköt)
    - N a csúcsok halmaza
    - A ⊆ { (n,M) ∈ N×N⁺ | 0 ≠ |M| < ∞ >} a hiperélek halmaza
    - |M| a hiperél rendje
    - c(n,M) az (n,M) él költsége
- Egy csúcsból véges sok hiperút
- 0 < δ ≤ c(n,M)

- hiperút:
    - egy csúcsból csúcsok sorozatába vezet
    - egyértelmű haladási irány
    - véges részgráf
    1. M csúcsaiból nem indul hiperél
    2. M-en kívüli csúcsokból pontosan egy hiperút indul
    3. a hiperút minden csúcsa elérhető az *n* csúcsból egy közönséges irányított úton
- megoldás gráf:
    - s⟶M hiperút
    - s startcsúcs
    - M célcsúcsok sorozata

## Hiperút bejárása
- Az első sorozat <n>
- C sorozatot a Cᵏ←ᴷ sorozat követi, amiben a *k* helyére *K* kerül, ahol k⟶K a hiperút által tartalmazott hiperéllel
- Így egy hiperutat közönséges irányított útként foghatunk fel, de nem egyértelmű, mert lehet több bejárása is

## Gráfreprezentáció fogalma
- Minden útkeresési probléma rendelkezik egy gráfreprezentációval, ami egy (R, s, T) hármas:
    - R=(N,A,c) a reprezentációs gráf (δ vagy ÉS/VAGY)
    - s ∈ N, startcsúcs
    - T ⊆ N, célcsúcsok
- és a probléma megoldásával:
    - t cél vagy <t₁,...,tₘ> célcsúcssorozat megtalálása vagy
    - s⟶t vagy s⟶<t₁,...,tₘ> esetleg egy optimális s⟶*T út megtalálása

## Útkeresés δ-gráfban
Algoritmus, ami elindul a **kezdeti aktuális csúcsból** és minden *nem-determinisztikus* módon új aktuális csúcsot *választ* (gyakran az akt. gyerekei).  
Ezeket a lépéseket tárolja, de felejthet is (memória spórolás).  
Megáll, ha célcsúcsot talál vagy tudja hogy nem lesz meg.  

## Útkeresés ÉS/VAGY gráfban
Visszavezetés δ-gráfos megoldásra.
A startból induló hiperútak bejárásai δ-gráfot alkotnak.
- Csúcsai az eredeti gráf csúcssorozatai
- Startcsúcs az eredti g. startcs.-ból álló sorozat
- Célcsúcsai az e. g. célcs.-ból álló sorozat

## !!HUH!! ##

# Konzi 2021.09.16

## δ-tul. 
- Kizárjuk azt hogy a végtelen hosszú út legyen a legrövidebb
- Általában magától adódik ez a tulajdonság
- nem végtelen feladatban sem lesz végtelen kifok
- súlyok alsó korlátja általában műveleti költségből jön
    - annak van minimuma általában
- gráf lehet kb végtelen nagy is

## ÉS/VAGY gráf
- Közönséges gráfnak megfeleltethető
    - át lehet alakítani
- ÉS él a hiperés
- VAGY él a sima él
- Hiperutak rendes utakká lesznek alakítva
- Hiperút bejárása szekvenciával
- Az átalakítás sok idő lenne
    - ezért az útkeresőbe kell beépíteni az átalakítást
- pl
    - a -+-> b
    - a -+-> c
    - < a > -> <b,c>
- átalakítás nagyobb problémát csinál
    - egyszerűsíteni kell
    - egy hiperút minden bejárása felesleges
    - általában elég néhány bejárása
    - Hamis bejárások is belekerülhetnek
    - Célcsúcsból kiinduló utakat el lehetne hagyni, felesleges
    - Irányított fát jobb építeni, mint gráfot

# 2.előadás ~2021.09.17

## Modellezés fontos
- Állapottér modell
    - fontos teknika
    - felvehető állapotok halmaza
    - invariáns állítássokkal lehet szűkíteni
    - műveletekkel lehet egyik állapotból a másikba jutni
    - kezdőállapot(ok)
    - célállapotok
    - feladat:
        - műveletsorozat amivel a kezdőből a célba jutunk
    - irányított gráffal reprezentálható
    - éleknek lehet súlya, ha nincs akkor egységnyi
    - feladat megoldásához útkeresési algoritmus
    - pl.: Hannoi tornyai
        - adatszerkezet pontosságig kell vinni a modellezést
        - pl lehetnek vermek
        - lehet a korongok helyzete is
        - Állapottér:
            - tömbök sorozata
        - művelet:
            - honnan hova kell rakni, korong egyértelmű lesz
        - nagy a problématér
    - pl.: n-királynő
        - állapottér: {királynő, _}ⁿ×ⁿ
        - művelet:
            - áthelyez(x,y,u,v)
        - hatalmas problématér
        - tetszőlegest start állapot
        - megoldás a célállapot

## Reprezentációs gráf bonyolultsága
- repr. gráf -> problématér -> keresés számításigénye
- Start csúcsból kivezető utak száma
- minél kisebb problématér kell
    - akár az állapottér bővítéssel is lehet javítani
    - műveletek előfeltételének szigorítása
    - pl.: n-királynő
        - üres tábláról indul
        - felhelyez királynőket
        - csak sorról sorra lehessen felrakni
        - ha már ütés van akkor ne lehessen többet felrakni
        - művelet: helyez(oszlop)
            - a sor egyértelműen jön
            - előfeltétel ellenőrzések

## Műveltek
- műveletek hatékonysága befolyásolja a keresés időtartamát
- invariáns szigorítás
- adatok számon tartása az állapotokban
- pl.: n-királynő
    - állapot: rec(t:{királynő, X, _}ⁿ×ⁿ, köv_sor:ℕ)
    - cél már csak annyi hogy az összes soron végigmentünk

## Tologatós játék
- csempéket kell tologatni (8-as, 15-ös)
- kezdőállapot bármi lehet
- célállomás a mérettől függ (8->körben, 15->sorfolytonos)
- állapotok: mártix
    - rec(m:{0..8}^3×3, üres:{1..3}×{1..3})
- művelet:
    - "üres hely eltolás", kevesebb művelet, mint az összes lap eltolása
    - Tol(irány)
        - nem szabad kitolni
- sok kör és út

## Visszafelé haladó keresés
- meg kell találni aztán át kell fordítani
- nem minden célból lehet visszajutni
- kétirányú élek kellenek
- ha ezek nem állnak fenn akkor probléma redukció kell
    - állapot halmazok
    - megelőző állapothalmazt kell kiszámolni
    - el lehet jutni a startig
    - redukciós operátor kell:
        - hogyan lehet létrehozni a megelőző állapothalmazt
    - redukciós operátor sorozat a célból a startba és abból visszaforgatás

## Probléma dekompozíció
- Részproblémák megoldása
- általános probléma leírása
- kiinduló probléma
- egyszerű probléma
- dekomponáló operátor
- ÉS/VAGY gráffal ábrázolható
- pl.: Integrál számítás
    - összeg szétválasztása
    - konstans kiemelés
    - alap integrál levezetés
    - parciálás szabálya

# MI Konzi 2021.09.23

## Tervgenerál modell
- Kockavilág
    - Robotkar tud kockákat felvenni, letenni és mozgatni
    - állapotokhoz szükséges állítások
        - on(x,y) - rajta van
        - clear(x) - teteje üres
        - ontable(x) - azstalon van
        - handempty - robotkar szabad
        - holding(x) - robotkar tartja az x kockát
        - predikátum szimbólumok - nulladrendű logikához vezet
    - elemi állítások konjungciója az állapot
    - konkrét és általános leírás
    - teljes és hiányos leírás
    - ellentmondást nem kellene tartalmazzon
    - műveltek
        - pickup(x)
            - előfelt. - P: ontable(x), clear(x), handempty
            - törlés lst - D: ontable(x), clear(x), handempty
            - bővítés lst - A: holding(x)
        - putdown(x)
            - P: holding(x)
            - D: holding(x)
            - A: ontable(x), clear(x), handempty
        - stack(x,y)
            - P: holding(x), clear(y)
            - D: holding(x), clear(y)
            - A: on(x,y), clear(x), handempty
        - unstack(x,y)
            - P: on(x,y), clear(x), handempty
            - D: on(x,y), clear(x), handempty
            - A: holding(x), clear(y)
        - a P,D,A meghatározza az új állapotot
        - ha tezdetben teljes és ellentmondásmentes volt akkor ezek is ilyeneket generálnak
- Program generálás modellezés
    - változó értékének megváltoztatása
    - cont(v,e) - v tartalma e
    - Start: cont(X,A), cont(Y,B), cont(Z,∅)
    - Finnish: cont(X,B), cont(Y,A)
    - értékadás: (u:=v):
        - assign(u,e,v,f):
            - P: cont(u,e), cont(v,f)
            - D: cont(u,e)
            - A: cont(u,f)

- Probléma Redukciós modellezés
    - célból a startba, de nem invertálható műveletek
    - tud hiányos leíráson is működni
    - ha L nincs a művelet D,A-ban akkor benne van az előző lépésben
    - ha L csak A-ban van akkor előző lépésben `true`
    - ha L a D-ben benne van akkor előzőben `false`
    - ha van egy állapotban `false` akkor az zsákutca, nem valid állapot
    - irányított gráfot kapunk

- Probléma dekompozíció
    - kevésbé általános
    - on(A,B), on(C,D)
        - két rész külön megoldása
        - stack(A,B) // C,D
        - két feltétel: 
            - holding(A) // C
                - pickup(A) // C
                - feltételek
                - stb...
            - clear(B) // D
    - szekvenciálni is lehet
        - az első ág a startból indul (startba akar dekomponálni) -> T1
        - a következő ágak az előző ág végállapotából indul ( T1(start)-ba akar dekomponálni) 
        - és így kb sorba lehet fűzni
        -visszalépéses keresés
    - Összefésülés
        - vagy párhuzamosan hajtja végre az ágakat
            - ha van olyan erőforrás, amit minden használ akkor ez nem lehetséges (pl egy robotkar a kockavilágban)
            - vannak műveletek amik párhuzamosak lehetnek
        - vagy úgy fésüli össze, hogy műveleteket rak hozzá vagy elvesz
            - visszalépéses keresés
    
# EA 3 2021.09.26

## Kereső Rendszer (KR)
```sql
Procedure KR
1. ADAT := kezdeti érték
2. while ¬terminálási feltétel(ADAT) loop
3.   SELECT SZ FROM alkalmazható szabályok
4.   ADAT := SZ(ADAT)
5. end loop
end
```
- Globális munkaterület
    - irányított gráf része
    - start csúcs
    - teminálási feltétel
    - a megtartandó adatokat tartalmazza
- Keresési szabályok
    - előfelt., hatás
    - megváltoztatja a globális munkaterületet
- Vezérlési stratégia
    - melyik szabály legyen végrehajtva
    - heurisztika ide van beépítve

## Vezérlési strat.
1. Általános
    - nem függ a feladattól, modelltől, modellezéstől
    1. Nem módosítható
        - Mindig ugyan úgy, programozó visszatérhet és dönthet máshogy
        - *lokális keresések*
        - *evolúciós algoritmusok*
        - *rezolúció*
    2. Módosítható
        - Korábbi rossz lépést máshogy csinálhat
        - *visszalépéses keresés*
        - *gráfkeresés*
        - *szabályalapú köv.*
2. Modellfüggő
    - adott modellezési technikához kapcsolódik
3. Heurisztika
    - Megoldó algoritmusba épül be

## Lokális keresések
- A probléma reprezentációs gráfjának csak kis részét tárolja
- Kezdetben a startcsúcsot ismeri
- akkor áll meg ha a célcsúcs megjelenik a látómezőben
- helyi csúcsok helyébe a szűk környezetéből választ újakat, "jobbakat"
- kiértékelő függvény (cél-, rátermettségi-, heurisztikus függvény) dönti el, hogy mi a "jobb"

### Hegymászó keresés
- Akt csúcs, szülő csúcs van tárolva
- Startból indul
- Célba vagy zsákutcába jut
- Akt csúcsot a gyerekére cseréli
- Azt a gyereket választja amelyik a legjobb és nem szülő
- Van olyan, ahol rosszabbra sem lehet lépni
- Memóriában kevés dolgot tárol, végtelen ciklusba kerülhet
- Hanoi tornyain lehet használni
    - Fgv min összeget keres
        - Start 3+3+3
        - Cél 1+1+1
        - Legjobb felé lép
```sql
1. akt := start
2. while akt ∈ T loop
3.   akt := arg opt_f(Γ(akt)-π(akt))
4. end loop
5. return akt
```
- Γ(akt) ~ akt gyerekei
- π(akt) ~ akt szülője
- arg opt_f rész kibővítve
    - `if Γ(akt) = ∅ then return 'ne talált megoldást'`
    - `if Γ(akt) = {π(akt)} then akt := π(akt)`
    - `else akt := arg opt_f(Γ(akt)-π(akt))`

- A keresési algoritmus nem sokat lát a gráfból
- köröket nem lája
- Fává egyenesedett gráfot "lát"
    - duplikátumok jönnek létre

- Künnyű implementálni
- Csak jó fitnessfüggvény esetén lesz hasznos
    - újra lehet indítani egy másik véletlenszerű csúcsból
        - **random restart locak search**
    - k akt csúcsa legyen é k legjobb gyereket választjuk
        - **local beam search**
    - a mohó stratégián enyhítünk - nem mindig az akt legjobb kell
        - **simulated annealing**
    - végtelen ciklus elkerülhető néhány megelőző lépéssel 
        - memória növeléssel
        - **tabu search**

### Tabu keresés
- tárolva:
    - akt - akt csúcs
    - Tabu - utoljára érintett néhány csúcs
    - opt - az eddigi legjobb
- Ha az opt célcsúcs vagy régóta nem változott vagy zsákutca van, akkor van vége
- Minden lépésben akt gyerekét választja, tabu és opt frissül
- Tabu halmazon kívüli gyereket választ
```sql
1. akt, opt, tabu := start, start, ∅
2. while not (opt∈T or opt rég nem változik) loop
3.   akt := arg opt_f(Γ(akt)-tabu)
4.   tabu := Módosít(akt, tabu)
5.   if f(akt) jobb, mint f(opt) then opt := akt
6. end loop
7. return akt
```
- Hanoi tornyai
    - két elemű tabu halmaz
    - már megoldja a (2,2,2)-ből
- Tabu méreténél kisebb köröket elkerüli
    - Repr. gráfról kell infó
    - vagy sok kísérletezéssel
- Zsákutcával itt sem lehet mit kezdeni

### Szimulált hűtés algoritmus
- Ne legyen mohó a stratégia
- véletlenszerűen választ és megvizsgálja
    - ha a heurisztikája viszonylag jó akkor elfogadja
    - általában, ha jobb vagy ha nem sokkal rosszabb
    - e^(f(akt)-f(új))/T > random[0,1]
    - T-t lehet állítani, szabályozható működés
- Hűtési ütemterv
    - Lépésenként más T-t használ
    - szig mon csökk - kezdetben inkább elfogadja a rossz csúcsot
- Azért ez a neve, mert
    - Grafikont rajzolva monoton cökken, de van ahol nő (az elején inkább)
    - Optimális kristály szerkezetre hozni egy folyadékot
        - ott is kellenek visszamelegítési szakaszok
        - az elején nagyobbak, később kisebbek
```sql
1. akt := start; k := 1; i := 1
2. while not (opt∈T or opt rég nem változik) loop
3.   if i>Lₖ then k := k+1; i := 1
4.   új := select(Γ(akt)-π(akt))
5.   if f(új)≤f(akt) or
        f(új)>f(akt) and e^(f(akt)-f(új))/T > random[0,1]
6.      then akt := új
7.   i := i+1
8. end loop
9. return akt
```
- Gráfszínezés feladata
    - gráf csúcsait osztályozzuk
        - osztályon belüli tagok között ne legyen él
    - minél kevesebb osztály kell
    - Állapotok:
        - gyengített osztályozás
        - erősíteni kell, meg kell találni a legjobbat
    - Műveletek:
        - osztályból egy csúcsot egy másikba rakunk
    - Kezdő áll.:
        - tetszőleges
    - Céláll.:
        - legjobb osztályozás
    - Áll.-gráf:
        - Exponenciális az eredeti gráfhoz képest
    - Kiértékelő függvény:
        - Annál jobb minél több van az első pár osztályban
        - Minél kevesebb él van egy osztályon belül
        - f(n) = ∑ⱼ wⱼ(λ|A(Oⱼ)| - |Oⱼ|)

## Lokális keresés
- Adott rossz döntés végzetes lehet
- Erősen összefüggő gráfban és erős heurisztikával rendelkező gráfban jók ezek
- Heurisztika nélkül esélytelen
    - mert kevés infó van eltárolva

## Heurisztikák hatása a KR működésére
- Heurisztika fogalma bizonytalan
    - feladathoz kapcsolódó ötlet
    - algoritmusba építjük
    - általában egyszerre javítja a futási és memória igényt
- nehéz jó heurisztikát találni
- iterációs lépések száma és egy lépés költsége határozza meg
- nem jó a túl sok heurisztika sem
    - túl sok lesz egy iterációs lépés értéke
    - átlagos mennyiség kell

- heurisztika találás
    - 8-as játék jó heurisztikái:
        - Rossz helyen levő lapkák száma (**W**)
            - min hány mozgatás kell
        - Manhattan heur. (**P**)
            - Lapkák Manhattan-távolsága a helyüktől
        - Keret, frame (**F**)
            - bűntetőpontok
            - +1 pont, ha a szélén van és nem a helyén
            - +2 ha sarokban van, de nem a helyén
    - Hannoi tornyai heurisztikák:
        - Darab **C** = ∑1 ha nem a megfelelő
            - mennyi van a megfelelőn
        - Súlyozott darab **WC** = ∑i ha nem ...
            - nagyobb korongot nehezebb átrakni
        - Összeg **S** = ∑ this[i]
        - Súlyozott összeg **WS** = ∑i*this[i]
        - Módosított összeg **EWS** = WS - magic
            - bűntető és jutalom pont
            - csökken ha a korongok növekvő sorrendben vannak a célhoz *-1*
            - növeljük ha olyan torony van ahol hiányzik egy közbenső torony *+2*
    - Fekete-fehér kirakó
        - feketék és fehérek kicserélése
        - állapottér:
            - tömb: fekete, fehér, üres hely
            - üres hol van
        - start : [B, ..., B, W, ..., W, _]
        - műveletek
            - üres tol jobb-bal
            - üres ugrik jobb-bal
        - heurisztika
            - inverziószám
                - min hány csere kell
            - mod inv.
                - *teknika*: meglévő súlyozása, büntető pontrendszer
            - 

# Konzi 4 2021.09.30

## Heurisztika teszi megoldhatóvá
- De nem garantált
- Becslések a hátralévő útra
- Milyen a jó heurisztika?
    - Lokális információkkal dolgozik
    - Relatív korrekt
        - Célhoz közelebbi csúcsnak kisebb értéket adjon
        - Nem kell tökéletes legyen
    - Arányos - 2× messzebbi csúcs 2× akkora érték
    - Reális - tényleges közelséghez közelít
    - Következetes - szomszédos csúcsok viszonya
    - Robosztusság 
- Tökéletes heurisztika Hanoi-ra
    - P(this) = f(1)₁ f:[1..n+1] → ℕ×ℕ
    - f(i) : csak az i-edik és annál nagyobb korongokat vesszük figyelembe
    - f(i)₁ : lépésszám
    - f(i)₂ : melyik rúd nincs használatban
    - f(n+1) = (0,1)
    - f(i+1) = 
        - (2*f(i)₁ + 1, 6 - f(i)₂ - this[i-1]) ha this[i-1]≠f(i)₂
        - (2*f(i)₁, f(i)₂) ha this[i-1]=f(i)₂

# EA 4 2021.10.03

## Visszalépéses keresés
- Ariadné és Theseus a minotaurusz labirintusában
- Módosítható stratégiájú keresés
- Egy utat tartalmaz
- Start-Start
    - bele kerülnek a lépések
- Terminál, ha megvan a cél vagy ha mindent leellenőrzött.
- Szabályok
    - Hozzá lehet venni élt
    - Ki lehet törölni élt - visszalépés
- Csak végső esetben lehet visszalépés
    - Zsákutca
    - Zsákutca torkolat
    - Kör
    - Mélységi korlát
- Gyengébb stratégiák is lehetnek beleépítve
    - Lehet modellfüggő vagy heurisztikus
    - Sorrendiség
        - Sorba állítja a kivezető éleket
        - Előbb próbál ki egy jobb élt
    - Vágó szabály
        - Kizár utakat
- Drágább, mint a hegymászó
- Van olyan verzió, amiben csak
    - Zsákutca és torkolat szabály van
    - véges körmentes irányított gráfon működik
- megoldás := VL1(startccsúcs);
```SQL
Recursive procedure VL1(akt: N) return (A*; hiba)
1.  if cél(akt) then retirn(nil) end if
2.  for ∀új ∈ Γ(akt) loop
3.      megoldás := VL1(új)
4.      if megoldás ≠ hiba then
5.          return( fűz((akt, új), megoldás) ) end if
6.  end loop
7.  return(hiba)
end
```
- n-királynő második állapottér modellje fa ezért működik rajta
- Heurisztikák az algoritmusba
    - n-királynőnél sorrendi heurisztika
        - hosszabbik átló hossza
            - ha nagy az érték akkor sokat kilő
        - páratlan páros
            - páratlan sorban balról jobbra
            - párosban jobbról balra
        - Ütés alá kerülő szabad mezők száma
            - dinamikus heurisztika, a többi statikus
    - n-királynő vágó heur.
        - azokat, ahova már nem lehet lerakni ki lehet vágni
        - részleges előre tekintés
            - szűrés
            - a következő sorba adott helyre rakás kiüti-e valamelyik sort
            - ha valamelyik sort teljesen kiüti akkor már vissza kell lépni
        - előre tekintés
            - mindent leellenőriz
            - összes kövi sorra ellenőriz, nem csak a 1-re
- Új modell az n-királynőhöz
    - folyamatosan töröljük a domain-eket
    - ha nincs már domain akkor visszalépés
    - **Bináris korlát-kielégítési modell**
        - Keressük (x₁,..,xₙ) ∈ D₁×..×Dₙ n-est ami kielégít néhány Cᵢⱼ⊆Dᵢ×Dⱼ bináris korlátot.
    - Töröl/szűr nem a visszalépéses kereséshez csatlakozik, hanem a modellhez
    - nem heurisztikák

- Második változat
- Minden feltétel beépítve a keresésbe
- ***VL2* δ-gráfban mindig terminál**
- Ha létezik a mélységi korlátnál nem hosszabb megoldás ó, akkor megtalál egy megoldást.
- rekurzió az alap implementáció
- az egész utat látni kell
```sql
Recursive procedure VL2(út : N*) return (A*; hiba)
1.  akt := utolsó_csúcs(út)
2.  if cél(akt) then return(nil) end if
3.  if hossza(út)≥korlát then return(hiba) end if
4.  if akt∈maradék(út) then return(hiba) end if
5.  for ∀új ∈ Γ(akt) - π(akt) loop
6.      megoldás := VL2(fűz(út,új))
7.      if megoldás ≠ hiba then
8.          return(fűz((akt,új), megoldás)) end if
9.  end loop
10. return(hiba)
end
```

- Mélységi korlát ellenőrzése biztosítja a terminálást
- Körfigyelés nem szükséges
    - Csak hamarabb megtalálja a visszalépést
    - Ha nincs vagy nagy körök vannak akkor nem általában optimálisabb kihagyni
- A mélységi korlátnál hosszabb a célhoz vezető utat nem találja meg
- tologatós játék
    - vágó heurisztika
        - ha az aktuális út hossza és a becsült lépésszám nagyobb, mint a mélységi korlát akkor vágás

- **előnyök**
    - terminál
    - talál megoldást, ha van a korláton belül
    - könnyen implementálható
    - kicsi memóriaigény
    - az egyik legfontosabb megoldási módszer
- **hátrányok**
    - nem garantál optimális megoldást
        - lehet ennek megfelelően módosítani
    - kezdeti rossz döntést sok lépés után lehet kijavítani
    - egy zsákutcát többször is megtalálhat
        - korlátos a memóriája
    - futás ideje nagyon rossz lehet
    
# EA 5 2021.10.10

## Gráfkeresések
- Lokális keresések
- δ-gráf
- minden felfedezett utat eltárol a globális mukaterültet
- nyílt csúcsok kiterjesztése
- legkedvezőbb csúcs kiterjesztése
- terminálás
    - sikertelen
        - nincs nyílt csúcs
    - sikeres
        - célcsúcsot megtalálja és ki akarja terjeszteni
- jelölések
    - **Keresőgráf (G)** - felismert gráfrész
    - **nyílt csúcsok halmaza (OPEN)**
    - **kiértékelő fgv. (f: OPEN → ℝ)** - megfelelő kiválasztás
- Kezdetben a startcsúcsok
- Másodlagos stratégiákat is be lehet vezetni az egyenlő csúcsokra
- két új függvény
    - szűlőre mutató pionter π
        - π(start) = nil
        - keresőgráfon egy feszítőfa lesz ebből
        - egyértelmű út a célból vissza
        - legolcsóbb út kiválasztása
    - költség fgv. g: N → ℝ
        - megtalált odavezető út súlya

- G gráf akkor korrekt ha minden csúcsa korrekt
- csúcs korrekt ha
    - konzisztens
        - költség a pi-ken keresztül
    - optimális
        - visszamutatók a legolcsóbb utat adják meg

- Kezdeteben: π(start):=nil, g(start):=0
- Az n csúcs kiterjesztése után minden m∈Γ(n) csúcsra
    1. ha m új csúcs
        - m ∉ G akkor  
        π(m):=n, g(m):=g(n)+c(n,m)  
        OPEN := OPEN ∪ {m}
    2. ha m régi csúcs, amelyhez olcsóbb utat találunk
        - m ∈ G és g(n)+c(n,m) < g(m) akkor  
        π(m):=n, g(m):=g(n)+c(n,m)  
    3. m régi és nincs jobb út
        - m ∈ G és g(n)+c(n,m) ≥ g(m) akkor SKIP 
- Ez lehet rossz is:
    - elromolhat ha a csúcshoz vezető utak belselyében van változás
    - ha van leszármazottja a csúcsnak akkor elromolhatnak dolgok
    - **megoldás** lehet egy-egy bejárás, amivel frissítjük a dolgokat
        - csak addig kell bejárni amíg korrekt csúcsot nem találunk
    - **megoldás** lehet egy olyan kiértékelő fgv amivel ez elkerülhető
    - **megoldás** az is, ha ezt a csúcsot megint berakjuk a nyílt csúcsokba
        - így majd helyreállnak a dolgok
        - de így lehet, hogy többször is eljutunk ugyanabba a csúcsba, de csak véges sokszor
        - ez tud lenni a legjobb sokszor

```SQL
1.  G := ({start}, ∅); OPEN:={start}; g(start):=0; π(start):=nil
2.  loop
3.      if empty(OPEN) then return -- nincs megoldás
4.      n := arg min(OPNE)
5.      if cél(n) then return -- megoldás
6.      OPEN := OPRN-{n}
7.      for ∀m∈Γ(n)-π(n) loop
8.          if m∉G or g(n)+c(n,m)<g(m) then
9.              π(m):=n; g(m):=g(n)+c(n,m); OPEN:=OPEN∪{m}
10.     end loop
11.     G := G ∪ {(n,m) ∈ A | m ∈ Γ(n)-π(n)}
12. end loop
```

- Bizonyítható
    - A GK δ-gráfban a működése során egy csúcsot legfeljebb véges sokszor terjeszt ki.
    - A GK véges δ-gráfban mindig terminál
    - Ha GK véges δ-gráfban létezik megoldás, akkor megtalálja azt

- Akkor lesz jó, ha jó a kiértékelő fgv

## Nevezetes gráfkereső algoritmusok
- Nem-informált 
    - mélységi
    - szélességi
    - egyenletes
- Heurisztikus
    - előre tekintő
    - A, A*, Aᶜ
    - B, B', A**

- Másodlagos vezérlési stratégia lehet heurisztikus függetlenül az elsődlegestől
    - egyenlőséget feloldó szabályok, tie-breaking rule

- Csökkenő kiértékelő függvény
    - akkor csökken, ha jobb utat találunk
    - soha nem terjeszt ki inkorrekt csúcsot
    - időről időre helyreállítja a korrektséget
    - működési grafikon, küszöbértékek
        - küszöbhöz ér akkor helyreáll, korrekt lesz

## Nem-informáltak
| Algoritmus     | Definíció     | Eredmény  |
| ----------     | ---------     | --------  |
| Mélységi <br> MGK  | f = -g <br> c(n,m) = l | - végtelen gráfokban csak mélységi korláttal garantál megoldást |
| Szélességi <br> SZGK| f = g <br> c(n,m) = l | - optimális (legrövidebb) megoldást ad, ha van (még végtelen δ-gráfban  is) <br> - egy csúcs kiterjesztésekor ismeri az odavezető legrövidebb utat (legfeljebb egyszer terjeszti ki) |
| Egyenletes <br> EGK | f = g| - optimális (legrövidebb) megoldást ad, ha van (még végtelen δ-gráfban is) <br> - egy csúcs kiterjesztésekor ismeri az odavezető legolcsóbb utat (legfeljebb egyszer terjeszti ki) |

- Mélységit sokszor visszalépésesnek hívják, de nem ugyan az

## Heurisztikus gráfkeresés
- A h heur. fgv. megbecsüli a hátralévő optimális út költsége
  - h* ami pontosan megmondja - tökéletes heurisztika
- Nevezetes tulajdonságok
    - Nem negatív
    - Megengedhető
        - alulról becsüli a h*-ot
    - Monoton megszorítás
        - a változás nem lehet nagyobb, mint választott él súlya

Algoritmus | Definíció | Eredmények
---------- | --------- | ----------
Előre tekintő gráfkeresés | f = h | nincs említhető extra tulajdonsága
A algoritmus | f = g+h és h ≧0 | - megoldást ad, ha van megoldás (még végtelen δ-gráfban is)
A* algoritmus |  f = g+h és h ≧0 és <br> h ≦h* | - optimális megoldást ad, ha van (még végtelen δ-gráfban  is)
Aᶜ algoritmus | f = g+h és h ≧0 és <br> h ≦h* és <br> h(n)−h(m) ≦c(n,m) | - optimális megoldást ad, ha van (még végtelen δ-gráfban  is) <br> - egy csúcs kiterjesztésekor ismeri az odavezető legolcsóbb utat (legfeljebb egyszer terjeszt ki)

- Magasabb memóriaigény, futási idő lehet jobb

# EA 6 ~2021.10.15

- Speciális heurisztikával nevezetes gráfkeresés lehet

## A algoritmus család
- A
    - f = g + I
    - a távolság és a heurisztika is számít
    - nem távolodik el egyik ágon sem
- A súlyozás, mágikus együtthatók
    - f = g + 2*I
    - néha jobb eredményeket lehet kapni
- Speciális plusz pontok
    - f = g + 2*I - (1 ha van BW_ vagy _BW)
- Aᶜ algoritmusok, ha megengedhető, nem negatív, és monoton megszorításos

## A* algoritmus
- f = g + h
- nem negatív és megengedhető

## Mérések
- Végtelen gráfon csak relatív összehasonlítás
- Feltérképezett csúcsok
- CLOSED_S - S alg. által lezárt csúcsok
- Memória igény
    1. X nem rosszabb Y alg.-nál ha CLOSED_X ⊆ CLOSED_Y
    2. X jobb Y alg.-nál ha CLOSED_X ⊂ CLOSED_Y
- Jobban informált nem feltétlenül lesz jobb
- Jobban informáltak kisebb memóriaigény
- A*-hoz hasonlíthatóak
    - Egyenletes gráfkeresés
    - A** az egész utat méri és onnan választ max-ot
    - B algoritmusok
- Nem lehet belátni hogy általánosan jobb lenne bármelyik
- Nem patológikus problémákon nem rosszabb 
- Monoton megszorításos feladatokon sem rosszabb

- Futási idő
    - k = |CLOSED|
    - Alsókorlát: k
    - Felső korlát: 2^(k-1)
    - Más heurisztika tud javítani a korláton, de a memóriaigény nőhet

    - Küszöb
    - Küszöb között árok
    - Árkon belül lehet más kiterjesztési sorrendet választani, pl g(él súly)
    - A futás idő attól lesz rossz, ha egy csúcs sokszor ki lesz terjesztve
    - B algoritmus lesz ez a módosítás
        1. F = f(s)
        4. ha van kisebb, mint az F akkor g lesz a kiterjesztési szabály
        - Egy csúcsot egy árokban egyszer terjeszt ki
        - Így legrosszabb esetben k² lesz a felső korlát

- Jó heurisztika nélkül nem lesz megoldás
    - Megengedhető heurisztika garantálja a legjobb megoldást
    - Hatékonyabb lehet egy gyengébb heurisztika
    - Monoton megszorításos heur.-nál egy csúcs egyszer lesz kiterjesztve 
    - Menet közben lehet módosítani: változó heurisztika
    - B' algoritmus:
        - magyar
        - tanul
        - menet közen megváltoztatja a heurisztika értékét
        - megengedhető marad
        - monoton megszorításosra próbálja rendezni a heurisztikát

# EA 7 2021.10.22

## Kétszemélyes játékok
- két személyes
- teljes információjú 
    - mindkét játékos ismeri az összes lehetséges és elérhető állást
    - kártyajáték kizárva, mert az ellenfél lapjait nem ismerjük
    - táblás játékban látjuk a dolgokat
- véges
- determinisztikus
    - véletlennek nincs szerepe
    - determinisztikus egy lépés következménye
- zéró összegű
    - nyeremény megegyezik a veszteséggel
    - nem nyerhet mindenki, stb.
- csak ezekkel foglalkozunk
    - de lehet ezeket tovább vinni a más játékokra is

- Állapottér modellel lehet modellezni
    - játéknak állapota + melyik játék jön
    - művelet - lépés
    - irányított gráf
    - játékfává lehet alakítani
        - egy lehetséges játszma egy ág
        - szintjeiből lehet tudni, hogy ki jön


- Grundy mama játéka
    - x érme egy oszlopban
    - nem egyenlő részre kell bontani
    - akinek nem megy az veszít

- Amikor az adott játékos jönn, akkor kell úgy lépni, hogy később biztosan nyerhessen
- Játékfa egy részfája
- Nyerő stratégia
    - mindig jó lépés a győzelemig
- Nem vesztő stratégia
    - legalább döntetlenre visz

- ÉS/VAGY fa építhető egy adott játékosra nézve
    - ellenfél lépésénél hiperél van az összes állapotba, ahova léphet
    - hiperutat kell keresni a győzelembe
    - Általában csak az egyik játékosnak lehet nyerő stratégia
        - az egyik játékosnak biztosan létezik nyerő stratégia
            - alulról fölfelé lehet címkézni
            - ki fogja onnan megnyerni
            - a startban valakinek lesz címkéje

- Játékfa egy része kell csak, azt a részét egy heurisztikával kiértékelik és meghatározzák a "jó" lépést
- Pozitív csúcs nekem jó, negatív az ellenfélnek, ha nulla közeli akkor döntetlen
- MINIMAX algoritmus
    - Részfa leveleit kiértékeli
    - Közbenső csúcsokra is kiszámolja
        - nálunk MAX, ellenfél MIN
        - ellenfélnek minnél kevesebbet akarunk
        - magunknak minnél többet
        - olyan irányba kell lépni ami nekünk a legjobb
        - Minden lépésben új fát kell építeni, kiértékelni és felfuttatni
- Átlagoló kiértékelés
    - Heurisztika rossz is lehet adott pontban
    - A környezetéhez hasonlítjuk és úgy lehet jobb felfuttatást kapunk
- Váltakozó mélységű kiértékelés
    - ahol el akarom vágni ott nyugalomban van-e
    - A szülő állapottól nem sokat változott
    - Ha sokat változott akkor még meg lehet nézni ott pár szintet
- Szelektív kiértékelés
    - lényeges és nem lényeges lépéseket szétválasztjuk
    - addot idő alatt több csúcsot tudunk kiértékelni (ami fontos csúcs)
- Negamax
    - -1 -el beszorozzuk a min szinteket
    - minden lépésben negálás és max keresés
- Alfa-béte algoritmus
    - visszalépéses keresés szerű
    - mélységi bejárás
    - egy út van csak a memóriában
    - út mentén, max-nél alfa, min-nál béte
        - alfa-nál rosszabb nem lehet
        - béte-nál jobb nem lehet
    - visszalépésnél hozza felfele az értékeket
    - ideiglenes értékeket összehasonlítani a hozott értékkel
    - vágás:
        - két csúcsnál az alfa nagyobb egyenlő, mint béta akkor a maradékot levághatjuk
        - nem kell egymás fölött közvetlen legyenek
    - ugyan azt állítja elő, mint a minimax
    - kevesebb memória kell
    - futás idő jobb a vágások miatt

- Algoritmus nem elég
    - jó modell és jó heurisztika kell ahhoz, hogy tényleg jó legyen

# EA 8 2021.11.04

## Evolúciós algoritmusok
- Globális munkaterületen egyedi populációk
- Egyedet vagy elfogadható populációt keresünk
- Rátermettségi függvény
- Rossz egyedeket a rátermettekhez hasonlóra cseréljük

### Evolúciós operátorok és a terminálás feltétele
- Szelekció: rátermettebb kiválasztása -> szülő
- Rekombináció: szülőkből gyerek
- Mutáció: gyerek kis módosítása
- Visszahelyezés: új populáció a gyerekekből és szülőkből
- Terminálás:
    - célegyed
    - populáció egyesített rátermettségi értéke nem változik

### Alapalgoritmus
- Nem egyedi
```SQL
Procedure EA
populáció := kezdeti populáció
while terminálási feltétel nem igaz loop
    szülők := szelekció(populáció)
    utódok := rekombináció(szülők)
    utódok := mutáció(utódok)
    populáció := visszahelyezés(populáció, utódok)
end loop
```

- nem mindegyik operátort kell beépíteni

### N-Királynő
- Modell 1
    - Egyed: királynő elrendezés, ahol egy oszlopban egy királynő hol van
    - Reprezentáció: királynő sorának száma az oszlopban
    - Rátermettségi fgv: ütésben nem lévő királynő párok

- Operátorok
    - Kiválasztás:
        - Páros darab kell
        - Csonkolás:
            - Korlátnál nagyobbakat választja ki
    - Rekombináció:
        - Keresztezés:
            - Szülőben lévő adatokat egy indexig kicseréljük
            - Index random
        - Kétpontos keresztezés
            - Két pont közötti adatok cserélődnek
    - Mutáció:
        - Kis valószínűséggel módosítás
    - Visszahelyezés:
        - Rosszabbak helyére jobbak
        - Mohó módszer nem mindig jó
- Modell 2
    - Egyed: n királynő, minden sorban és oszlopban egy királynő
    - Reprezentáció: ugyan az, így most egy permutáció
    - Rekombinációban az invariánsokat be kell tartani
        - Kétpontos:
            - Gyerekek között a duplikátumokat cseréljük
    - Mutációnál párokat kell cserélni

### Kielégíthetőségi probléma
- Boolean formula KNF alakban
- Egyed: változók igazságértéke
- Reprezentáció: bitek sorozata
- Rátermettségi függvény: igaz klóz-ok száma

- Szelekció
    - Rulettkerék
        - Rátermettség összege alapján rulett
        - Össz rátermettség db cella
        - Rátermettség értéke alapján hány db helyen van egy egyed
        - sorsolunk szükséges darabszámú egyedet

## Evolúciós algoritmus tervezése
- Egyed meghatározás
- Reprezentáció
- Rátermettségi fgv kitalálása
- Operátorok benne léte és implementációja
- Kezdő populáció, megállás feltétele
- Stratégia paraméterek
    - populáció száma
    - mutáció valószínűsége
    - utódképzési ráta
    - visszaállítási ráta
    - stb.

### Kódolás
- "Kromoszóma"
- Jelsorozatként kódolva
- Egyedeket a kódokon keresztül manipuláljuk
- Jelcsoport, kód feldarabolható kell legyen
    - Kis változás legyen

### Fitnesz fgv
- Modellezéstől függ
- Gráfszínezési probléma
    - Két különböző modellhez más fgv kell
    - Direkt kódolás
        - I-edik szín az i-edik csúcs színe
        - Élek, ahol különböző a két csúcs színe
    - Indirekt kódolás
        - Színek világosság szerint a tömb, csúcs száma a tömbben
        - Minden él különböző színt köt össze
        - FGV: mennyi kiszínezettlen van
- Kő-Papír-Olló
    - Előző lépések alapján mond valamit
    - Stratégia kitenyésztés
    - Kódolás: 0,1,2 sorozat
        - Hármas számrendszer beli száma
    - fgv: megnézzük a tavalyi eredményeket
        - a mintához mérjük
        - ott a mi stratégiánk nyerne-e

## Evolúciós Operátorok
### Szelekció
- Rátermettség arányos - roulett kerék
- Rangsorolásos - fgv érték különbsége nem meghatározó, ezért csak a sorszám számít
- Versengő - véletlen csoportokban a legjobb kiválasztása
- Csonkolásos v selejtező - ha alacsony érték van akkor biztosan rossz - azt ki lehet dobni

### Rekombináció
- Keresztezések
    - Jelek/gének cseréje
    - Egy és többpontos keresztezések
        - Kijelölt csoportok cseréje
    - Egyenletes
        - Véletlen pozíción csere
        - Ha egy pozíció egyedi tulajdonság
    - Parciálisan illesztett keresztezés
        - Kétpontos
        - Majd permutáció fenntartása
        - Duplikátumok párba állítása és csere
    - Ciklikus keresztezés
        - Egyenletes aztán ciklus amíg kijavul
- Más számítások is lehetnek
- Invariánsokat meg kell őrizni
- Általános rekombinációk
    - Köztes rekombináció
        - (x, y) pont alapján kifeszített hipertéglalapból vagy szűk környezetéből kell utódot választani
    - Lineáris rekomb.
        - x és y pont közötti egyenesen vagy kicsit a pontokon túl lehet utódot választani

### Mutáció
- Kis méretű véletlen változtatás
    - random számmal növeljük
    - random bitet megfordítunk
- Permutáció esetén be kell tartani a szabályt
    - jelpár csere
    - ciklikus forgatás
    - stb

### Visszahelyezés
- Használja a kiválasztás technikáit
- Ki kell választani a cserélendőket
- Ki kell választani a visszarakandókat

### Paraméterek
- h - távolság az általános rekombinációban
- p - valószínűség
- u,v - a visszahelyezés paraméterei

## Evolúciós algoritmus használata programozáshoz
- Melyik algoritmus oldja meg legjobban a feladatot
- Egyedek az algoritmusok
- Rátermett a gyorsabb, pontosabb, kisebb memóriaigényű





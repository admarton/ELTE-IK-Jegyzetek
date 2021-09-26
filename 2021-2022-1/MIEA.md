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
    - oldalom van minta
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
    - (Az ember a robot akia a felszabadító)
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
- Megoldhatatlannak tűnő problémát próbál megoldani és ementén létrejönnek hasznos teknológiát
## MI kutatók csoportjai
- Erős MI
    - Szélsőséges Redukció
        - Elemi részekre bontás
        - Azok jellemzése
        - Kapcsolataik jellemzése
        - Így minden pontosan leírható és megérthető
    - Church-Turing tézis
        - Adott folyamatot kellő pontossággal le tudunk írni, úgy hogy mindenkinek egyértelmű legyen, akkor az algoritmussal is leírható
    - Ha az emberi inteligenciát részekre tudjuk bontani és kellő pontossággal le tudjuk írni, akkor algoritmizálható
- MI szkeptikusok
    - A számítógép soha sem lesz okosabb az embernél
- Gyenge MI - Közép csoport - Technokrata, mérnök szemlélet
    - Probléma megoldásához sokszor mesterséges intelligencia szerű megoldások jönnek lére
## MI története
- 1956. Nyara - Deklarálták az MI létrejöttét
    - Kutatási irány elindult
    - Az emberi gondolkorás számítógépes reprodukálása
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
        - Két általános fogalomat összeéselt
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
    - Olyan terület ami olyan problémákkal foglalkozik amit nem lehet számítógéppel megoldani
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
        - Feladat megoldásához a problématérban keresünk egy bizonyos megoldást
    - Brute force nem ad megoldást
    - Ötlet, intuíció kell, **heurisztika**
        - Utazó ügynök
            - ugyan azok a városok között ugyan az lesz a  legjobb út
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
- hasznos ill. haszintalan elemek
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
    - egyértelmú haladási irány
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
- C sorozatot a Cᵏ←ᴷ sorozat követi, amiben a *k* helyére *K* kerül, ahol k⟶K a hiperút által tartalmazott hiperélel
- Így egy hiperutat közönséges irányított útként foghtunk fel, de nem egyértelmű, mert lehet több bejárása is

## Gráfreprezentáció fogalma
- Minden útkeresési probléma rendelkezik egy gráfreprezentációval, ami egy (R, s, T) hármas:
    - R=(N,A,c) a reprezentációs gráf (δ vagy ÉS/VAGY)
    - s ∈ N, startcsúcs
    - T ⊆ N, célcsúcsok
- és a probléma megoldásával:
    - t cél vagy <t₁,...,tₘ> célcsúcssorozat megtalálása vagy
    - s⟶t vagy s⟶<t₁,...,tₘ> esetleg efy ooptimális s⟶*T út megtalálása

## Útkeresés δ-gráfban
Algoritmus ami elindul a **kezdeti aktuális csúcsból** és minden *nem-determinisztikus* módon új aktuális csúcsot *választ* (gyakran az akt. gyerekei).  
Ezeket a lépéseket tárolja, de felejthet is (memória spórolás).  
Megáll ha célcsúcsot talál vagy tudja hogy nem lesz meg.  

## Útkeresés ÉS/VAGY gráfban
Visszavezetés δ-gráfos megoldásra.
A startbúl induló hiperútak bejárásai δ-gráfot alkotnak.
- Csúcsai az eredeti gráf csúcssorozatai
- Startcsúcs az eredti g. startcs.-ból álló sorozat
- Célcsúcsai az e. g. célcs.-ból álló sorozat

## !!HUH!! ##

# Konzi 2021.09.16

## δ-tul. 
- Kizárjuk azt hogy a végtelen hosszú út legyen a legrövidebb
- Általában magától adódik ez a tulajdonság
- nem végtelen feladatban sem lesz végtelen kifok
- súlyok alsó korlátja általában műveleti költségből jönű
    - annak van minimuma általában
- gráf lehet kb végtelen nagy is

## ÉS/VAGY gráf
- Kövönséges gráfnak megfeleltethető
    - át lehet alakítani
- ÉS él a kiperés
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
    - Irányított fát jobb építeni mint gráfot

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
            - áthelyet(x,y,u,v)
        - hatalmas problématér
        - tetszőlegest start állapot
        - megoldás a célállapot

## Reprezentációs gráf bonyolultsága
- repr. gráf -> problématér -> keresés számításigénye
- Start csúcsból kivezető utak száma
- minnél kisebb problématér kell
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
    - "üres hely eltolás", kevesebb művelet mint az összes lap eltolása
    - Tol(irány)
        - nem szabad kitolni
- sok kör és út

## Visszafelé haladó keresés
- meg kell találni aztén át kell fordítani
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
        - ha tezdetben teljes és ellentmondásmentes volt akkor ezek is ilyeneket genrálnak
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
    - ha L nincs a művelet D,A-ban akkor benne ven az előző lépésben
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
            - ha van olyan erőforrás amit minden használ akkor ez nem lehetséges (pl egy robotkar a kockavilágban)
            - vannak műveletek amik párhuzamosak lehetnek
        - vagy úgy fésűli össze, hogy műveleteket rak hozzá vagy elvesz
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
        - Mindig ugyan úgy, programmozó visszatérhet és dönthet máshogy
        - *lokális keresések*
        - *evolúciós algoritmusok*
        - *rezolúció*
    2. Módosítható
        - Korábbi rossz lépést máshogy csinálhat
        - *visszalépéses keresés*
        - *gráfkeresés*
        - *szabályalapú köv.*
2. Modellfüggő
    - adott modellezési teknikához kapcsolódik
3. Heurisztika
    - Megoldó algoritmusba álül be

## Lokális keresések
- A probléma reprezentációs gráfjának csak kis részét tárolja
- Kezdetben a startcsúcsot ismeri
- akkor áll meg ha a célcsúcs megjelenik a látómezőben
- helyi csúcsok helyébe a szűk környezetéből válszt újakat, "jobbakat"
- kiértékelő függvény (cél-, rátermettségi-, heurisztikus függvény) dönti el, hogy mi a "jobb"

### Hegymászó keresés
- Akt csúcs, szülő csúcs van tárolva
- Startból indul
- Célba vagy zsákutcába jut
- Akt csúcsot a gyerekére cseréli
- Azt a gyereket választja amelyik a legjobb és nem szülő
- Van olyan ahol rosszabbra sem lehet lépni
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

- Künnyú implementálni
- Csak jó fitnessfüggvény esetén lesz hasznos
    - újra lehet indítani egy másik véletlenyszerű csúcsból
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
- Ha az opt célcsú vagy régóta nem változott vagy zsákutca van, akkor van vége
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
- Tabu méreténél kisebb köröke elketüli
    - Repr. gráfról kell infó
    - vagy sok kísérletezéssel
- Zsákutcával itt sem lehet mit kezdeni

### Szimulált hűtés algoritmus
- Ne legyen mohó a stratégia
- véletlenszerűen választ és megvizsgálja
    - ha a heurisztikája viszonylag jó akkor elfogadja
    - általában ha jobb vagy ha nem sokkal rosszabb
    - e^(f(akt)-f(új))/T > random[0,1]
    - T-t lehet állítani, szabályozható működés
- Hűtési ütemterv
    - Lépésenként más T-t használ
    - szig mon csökk - kezdetben inkább elfogadja a rossz csúcsot
- Azért ez a neve, mert
    - Grafikont rajzolva monoton cökken, de van ahol nő (az elején inkább)
    - Optimális kristály szerkezetrre hozni egy folyadákot
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
    - minnél kevesebb osztály kell
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
        - Annál jobb minnél több van az első pár osztályban
        - Minnél kevesebb él van egy osztályon belül
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
- iterációs lépések száma és egy lépés kültsége határozza meg
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
            - +1 pont ha a szélén van és nem a helyén
            - +2 ha sarokban van de nem a helyén
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
                - *teknika*: meglévő súlyozása, büntető pont rendszer
            - 
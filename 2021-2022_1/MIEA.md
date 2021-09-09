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
**Def.:** Útkeresési probléma az, amelynek megoldása megfeleltethető egy *élsújozott irányítatlan gráfbeli*
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
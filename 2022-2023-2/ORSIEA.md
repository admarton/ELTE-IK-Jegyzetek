<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
        inlineMath: [['$','$']]
      }
    });
</script>
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# Osztott rendszerek specifikációja és implementációja

# 1. EA

- Fogalmak tömege lesz
- Leggyengébb előfeltétel a leggyengébb előfeltétele a tárgynak és a programozásnak is
- Időtől függő logika kell a programozáshoz, párhuzamaos programozáshoz

- Bevezetés a programozásba
  - Fóti Ákos
- Párhuzamos és elosztott programozás
  - Horváth Zoltán
  - Tárgymutató - fogalmak
  - Tételek és lemmák jegyzéke
  - Jelölések jegyzéke - Gyakran használt jelölések
- Ajánlott irodalom
  - Parallel Program Design - Chendy K.M., Mistr J.
  - 1978 Tony Howre C.A.R.- Communicating Sequential Processis
    - Occam nyelv alapja
    - Actor alapú párhuzamosság
    - Ada és erlang processek
  - Hennessy - Theory of processes
  - 1976 Dejkstra - Disciplin of programming
  - Lamport - Temporal logic of actions

## Étkező filozófusok

- Filozófusok körben ülnek, közös villák vannak és középről esznek
- Most egyszerre veszik fel mindkét villát, atomi-pillanatszerű művelet
- Négy állapot a filozófusnak
  - Gondolkodik
  - Van villa
  - Eszik
  - Otthon van
- Nem egy pillanatbeli logikai operátorok
  - Jövőidejű temporális logikai operátorok
- $ f(i).g \triangleright f(i).v \bigvee f(i).o $
  - Ha gondolkodik, akkor utána csak villás állapotban lehet vagy otthon lehet
  - Nem biztos, hogy valaha fog villát fogni
  - **unless**
- $ f(i).v \triangleright f(i).e $
  - Ha villa van nála, akkor enni fog
  - Nem biztos, hogy továbblép
  - Kiéheztetheti a többit
- $ f(i).e \mapsto f(i).g $
  - Ha eszik, utána mindenképp gondolokdni fog
  - **ensures**
- $ f(i).g \hookrightarrow f(i).o $
  - odavezet, leadsto
  - Egyszer hazamegy
  - **leads to**

# 2. EA

## Étkező filozófusok folytatás

- Háromszög tilt mindent ami nincs megengedve
  - Biztonsági kikötés
  - Nincs haladási kényszer
- Nyil
  - Haladási kényszer
  - Mindenképp tovább kell lépnie
  - A következő állapot van megadva
- Kampós nyil
  - Nincs biztonsági tényező
  - Oda jut de nem tudni, hogy min megy keresztül
- Invariáns
  - Globális invariáns
  - Program teljes működésére vonatkozó állítás, összefüggés
  - $ (f(i).e \rightarrow (\neg f(i+1).e \wedge \neg f(i-1).e)) \in inv $
    - **Kölcsönös kizárás**
  - Legtöbb feladatben ez a legfontosabb
  - Megoldási ötletet adja meg
    - Egy statikus dolog, nem változik, de mágis a működés ötlete
- Egy feladatban lehet többféle kikötés vagy egy-egy kikötésből több is
- Fixpont kikötés
  - $ FP \Rightarrow f(i).o $
  - Fixpontolyasmi mint az utófeltétel
    - de olyan program most már nem elég aminek vége van
  - Fixpontban nem kell megállnia a programnak
    - De ha megáll, akkor fixpontban kell megállnia
    - Rendezett leállás
  - Ha megáll akkor otthon van
  - Akkor áll meg ha nincs már változás
  - **Parciális helyesség**
    - Teljes helyesség az utófeltétel
- Megkövetelhetjük a megállást
  - **Terminálási kikötés**
  - $ \forall i : f(i).g \in TERM $
  - Ha mindenki gondolkodik, akkor előbb-utóbb megáll
- Kezdeti feltételt is lehet megadni
  - Ha terminálási megegyezik a kiindulásival, akkor meg fog állni
  - **INIT**
- Holtpont egy rossz megállás
  - nemkívánt
- Redundáns-e
- Ellentmondásmentes-e
- Teljes-e
  - Otthonra nincs semmi biztonsági feltétel
  - Gondolkodik -> hazamegy -> eszik nincs letiltva
- 7 féle új kikötés
  - Elég a legtöbb program specifikálásához
  - Valós idejü programhoz nem elég

## Példa program

- Közös változókon lehet interferencia
- Meg kell mutatni, hogy nincs interferencia
  - Első ötlet a párhuzamos program helyességének bizonyítására
  - n lépéses és m lépéses programnál n×m bizonyítás
- Rendezés nélkül tegyük egy halmazba a lépéseket
  - Írjuk le hogy a lépést mikor lehet végrehajtani
  - Előfeltételekből lesznek feltételes értékadások
  - Először a lépés halmazt könnyebb megadni
    - Utána abból lehet folyamat halmazt megadni
    - Szokatlan ez a programozási mód
    - Sokmindentől független megoldást kapok
      - Ezeket lehet egy konkrét platformra megadni
        - Optimalizált megoldást lehet adni
- $ S = (SKIP, \{\square\_{i \in [1..n-1]} a(i),a(i+1) := a(i+1), a(i) $ ha $ a(i) > a(i+1) \}) $
  - Buborék rendezés
  - SKIP nem semmit csinál, hanem mindent ugynolyanra csinál hogy ne változzon
  - Doboz a vessző nagy verziója
- Akkor áll meg ha már nem lehet több állapotváltozás
  - Ha már rendezett a tömb akkor már nem fog változást okozni egyik értékadás sem
- Kell ütemezési minimum feltétel
  - Mindegyik értékadásnak oka van
  - Nem lehet az hogy egy idő után nem választanak egyet
  - Feltételektől nem függő pártatlan ütemezés
- Atomicitás, Pillanatszerű minden feltételes szimultán értékadás
  - Közbenső állapotot nem tudnak mások módosítani

# 3. EA

- $ S = (SKIP, \{\square\_{i \in [1..n-1]} a(i),a(i+1) := a(i+1), a(i) $ ha $ a(i) > a(i+1) \}) $
- Kezdő értékadás
  - Invariánshoz kapcsolódik
  - Beállítom hogy teljesüljön
- Szimultán értékadásnak vannak fázisai
  - ki kell értékelni mindent és csak utána lesz értékadás
- Atomicitás miatt várni kell
- Nincs több állapotváltozás - fixpont
  - akkor ha mindegyik feltétel hamis
  - azaz rendezett a vektor
- Ez az absztrakt program lehet párhuzamos és szekvenciális is
- Szuperpozícióval detektálom a másik folyamat fixpontját

- Leképezés
  - Hatékony-e
    - Absztrakt programra ez értelmetlen
    - Attól függ
      - Hány folyamat, processzor, milyen ütememzés
    - Konkrét programról lehet ilyet kérdezni
  - Állapotváltozások várható száma
    - nem a lépésekkel araányos

## A relációs modell alapfogalmai

- Matematikai modelltől is függ
  - Egyszerű halmazelmélet
  - Egyszerű csak bonyolult hatványhalmazok lesznek

### Állapot

- A változók értékei.
- n változó n érték, rendezett n-es
  - típusai vannak a változóknak

### Állapottér

- Az össues lehetséges állapot halmaza
- A::= X_A_i_j annyi típus direkt szorzata ahány változó van

### Elérhető állapotok

- Az amit kezdőállapot függvényében el tudunk érni
- Statikusan az invariánstól függ
- Invariáns megmondja, hogy mi az ami biztosan nem érhető el
  - Amire igaz abból nem tudjuk, h elérhető-e
  - De amire hamis az biztosan nem elérhető

### Relációk

- Állapotpárok
  - Honnan hova akarok eljutni

### Reláció értéke

- r(a) = {b | (a,b) \in r}

### Reláció értelmezési tartománya

- Domain, A-beli értékek amihez van B

### Jelölések

- véges sorozat: a = (a_1,...,a_n)
- végtelen sorozat: a = (a_1,...)
- A\* : A elemeiből képzett véges sorozatok halmaza
- $A^\infty$: A elemeiből képzett végtelen sorozatok halmaza
- $ A^{\*_} ::== A^_ \cup A^\infty $

### Hatványhalmaz

- Állapottér összes lehetséges részhalmazának a halmaza
- P(A) a hatványhalmaz (2^n) eleme van

### Specifikáció

- Paramétertől függő előfeltétel és utófeltétel
  - Kiindulási állapotok hamaza
  - Végállapototk halmaza

### Parciális függvény

- Minden értékhez max egy értéket rendel

### Függvény

- Minden értékhez pontosan egy értéket rendel
- Mindenhol értelmezve van

### Logikia fgv.

- Igaz hamis értéket rendel mindenden függvényparaméterhez
- Igaz: A -> igaz
- Hamis: A -> hamis

### logikai műveletek

- Függvénykompozíció
- Implikáció is függvénykkompozíció
- Duplanyil egy állítás, részhalmaz-e vagy sem

### Reláció inverz képe, ősképe

- inverz képe az amihez hozzá van rendelve
  - honnan jutok el ide
- őskép, ahonnan csak oda jutok biztosan
  - csak oda juthatok
  - leggyengébb előfeltétel
  - $ p(S)^{-1}(\lceil R \rceil) = \lceil lf(S,R) \rceil $

### Reláció kompozíció

- Programfüggvény szekvencia
- Reláció a->b és b->c akkor a kettő kompozíciója a->c

### Szigorú kompozíció

- Csak akkor eleme egy pár ha az első reláció eredményének összeségére folytatódik a második
- Nemdeterminisztikus progrmnál fontos
- Ha holtágba kerül, akkor nem kerülnek be a relációba
- Ősképhez hasonló szigprítás
  - Kiindulóállapotból biztosan a végállapotba jut
    - nem futhat rá valami mellékágra
  - A nemdeterminiszikus programok miatt kellenek ezek a szigorítások

# 6. EA

- Atomicitás
  - Register test-and-set
    - Gépi utasítás - ez a legatomibb utasítás
  - Milyen szintre megyünk az atomicitással
  - Szimultán értékadás egy nagyobb ilyen
  - Ha nagyobb egységek lesznek atomiak, akkor lassabb lesz
    - Kvázi szekvencializálom

## Hatásreláció

- Egy állapothoz csak véges sorozatok vannak, akkor értelmes
- A véges sorozatok végét összegyűjtjük

## Üres utasítás SKIP

- $\forall a \in A: SKIP(a) = {(a)}$
- Megegyező állapotba visz át.

## Egyszerű értékadás

- Egy lépésben az új állapotba ugrok vagy maradok ahol voltam vagy abortálok (végtelen sorozat ami nem változik).
- red függvény, kettő hosszú sorozatot helyettesíti eggyel ha a kettő megegyezik
- Egy feladat hozza létre
  - Megadom hogy milyen értékek legyenek az állapotban
    - A feladat részfeladatokból áll, ami egy változó értékét adja meg
- Akkor lesz jó állapot ha a feladatban minden változó értéke definiált
  - Ezt nem szeretnénk
  - Ahol nem definiált ott definiáltá tesszük
    - Ezért van a feltételes értékadás
  - Megjegyzés: Amikor leírjuk, akkor nem írjuk ki az összeset, akkor is ott van az összes

## Feltételes értékadás

- Ha nincs definiálva egy változó, akkor azt nem módosítjuk
- Sosem száll el, mindig oda ugrik ahova kell és rögtön teljesíti
- Nem lesz végtelen sok nem determinisztikus állapot
  - Konkrét programok ez mindenképp betartják
  - Emiat lesz monoton és folytonos az lf

## Állapotátmenetfák

- Aki nem jár órára az nem tudja, hogy ez vizsgára nem kell
- Csak a rajzot kell tudni elmagyarázni
  - Akkor címzett helyesen ha az élcímkék ás az állapotok megfelelnek
  - Minden csomópontban legalább m irányba ágazunk
    - m a programok száma
    - ha S_i nem determinisztikus akkor ott nem csak egy ág lesz S_i-hez
  - Egy futtatás csak egy ágon futhat végig
  - Tesztelni nagyon nehéz
    - Lehet hogy minden teszt alkalommal más utat jár be
  - Vannak olyan utak amik nem felelnek meg a pártatlan ütemezésnek
- Absztrakt program már kell

## Absztrakt program

- Állapothoz nem sorozat hanem fák vannak rendelve
- s_0 adja az első ágakat, utána a S elemei
- Csak azok az elérhető állapotok amik szerepelnek csúcscímként
- Lineáris és elágazó időben függő logika nem ekvivalens
  - Lineáris: előrehozta az összes döntést a kiindulásba

# 7 vagy 8. EA

## Különbség az invariáns és a mindig igaz között

- Invariáns elérhetetlen esetben is stabil
- Mindig igaz az elérhetetlen állapotokban kivihet a P-ből
- Ez akkor lesz fontos ha több program dolgozik egy állapottérben
  - Ha zárt a rendszer, akkor a mindig igaz is jó
  - Ha csak egy komponenes egy nyílt rendszerben, akkor invariáns kell
    - A következő komponenseknek is teljesíteni kell az invariánst

|     |  a  |  b  |  c  |  d  |
| :-: | :-: | :-: | :-: | :-: |
|  1  |  #  |  -  |  w  |  -  |
|  2  |  -  |  #  |  w  |  w  |
|  3  |  w  |  w  |  #  |  -  |
|  4  | (#) |  w  |  -  |  w  |

- (#) a kezdő helyzet
- "-" mező nincs
- Innen mindig igaz, hogy a ló minding csak feketére léphet
- A legkisebb invariáns az a [2-4][a-c] résztábla
  - Arra már igaz, hogy a ló csak feketére léphet
- $ P,K inv_S(Q) $ akkor $ (P \wedge K) inv_S(Q) $
- Az összes invariáns metszete a legszigorúbb invariáns
- Invariáns mindig létezik és egyértelműen létezik a legszigorúbb is
- $ INV_S(Q) $ - legkisebb invariáns, elérhető állapotok halmaza
- Aki tartalmazza a legszigorúbb invariánst az mindig igaz, akkor is ha nem invariáns
- Komponenseknél előre meg kell egyezni az invariánsban.
- Metszésekkel egyre kisebb invariánst kapok
  - Pl.: Invariáns és mindig igaz metszete

## Háromszög

- Csak a $ P\wedge\neg Q $ állapotokról tudunk valamit
- Ha P stabil akkor nem hagyhatom el
  - Nem P - ha átmegy a P-be akkor ott marad
- P konstans, ha a P és a nem P is stabil, azaz nem mehez egyikből a másikba
- Minden invariáns stabil

## Egyenesnyil

- Egyenesnyíl nem diszjunktív - sokáig nem tudtuk ezt

## Görbenyil

- Egyenesnyil tranzitív diszjunktív lezártja
- Statikusan számolódik az lf-ekkel, levezethető
  - De csak, akkor ha a görbenyil is teljesül
- Szerkezeti típuskonstrukciók a konstruktorokkal
  - Struktúrális indukcióval lehet bizonyítani

## Hullámosnyíl

- Minden P-ből induló feltétlen pártatlan út átmegy Q-n is

# 9.EA

## TERM_S

- Ha abból az állapotból indul ami eleme a TERM_S-nek, akkor előbb vagy utóbb fixpontba jut

## Absztrakt program viselkedési relációja

- A Tulajdonságok felsorolva
- 6 tulajdonság
- Ezek mind halmazok
  - háromszög, egyenes görbe: Igazsághalmazok párjainak halmaza
  - fixpont, term, inv: Igazsághalmazok halmaza
- Tulajdonságoknál init nincs, feldat specifikációnál van ilyen
- Reláció hatos
  - Feladat egy reláció hetes

## Megoldás

- Paramétertér
- Kikötések a paraméterekre
- Nem determinisztikusság lehetséges de nem sűrűn használt
- Olyan program kell ami az init feltétel mellett megfelel a kikötéseknek
- Init a kezdőállapotot adja meg
  - Ezt a program nem tudja befolyásolni
  - User garantálja neki
  - Ha nem onnan indul a program, akkor nem tudunk semmit a programról
  - Ez nem a programmal szembeni követelmény, de plusz infó a programnak
- Minden kikötéshez van egy hasonló programtulajdonság
  - Megnézzük, hogy megvan-e a programnak a szükséges tulajdonsága
  - Megfelel-e a kikötéseknek
  - Nem egy az egyben átírjuk, hanem feltesszük, hogy csak az elérhető állapotokat kell ellenőrizni, mert máshova nem juthatunk
    - Itt már ismert minden komponenes, nincs ismeretlen ami elronthatja
  - Legszűkebb invariánssal lehet jellemezni az elérhető állapotok halmazát
    - INV_S(Q)- t nehéz számolni
    - Ha veszek egy P \in inv_s(Q) akkor annak része a nagy inv
      - Valamilyen invariánst könnyebb találálni mint a legszigorúbbat
- A Kikötést csak egy invariánsra nézzük és abből lesz programtulajdonság
- INIT-et nem kell nézni csak felhasználjuk
- S program akkor felel meg a ha van olyan invariáns ami mellett teljesülnek a tulajdonságok

## Variáns függvény

- Állapottérbeli pontokhoz rendel egy értéket
- Nem egy változó ami egész értéket ad

## Variánsfüggvény alkalmazása

- P,Q feltétel
- $ P \wedge \neg Q \Rightarrow t > 0 $
- $ P \wedge \neg Q \wedge t = m \hookrightarrow_S (P \wedge t < m) \vee Q $
- Olyasmi mint a termináló függvény a ciklusnál, csak ez nem olyan szigorú
  - Nem kell monoton csökkennie - görbenyíl

# 10. EA

- MVM-en voltam

# 11. EA

## Futószalag

- Invariáns és a fixpont a végén egyszerre kell teljesüljön
- Futószalag
  - Kiválasztunk egy véletlen elemét
  - Nem termel zajt és nem veszít adatot
- Lineáris folyamathálózat
- (Összes adat) - (még megvan) = (eltűnt)
  - Nem eltűnt, hanem hiánytalanul át lett adva másnak
    - A következő történetében kell benne legyen
      - Nem az aktuálisban, mert lehet, hogy már feldolgozta
- Sorrendtartóan feldolgozta a doboz az adatokat
  - Ennek minden pillanatban teljesülnie kell
    - Nem lehet olyan, hogy eltűnik és megkerül
  - Ha van ilyen akkor az az atomi művelet belselyében van -> nem megfigyelhető
- Ez olyan szigorítás, hogy csak futószalaggal lehet megoldani
- Fixpont finomítás
  - Szigorítás
  - Új invariáns és új fixpont -> eredeti fixpont
- $ \forall i:[0..n]: f_i(\bar x_i-x_i) = \bar x_{i+1} $
- $ FP_h \Rightarrow x_i = <> $
- $ f^i(\bar x_i) = \bar x_{i+1} $
- Variáns függvény erre a futószalagra
  - Csökkennek az elemszámok minden állomáson
  - Súlyozzuk az elemek számát az adott helyen
  - |D|+1 alapú számrendszer
  - Példa 9 elem a rendszerben, |D|+1=10
    - 9, 0, 0, 0 -> 9000 - kezdeteben az állomásokon lévő elemszám
    - 8, 1, 0, 0 -> 8100
    - 7, 2, 0, 0 -> 7200
    - 7, 1, 1, 0 -> 7110
    - ...
    - 1, 0, 0, 8 -> 1008
    - 0, 1, 0, 8 -> \_108
    - ...
    - 0, 0, 1, 1 -> \_\_11
    - Ha ezeket egy-egy számnak vesszük, akkor látszik, hogy csökkenek
- $ \bar{x}_i - lorem(x_i) = (\bar{x}_i - x_i);lov(x_i) $
- $ \square_{i=n}^n x_i,x _{i+1} := lorem(x_i), hiext(x_{i+1};f_i(x_i.lov)) \space ha \space x_i\neq <> $

## Elágazás

```
  a  +-----+      +------+  y
---->|     |  x   |      |---->
     | MUX |----->| FORK |
---->|     |      |      |---->
  b  +-----+      +------+  z
```

- Telekommunikációban a multiplexálás egyszerűsített modellje
- $ (\bar{x}-x)=merge(\bar{y}, \bar{z}) $
  - Erre nehéz lf-et számolni ezért feladatot finomítunk
- $ split(<>,<>,<>) = igen $
- $ split(a,b,c) => slpit(a;e, b;e, c) \wedge split(a;e, b, c;e) $
- A legkisebb ilyen függvény
- $ split(\bar{x}-x, \bar{y}, \bar{z}) $
- INV: $ \forall k \in \N: (|\bar{x}|=k) \hookrightarrow (|\bar{y}|+|\bar{z}|=k) $
- Ha felváltva csinálja, és kétszer szed és egyszer tesz, akkor a második elől kiszedi az első mindig

## Összefésülés

- $ split(\bar{x},\bar{a}-a, \bar{b}-b) $
- $ |\bar{a}| = k \hookrightarrow |\bar{x}|=k $
- $ |\bar{b}| = k \hookrightarrow |\bar{x}|=k $

## Kis programokból nagy program

### Két program uniója

- Egyszerre fut a két program
- Olyan mintha az összes részprogramból egyszerre válogatnánk
- Legtermészetesebb programkonstrukció
- Komponensek összeípítése
- Mi lesz a kezdő értékadással?
  - Csak egy közös változója van a két programnak
  - Közös változón össze tudnak veszni a kezdeti értékadáson
  - Nem determináns értékadás
    - Ez elronthatja az invariánsokat
  - Ha a kezdő értékadásoknál a közös változónál különböző értéket állítanának be, akkor nem lehet uniót venni
    - Ha függvény van a közös változó értékére, akkor a föggvényeknek is meg kell egyeznie
    - Az se egyenlő ha az egyikben értéket ad a másikban meg skip van
    - A teljes program számít
- Tulajdonságokat ki lehet számolni a komponensek tulajdonságaiból
- EventB program modell ellenőrzés az iparban
  - Nem magától bizonyít csak emberi támogatással
  - Bizonyítás ellenőrzés könnyű, konstrukció nehéz
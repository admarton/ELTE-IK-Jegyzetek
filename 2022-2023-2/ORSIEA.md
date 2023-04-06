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

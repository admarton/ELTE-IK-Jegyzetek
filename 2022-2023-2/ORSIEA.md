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
    - Hennessy - Theory  of processes
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
    -  odavezet, leadsto
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
- $ S = (SKIP, \{\square_{i \in [1..n-1]} a(i),a(i+1) := a(i+1), a(i) $ ha $ a(i) > a(i+1) \}) $
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
    


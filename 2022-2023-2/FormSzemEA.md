<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
        inlineMath: [['$','$']]
      }
    });
</script>
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script> 

# Formális szemantika

# 1. EA

- Horpácsi Dániel
- Nem marad el előadás
- Követelmények:
    - Nincs semmi kötelező számonkérés
    - Végén vizsga
        - Írásbeli, gépes teszt
        - Vizsgaidőszak
        - Elméleti és gyakorlati rész
            - ZH számonkérés pótlása
- Érdemes átnézni az előző óra anyagát
    - Kevesebbet többször átnézni könnyebb mint a végén az egészet megtanulni
- Alternatív jegyszerzés
    - Projekt, tudományos cikk feldolgozás, semantika implementáció vagy hasonló
    - Alkalmazott tudás
    - Előadást kell tartani és abból lehet jegyet kapni

## Bevezető

- Formális szemantika
    - Jelentés, definíció megadása
    - Formalitás teszi egyértelművé és pontossá

## Programozási nyelv

- Mesterséges nyelv
    - Nem természetesen alakultak ki, fejlődtek
    - Formálisan definiáltak
    - Alacsony szintről mentünk felfelé
    - Absztrakciók növelik a produktivitást
    - Formális lieírás teszi lehetővé, a helyesség ellenőrzést
    
# 2. EA

- Formália mert mert matematikai
- Szemantika mert a jelentés a lényeg
- K keretrendszer
    - Implementálták a C, Rust, Python, lassan C++ szintaxisát ebben
- Miért nem használ mindenki formális szemantikát?
    - Legtöbb programozó nem kíváncsi a formális szemantikára
    - Nincsenek barátságban a nyelvezettel
    - Az egyértelműségnek biztosításához kell
- Formálisan kell definiálni a nyelvet
    - Attól lehet szabályosan levezetni a dolgokat
    - Ellenpélda javascript
- Fordító program nem definiálja a nyelvet
    - Szemantika absztraktabb mint az implementáció - undefined behavior

## Programozási nyelv definíciója

- Szintaxis
    - Milyen szimbólumsorozatnak van értelme?
    - Nyelvtan mondja meg, hogy mi a helyes sorozat.
    - Formális grammatika
    - Szintax error
    - Környezetfüggetlen grammatika
        - Nem elég egy ilyen a nyelv leírásához
    - Nem biztos, hogy a grammatikában egyértelmű a szintaktika
- Szemantika
    - Összes szintaktikailag helyes kódra meg lehet mondani, hogy mit jelent?
    - Mi a hatása a programnak?
        - Mi történik az állapotterében és a környezetében?
        - Milyen állapotokon ment keresztül?
    - Statikus szemantikai hibák
        - Statikusan meg lehet mondani pl int-et és bool-t nem lehet összeadni, ismeretlen változó használat, stb.
        - Ez még inkább a szintaxis része, de szemantika
        - Környezetfüggő tulajdonságok
    - Szintaxis fán dolgozunk, nem a fává alakítás most a feladat
- Pragmatika
    - Hogyan lehet olvasható, konvencionális és hatékony a kód?

## Formális szemantika formális megadása

- Alapvető dokumentációt ad a nyelvhez
- Matematikai leírást már lehet elemezni
    - Tulajdonságokat lehet mondani
        - Gyorsaság, energiaigény
    - Ekvivalenciát lehet megadni programok között
    - Helyességet vizsgálhatunk

## Formális szemantika megadása

- Különböző felhasználók
    - Fordítóprogramtervező
        - Hogyan tud bájtkódot csinálni
    - Nyelvtervező és helyességbizonyító
        - Mi lesz a program hatása
    - Programozó
        - Terminál-e
        - Egyéb tulajdonságok
- Megközelítések
    - (Attribútum grammatika)
    - Operációs (műveleti) szemantika 
    - Denotációs (leíró) szemantika
    - Axiomatikus szemantika
- Variációk
    - Reduction semantics
    - Action semantics
    - Categorical semantics
    - Game semantics

# 3. EA

## Egyszerű kifejezés formális szemantikája

- Ez az első lépés a programozási nyelvek szemantikájának megadása felé
- **Fontos**
    - Csak olyan nyelvekkel foglakozunk aminek nincs környezetfüggő grammatikája
    - Minden környezetfüggetlen grammatikákkal foglakozunk a félév során
- **Konkrét szintaxis**
    - hogyan lehet megadni helyes mondatokat
    - erre tudunk írni szintaktikus elemzőt - parsert
- **Absztrakt szintaxis**
    - sok szimbólumot el lehet absztahálni
    - elválasztójelek is ilenek
    - pl listában lehet-e az első elem előtt vessző
        - a lényeg az elemek
    - ez alapján nem tudsz parser-t írni
    - mi az absztrakt szintaxisfából megmondjuk, hogy mit jelent a program
    - Kimaradnak ilyenek
        - Kulcsszavak
        - Precedenciák, asszociativitási szabályok
            - ezek már tisztázottak
        - Zárójelek
        - Elválasztó és termináló szimbólumok
            - szintaktikus elemzést segítik
        - Olvasást segítő szimbólumok
- Megközelítés
    - Operációs (műveleti) szemantika
        - reláció, átmenetrendszer, levezetés
        - Megdja hogyan kell végrehajtani
        - Lépésről lépésre hogyan kell végrehajtani, levezetni
    - Denotációs (leíró) szemantika
        - kompozicionális függvény
            - részjelentésekből komponálom össze
        - A jelentést denotációk hozzárendelésével adja meg
        - A hatásra vagyok kíváncsi - az eredményre
    - *Axiomatikus - Hoare hármas*
        - Nem viselkedés, hanem tulajdonságokat vezet le
    
## Első nyelv

- Kifejezésnyelv
- Két résznyelv
    - a - Aexp - aritmetikai kifejezés
    - b- Bexp - logikai kifejezések
- Egyéb
    - n - Num - szám
    - x - Var - változó
- Szabályok, konstruktorok
    - a ::== n | x | a1 + a2 | a1 - a2 | -a
    - b ::== true | false | a1 = a2 | a1 < a2 | ¬b | b1 ∧ b2
- Ki akarjuk értékelni a kifejezéseket
    - Minden változó előre definiált és inicializált
        - Minden állapotban egész számok vannak a változókban
- Fogalom - **Konfiguráció**
    - $ s \in State = Var \rightarrow \Z $
    - s ∈ State = Var → Z
    - s[x] - x értéke
    - s[y |-> x] - érték módosítás
    - < a, s > - állapot és szemantika
- Operációs szematika
    - megadjuk hogy hogyan kell kiértékelni
    - és kiértékelgetem egy absztrakt gépen
    - Konfiguráció és átmenet
        - relációk
        - általános levezetési szabályok
        - sajátos jelölésrendszer
    - ha az átmenet levezethető akkor helyes
    - $ \frac{Premises}{Conclusion} Conditions $
    - $ \frac{}{Axiom} Conditions $
    - Előfeltétel és peremfeltételekből konklúzió
    - Ha nincs előfeltétel akkor axioma
    - $ [Num] \frac{}{<n,s>\Rightarrow N[[n]]} $
    - $ [Var] \frac{}{<x,s>\Rightarrow s[x]} $
    - $ [LHS] \frac{<a1,s>\Rightarrow <a1',s>}{<a1 \circ a2,s>\Rightarrow <a1' \circ a2,s >} \circ \in \{+,-,<,=\} $
    - $ [LHSLast] \frac{<a1,s>\Rightarrow i}{<a1 \circ a2,s>\Rightarrow <n \circ a2,s >} \circ \in \{+,-,<,=\}, N[[n]] = i $
    - $ \frac{<a2,s>\Rightarrow <a2',s>}{<n \circ a2,s>\Rightarrow <n \circ a2',s >} \circ \in \{+,-,<,=\} $
    - $ \frac{<a2,s>\Rightarrow i}{<n \circ a2,s>\Rightarrow N[[n]] \circ i} \circ \in \{+,-,<,=\}, i \in Z $
    

# 4. EA

- Kis kifejezésnyelv
- Aritmetikai és logikai kifejezések
- Csak a szemantikával foglalkozunk, szintaktika már kész van
- Szemantikába be van építve, hogy balról jobbra normalizáljuk
    - előbb ki kell értékelni a baloldalt
- Determinisztikusság
    - Csak egy következő konfiguráció lehetséges-e
- Konfluens
    - Ha külön úton ugyan-oda visz
- Direkt átmenet reláció reflexív-tranzitív-lezártja
    - 0 vagy több lépéssel az egyik konfigurációból a másikba jutok
    - reflexív - bármilyen konfig relációban áll magával
    - tranzitív - a=>b és b=>c akkor a=>c

## Denotációs-leíró szemantika

- Jelentéssel akarom jellemezni
- Egy szemantikus függvényt adok ami a szintaktikábó szemantikát csinál
- Szemtikus megfeleltetés
    - $ A[[n]]s = \N[[n]] $
    - $ A[[x]]s = x[s] $
    - $ A[[a_1 + a_2]]s = A[[a_1]]s + A[[a_2]]s $
    - $ A[[a_1 - a_2]]s = A[[a_1]]s - A[[a_2]]s $
    - $ A[[-a]]s = 0 - A[[a]]s $
- Részszavak jelentése kiadja a teljes kifejezés jelentését
- Kompozícionális akkor ha csak a részeit használjuk az eredetiben
    - Így fog terminálni a rekurzió
- Szintaktikus elemek a "[[_]]" zárójelek közé írjuk
    - Metanyelv és objektumnyelv megkülönböztetése
- Kompozícionalitás
    - Minden szintatktikus konstrukcióhoz függvény
    - Összetett kifejezéseket a részkifejezések kombinálásával adom meg
    - Struktúrális indukciós bizonyításokhoz kell

## Tuljadonságok

- A szemantika teljes-e
    - Minden kofigurációra van-e rákövetkező
    - Minden lehetséges kifejezést lekezel-e
    - Egyértelmű-e
- Determinisztikus és termináló-e
- Operációs és denotációs szemantika ekvivalens-e

- Kifejezés kiértékelése determinisztikus
    - Ha <a,s>=>y és <a,s>=>y' akkor y=y'
    - Átmeneteszerkezet szerinti indukció

- Optimalizációkat lehet megadni
    - O[[0+a]] = O[[a]]
    

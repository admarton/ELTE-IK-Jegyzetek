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
  - _Axiomatikus - Hoare hármas_
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

# 5. EA

- $ S \in Stm$ (utasítás halmaz)
- S ::== **skip** | x:=a | S1;S2 | **if** b **then** S1 **else** S2 | **while** b **do** S
- Konfiguráció
  - <S, s> => <S',s'>
  - <S, s> => s' - ez a végkonfigutáció, elfogyott a kifejezés
    - Lehet olyan, hogy nem tudja megdni a következőt, az kiértékelési hiba
- SKIP
  - $ \frac{}{<skip, s> => s}$
- Ass
  - $ \frac{}{ <x:=a,s> => s[x->A[[a]]s] } $
- Seq
  - $ \frac{<S1,s>=><S1', s'>}{<S1;S2,s>=><S1';S2,s'>} $
  - $ \frac{<S1,s>=>s'}{<S1;S2,s>=><S2,s'>} $
- If
  - $ \frac{}{<if \space b \space then \space S1 \space else \space S2, s>=><S1,s>}B[[b]]s = tt $
  - $ \frac{}{<if \space b \space then \space S1 \space else \space S2, s>=><S2,s>}B[[b]]s = ff $
- While
  - <while b do S, s>=><if b then (S;while b do S) else skip, s>
- Levezetési lánc
  - Véges ha az utolsónak nincs rákövetkezője
  - Végtelen ha mindegyiknek van rákövetkezője
- =>^i - i átmenettel megy át oda
- =>\* - valamennyi átmenettel megy át
- Szekvencia
  - S1 kiértékelése és S2 kiértékelése lépészszámának összege a szekvenciájuk kiértékeléséen k a lépésszáma
  - S1 kiértékeléséhez k lépés kell
    - akkor a szekvencia kiértékelésénél k lépés után az S1 ki lesz értékelve
- Minden konfigutációra megmondja, hogyan lehet tovább haladni
- Determinisztikus
- Ebben a nyelvben nincs zsákutca, nem akad meg a végrehajtás
- Smallstep erősebb mint a denotációs

# 6. EA

- Lehet bizonyítani két programról, hogy ekvivalens

## Természetes szemantika - BigStep operationsal semantics

- Nincs kétféle átmenet
- Kezdő konfigutációból a vég konfigurációba jutok
- Egyszerűbb az érvelés
- Ez is reléció
- Szintaxis nem változik
- SKIP,s -> s - SKIP
- x:=a,s -> s[x->A[[a]]s] - Értékadás
- $ \frac{<S1,s>->s' \quad <S2,s'>->s''}{<S1;S2,s>->s''} $ - Szekvencia
- Lehet nem determinisztikus is
- Elágazás
  - $ \frac{<S1,s>->s'}{<if \space b \space then \space S1 \space else \space S2, s>->s'} $ - ha b igaz
  - $ \frac{<S2,s>->s'}{<if \space b \space then \space S1 \space else \space S2, s>->s'} $ - ha b hamis
- Ciklus
  - $\frac{<S,s>->s' \quad <while \space b \space do \space S,s'>->s''}{<while \space b \space do \space S,s>->s''}$ - ha a feltétel igaz
  - <while b do S, s> -> s' - ha a feltétel hamis
  - Csak a levezetésben vannak köztes állapotok
    - A relációban csak a végeredmény van
- Terminálás, divergálás
  - Nincs olyan hogy megakad a program
  - Olyan van hogy terminál vagy divergál
  - minden s állapotból mindig terminál vagy mindig divergál
- SmallStep általában könnyebb
- Levezetési fa
  - A reláció levezetés = program kimenete
  - Utasítás szintaxisa szerint vezérelhetődik
    - Meg lehet keresni a megfelelő szabályt
      - Lehet automatizálni
      - Automatikusan csak azzal lehet tovább menni
    - Ha nincs szamantika szabály akkor az hiba
      - Leszivárog részprogramról/részkifejezésről a tejes programra
- Extra info
  - Determinisztikus a programunk
  - Itt van rekurzió, denotációban ez nem működik
  - Erre is meg lehet mondani a szamtikus függvényt és lehet ekvivalenciát mondani a denotációs szemantikával
- Be lehet bizonyítani, hogy a small step és a big step egyenlő
  - Szemantikus fünnyvényt használva
  - <S,s>=>s' = <S,s>->s'
    - Small -> big
      - 1 lépéses levezetésre (skip, értékadás) triviális, mert ua a def
      - Feltesszük, h smallstep K lépés egy lépés a bigstep-ban
      - Bizonyítjuk k+1 lépésre
        - Szekvenciára lehet úgy bizonyítani, hogy k1 és k2 lépésben lehet megcsinálni és mindkettő kisebb mint k+1 ezért igaz az indukciós hipotézis és utána lehet használni a bigstep szekvenciát
        - Elágazásra esetszétválasztás és használható a bigstep
        - Ciklusra smallstepben egy szabály van csak és utána k lépés marad, arra meg lehet használni a hipotézist
          - elégazés igaz ágában szekvencia bizonyítás
          - hamis ágban skip bizonyítás
    - Big -> small
      - Nem lépésszám szerinti indukció
      - skip és értékadás triviális
      - Szekvencia vissza avn vezetve a smallstep szekvenciáre
      - Elágazásnál esetszétválasztás tranzitívitás, kipótoljuk a hiányzó lépéseket
      - Ciklusnál is esetszétválasztás, hipotézis a részeire, utána smallstep levezetés
      - Kipótoljuk a smallstep lépéseket

# 7.EA

## Denotációs szemantika

- Teljes függvény ami parciális függvényt ad vissza

- $S_{ds}:Stm\rightarrow (State \hookrightarrow State)$
- $S_{ds}[[SKIP]]=id_{State}$
- $S_{ds}[[x:=a]]=s[x\mapsto A[[a]]s]$
- $S_{ds}[[S1;S2]]=S_{ds}[[S2]] \circ S_{ds}[[S1]]$
- $S_{ds}[[IF \space b \space THEN \space S1 \space ELSE \space S2 ]]= cond(B[[b]],S_{ds}[[S1]],S_{ds}[[S2]])$
- $S_{ds}[[WHILE \space b \space DO \space S]]=FIX \space F$
  - $F g = cond(B[[b]], g \circ S_{ds}[[S]], id_{State})$

# 8. EA

## Denotációs szemantika -ciklus

- Lexikális elem: `undef`
  - Ciklus nem visz végállapotra
- Iterációval lehet megadni
- $ iter_0 (p,g)s = undef $
- $ iter\_{k+1} (p,g)s = s $ ha $ p s = ff $
- $ iter\_{k+1} (p,g)s = iter_k (p,g)(g s) $ ha $ p s = tt $
- vagy
- $ iter_0 (p,g) = \bot $
- $ iter\_{k+1} (p,g)s = cond(p, iter_k(p,g) \circ g, id) $
- Ciklus lehet az, hogy s' ha van olyan k amire az iter_k nem undef, különben undef.
- FIX F = Legkisebb felső korlátja az F^n(bot) sorozatnak

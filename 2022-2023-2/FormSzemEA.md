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


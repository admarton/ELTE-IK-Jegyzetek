# Programozás Módszertan

# 1. GYAK

- 10:15 kezdés
- +/- minden órán
- Két algoritmus minta
    - Összegzés és számlálás
    - Specifikáció, program
- Első ZH-ban ciklusokat kell írni

## Feladatok - 24

- Hány számjegye van egy adott pozitív egésznek?
    - $ A = ( x:\mathbb{N}^+, d:\mathbb{N}^+ ) $  
    - $ B = ( x':\mathbb{N}^+ ) $  
    - $ Q = ( x = x' ) $  
    - $ R = ( Q \wedge d = \lfloor log_{10}x \rfloor + 1 ) $  

- Megoldás: $ d := \lfloor log_{10}x \rfloor + 1 $  
    - Bizonyítás:  
    - Specifikáció tétele alapján:  
    - $ Q => lf(d:=\lfloor log_{10}x \rfloor + 1, R) $  
    - $ (Q \wedge \lfloor log_{10}x \rfloor + 1 = \lfloor log_{10}x \rfloor + 1) $

- Megoldás 2:  
    - $ R =( Q \wedge d = 10^{d-1} \leq x \wedge x < 10^d ) $  
    - P - ciklus invariáns  
    - $ P = ( Q \wedge 10^{d-1} \leq x ) $
    - Ciklus levezetés 5 szabálya:
        1. $ Q \Rightarrow P $  
            $ q \Rightarrow ( Q \wedge 10^{d-1} \leq x ) $  
        2. $ P \wedge \neg \pi \Rightarrow R $  
            $ P \wedge x < 10^d \Rightarrow R $  
            Ebből:  
            $ \pi = (x \geq 10^d) $    
        3. $ P \Rightarrow x \geq 10^d \vee x < 10^d $  
            Igaz mert minden pozitív egész
        4. $ P \wedge \pi \Rightarrow t > 0 \quad\quad t:x-d $  
            $ d < 10^d < x \Rightarrow d < x $  
        5. $ P \wedge \pi \wedge t=t_0 \Rightarrow lf(s_0, P \wedge t < t_0) $  
            $ P \wedge x \leq 10^d \wedge x-d=t_0 \Rightarrow lf(d:=d+1, P\wedge x-d < t_0) $  
            $ = (Q \wedge 10^d\leq x \wedge x-(d+1)<t_0 ) $  
    - A ciklusmagban növeljük a *d* értékét, hogy megálljon a ciklus
    ```
    ┌──────────┐
    │ x>=10^d  │
    │  ┌───────┤
    │  │d:=d+1 │
    └──┴───────┘
    ```
    - **NEM LETT JÓ, MERT AZ ELSŐ PONT NEM TELJESÜL**
    - Szekvencia
    - Egy értékadás és az előző ciklus
    - Levezetés:
        1. $ Q \Rightarrow lf(S_1, Q') $  
            - S_1 kitalálásához meg kell mondani a Q'-t
            - Utána van értelme a programmot megadni
            - $ Q' = (Q \wedge d=1) $
            - $ S_1 = (d := 1) $  
        2. $ Q' \Rightarrow lf(DO, R) $  
    - MOST VAN KÉSZ

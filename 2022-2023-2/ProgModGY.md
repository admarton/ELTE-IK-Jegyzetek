<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
        inlineMath: [['$','$']]
      }
    });
</script>
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script> 

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

# 2. GYAK

## 2. feladat

- Két pozitív egész legnagyobb közös osztója
- $ A = (x:\N^+, y:\N^+, z:\N^+) $
- $ B = (x':\N^+, y':\N^+) $  
- $ Q = (x=x' \wedge y=y') $
- $ R = ( Q \wedge z=lnko(x,y) )  $ - lnko nem használható a programban
- $ R = ( Q \wedge z \vert x \wedge z \vert y \wedge \forall k\in\N^+:k>z\rightarrow \neg (k \vert x \wedge k \vert y) )  $
- $ R = ( Q \wedge z \vert x \wedge z \vert y \wedge \forall k\in[z+1,...,min(x,y)]:\neg (k \vert x \wedge k \vert y) )  $

- Ciklus
    - $ P = (Q \wedge \forall k\in[z+1,...,min(x,y)]:\neg (k \vert x \wedge k \vert y) ) $
    - (2.) $ P \wedge z \vert x \wedge z \vert y \Rightarrow R  $ 
    - (3.) $ P \Rightarrow \neg (z \vert x \wedge z \vert y) \vee (z \vert x \wedge z \vert y) $
        - Ez most igaz, mert z nem lehet 0 a típusa miatt
    - $ t : z $
    - (4.) $ P \wedge \pi \Rightarrow t > 0 $ 
        - z a típusa miatt fixen nagyobb mint 0
    - (5.) $ P \wedge \pi \wedge t=t_0 \Rightarrow lf(S_0, P \wedge t<t_0 ) $
        - $ S_0 : z:=z-1 $
        - $ (Q \wedge \forall k\in [z,..,min(x,y)]:\neg (k \vert x \wedge k \vert y) \wedge z-1<t_0 \wedge z\neq 1) $
            - Q része P-nek
            - Szétválasztuk a mindenes feltételt z-re és z+1-től min-ig részre
                - Második ele az invariánsban benne van
                - Első fele a ciklus feltétel
            - z-1 < t_0
            - z != 1 
                - igaz mert a ciklusfeltétel miatt nem lehet z közös osztó, de 1 közös osztó
    - (1.) $ Q \Rightarrow P $
        - Ez nem igaz
- Szekvenciát csinálunk
    - $ Q' \Rightarrow P $
    - $ Q' = (Q \wedge z=min(x,y) ) $
    - **Üres halmaz minden elemére minden igaz**
    - Ezek miatt $ Q' \Rightarrow P $
    - $ Q \Rightarrow lf(z:=min(x,y),Q') $ - teljesül
    - - Ezt elágazással lehetne megcsinálni

## 15. feladat
            
- **n** alatt a **k**
- $ A = (n:\N,k:\N,s:\N^+) $
- $ B = (n':\N,k':\N) $
- $ Q = (n=n' \wedge k=k') $
- $ R = (Q \wedge S=\binom{n}{k}) $ - binom-ot nem lehet használni
- $ R = (Q \wedge S=\frac{n!}{k!(n-k)!}) $ - faktoriálist nem lehet használni
- $ \binom{n}{k} = \frac{n!}{k!(n-k)!} = \frac{(n-k+1)*...*n}{k!} = \prod_{i=0}^{k-1} \frac{n-i}{i+1} $
- $ R = (Q \wedge S=\prod_{i=0}^{k-1} \frac{n-i}{i+1}) $
- Ciklus
    - $ P = (Q \wedge S=\prod_{i=0}^{x} \frac{n-i}{i+1} \wedge x\in[-1..k-1]) \mid x:\Z $
    - (2.) $ P \wedge x=k-1 \Rightarrow R $
        - $ \pi = (x \neq k-1 ) $
    - (3.) $ P \Rightarrow x \neq k-1 \vee x = k-1 $
    - $ t: k-x $
    - (4.) $ P \wedge \pi \Rightarrow k-x > 0 $
        - Az invariánsból következik (**az invariánsba be kellett írni az x megkötését**)
    - (5.) $ P \wedge \pi \wedge k-x=t_0 \Rightarrow lf(x,s:=x+1,s*\frac{n-x-1}{x+2}, P \wedge k-x<t_0) $
        - $ (Q \wedge s*\frac{n-x-1}{x+2}=\prod_{i=0}^{x+1} \frac{n-i}{i+1} \wedge x+1\in[-1..k-1] \wedge k-x-1<t_0) \wedge s*\frac{n-x-1}{x+2}\in\N^+ $
            - Q - P-ből
            - algebrai egyenlőség
            - x < k-1 akk x+1 <= k-1
            - egyel kisebb kisebb lesz
            - egyenlő az n alatt az x+2-vel ami egész
- Szekvencia az elején
    - **Def.:** $ \prod_{i=0}^{-1}...=1 $
    - $ Q' = (Q \wedge x=-1 \wedge s=1) $

## +/-

- Összegzés és számolás
- Specifikáció és program
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

# 3. GYAK

## 28. Feladat

- Fordítsuk meg a tömb elemeit
- $ A = (x:\mathbb{Z}^n) $
- $ B = (x':\mathbb{Z}^n) $
- $ Q = (x=x') $
- $ R = (\forall i \in [1..n]: x[i]=x'[n-i+1]) $
- $ P = (\forall i \in [1..k]: (x[i]=x'[n-i+1] \wedge $  
    $ x[n-i+1]=x'[i]) \wedge $   
    $ \forall i \in [k+1..n-k]: x[i]=x'[i] \wedge $   
    $ k \in [0..\lfloor \frac{n}{2} \rfloor]) \quad k:\mathbb{Z} $ 
- 2.pont: $ P \wedge k = \lfloor \frac{n}{2} \rfloor \Rightarrow R $
    - azért egyezik meg önmagával, mert az invariáns biztosítja, hogy ez igaz
- 3.pont: $P \Rightarrow k=\lfloor \frac{n}{2} \rfloor \vee k \neq \lfloor \frac{n}{2} \rfloor$
- 1.pont: $Q \Rightarrow P$
    - Önmagában nem teljesül
    - Szekvenciával oldjuk meg
    - $ Q' = (Q \wedge k=0) $
        - Első minden igaz mert üres halmaz
        - Második minden a Q miatt teljesül
        - 0 benen van a [0...] intervallumban
- 4.pont: $ P \wedge \lfloor \frac{n}{2} \rfloor \neq k \Rightarrow \lfloor \frac{n}{2} \rfloor - k > 0 $
    - termináló fgv.: $ \lfloor \frac{n}{2} \rfloor - k $
    - Invariáns és a nem egyenlő miatt igaz
- 5.pont $P \wedge \pi \wedge t=t_0 \Rightarrow lf(S_0, P \wedge t<t_0)$
    - S_0 szekvencia
    - $ P \wedge \lfloor \frac{n}{2} \rfloor \neq k \wedge \lfloor \frac{n}{2} \rfloor -k = t_0 \Rightarrow lf(x[k+1],x[n-k]:=x[n-k],x[k+1], Q'' \wedge \lfloor \frac{n}{2} \rfloor-k=t_0) $
    - $ Q'' = P^{k\leftarrow k+1} $
    - $ Q'' \wedge \lfloor \frac{n}{2} \rfloor -k =t_0 \Rightarrow lf(k:=k+1, P \wedge \lfloor \frac{n}{2} \rfloor-k < t_0 ) $
    - $ Q'' = \forall i \in [1..k]: (x[i]=x'[n-i+1] \wedge $  
        $ x[n-i+1]=x'[i]) \wedge $   
        $ (x[k+1]=x'[n-k] \wedge x'[k+1]=x[n-k])  \wedge $ // azért van így hogy könnyű legyen bizonyítani  
        $ \forall i \in [k+1+1..n-k-1]: x[i]=x'[i] \wedge $   
        $ k+1 \in [0..\lfloor \frac{n}{2} \rfloor]) $ 
    - Értékadásnál figyelni kell hogy nem indexelek ki
        - $ k+1,n-k \in [1..n] $
        - lf-ben: A mindentől különválasztott részt kell behelyettesíteni
            - A többi nem változik
        
## 24. feladat

- Számjegyeinek száma
- $ A = (x:\mathbb{Z}^+, d:\mathbb{N}) $
- $ B = (x':\mathbb{Z}^+) $
- Q = (x=x')
- $ R = (Q \wedge d=szjsz(x)) $
- szjsz(x) = 
    - 1 + szjsz(x div10) x!=0
    - 0 ha x=0
- $ P = (Q \wedge szjsz(x)=d+szjsz(y)) \quad y:\mathbb{N}$
- 2: $ P \wedge szjsz(y) = 0 \Rightarrow R $
- 2: $ P \wedge y = 0 \Rightarrow R $
    - $ \pi = (y \neq 0) $
- 1: $ Q \Rightarrow P $
    - Szekvencia lesz a megoldás
    - $ Q' = (Q \wedge y=x \wedge d=0) $
    - $ Q' \Rightarrow P $ 
        - szjsz(x) = 0 + szjsz(x)
- 3: $ P \Rightarrow y=0 \vee y\neq 0 $
- $ S_0 = (y,d := y div 10, d+1) $ 
- $ t = y $
- 4: $ P \wedge y\neq 0 \Rightarrow y > 0 $
- 5: $ P \wedge y\neq 0 \wedge y=t_0 \Rightarrow lf(y,d := y div 10, d+1, P \wedge y<t_0) $
    - $ Q \wedge szjsz(x)=d+1+szjsz(y div 10) \wedge y div 10 < t_0 $

## +/-

- Maximum keresés
- Specifikáció és stuktrogram

# 5.GYAK
Keddi gyak:


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

# 1. GYAK

- Kezdés 16:00
- +/- az óra elején
    - legalább 0-ba kell kihozni, hiányzás minusz
- 2 DB ZH
    - félév fele (kb 6. hét), vizsgaidőszak eleje
- Beadandó nem lesz valszeg
- Gyak jegy kell az EA-hoz
- CANVAS - slideok, plusz infók, teams csoport nem lesz
- matej@inf.elte.hu
    - 2.616 a szoba

## Elméleti programozás lesz

- Feladat formális leírása
    - specifikáció
- Absztrakt program
    - Megfeelel-e a spec-nek, megoldja a feladatot
- Párhuzamos programokra
- Levezetés és tételre visszavezetés

## Leggyengébb előfeltétel - lf

- Def.: lf(S,R) - leggyengébb előfeltétele egy programnak egy specifikációra nézve
    - Állapottérbeli pontok amiből az S R-be visz
    - $ \lceil lf(S,R) \rceil ::= \{ a \in D_{p(s)} \mid p(s)(a) \subseteq \lceil R \rceil \}  $

- Értékadás  
    lf( x := 5, 0 < x + y )= 0 < 5 + y
- Feltételes értékadás  
    $ lf( x := 5 \quad ha \quad y < 1, 0 < x + y )=( y < 1 \rightarrow 0 < 5 + y) \wedge (s \geq 1 \rightarrow 0 < x + y) $
- Szimultán értékadás 
    $ lf(x,y:=5,x+1 \space ha \space y < 1, 0 < x+y) = (y<1 \rightarrow 0<5+x+1) \wedge (y \geq 1 \rightarrow 0 < x+y) $

## **Párhuzamos absztrakt program**

- $ S = (s_0, \{s_1,...,s_n \}) $ 
    - Kezdeti állapot: s_0
    - Utasítások halmaza
        - Addig hajtjuk végre őket ameddig még tudnak változtatni

### Megszorítás

- A kis utasításokat atominak tekintjük
- Nem foglalkozunk a műveletek végrehajtásának összelapolódásával
- Különböző szekvenciális sorrendek lehetséges eredményeit nézegetjük
    - **Összefésüléses szemantika**
- **Feltétlenül pártatlan ütemezés**
    - Mindegyikből végtelen legyen, ne legyen olyan amiből véges sok van
    - Bármelyik utasítástól nézem az ütemezést, akkor egy idő után mindegyik utasítás végrehajtódik

### Példa

$ A = \mathbb{N}_0×\mathbb{N}_0 $  
$ S = (s_0 : x,y := (21,7), \{ s_1 :x := \space ha \space y < 4; s_2 : y := 2 \}) $  

(10,12) -> (21,7) -> (21,7) ->...-> (21,7) -> (5,2) -> (5,2) ->...-> (5,2) 

- Hol van olyan pont ahonnan már nem tud változtatni? -> **FIX PONT**
    - nem feltétlenül jut oda
    - **s_0 nem változtat rajta**
- Milyen FIX PONTokba jut el?
- Milyen állapotokat érinthet?
- Mik a nem elérhető állapotok?

## Leggyengébb előfeltétel párhuzamos programra

- Legkisebb építőelem, utána a többi tulajdonság
- Milyen pontból induljak, hogy egy lépés után R-be érjek?
- **s_0 nem számít itt sem**
- $ lf(S,R) = \bigwedge_{i=1}^n lf(s_i, R) $
- *S* párhuzamos program pár = (s_0, S)
- *S* az utasításhalmaz is

### Példa

$ A = \mathbb{N}_0×\mathbb{N}_0 $  
$ S = (s_0 : x,y := (21,7), \{ s_1 :x := 5 \space ha \space y < 4; s_2 : y := 2 \}) $  
$ R = 0 < x + y $

$ lf(S,R) = lf(s_1,R) \wedge lf(s_2,R) = ((y < 4 \rightarrow 0 < 5 + y) \wedge (y \geq 4 \rightarrow 0 < x + y)) \wedge (0 < x + 2) $

## LF tulajdonságok
- Csoda kizárása  
    $ lf(S,\downarrow) = \downarrow $
- Monotonitás  
    ha $ P \Rightarrow Q $ akkor $ lf(S,P) \Rightarrow lf(S,Q) $
- Konjunkció  
    $ lf(S, P \wedge Q) = lf(S,P) \wedge lf(S,Q) $
- Diszjunkció  
    $ lf(S, P \vee Q) \Leftarrow lf(S,P) \vee lf(S,Q) $

# 2. GYAK

## Háromszög tulajdonság

- $ P \triangleright_S Q ::== P \wedge \neg Q \Rightarrow lf( S,P \vee Q)$
- P-ből csak úgy mehetek ki, ha előtte beléptem Q-ba
    - Pl helyes állapotból csak úgy léphetek ki ha előtte bementem a hibakezelési állapotba :  
    $ Helyes \triangleright Hibakezelés $
- Biztonságossági tulajdonság
- $ P \triangleright_P \downarrow = P \Rightarrow lf(S,P) $
    - Ha egyszer teljesül akkor onnan nem tud kilépni
    - **Stabil**

### Példa

- $ A=\Z × \Z $
- $S = (s_0, \{s_1: x:=x-1 , s_2: y := x \}) $
- $P = ( x > 0 \wedge y > 0 )$
- $Q = (x = 0)$
- $ P \triangleright_SQ = P \wedge \neg Q \Rightarrow lf( S,P \vee Q) $  
    $ = ( x > 0 \wedge y > 0 ) \wedge \neg (x = 0) \Rightarrow lf(S, ...)$  
    $ = ( x > 0 \wedge y > 0 ) \Rightarrow lf(s_1, P \vee Q) \wedge lf(s_2, P \vee Q) $  
    $ = ( x > 0 \wedge y > 0 ) \Rightarrow ((x-1 > 0 \wedge y > 0) \vee x-1=0) \wedge ( x > 0 \vee x = 0 ) $  
    $ = ( (x > 1 \vee x=1) \wedge y > 0 ) \Rightarrow ((x-1 > 0 \wedge y > 0) \vee x-1=0) \wedge ( x > 0 \vee x = 0 ) $
- Teljesül

### Példa Stabil
- $ S = (s_0: x,y:=10,20, \{ s_1: x := x+y \}) $
- $ P = x > 0 $
- $ P \triangleright_S \downarrow = P \Rightarrow lf( S,P) $  
    $= x > 0 \Rightarrow lf(s_1, x>0) $  
    $= x > 0 \Rightarrow x+y>0 $
- Nem feltétlenül tejesül
    - y-ról nem tudunk ehhez megfelelő infót
- Nem stabil a P
- A nem elérhető állapotokkal is foglakozni kell
    - Feltételt úgy kell megadni, hogy minden benne legyen
    - P-be be lehet írni, hogy y is legyen nagyobb mint 0

## 1. Feladat

- $ P \triangleright_S P $ teljesül bármilyen P és S-re
- $ P \wedge \neg P \Rightarrow lf(S,P \vee P) $
- $ \downarrow \Rightarrow lf(S,P) $
- Ez mindig teljesül

## 2. Fealdat

- $ P \triangleright_S \neg P $ teljesül bármilyen P és S-re
- $ P \wedge P \Rightarrow lf(S,P \vee \neg P) $
- $ P \Rightarrow lf(S,\uparrow) $
- $ \lceil lf(S,\uparrow) \rceil = \bigcap_{i=1}^nD_r(s_i) $
- Úgy kell megadni a programot, hogy a teljes állapotteren értelmes legyen
    - $ \forall i\in[0,n] : D_r(s_i) = A $
    - explicit meg kell mindent mondani
        - ha x pozitív, akkor a csökkentése feltételes kell legyen
- $ \bigcap_{i=1}^nD_r(s_i) = \bigcap A = A $

## 3. Fealdat

- $ \frac{P \triangleright_S Q, Q \Rightarrow R}{P \triangleright_S R}$
    - $ P \wedge \neg Q \Rightarrow ... $

## Héromszög **jobboldal gyengítés**

- $ \frac{P \triangleright_S Q, Q \Rightarrow R}{P \triangleright_S R}$

## Hárpmszög **diszjunktivitás**

- $ \frac{P \triangleright_SR, Q \triangleright_SR}{(P\vee Q) \triangleright_SR} $

# 3. GYAK


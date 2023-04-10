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
  - $ \lceil lf(S,R) \rceil ::= \{ a \in D\_{p(s)} \mid p(s)(a) \subseteq \lceil R \rceil \} $

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

$ A = \mathbb{N}\_0×\mathbb{N}\_0 $  
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
- $ lf(S,R) = \bigwedge\_{i=1}^n lf(s_i, R) $
- _S_ párhuzamos program pár = (s_0, S)
- _S_ az utasításhalmaz is

### Példa

$ A = \mathbb{N}\_0×\mathbb{N}\_0 $  
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
- $ \lceil lf(S,\uparrow) \rceil = \bigcap\_{i=1}^nD_r(s_i) $
- Úgy kell megadni a programot, hogy a teljes állapotteren értelmes legyen
  - $ \forall i\in[0,n] : D_r(s_i) = A $
  - explicit meg kell mindent mondani
    - ha x pozitív, akkor a csökkentése feltételes kell legyen
- $ \bigcap\_{i=1}^nD_r(s_i) = \bigcap A = A $

## 3. Fealdat

- $ \cfrac{P \triangleright_S Q, Q \Rightarrow R}{P \triangleright_S R}$
  - $ P \wedge \neg Q \Rightarrow ... $

## Háromszög **jobboldal gyengítés**

- $ \cfrac{P \triangleright_S Q, Q \Rightarrow R}{P \triangleright_S R}$

## Háromszög **diszjunktivitás**

- $ \cfrac{P \triangleright_SR, Q \triangleright_SR}{(P\vee Q) \triangleright_SR} $

# 3. GYAK

## Háromszög tranzitivitás - **nem teljesül**

- $ \cfrac{P \triangleright_S Q, Q \triangleright_S R}{P \triangleright_S R} $
- Ellenpéldát kell adni

<svg width="400" height="400" xmlns="http://www.w3.org/2000/svg">
  <rect width="400" height="400" fill="#fff" />
  <ellipse stroke-width="5" ry="98.33334" rx="106.11112" id="svg_2" cy="143.33334" cx="137.22222" stroke="#000" fill="none"/>
  <ellipse ry="101.38889" rx="102.77778" id="svg_5" cy="154.72223" cx="274.44445" stroke-width="5" stroke="#000" fill="none"/>
  <ellipse ry="97.22223" rx="95.83334" id="svg_6" cy="261.11112" cx="209.72224" stroke-width="5" stroke="#000" fill="none"/>
  <text xml:space="preserve" text-anchor="start" font-family="'Petrona'" font-size="30" id="svg_9" y="57.22223" x="47.22223" stroke-width="0" stroke="#000" fill="#000000">P</text>
  <text xml:space="preserve" text-anchor="start" font-family="'Petrona'" font-size="30" id="svg_10" y="51.66667" x="322.22225" stroke-width="0" stroke="#000" fill="#000000">Q</text>
  <text xml:space="preserve" text-anchor="start" font-family="'Petrona'" font-size="30" id="svg_11" y="364.44446" x="265.55557" stroke-width="0" stroke="#000" fill="#000000">R</text>
  <path id="svg_12" d="m97.31612,106.99668l5,-5.27778l5,5.27778l-5,5.27778l-5,-5.27778z" stroke-width="5" stroke="#000" fill="#fff"/>
  <path id="svg_13" d="m305.13841,147.18943l6.3889,-8.05555l6.3889,8.05555l-6.3889,8.05555l-6.3889,-8.05555z" stroke-width="5" stroke="#000" fill="#fff"/>
  <line id="svg_14" y2="107.22223" x2="284.44447" y1="106.11112" x1="103.33335" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_15" y2="107.22223" x2="283.88891" y1="93.88889" x1="266.11113" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_16" y2="110.55556" x2="283.88891" y1="121.66667" x1="270.55558" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_17" y2="103.33334" x2="105.00001" y1="77.22223" x1="122.77779" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_18" y2="287.22224" x2="213.33335" y1="154.44445" x1="312.22225" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_19" y2="77.22223" x2="123.8889" y1="78.33334" x1="105.00001" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_20" y2="286.66668" x2="215.55557" y1="285.00001" x1="235.55558" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_21" y2="152.77779" x2="316.11114" y1="194.44445" x1="326.66669" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_22" y2="77.22223" x2="122.77779" y1="94.44445" x1="125.00002" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_23" y2="197.77779" x2="327.7778" y1="187.77779" x1="312.22225" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_24" y2="286.11113" x2="214.44446" y1="263.8889" x1="212.7778" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_25" y2="198.33334" x2="327.22225" y1="182.77779" x1="334.44447" stroke-width="5" stroke="#000" fill="none"/>
  <path id="svg_26" d="m89.55501,160.79056l11.67127,0l3.60651,-13.15664l3.60651,13.15664l11.67126,0l-9.44224,8.13116l3.6067,13.15664l-9.44224,-8.13138l-9.44224,8.13138l3.6067,-13.15664l-9.44224,-8.13116z" stroke-width="5" stroke="#000" fill="#fff"/>
  <line id="svg_27" y2="178.8889" x2="103.33335" y1="212.22223" x1="95.55557" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_28" y2="177.22223" x2="111.66668" y1="305.00002" x1="178.33335" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_29" y2="162.22223" x2="110.55557" y1="148.8889" x1="257.7778" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_30" y2="217.22223" x2="95.55557" y1="197.22223" x1="85.00001" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_31" y2="148.33334" x2="256.11113" y1="137.77779" x1="237.7778" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_32" y2="302.77779" x2="177.22224" y1="292.22224" x1="156.11113" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_33" y2="216.66668" x2="95.55557" y1="202.77779" x1="110.00001" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_34" y2="150.00001" x2="258.88891" y1="163.33334" x1="244.44447" stroke-width="5" stroke="#000" fill="none"/>
  <line id="svg_35" y2="305.00002" x2="179.44446" y1="283.33335" x1="181.11113" stroke-width="5" stroke="#000000" fill="none"/>
  <line id="svg_36" y2="146.11112" x2="163.33335" y1="171.11112" x1="146.11113" stroke-width="5" stroke="#ff0000" fill="none"/>
  <line id="svg_37" y2="173.33334" x2="167.77779" y1="146.11112" x1="140.00002" stroke-width="5" stroke="#ff0000" fill="none"/>
  <path id="svg_38" d="m6.04668,257.76445l9.72222,-10.83334l9.72222,10.83334l-9.72222,10.83334l-9.72222,-10.83334z" stroke-width="5" stroke="#000000" fill="#fff"/>
  <path id="svg_39" d="m5.51056,293.70248l10.61024,0l3.27865,-10.6102l3.27865,10.6102l10.61024,0l-8.58385,6.55739l3.27882,10.6102l-8.58385,-6.55757l-8.58385,6.55757l3.27882,-10.6102l-8.58385,-6.55739z" stroke-width="5" stroke="#000000" fill="#fff"/>
  <text xml:space="preserve" text-anchor="start" font-family="'Petrona'" font-size="30" id="svg_40" y="265.55557" x="27.77779" stroke-width="0" stroke="#000000" fill="#000000">ez van</text>
  <text xml:space="preserve" text-anchor="start" font-family="'Petrona'" font-size="30" id="svg_41" y="332.22224" x="13.8889" stroke-width="0" stroke="#000000" fill="#000000">ezt</text>
  <text xml:space="preserve" text-anchor="start" font-family="'Petrona'" font-size="30" id="svg_42" y="350.00002" x="4.44446" stroke-width="0" stroke="#000000" fill="#000000">szeretnénk</text>
</svg>

- $ A = (x:\mathbb{N}) $
- $ P = (x=1) $
- $ Q = (x=2) $
- $ R = (x=3) $
- $ S = (SKIP, {s:x:=x+1}) $
- $ P \triangleright_S Q $
  - $ P \wedge \neg Q \Rightarrow lf(S, P \vee Q) $
  - $ x = 1 \Rightarrow lf(x:=x+1, x=1 \vee x=2) $
  - $ x = 1 \Rightarrow x+1=1 \vee x+1=2 $
  - Teljesül
- $ Q \triangleright_S R $
  - $ Q \wedge \neg R \Rightarrow lf(S, Q \vee R) $
  - $ x = 2 \Rightarrow lf(x:=x+1, x=2 \vee x=3) $
  - $ x = 2 \Rightarrow x+1=2 \vee x+1=3 $
  - Teljesül
- $ P \triangleright_S R $
  - $ P \wedge \neg R \Rightarrow lf(S, P \vee R) $
  - $ x = 1 \Rightarrow lf(x:=x+1, x=1 \vee x=3) $
  - $ x = 1 \Rightarrow x+1=1 \vee x+1=3 $
  - Nem teljesül
- Erre a példára nem teljesül, tehát nem igaz az összes esetben

## ZH hibák

- Ha minden állítás teljesül az nem jó
  - Se nem bizonyítás, se nem cáfolat
- Ha a feltételelk bármelyike nem teljesül, az is hiba
  - Nem megfelelő ellenpélda

## Háromszög **stabil metszés**

- $ \cfrac{P \triangleright_S Q, K \triangleright_S \downarrow}{(P \wedge K) \triangleright_S (Q \wedge K)} $

## Egyenesnyil tulajdonság

- $ P \mapsto_S Q ::== P \triangleright_S Q $ és $ \exists s \in S : P \wedge \neg Q \Rightarrow lf(s,Q) $
- P-ből csak P-be és Q-ba lehet továbbmenni
  - De véges sok lépés után biztosan Q-ba átmegy.
- Ha P-ben vagyok, akkor előbb vagy utóbb át kell jutnom Q-ba
  - Úgy, hogy közben máshova nem mehetnek
- Ez egy **haladási tulajdonság**
- Szigorú tulajdonság, nem triviális, hogy mikor teljesül

### Példa I.

- $ A = x:\mathbb{Z} $
- $ S = (s_0 : x:=10, \{ s_1:x:=x+1 \}) $
- $ P = (x=1 \vee x=2) $
- $ Q = (x=3) $
- $ P \mapsto_S Q $ ?
  - $ P \triangleright_S Q $ és $ \exists s \in S : P \wedge \neg Q \Rightarrow lf(s,Q) $
  - Ha csak egy utasítás van, akkor a háromszög rész nem kell ellenőrizni, mert egy gyengébb állítás lesz
  - $ x=1 \vee x=2 \Rightarrow lf(s_1, Q) $
  - $ x=1 \vee x=2 \Rightarrow lf(x:=x+1, x=3) $
  - $ x=1 \vee x=2 \Rightarrow x+1=3 $
  - Ez így nem igaz
    - Ha x=1 akkor nem igaz
    - Ha x=2 akkor igez
    - Ezért $ P \mapsto_S Q $ nem igaz

### Példa III.

- $ A = x:\mathbb{Z} $
- $ S = (s_0 : x:=10, \{ s_1:x:=3 \}) $
- $ P = (x=1 \vee x=2) $
- $ Q = (x=3) $
- $ P \mapsto_S Q $ ?
  - $ P \triangleright_S Q $ és $ \exists s \in S : P \wedge \neg Q \Rightarrow lf(s,Q) $
  - $ x=1 \vee x=2 \Rightarrow lf(s_1, Q) $
  - $ x=1 \vee x=2 \Rightarrow lf(x:=3, x=3) $
  - $ x=1 \vee x=2 \Rightarrow 3=3 $
  - Ez így igaz
    - Ezért $ P \mapsto_S Q $ igaz

## 1. Feladat

- $ P \mapsto_S P $
- Igaz ha S nem üres
  - Ezt monstantól mindig feltesszük

## 2. Feladat

- $ P \mapsto_S \neg P $
- Nem igaz
- Ellenpélda:
  - $ A = x \in {1,2} $
  - $ P = (x=1) $
  - $ S = (SKIP, {SKIP}) $

## 3. Feladat - Enegyenesnyíl **jobboldal gyengítés**

- $ \cfrac{P\mapsto_S Q, Q\Rightarrow R}{P\mapsto_S R} $
- Ha S-ben van olyan s* ammivel az lf(s*,Q) megfelelő akkor az R-re is megfelelő lesz

# 4. GYAK

## 4. feladat - Egyenesnyil diszjunktivitás - **nem teljesül**

- $ \cfrac{P\mapsto_S R, Q\mapsto_S R}{(P\vee Q)\mapsto_S R} $
- Nem biztos, hogy van olyan program
- Ellenpélda
  - $ S = (SKIP, {x:=x+1 ha x=2, x:=x+2 ha x=1}) $
  - $ x=1 \vee x=2 \not \mapsto_S x=3 $
    - előző óra
  - $ x=1 \mapsto_S x=3 $
    - Háromszög teljesül
    - $s_2$ megoldaj
  - $ x=2 \mapsto_S x=3 $
    - Háromszög teljesül
    - $s_1$ megoldaj

## 5. feladat

- $ \cfrac{P\Rightarrow Q}{P \mapsto_S Q} $
- Jobboldal gyengítéssel be lehet látni
- Használni kell a $ P \mapsto_S P $
  - Már bizonyítottuk

## 6. feladat - egyenesnyil tranzitivitás - **nem teljesül**

- $ \cfrac{P \mapsto_S Q, Q \mapsto_S R}{P \mapsto_S R} $
- Ellenpélda
  - $ P = x = 1 $
  - $ Q = X = 2 $
  - $ R = X = 3 $
  - $ S = (SKIP, {x:=x+1}) $
  - Első két háromsszög teljesül, harmadik nem
  - $ s_1 $ jó az első két egyenesnyílhoz
  - Harmadik egyenesnyilhoz nincs megfelelő s
    - $ x=1 \Rightarrow x+1=3 $
    - Hamis az egyetlen programra

## 7. feladat - egyenesnyil csodakizárás

- $ \cfrac{P\mapsto_S \downarrow}{P = \downarrow} $
- $ P \triangleright_S \downarrow $ és $ \exists s \in S : P \wedge \neg \downarrow \Rightarrow lf(s, \downarrow) $
- $ P \triangleright_S \downarrow $ és $ \exists s \in S : P \Rightarrow lf(s, \downarrow) $
- $ P \triangleright_S \downarrow $ és $ \exists s \in S : P \Rightarrow \downarrow $
- $ P \triangleright_S \downarrow $ és $ \exists s \in S : P = \downarrow $

## 8. feladat - egyenesnyil **stabillal metszés**

- $ \cfrac{P\mapsto_S Q, K \triangleright_S \downarrow}{(P \wedge K)\mapsto_S (Q \wedge K)} $
- Bizonyítás
  - $ P \triangleright_S Q $
  - $ \exists s \in S : P \wedge \neg Q \Rightarrow lf(s,Q) $
    - Legyen s\* ilyen
  - $ K \Rightarrow lf(S,K) $
    - $ \bigwedge\_{s \in S} lf(s, K) \Rightarrow lf(s\*, K) $
  - $ (P \wedge K) \triangleright_S (Q \wedge K) $
    - Háromszög stabil metszés
  - $ \exists s \in S : (P \wedge K) \wedge \neg (Q \wedge K) \Rightarrow lf(s,(Q \wedge K)) $
    - $ P \wedge \neg Q \wedge K \Rightarrow lf(s*, Q) \wedge lf(s*, K) $
    - $ P \wedge \neg Q \wedge K \Rightarrow lf(s\*, Q \wedge K) $
- Nagy S-ből lehet kis s-t csinálni
  - Ha lf(S,K) akkor lf(s,K) is

## Görbenyil definíció

- $ P \hookrightarrow_S Q = (P \mapsto_S Q)^{tdl} $
- tranzitív diszjunktív lezártja
- Haladási reláció
- ha $ P \mapsto_S Q $ akkor $ P \hookrightarrow_S Q $
- ha $ P \hookrightarrow_S Q $ és $ Q \hookrightarrow_S R $ akkor $ P \hookrightarrow_S R $
  - tranzitív
- ha $ \forall i \in W: P*i \hookrightarrow_S Q $ akkor $ (\bigvee*{i=1}^{n} P) \hookrightarrow_S Q $
  - diszjunktív
- legszűkebb ilyen reláció
- Egyszer átvisz P-ből Q-ba de közben kimehet P-ből nem csak Q-ba
  - Használhat külső pontot

## 1. fealadat - Görbenyil **jobboldal gyengítés**

- $ \cfrac{P \hookrightarrow_S Q, Q \Rightarrow R}{P \hookrightarrow_S R} $
- $ \cfrac{Q \Rightarrow R}{\cfrac{Q \mapsto_S R}{Q \hookrightarrow_S R}} $
- Utána tranzitívitás

## Hasznos tételek

- Görbenyil csoda kizárás
  - $ \cfrac{P \hookrightarrow_S HAMIS}{P = HAMIS} $
- Görbenyil stabillal metszés
  - $ \cfrac{P\hookrightarrow_S Q, K \triangleright_S \downarrow}{(P \wedge K)\hookrightarrow_S (Q \wedge K)} $
- PSP - Progress Safty Progress
  - $ \cfrac{P\hookrightarrow_S Q, R \triangleright_S B}{(P \wedge R)\hookrightarrow_S (Q \wedge R) \vee B} $

# 5. GYAK

## 2. Feladat - Dupla disjunkció

- $ \cfrac{P_1 \hookrightarrow_S Q_1, P_2 \hookrightarrow_S Q_2}{(P_1 \vee P_2) \hookrightarrow_S (Q_1 \vee Q_2)} $
- Visszafele gondolkodva
- $ P_1 \hookrightarrow_S (Q_1 \vee Q_2) $ és $ P_2 \hookrightarrow_S (Q_1 \vee Q_2) $
- Jobboldal gyengítéssel ez már kijön
  - $ Q_1 \Rightarrow Q_1 \vee Q_2 $
- Dupla diszjunkció

## 3. Feladat

- $ \cfrac{P \hookrightarrow_S (Q_1 \vee Q_2), Q_1 \hookrightarrow_S R}{P \hookrightarrow_S (R \vee Q_2)} $
- Lentről felfelé dupla diszjunkció és jobboldal gyengítéssel is kijön
- $ Q_1 \vee Q_2 \hookrightarrow_S R \vee Q_2 $

## Def

- $ P \hookrightarrow_S Q $ teljesül bármely P-beli S program bármelyik, feltétlenül pártatlan ütememzésének megfelelő végrehajtása eljut Q-beli pontba.
- Ezzel a def-el lehet cáfolni

## 4. Feladat

- $ \cfrac{P \hookrightarrow_S Q, Q \hookrightarrow_S (P \vee R)}{P \hookrightarrow_S R} $
- Cáfolat
- A = {-1,0,1}
- P = (x=1)
- Q = (x=-1)
- R = (x=0)
- S = (SKIP, {x:=-1})
- Görbenyilat egyenes nyillal lehet kiszámolni
- Ellenpéldához pont és ütemezés
  - Pont: x=1
  - Ütememzés: s1, s1, s1, s1, s1, ...

## 5. Feladat

- $ \cfrac{P\mapsto_S(Q\wedge \neg B),Q\hookrightarrow_S R, Q \triangleright_S HAMIS, R\Rightarrow B}{(P\wedge Q)\hookrightarrow_S(B\wedge Q)} $

$\cfrac{\cfrac{\cfrac{\cfrac{P\mapsto_S(Q\wedge \neg B)}{P\hookrightarrow_S(Q\wedge \neg B)}, Q\wedge \neg B\Rightarrow Q}{P\hookrightarrow_S Q},\cfrac{Q\hookrightarrow_S R, R\Rightarrow B}{Q\hookrightarrow_S B}}{P\hookrightarrow_S BS},Q \triangleright_S HAMIS}{(P\wedge Q)\hookrightarrow_S(B\wedge Q)}$

## 6. Feladat

- $\cfrac{P \hookrightarrow_S Q, Q \triangleright_S R, P \triangleright_S R}{P \hookrightarrow_S R}$
- Ellenpéldában úgy jussunk Q-ba, hogy nem hagyjuk el P-t
- P = (x=1 v x=2)
- Q = (x = 1)
- R = (x = 3)
- S = (SSKIP, {x:=1})
- Állapot: x=2
- Ütemezés: s1,s1,s1,...

# 6. GYAK

**Április 26 ZH az EA idejében**

## Invariáns tulajdonság

- Definíció
  - $P \in inv_S(Q)$ ha
    1. $ Q \Rightarrow lf(s_0, P) $
    2. $ P \Rightarrow lf(S,P) $
- P invariánsa S programnak a Q-beli állapotokból índítva, ha
  1. minden Q-beli állapotból $s_0$ P-beli állapotba visz és
  2. P stabil S-re nézve.

## 1. feladat

- $\cfrac{V\Rightarrow W, W \mapsto_S R, P \in inv_S(Igaz)}{(Q \vee (V \wedge P))\hookrightarrow_S(Q \vee (R \wedge P))}$

- $\cfrac{\cfrac{\cfrac{\cfrac{\cfrac{V \Rightarrow W}{V\mapsto_S W}}{V\hookrightarrow_S W},\cfrac{W \mapsto_S R}{W \hookrightarrow_S R}}{V \hookrightarrow_S R}, \cfrac{P \in inv_S(Igaz)}{P \triangleright_S HAMIS}}{V\wedge P \hookrightarrow_S R \wedge P}, Q \hookrightarrow_S Q}{(Q \vee (V \wedge P))\hookrightarrow_S(Q \vee (R \wedge P))}$

## Fixpont tulajdonság

- Definíció
  - Legyen $S = (s_0, {\square_{i=1}^n x_i,y_i:=w_i,z_i \space ha \space \pi_i})$ program  
    fixpont feltétele: $\varphi_S = \bigwedge_{i=1}^n(\neg\pi_i \vee (x_i=w_i \wedge y_i=z_i))$
- Akkor fixpont ha egy feltétel sem teljesül vagy ha teljesül, akkor az értékadás nem változtatja meg az állapotot.

# Programozási Módszertan EA

# 1. EA 

- 16:15 kezdés
- Első ZH min 20 pont kell

## Ciklus

- Ciklus Feltétel: $ \pi $
- Ciklus Mag: $ s_0 $
- Levezetési szabályok
    1. $ Q \Rightarrow P $
    2. $ P \wedge \neg\pi \Rightarrow R $
    3. $ P \Rightarrow \pi \vee \neg\pi $
    4. $ P \wedge \pi \Rightarrow t > 0 $
    5. $ P \wedge \pi \wedge t=t_0 \Rightarrow lf(s_0, P \wedge t < t_0) $
- Ha ezek igazak, akkor $ Q \Rightarrow lf(DO,R) $

- Próbáljuk az invariánst kitalálni
    - Mindegyik szabályban benne van
    - Ezért érdemes ezzel kezdeni
    - 2 pontból érdemes kiindulni
    - Rossz ötlet ha az invariáns szigorúbb mint az utófeltétel
        - $ P \Rightarrow R $
        - 1-es szabály alapján: $ Q \Rightarrow R $
            - Nem kell cikllus
    - **Invariáns legyen gyengébb mint az utófeltétel**

## SKIP

- Program ami nem csinál semmit
- $ Q \Rightarrow lf(SKIP,R) = R $

## Összegzés

- [m..n] intervallumon összegzése az f függvénynek
- $ f: \Z \rightarrow \Z $
- $ A = ( m:\Z, n:\Z, s:\Z ) $
- $ B = ( m':\Z, n':\Z ) $
- $ Q = ( m=m' \wedge n=n' \wedge m \leq n+1 ) $
- $ R = ( Q \wedge s = \sum_{i=m}^n f(i) ) $
- Ciklussal oldjuk meg
- $ P = ( Q ) $ - s-ről nem mondunk semmit
- $ P = ( Q \wedge s = \sum_{i=m}^k f(i) \wedge k \in [m-1..n] ) $
- Belátjuk az 5 pontot
    1. $ Q \Rightarrow P $
        - $ Q \Rightarrow ( Q \wedge s = \sum_{i=m}^k f(i) \wedge k \in [m-1..n] ) $ 
        - Nem teljesül ezért inkább szekvenciát írunk
            1. $ Q \Rightarrow lf(k,s:=m-1,0,Q') $
            2. $ Q' \Rightarrow lf(DO,R) $
                - $ Q' \Rightarrow P $
                - $ Q' = (Q \wedge k=m-1 \wedge s=0) $
    2. $ P \wedge \neg\pi \Rightarrow R $
        - $ P \wedge k = n \Rightarrow R $
        - $ \pi = k \neq n $
    3. $ P \Rightarrow \pi \vee \neg\pi $
        - $ P \Rightarrow (k \neq n) \vee \neg(k \neq n) $
        - Igaz mert egész számok
    4. $ P \wedge \pi \Rightarrow t > 0 $
        - t-t okosan kell kitalálni
        - 5 alapján t-t csökkenteni kell
        - $ t = n-k $ - távolság csökken
        - P és $\pi$ kiadja
    5. $ P \wedge \pi \wedge t=t_0 \Rightarrow lf(s_0, P \wedge t < t_0) $
        - $ P \wedge k \neq n \wedge n-k=t_0 \Rightarrow lf(s_0, P \wedge n-k < t_0) $
        - $s_0$ egy szekvencia, ezért a fenti helyett kettő másikat látuk be
            1. $P \wedge k \neq n \wedge n-k=t_0 \Rightarrow lf(s:=s+f(k+1), Q'' \wedge n-k=t_0)$
                - $ lf(..) = (Q\wedge s+f(k+1)=\sum_{i=m}^{k+1} f(i) \wedge k+1 \in [m-1..n] \wedge n-k=t_0) $
            2. $Q'' \wedge n-k=t_0 \Rightarrow lf(k:=k+1, P \wedge n-k < t_0)$
                - Helyettesítés
                - $Q'' \wedge n-k=t_0 \Rightarrow (P^{k \leftarrow k+1} \wedge n-(k+1) < n-k)$
                - $Q'' := P^{k \leftarrow k+1} $

<svg width="200" height="200">
    <rect x="0" y="0" width="400" height="100" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="0" y="50" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="40" y="100" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="40" y="150" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <text x="30" y="30">k,s:=m-1,0</text>
    <text x="40" y="80">k != n</text>
    <text x="60" y="130">s:=s+f(k+1)</text>
    <text x="60" y="180">k:=k+1</text>
</svg>

## Számlálás

- [m..n] intervallumban hány olyan szám van amire teljesük a $\beta$
- $\beta:\Z \rightarrow \mathbb{L}$
- $\chi :\mathbb{L} \rightarrow \{0,1\}$
- $ A = ( m:\Z, n:\Z, d:\Z ) $
- $ B = ( m':\Z, n':\Z ) $
- $ Q = ( m=m' \wedge n=n' \wedge m \leq n+1 ) $
- $ R = ( Q \wedge d = \sum_{i=m}^n \chi(\beta(i)) \wedge k\in[m-1..n] ) $

## Jelölések

- [a..b] intervallum, ahol $ a,b \in \Z $
- [10..9] üres $ = \empty $ 
- [10..2] nagyon üres, nem szeretjük

# 2. EA

## Számlálás

- $ A = (m,n:\Z, d:\N) $
- $ B = (m',n':\Z) $
- $ Q = (m=m' \wedge n=n' \wedge m\leq n+1) $
- $ R = (Q \wedge d = \sum_{i=m}^{n} \chi(\beta(i))) $
- $ P = (Q \wedge d = \sum_{i=m}^{k} \chi(\beta(i)) \wedge k\in[m-1..n]) $

<svg width="200" height="250">
    <rect x="0" y="0" width="400" height="100" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="0" y="50" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="40" y="100" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="40" y="150" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="120" y="150" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <line x1="40" y1="100" x2="80" y2="150" stroke="black" />
    <line x1="200" y1="100" x2="160" y2="150" stroke="black" />
    <rect x="40" y="200" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <text x="30" y="30">k,d:=m-1,0</text>
    <text x="40" y="80">k != n</text>
    <text x="80" y="130">β ( k+1 )</text>
    <text x="60" y="180">d:=d+1</text>
    <text x="140" y="180">SKIP</text>
    <text x="60" y="230">k:=k+1</text>
</svg>

## Maximumkeresés

- $ f:\Z \rightarrow H $
- $ A = (m:\Z, n:\Z, max:H, i:\Z) $
- $ B = (m':\Z, n':\Z) $
- $ Q = (m=m' \wedge n=n' \wedge m\leq n) $
- $ R = (Q \wedge i\in[m..n] \wedge max=f(i) \wedge \forall j \in [m..n]:f(j)\leq f(i)) $
- P = (Q ∧ i ∈ [m..k] ∧ max=f(i) ∧ ∀j∈[m..n]: f( j ) ≤ f( i ))
- Q' = (Q ∧ k=m ∧ i=m ∧ max=f(m))
- Q' ⟹ P
- $ \pi : k \neq n $ 
- π : k ≠ n
- t : n - k

<svg width="250" height="250">
    <rect x="0" y="0" width="400" height="100" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="0" y="50" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="40" y="100" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="150" y="100" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <line x1="40" y1="100" x2="60" y2="150" stroke="black" />
    <line x1="150" y1="100" x2="170" y2="150" stroke="black" />
    <rect x="40" y="150" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="150" y="150" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <rect x="40" y="200" width="400" height="400" style="fill:rgb(255,255,255);stroke-width:3;stroke:rgb(0,0,0)" />
    <text x="30" y="30">i,k,max:=m,m,f(m)</text>
    <text x="40" y="80">k ≠ n</text>
    <text x="60" y="130">f(k+1)>=max</text>
    <text x="165" y="130">f(k+1)<=max</text>
    <text x="50" y="170">i,max := </text>
    <text x="60" y="190">k+1,f(k+1)</text>
    <text x="160" y="180">SKIP</text>
    <text x="60" y="230">k:=k+1</text>
</svg>

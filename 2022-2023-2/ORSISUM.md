<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
        inlineMath: [['$','$']]
      }
    });
</script>
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# Osztott rendszerek specifikációja és implementációja - Összefoglaló

## Tulajdonságokat összefoglaló táblázat

|                                                                        | Jobboldal gyengítése                                | Diszjunktivitás                                      | Tranzitivitás                                   | Stabillal metszés                                                                       | Csoda kizárása                       | PSP                                                                                                     |
| ---------------------------------------------------------------------- | --------------------------------------------------- | ---------------------------------------------------- | ----------------------------------------------- | --------------------------------------------------------------------------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| Képlet <br> $\circ \in \{ \triangleright, \mapsto, \hookrightarrow \}$ | $\cfrac{P \circ_S Q, Q \Rightarrow R}{P \circ_S R}$ | $\cfrac{P \circ_SR, Q \circ_SR}{(P\vee Q) \circ_SR}$ | $\cfrac{P \circ_S Q, Q \circ_S R}{P \circ_S R}$ | $\cfrac{P \circ_S Q, K \triangleright_S \downarrow}{(P \wedge K) \circ_S (Q \wedge K)}$ | $\cfrac{P \circ_S HAMIS}{P = HAMIS}$ | $\cfrac{P\hookrightarrow_S Q, R \triangleright_S B}{(P \wedge R)\hookrightarrow_S (Q \wedge R) \vee B}$ |
| Háromszög                                                              | IGEN                                                | IGEN                                                 | NEM                                             | IGEN                                                                                    | ?                                    | -                                                                                                       |
| Egyenesnyíl                                                            | IGEN                                                | NEM                                                  | NEM                                             | IGEN                                                                                    | IGEN                                 | -                                                                                                       |
| Görbenyíl                                                              | IGEN                                                | Dupla IGEN                                           | Dupla IGEN                                      | IGEN                                                                                    | IGEN                                 | IGEN                                                                                                    |

## Leggyengébb előfeltétel

- Egyszerű értékadás: $lf(x:=5, 0<x+y) = (0<5+y)$
- Feltételes értékadás: $lf(x:=5,ha \space y<1, 0<x+y) = (y<1\rightarrow 0<5+y)\wedge(y\geq 1\rightarrow 0<x+y)$
  - Általánosan: $lf(x:=y,ha \space \pi, R) = (\pi\rightarrow R^{x\leftarrow y})\wedge(\neg \pi \rightarrow R)$
- Szimultán értékadás: $lf(x,y:=5,x+1 \space ha \space y<1, 0<x+y)=(y<1\rightarrow 0<5+x+1)\wedge(y\geq 1\rightarrow 0<x+y)$
  - Általánosan: $lf((||_{i=1}^nx_i=y_i \space ha \space \pi),R)=(\pi\rightarrow R^{x_1\leftarrow y_1, ..., x_n \leftarrow y_n})\wedge(\neg\pi\rightarrow R)$

### lf(S,R) tulajdonságok

- Csoda kizárása  
   $ lf(S,\downarrow) = \downarrow $
- Monotonitás  
   ha $ P \Rightarrow Q $ akkor $ lf(S,P) \Rightarrow lf(S,Q) $
- Konjunkció  
   $ lf(S,P) \wedge lf(S,Q) = lf(S, P \wedge Q) $
- Diszjunkció **(egyirányú)**  
   $ lf(S,P) \vee lf(S,Q) \Rightarrow lf(S, P \vee Q) $

## Háromszög tulajdonság

- Hásomszög S definíció:
  - $P \triangleright_S Q ::== P \wedge \neg Q \Rightarrow lf(S,P\vee Q) $
- Ha olyan állapotban vagyunk ahol P teljesül és Q nem, abból S programot végrehajtva olyan állapotba lépünk ahol P vagy Q teljesül.
- P-ből csak P-be vagy Q-ba mehetek.
- P-t csak Q-n keresztül hagyhatom el.
- Biztonsági tulajdonság
- Stabil tulajdonság
  - $P\triangleright_S HAMIS = P \Rightarrow lf(S,P)$
  - Ha P-be jutottunk, akkor nem hagyhatjuk el.
- $P\triangleright_S P$ teljesül bármilyen P és S esetén.
- $P\triangleright_S \neg P$ teljesül bármilyen P és S esetén.
- Jobboldal gyengítés $\cfrac{P \triangleright_S Q, Q \Rightarrow R}{P \triangleright_S R}$ teljesül
- Diszjunkció $\cfrac{P \triangleright_S R, Q \triangleright_S R}{(P\vee Q) \triangleright_S R}$ teljesül
- Tranzitivitás $\cfrac{P \triangleright_S Q, Q \triangleright_S R}{P \triangleright_S R}$ **nem teljesül**
- Stabillal metszés $\cfrac{P \triangleright_S Q, K \triangleright_S \downarrow}{(P \wedge K) \triangleright_S (Q \wedge K)}$ teljesül

## Egyenesnyíl tulajdonság

- Egyenesnyíl S definíció
  - $P\mapsto_S Q ::== P\triangleright_S Q$ és $\exists s \in S: P \wedge \neg Q \Rightarrow lf(s,Q)$
- Ha teljesül a P háromszög S Q és ha P-ben vagyunk, akkor van olyan s utasítás, ami P-ből Q-ba visz.
- Haladási tulajdonság
  - P-ből mindenképp Q-beli állapotba jutunk, úgy, hogy közben nem hagyjuk el P-t.
  - Véges sok lépés után Q-ba jutunk.
- $P\mapsto_S P$ teljesül bármilyen P és S esetén.
- $P\mapsto_S \neg P$ **nem teljesül** bármilyen P és S esetén.
- Jobboldal gyengítés $\cfrac{P \mapsto_S Q, Q \Rightarrow R}{P \mapsto_S R}$ teljesül
- Diszjunkció $\cfrac{P \mapsto_S R, Q \mapsto_S R}{(P\vee Q) \mapsto_S R}$ **nem teljesül**
- Tranzitivitás $\cfrac{P \mapsto_S Q, Q \mapsto_S R}{P \mapsto_S R}$ **nem teljesül**
- Stabillal metszés $\cfrac{P \mapsto_S Q, K \triangleright_S \downarrow}{(P \wedge K) \mapsto_S (Q \wedge K)}$ teljesül
- Csoda kizárás $\cfrac{P\mapsto_S HAMIS}{P = HAMIS}$
- "Hasznos lehet": $\cfrac{P\Rightarrow Q}{P\mapsto_S Q}$

## Görbenyíl tulajdonság

- Görbenyíl S definíció
  - $P \hookrightarrow_S Q ::== (P \mapsto_S Q)^{tdl}$ [tranzitív, diszjunktív lezártja]
    1. Ha $P\mapsto_S Q$, akkor $P\hookrightarrow_S Q$
    2. Ha $P\mapsto_S Q$ és $Q\mapsto_S R$, akkor $P\mapsto_S R$
    3. Ha $\forall i \in W:P_i\hookrightarrow_S Q$, akkor $(\bigvee_{i \in W}P_i)\hookrightarrow_S Q$
    4. Legkisebb ilyen reláció
- P-ből egyszer biztosan Q-ba jutunk, de lehet, hogy közben kimegyünk P-ből
- Haladási tulajdonság
- $P\hookrightarrow_S P$ teljesül bármilyen P és S esetén.
- $P\hookrightarrow_S \neg P$ **nem teljesül** bármilyen P és S esetén.
- Jobboldal gyengítés $\cfrac{P \hookrightarrow_S Q, Q \Rightarrow R}{P \hookrightarrow_S R}$ teljesül
- Diszjunkció $\cfrac{P \hookrightarrow_S R, Q \hookrightarrow_S R}{(P\vee Q) \hookrightarrow_S R}$ teljesül
- Tranzitivitás $\cfrac{P \hookrightarrow_S Q, Q \hookrightarrow_S R}{P \hookrightarrow_S R}$ teljesül
- Stabillal metszés $\cfrac{P \hookrightarrow_S Q, K \triangleright_S \downarrow}{(P \wedge K) \hookrightarrow_S (Q \wedge K)}$ teljesül
- Csoda kizárás $\cfrac{P\hookrightarrow_S HAMIS}{P = HAMIS}$
- "Hasznos lehet": $\cfrac{P\Rightarrow Q}{P\hookrightarrow_S Q}$
- PSP - (Progress-Safety-Progress) $\cfrac{P\hookrightarrow_S Q, R \triangleright_S B}{(P \wedge R)\hookrightarrow_S (Q \wedge R) \vee B}$ teljesül
- Dupla diszjunkció $\cfrac{P_1 \hookrightarrow_S Q_1, P_2 \hookrightarrow_S Q_2}{(P_1 \vee P_2)\hookrightarrow_S(Q_1 \vee Q_2)}$ teljesül
- Egyik oldallal megyek csak tovább: $\cfrac{P\hookrightarrow_S(Q_1 \vee Q_2), Q_1 \hookrightarrow_S R}{P\hookrightarrow_S(R \vee Q_2)}$ teljesül

## Hullámos görbenyíl

- Akkor teljesül, ha bármelyik P-beli állapotból S program bármelyik feltétlenül pártatlan ütemezésének megfelelő végrehajtása Q-beli állapotba visz.
- Görbenyíl és hullámos görbenyíl ekvivalens.
- Ezt a definíciót használjuk ellenpélda adásra, ha cáfolni akarjuk a görbenyílat.

## Invariáns tulajdonság

- Definíció
  - $P \in inv_S(Q)$ ha
    1. $ Q \Rightarrow lf(s_0, P) $
    2. $ P \Rightarrow lf(S,P) $
- P invariánsa S programnak a Q-beli állapotokból índítva, ha
  1. minden Q-beli állapotból $s_0$ P-beli állapotba visz és
  2. P stabil S-re nézve.

## Fixpont tulajdonság

- Definíció
  - Legyen $S = (s_0, {\square_{i=1}^n x_i,y_i:=w_i,z_i \space ha \space \pi_i})$ program  
    fixpont feltétele: $\varphi_S = \bigwedge_{i=1}^n(\neg\pi_i \vee (x_i=w_i \wedge y_i=z_i))$
- Akkor fixpont ha egy feltétel sem teljesül vagy ha teljesül, akkor az értékadás nem változtatja meg az állapotot.

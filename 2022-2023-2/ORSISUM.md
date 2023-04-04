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

# Összefoglaló

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
- Szimultán értékadás: $$
  - Általánosan: $$

### lf(S,R) tulajdonságok

- Csoda kizárása  
   $ lf(S,\downarrow) = \downarrow $
- Monotonitás  
   ha $ P \Rightarrow Q $ akkor $ lf(S,P) \Rightarrow lf(S,Q) $
- Konjunkció  
   $ lf(S,P) \wedge lf(S,Q) = lf(S, P \wedge Q) $
- Diszjunkció **(egyirányú)**  
   $ lf(S,P) \vee lf(S,Q) \Rightarrow lf(S, P \vee Q) $

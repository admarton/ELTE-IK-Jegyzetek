# SZámításelmélet EA 2021.09.08

## Vizsga
- Beugró: def, tét
- Kifejtés

## Formális nyelvek ismétlés
- ábécé                     V
- betű                      a ∈ V
- szó                       u ∈ V*
- üres                      ɛ
- nyelv (véges, végtelen)   
- hatványhalmaz P(X)
- nyelvcsalád

- Grammatika:
    - G = < N, T, P, S >
    - N, T diszjunkt véges ábécé
    - S ∈ N - kezdőszimbólum
    - P - levezetési szabályok
    - levezethető u ⇒_G v --> u = u₁xu₂, v = u₁yu₂, x → y ∈ P
    - generált nyelv - ami S-ből indulva levezethető (⇒*)

- Grammatika osztályok  
    0. nincs korlát
    1. ∀ u₁Au₂ → u₁vu₂ ∈ P, u₁,u₂,v ∈ (N ∪ T)*, A ∈ N, v ≠ ɛ  
        S → ɛ lehet, de akkor S nem lehet szabály jobb oldalán (KES)
    2. A → v, A ∈ N, v ∈ (N ∪ T)*
    3. A → uB vagy A → u, A,B ∈ N, u ∈ T*

- Nyelvek osztályozása  
    A grammatika által generált nyelv osztálya megeggyezik a grammatika osztályával.

    L₃ ⊂ L₂ ⊂ L₁ ⊂ L₀

- Formális nyelvek megadása  
    - Generatív grammatikával előállítható.
    - Matematikai gépek, autómaták
    - Egyéb: felsorolás, regexp

- Véges autómata
    - Input szalagról olvas, belső állapota változik

- 3-as típusú nyelvek
    - 3-as t. grammatikák
    - 3-as norm.f. grmmatikák
    - regexp
    - determinisztikus, n.d. véges autómaták

- Veremautómata
    - input szallag + verem szerkezetű memória, belső állapota + verem változik
    - egylépéses redukció

## Chomsky normálforma
**Def:** Egy G. Chomsky nf. ha P-ben ilyenek vannak:
- S → ɛ
- A → BC, A,B,C ∈ N; B,C ≠ S, ha S → ɛ ∈ P
- A → a, A ∈ N, a ∈ T

## Chomsky Normálformára hozás
1. Új kezdőszimbólum
2. Álterminálisok bevezetése  
    - Terminális helyett neki létrehozott nemterminális lesz
    - felvesszük az új nt-ből a terminálisba vezető szabályt
3. Hosszredukció
    - X -> Y₁Y₂...Yₖ, k ≥ 3 szabályt kelyettesítjük:
        - { X -> Y₁Z₁, Z₁->Y₂Z₂,...Zₖ-₁->Yₖ}
4. ɛ-mentesítés
    - Uᵢ ⊆ N
        - U₁ := { X | X -> ɛ ∈ P}
        - Uᵢ₊₁ := Uᵢ ∪ { X | X -> u ∈ P és u ∈ Uᵢ* }
    - Ha S benne van az U-ban, akkor az ɛ benne van a nyelvben
    - X -> ɛ szabályokat elhagyjuk
    - Új szabályok:
        - A -> BC, B,C ∈ U  akkor A->B és A->C
        - A -> BC, B ∈ U, C ∉ U akkor A->C
        - A -> BC, C ∈ U, B ∉ U akkor A->B
5. Láncmentesítés
    - H(A) az A-ból levezethető nemterminálisok
        - H₀(A) := {A}
        - Hᵢ₊₁(A) := Hᵢ(A) ∪ {B ∈ N | ∃C ∈ Hᵢ(A) : C -> B ∈ P}
    - X -> Y szabályokat kihagyjuk
    - X->w szabályt felvesszük ha volt Y->w

# Számelm EA 2021.09.15

## Méretek
p : X → Y₁...Yₘ ∈ P, |p| = m + 1  
|G| 

## Hossz- nemcsökkentő grammatika
- S → ɛ, S nem szerepel jobb oldalon
- u → v, ahol u,v ∈ (T ∪ N)+ és |u|≤|v|

**Tét.:** Minden hossz-nemszökkentő grammatika környezetfüggő nyelvet generál.
1. Álterminálisok bevezetése
    - A → a
2. Környezetfüggő szabályokkal való helyettesítés
    - X₁...Xₙ → Y₁...Yₘ szabályt kell átalakítani
    - Helyettesítjük:
        - X₁...Xₙ → Z₁X₂...Xₙ
        - Z₁X₂...Xₙ → Z₁Z₂...Xₙ
        - ...
        - Z₁...Zₙ₋₁Xₙ → Z₁...Zₙ...Yₘ
        - Z₁...Zₙ...Yₘ → Y₁Z₂...Zₙ...Yₘ
        - Y₁Z₂...Zₙ...Yₘ → Y₁Y₂Z₃...Zₙ...Yₘ
        - ...
        - Y₁...Yₙ₋₁Zₙ...Yₙ → Y₁...Yₘ

## Kuroda normálforma
- S → ɛ
- A → a
- A → BC
- AB → AC
- BA → CA
- Környezetfüggő g.
- Azért normálf. mert minden kf.g.-hez meg lehet adni Kurodát
1. Álterminálisok
2. Környezetfüggetlen sz. Hosszredukció
3. Láncmentesítés
    - Környezetfüggőknél bonyolult
4. Környezetfüggő sz. Hosszredukció
    - X₁X₂ → Y₁Z₁
    - Z₁X₃ → Y₂Z₂
    - ...
5. AB → CD, A≠C, B≠D elimináció
    - AB → AW
    - AW → CW
    - CW → CD

## 0-s normál forma
- S → ɛ
- A → a
- A → B
- A → BC
- AB → AC
- AC → AB
- ...


## Algoritmikus problémák
**Tét.:**
Lᵢ zárt a reguláris műveletekre.

**Tét.:**
L₃ zárt a komplementer, metszet és különbségre is.

**Tét.:**
Eldönthető, hogy egy G₃ az üres nyelvet kenerálja-e.  
**Biz.:**
Szélességi keresés.

**Tét.:**
Eldönthető, hogy két G₃ által generált nyelv diszjunkt-e.

**Tét.:**
Eldönthető, hogy két G₃ ugyan azt a nyelvet generálja.

**Tét.:**
Eldönthető, hogy egy G₃ bővebb nyelvet generál-e mint a másik.

### Szóprobléma (membership problem)
**Tét.:** G₃-nál lineáris időben eldönthető, hatékonyan.
- t a szó
- H₀ := {S}
- Hᵢ₊₁ := { A ∈ N | ∃B ∈ Hᵢ ∧ B → tᵢ₊₁A ∈ P}
- Hᵢ az i. lépésben a szó végén álló terminálisok halmaza 
- VDA-val autómatizálható a H-k kiszámítása
- Ha a szavunk kisebb mint a grammatika jóval, akkor hatékonyabb a H-k kiszámolása mint a VDA elkészítés és futtatás.


**Áll.:** G₂ generálje-e a szót eldönthető.  
CYK-algoritmus |G|*n³ lépésben eldönti, ahol n a szó hossza.

## CYK-algoritmus
- CNF-ben kell lennie a grammatikának
- H(i,i) := {Aⱼ | βⱼ = tᵢ}
- H(i,j) := {Aₖ | βₖ ∈ ⋃ₕ₌ᵢʲ⁻¹ H(i,h)H(h+1,j)}
- H(i,j) = { X ∈ N | X ⇒* tᵢ...tⱼ }


# EA 3 2021.09.22

## CYK algoritmus
- szó generálható-e a grammatikával (CNF-ben van megadva)
- a terminálisok mikből vezethetőek le
- az eddig meglévő részszavak mikből vezethetőek le
- ha a tetején kijön az S, akkor levezethető 

## Algoritmikusan Eldönthető
1. G 2-es grem., L véges nyelv
    - L ⊆ L(G) 
2. G 2-es grem., L véges nyelv
    - L ∩ L(G) = ∅
3. Környezetfüggetlen G végtelen nyelvet generál-e
4. ...

## Algoritmikusan nem eldönthető
1. L(G1) = L(G2) 
2. L(G1) ⊆ L(G2) 
3. L(G1) ∩ L(G2) = ∅
4. L(G) = T*
5. G egyértelmű-e

## Hossznemcsökkentő grammatika szóprobléma
- **Biz.:** Ha u=ɛ, akkor L(G) ⇔ S → ɛ ∈ P.
- n
- r
- n hosszú mondatformában vannak r hosszú résszavak
- ???

## 0-ás típusú grammatika esetén a szóprobléma algoritmikusan nem eldönthető
- De van parciálisan eldöntő algoritmus
- a pozitív eleteket felismeri
- a negatívat nem biztos
- gráfot lehet csinálni
- ???


## Témák
- Nulladrendű logika
- Elsőrendű logika
- Függvények aszimptotikus viselkedése
- Turing gépek, alapfogalmak
- TG változatok
- számosságok
- eldönthetőség
- eldönthetetlen problémák
- bonyolultság elmélet
- NP-teljesség

## Nulladrendű logika - Ítéletkalkulus
- Állítások összekapcsolása műveletekkel
- Az állítások igazságértéke egyértelmű, eldönthető
- implikáció : Ha süt a nap, akkor le megyek a térre
- Ítéletváltozó: Var = {x1, x2, ...}
    - x ∈ Var ⇒ x ∈ Form
    - ϕ ∈ Form  , akkor ¬ϕ ∈ Form
    - a, b ∈ Form, akkor (a ∨ b), (a ∧ b), (a → b) ∈ Form

- Formula szerkezeti fával reprezentálható
- Részformulákkal címkézett

- ¬, ∧, ∨, → csökkenő precedencia sorrendben

- **Def.:** Interpretáció
    - I : Var(a) → {i, h} - változó kiértékelés

- Formula igazságértéke: 
    - 𝔹_I(x) := I(x)
    - 𝔹_I(¬x) := ¬I(x)
    - 𝔹_I(x ∘ y) := 𝔹_I(x) ∘ 𝔹_I(y)  //  ∘ ∈ { ∧, ∨, →}

| 𝔹_I(x) | 𝔹_I(y) |   | 𝔹_I(¬x) | 𝔹_I(x ∧ y) | 𝔹_I(x ∨ y) | 𝔹_I(x → y) |
| :----: | :----: |---| :----: | :----: | :----: | :----: | 
| i | i | | h | i | i | i |
| i | h | | h | h | i | h |
| h | i | | i | h | i | i |
| h | h | | i | h | h | i |

- Minden formulához lehet adni igazságtáblát
- Interpretáció kielégít egy formulát ha felvesz igaz értéket
- Kielégíthetó ha van olyan eterpretáció ami kielégíti
- Tautologia ha minden interetáció kielégíti
- tautologikusa nekvivalensek ha pontosan ugyanazok az interpretációk elégítik ki
- ⊤ : tautológia, ⊥ : kielégíthetetlen
- Szabályok:
    1. ¬¬a = a
    2. a ∨ a ~₀ a , a ∧ a ~₀ a
    3. a ∨ b ~₀ b ∨ a , a ∧ b ~₀ b ∧ a
    4. (a ∨ b) ∨ c ~₀ a ∨ (b ∨ c)  
        (a ∧ b) ∧ c ~₀ a ∧ (b ∧ c)
    5. (a ∨ b) ∧ c ~₀ (a ∧ c) ∨ (b ∧ c)  
        (a ∧ b) ∨ c ~₀ (a ∨ c) ∧ (b ∨ c)
    6. (a ∨ b) ∧ b ~₀ b, (a ∧ b) ∨ b ~₀ b
    7. a → b ~₀ ¬a ∨ b
    8. ¬(a ∧ b) ~₀ ¬a ∨ ¬b, ¬(a ∨ b) ~₀ ¬a ∧ ¬b
    9. a ∨ ¬a ~₀ ⊤ , a ∧ ¬a ~₀ ⊥
    10. a ∨ ⊤ ~₀ ⊤ , a ∧ ⊥ ~₀ ⊥
    11. a ∨ ⊥ ~₀ a , a ∧ ⊤ ~₀ a

- Szabályok használata nem változtatja az igazságértéket

- **Tételek**
    - a kielégíthetetlen, ha ¬a ~₀ ⊤
    - F ⊧(\models)₀ a akkor és csak akkor ha F∪{¬a} kilégíthetetlen

- Literál : x és ¬x
- Elemi diszjunkció (klóz) : a₁ ∨ ... ∨ aₙ, aᵢ-k kölönböző literálok
- Konjunktív normálforma (KNF) : k₁ ∧ ... ∧ kₙ ahol kᵢ klóz
- Elemi konjunkció : hasonlóan
- Diszjunktív normálforma (DNF) : hasonlóan 

- Ítéletkalkulusbeli formulához megadható vele ekviv. DNF
    - Az igazságtábla igaz sorai adják hogy mi kell bele
- Ítéletkalkulusbeli formulához megadható vele tautológikusan ekviv. KNF
    - A hamis sorok negáltjai kellenek
    1. implikáció eliminálás
    2. negációs operátorok csak ítéletváltozólk előtt legyenek
    3. disztributív szabályokkal 2 szintűvé lapítjuk

- Rezolvens
    - 1 komplemens literálpárt tartalmaz klózoknak lehet rezolvense kivesszük  belőlük a komplemens literálpárt és összevagyoljuk 
    (x ∨ y, ¬y ∨ z) = x ∨ z

# EA 4 2021.09.29

## Logika
### Rezolvens
Komplemens literálpárok diszjunkciója

### Rezolúciós levezetés
- Véges klóz sorozat
- Mindegyik klóz vagy eredeti, vagy kisebb indexű klóznak rezolvense
- Ha levezethető az üres klóz, akkor kielégíthetetlen

#### Feladat
S = {y ∨ z, ¬x ∨ W ∨ ¬z, y ∨ ¬z ∨ ¬w, x ∨ z}
1. ¬y           (∈ S)
2. y ∨ z        (∈ S)
3. z            (=res(1,2))
4. ¬x ∨ W ∨ ¬z  (∈ S)
5. y ∨ ¬z ∨ ¬w  (∈ S)
6. ¬x ∨ y ∨ ¬z  (=res(4,5))
7. ¬x ∨ y       (=res(3,6))
8. x ∨ y        (∈ S)
9. y            (=res(7,8))
10. □           (=res(1,9))

## Elsődrendű logika
- Minden ember halandó! Szokratész ember! -> Szokratész halndó!

### Szintaxis
- Ábécé
    - Pred - predikátumszimbólumok véges halmaza
    - Func - függvényszimbólumok véges halmaza
    - Cnst - konstansszimbólumok véges halmaza
    - Ind  - Individuumváltozók
    - 0-d rendű műveletek és univerzális és egzisztenciális kvantor
    - Zárójelek és vessző
- Termek
    - Minden x ∈ Ind akkor x ∈ Term
    - Minden c ∈ Cnst akkor c ∈ Term
    - Minden f ∈ Func akkor f(t₁, .., tₐᵣ₍f₎) ∈ Term
- Formulák
    - minden p ∈ Pred és t₁, .., tₐᵣ₍p₎ ∈ Term akkor p(t₁, .., tₐᵣ₍p₎) ∈ Form, atomi formula
    - ...
- Interpretáció és változókiértékelés
    - I = < U, I_Pred, I_Func, I_Cnst> rendezett négyes az interpretáció
    - I_Pred : a pred-ekhez rendel értékeket
    - I_Func : függvényeket rendel a szimb.-hoz
    - I_Cnst : Konst. szimb.-hoz rendel értéket

    - κ : Ind → U egy változókiértékelés

#### Példa
- I = < ℕ, I_Pred, I_Func, I_Cnst>
    - I_Pred(p) = p', (m,n) :∈ p' ↔ m ≥ n
    - I_Pred(q) = q', (m,n) :∈ q' ↔ m = n
    - I_Func(f) = f', f'(m,n := m+n)
    - I_Cnst(a) := 0
    - κ*(y) = κ(y) minden y ∈ Ind, y ≠ x
- |p(f(y,y),x)|^(I,κ) = i : y=3, x=2
- |q(f(y,y),x)|^(I,κ) = h : y=3, x=2

### Szabad és kötött előfordulás
- Kötött: ∃xϕ -> x zárt előfordulés
- Szabad: különben
- Ha ϕ minden változója kötött akkor zárt

### Szemantikus fogalmak
- Kiélégíthető, kielégíthetetlen
- Logikailag igaz(érvényes) ha minden kielégíti
- Logikai ekvivalens
- ...

### Törnények
1. nulladrendű törvények
2. ha x nem szabad vélt. A-nak
    ∀xA ~ A és ∃xA ~ A
3. ∀x∀yS ~ ∀y∀xA és ∃x∃yS ~ ∃y∃xA
4. ¬∃xA ~ ∀x¬A és ¬∀xA ~ ∃x¬A
5. ha x nem szabad vált. A-nak
    - ...
    - ...
    - ...
    - ...
6. ∀xA ∧ ∀xB ~ ∀x(A ∧ B) és ∃xA ∨ ∃xB ~ ∃x(A ∨ B)

#### Példa
- E(x) : x ember
- H(x) : x halandó
- s : Szókratész (cnst)
- Minden ember halandó : ∀x(E())
- 4. ea 103.oldal 
- ...

## Függvények aszimptotikus nagysága
- Ω
- Θ
- O
- f, g = O(h) -> f + g = O(h) (összeadásra zártság)
- (pozitív konstanasal szorzásra zártság)
- (szekvencia tétel)
- ... cuccok

## Algoritmikus megoldás
- Véges utasítással megoldja a problémát minden inputra
- Eldöntés algoritmusnaál
    - nem eredménynél nem mindig terminál akkor parciális algoritmus
- Kurt Göbel - rekurzív függvényi
- Alonso Church - λ kalkulus
- Alan Turing - Turing gép

- Church-Turing tézis
    - Minden algoritmizálható probléma megoldható Turing-géppel


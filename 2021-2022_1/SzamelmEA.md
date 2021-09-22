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
|--------|---------|---|---------|------------|-----------|---------| 
| | | | | | | |

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
    4. 
    5. 
    6. 
    7. a → b ~₀ ¬a ∨ b
    8. 
    9. a ∨ ¬a ~₀ ⊤ , a ∧ ¬a ~₀ ⊥
    10. a ∨ ⊤ ~₀ ⊤ , a ∨ ⊥ ~₀ a
    11. 

- Szabályok használata nem változtatja az igazságértéket

- **Tételek**
    - a kielégíthetetlen, ha ¬a ~₀ ⊤
    - 

- Literál : x és ¬x
- Elemi diszjunkció (klóz) : a₁ ∨ ... ∨ aₙ, aᵢ-k kölönböző literálok
- Konjunktív normálforma (KNF) : k₁ ∧ ... ∧ kₙ ahol kᵢ klóz
-  Diszjunktív normálforma (DNF) : 

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

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





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


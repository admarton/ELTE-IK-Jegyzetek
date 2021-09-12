# Számításelmélet GY 2021.09.7

## Grammatika G = (N,T,P,S)
- Nemterminálisok
- Terminálisok
- Produkciós szamélyok
- Start szimbólum

## Chomsky Grammatikák
Chomsky kitalálta a típúsokat  
0. nincs korlát
1. ∀ u₁Au₂ → u₁vu₂ ∈ P, u₁,u₂,v ∈ (N ∪ T)*, A ∈ N, v ≠ ɛ  
        S → ɛ lehet, de akkor S nem lehet szabály jobb oldalán (KES)
2. A → v, A ∈ N, v ∈ (N ∪ T)*
3. A → uB vagy A → u, A,B ∈ N, u ∈ T*

Nevek  
1. Környezetfüggő
2. Környezetfüggetlen
3. Reguláris

## Chomsky Normálforma (CNF)
**Def:** Egy G. Chomsky nf. ha P-ben ilyenek vannak:
- S → ɛ
- A → BC, A,B,C ∈ N; (B,C ≠ S, ha S → ɛ ∈ P)
- A → a, A ∈ N, a ∈ T

Környezetfüggetlenből mindig lehet CNF-et csinálni

## Chomsky Normálformára hozás
1. Új kezdőszimbólum (S₀→S, ha S szerepel szabály jobb oldalán)
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
    - Ha S benne van az U-ban, akkor az ɛ benne van a nyelvben. A kezdő szimnbólumból epszilonba is el lehet jutni
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

    - Gyakvez: a lánc helyére tegyük be a kövi láncszem szabályait.

## Feladat
Hozzuk CNF-re.  
S → AB | AC  
A → aba | DS  
B → DCC | aS  
C → bbD | ɛ  
D → SS | ɛ  

0. Lépés
    - 2-es grammatike-e
        - igen
1. Új kezdőszimbólum (S₀→S, ha S szerepel szabály jobb oldalán)
    - Kell 
        - S₀ → S
2. Álterminálisok bevezetése   
S₀ → S  
S → AB | AC  
A → X₁X₂X₁ | DS  
B → DCC | X₁S  
C → X₂X₂D | ɛ  
D → SS | ɛ
X₁ → a  
X₂ → b  
    
3. Hosszredukció  
S₀ → S  
S → AB | AC  
A → X₁Z₁ | DS  
B → DZ₂ | X₁S  
C → X₂Z₃ | ɛ  
D → SS | ɛ
X₁ → a  
X₂ → b  
Z₁ → X₂X₁  
Z₂ → CC  
Z₃ → X₂D 

4. ɛ-mentesítés   
    - *U halmaz:*
        U₁ = {C,D}  
        U₂ = {C,D,Z₂}  
        U₃ = {B,C,D,Z₂} = U  
    - *P szabályok:*  
    S₀ → S  
    S → AB | AC | A   
    A → X₁Z₁ | DS | S  
    B → DZ₂ | X₁S | Z₂ | D  
    C → X₂Z₃  
    D → SS   
    X₁ → a  
    X₂ → b  
    Z₁ → X₂X₁  
    Z₂ → CC | C  
    Z₃ → X₂D | X₂  

5. Láncmentesítés   
S₀ → **S**  
S → AB | AC | **A**   
A → X₁Z₁ | DS | **S**  
B → DZ₂ | X₁S | **Z₂** | **D**  
C → X₂Z₃  
D → SS   
X₁ → a  
X₂ → b  
Z₁ → X₂X₁  
Z₂ → CC | **C**  
Z₃ → X₂D | **X₂**  


S₀ → AB | AC | X₁Z₁ | DS      
S → AB | AC | X₁Z₁ | DS     
A → AB | AC | X₁Z₁ | DS    
B → DZ₂ | X₁S | CC | X₂Z₃ | SS  
C → X₂Z₃  
D → SS   
X₁ → a  
X₂ → b  
Z₁ → X₂X₁  
Z₂ → CC | X₂Z₃  
Z₃ → X₂D | b

## Feldat megoldás
1. Új kezdőszimbólum (S₀→S, ha S szerepel szabály jobb oldalán)
2. Álterminálisok bevezetése  
3. Hosszredukció
4. ɛ-mentesítés
5. Láncmentesítés

## Házi
N = {A,B,S}  
T = {+,*,(,),d}  
S → A | A + S   
A → B | B * A   
B → d | ( S )   

1. Új kezdőszimbólum (S₀→S, ha S szerepel szabály jobb oldalán)  
    - Szerepel
2. Álterminálisok bevezetése
S₀ → S    
S → A | A X₁ S   
A → B | B X₂ A   
B → d | X₃ S X₄  
X₁ → +  
X₂ → *  
X₃ → (  
X₄ → )  

3. Hosszredukció  
S₀ → S    
S → A | A Z₁   
A → B | B Z₂   
B → d | X₃ Z₃  
X₁ → +  
X₂ → *  
X₃ → (  
X₄ → )  
Z₁ → X₁ S  
Z₂ → X₂ A  
Z₃ → S X₄

4. ɛ-mentesítés  
    - **Nincs ɛ !!!**  

5. Láncmentesítés  
S₀ → **S**    
S → **A** | A Z₁   
A → **B** | B Z₂   
B → d | X₃ Z₃  
X₁ → +  
X₂ → *  
X₃ → (  
X₄ → )  
Z₁ → X₁ S  
Z₂ → X₂ A  
Z₃ → S X₄

S₀ → d | X₃ Z₃ | B Z₂ | A Z₁    
S → d | X₃ Z₃ | B Z₂ | A Z₁   
A → d | X₃ Z₃ | B Z₂   
B → d | X₃ Z₃  
X₁ → +  
X₂ → *  
X₃ → (  
X₄ → )  
Z₁ → X₁ S  
Z₂ → X₂ A  
Z₃ → S X₄  
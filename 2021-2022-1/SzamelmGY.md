# Számításelmélet GY 2021.09.7

## Grammatika G = (N,T,P,S)
- Nemterminálisok
- Terminálisok
- Produkciós szamélyok
- Start szimbólum

## Chomsky Grammatikák
Chomsky kitalálta a típusokat  
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
    - X -> Y₁Y₂...Yₖ, k ≥ 3 szabályt helyettesítjük:
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

## Feldatmegoldás
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

# Számelm GY 2021.09.14

## CYK Algoritmus
- CNF-ben kell lennie
- Eldönti a szóproblémát
    - Igen / nem a kimenete
    - Egy szó a bemenete
    - Eldönti, hogy a nyelvben van
- Lentről felfelé elemez
- **Szorgalmi a szintaxisfához**
- Mátrix van
    - A részszót hogyan tudjuk előállítani
    - Sorok az, hogy milyen hosszú résszóról van szó
    - Az oszlopok meg az, hogy hányadik betűtől
    - Minden cellában nemterminálisok vannak amiből le lehet vezetni az alatta lévő résszót
- Ha az első sor első oszlopában van S, akkor előállítható a szó
- (i,j)-ben szerepel A, ha van olyan A ⟶ BC ∈ P
    - B szerepel (k,j)-ben
    - C szerepel (i-k, k+j)-ben
    - k ∈ [1,...,i-1]
- O(n³) műveletigény

|u_1|u_2|...|u_n|
|---|---|---|---|
|   |
|

## Példa 1

- G:  
    S → AB  
    A → AA | a  
    B → b  
- Input:
    aaaab

| n | 1 | 2 | 3 | 4 | 5 |
|:--|---|---|---|---|---|
| 1 | S |   |   |   |   |
| 2 | A | S |   |   |   |
| 3 | A | A | S |   |   |
| 4 | A | A | A | S |   |
| 5 | A | A | A | A | B |
|   | a | a | a | a | b |


## Példa 2

- G:  
    S → AB | BC  
    A → XA | a  
    X → a  
    C → YC | c  
    Y → c
    B → UV | VW  
    U → XX  
    W → YY  
    V → ZZ  
    Z → b  
- Input:
    aabbcc

| n | 1 | 2 | 3 | 4 | 5 | 6 |
|:--|---|---|---|---|---|---|
| 6 | S |   |   |   |   |   |
| 5 | S | S |   |   |   |   |
| 4 | B | ∅ | B |   |   |   |
| 3 | ∅ | ∅ | ∅ | ∅ |   |   |
| 2 |A,U| ∅ | V | ∅ |C,W|   |
| 1 |A,X|A,X| Z | Z |C,Y|C,Y|
|   | a | a | b | b | c | c |

## Házi

- G:  
    S → BZ₂ | a | X₃Z₃ | AZ₁  
    A → a | X₃Z₃ | BZ₂  
    B → a | X₃Z₃     
    Z₁ → X₁S  
    Z₂ → X₂A
    Z₃ → SX₄  
    X₁ → +  
    X₂ → *  
    X₃ → (  
    X₄ → )  
- Input:
    (a+a)*a

| n | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|:--|---|---|---|---|---|---|---|
| 7 |S,A|   |   |   |   |   |   |
| 6 | 0 | 0 |   |   |   |   |   |
| 5 |SAB| 0 | 0 |   |   |   |   |
| 4 | 0 | z₃| 0 | 0 |   |   |   |
| 3 | 0 | S | 0 | 0 | 0 |   |   |
| 2 | 0 | 0 | Z₁| Z₃| 0 | Z₂|   |
| 1 | X₃|SAB| X₁|SAB| X₄| X₂|SAB|
|   | ( | a | + | a | ) | * | a |

## Szorgalmi
+ 7,5% a ZH-n (fél jegy)  
CYK-ból hogyan lehet szintaxisfát csinálni + példa (kb 2 oldal)  
ZH-ig teamsen

# Gyak 2021.09.21

## Veremautomata
- állapotok
- szallag
- verem - pop van mindig
- ɛ-átmenet
    - helyben marad de a veremmel történik dolog
    - első input előtt és utolsó után is lehet
- nem determinisztikus
- (Z, Q, T, δ, z₀, q₀, F)
- Z - Verem szim
- Q - Állapotok
- T - inputok
- z₀ - verem kezd.
- q₀ - kezd. áll.
- F - elfogadó áll. 
- δ - átmeneti szabályok
    - δ : z×q×{T∪{ɛ}} → 2^(Z*×Q)

- konfiguráció : egy "állapota" 
    - zqw szó, ahol z∈Z*, q∈Q, w∈T*
    - mi van a veremben, állapot, mi van a szalagon

- közvetlen lépés:
    - q állapotban vagyunk, z van a verem tetején és x-et olvasunk
    - δ(z,q,x)={(u₁,p₁),..,(uₙ,pₙ)} // uᵢ∈Z*, pᵢ∈Q
    - δ(z,q,ɛ)={(u₁,p₁),..,(uₙ,pₙ)} // uᵢ∈Z*, pᵢ∈Q

- redukció:
    - α-t β-ra redukálja az A autómata : α ⇒_A β
    - α = rzqaw
    - β = rupw
    - //r - még van valami a veremben, w - van még valami a szalagon
    - (u,p) ∈ δ(zqa)

- többlépéses redukció:
    - egylépéses tranz. refl. lezártja
    - α ⇒* β

- elfogadó állapottal elfogadó nyelv
    - L(A) = {u∈T* | z₀q₀u ⇒* rp, r∈Z*, p∈F}

- üres veremmel elfogadott nyelv
    - ha kiürül a verem és végigér a szón, akkor elfogadja
    - L(A) = {u∈T* | z₀q₀u ⇒* p, p∈Q}

## Feladat 1
- L = { aⁿbⁿ | n≥1 }
- ehhez a nyelvhez automata
- le kell modellezni h kb mit csináljon
- mutasd be a működéstő
    - olvas a szalagon a-t, akkor beleteszi a verembe
    - ha b-t olvas megnézi hogy van-e a veremben a
    - minden b-re legyen a veremben egy a
- gráf
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="600" height="200" version="1.1" xmlns="http://www.w3.org/2000/svg">
	<ellipse stroke="black" stroke-width="1" fill="none" cx="98.5" cy="126.5" rx="30" ry="30"/>
	<text x="88.5" y="132.5" font-family="Times New Roman" font-size="20">q0</text>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="262.5" cy="127.5" rx="30" ry="30"/>
	<text x="252.5" y="133.5" font-family="Times New Roman" font-size="20">q1</text>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="433.5" cy="127.5" rx="30" ry="30"/>
	<text x="422.5" y="133.5" font-family="Times New Roman" font-size="20">q2</text>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="433.5" cy="127.5" rx="24" ry="24"/>
	<path stroke="black" stroke-width="1" fill="none" d="M 95.099,96.811 A 22.5,22.5 0 1 1 119.996,105.742"/>
	<text x="120" y="52.5" font-family="Times New Roman" font-size="20">(#,a) → #a</text>
	<polygon fill="black" stroke-width="1" points="119.996,105.742 129.423,105.37 123.792,97.105"/>
	<polygon stroke="black" stroke-width="1" points="128.499,126.683 232.501,127.317"/>
	<polygon fill="black" stroke-width="1" points="232.501,127.317 224.531,122.268 224.47,132.268"/>
	<text x="140" y="148.5" font-family="Times New Roman" font-size="20">(a,b) → ɛ</text>
	<path stroke="black" stroke-width="1" fill="none" d="M 79.097,103.773 A 22.5,22.5 0 1 1 104.736,97.275"/>
	<text x="25" y="49.5" font-family="Times New Roman" font-size="20">(a,a) → aa</text>
	<polygon fill="black" stroke-width="1" points="104.736,97.275 112.347,91.701 103.061,87.991"/>
	<path stroke="black" stroke-width="1" fill="none" d="M 249.275,100.703 A 22.5,22.5 0 1 1 275.725,100.703"/>
	<text x="230" y="51.5" font-family="Times New Roman" font-size="20">(a,b) → ɛ</text>
	<polygon fill="black" stroke-width="1" points="275.725,100.703 284.473,97.17 276.382,91.292"/>
	<polygon stroke="black" stroke-width="1" points="292.5,127.5 403.5,127.5"/>
	<polygon fill="black" stroke-width="1" points="403.5,127.5 395.5,122.5 395.5,132.5"/>
	<text x="305" y="148.5" font-family="Times New Roman" font-size="20">(#,ɛ) → #</text>
</svg>

- leírás
    - δ(#,q0,a) = (#a,q0)
    - δ(a,q0,a) = (aa,q0)
    - δ(a,q0,b) = (ɛ,q1)
    - δ(a,q1,b) = (ɛ,q1)
    - δ(#,q1,ɛ) = (#,q2)
    - ha üressel elfogadható: δ(#,q1,ɛ) = (ɛ,q2)
    - A = ({q0,q1,q2}, {a,b}, {#,a,b}, δ, q0, #, {q2})

- levezetés:
    1. #q0aaabbb → #aq0aabbb
    2. #aq0aabbb → #aaq0abbb
    3. #aaq0abbb → #aaaq0bbb
    4. #aaaq0bbb → #aaq1bb
    5. #aaq1bb → #aq1b
    6. #aq1b → #q1
    7. #q1 → #q2
    - ha üressel elfogadható: #q1 → q2

## Feladat 2
- L = { ucu⁻¹ | u∈{a,b}⁺ }
- amíg c jön addig berakom a cuccokat
- a c után nézem h ugyanaz van-e a veremben

<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="800" height="300" version="1.1" xmlns="http://www.w3.org/2000/svg">
	<polygon fill="black" stroke-width="1" points="1,0 31,30 25,35 35,35 35,25 29,30 0,1"/>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="61.5" cy="54.5" rx="30" ry="30"/>
	<text x="51.5" y="60.5" font-family="Times New Roman" font-size="20">q0</text>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="294.5" cy="54.5" rx="30" ry="30"/>
	<text x="284.5" y="60.5" font-family="Times New Roman" font-size="20">q1</text>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="557.5" cy="54.5" rx="30" ry="30"/>
	<text x="547.5" y="60.5" font-family="Times New Roman" font-size="20">q2</text>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="557.5" cy="54.5" rx="24" ry="24"/>
	<polygon stroke="black" stroke-width="1" points="91.5,54.5 264.5,54.5"/>
	<polygon fill="black" stroke-width="1" points="264.5,54.5 256.5,49.5 256.5,59.5"/>
	<text x="147.5" y="75.5" font-family="Times New Roman" font-size="20">(a,c) → a</text>
	<text x="147.5" y="95.5" font-family="Times New Roman" font-size="20">(b,c) → b</text>
	<path stroke="black" stroke-width="1" fill="none" d="M 74.725,81.297 A 22.5,22.5 0 1 1 48.275,81.297"/>
	<text x="22.5" y="143.5" font-family="Times New Roman" font-size="20">(#,a) → #a</text>
	<text x="22.5" y="163.5" font-family="Times New Roman" font-size="20">(#,b) → #b</text>
	<text x="22.5" y="183.5" font-family="Times New Roman" font-size="20">(a,a) → aa</text>
	<text x="22.5" y="203.5" font-family="Times New Roman" font-size="20">(a,b) → ab</text>
	<text x="22.5" y="223.5" font-family="Times New Roman" font-size="20">(b,b) → bb</text>
	<text x="22.5" y="243.5" font-family="Times New Roman" font-size="20">(b,a) → ba</text>
	<polygon fill="black" stroke-width="1" points="48.275,81.297 39.527,84.83 47.618,90.708"/>
	<polygon stroke="black" stroke-width="1" points="324.5,54.5 527.5,54.5"/>
	<polygon fill="black" stroke-width="1" points="527.5,54.5 519.5,49.5 519.5,59.5"/>
	<text x="400.5" y="75.5" font-family="Times New Roman" font-size="20">#,ɛ → #</text>
	<path stroke="black" stroke-width="1" fill="none" d="M 307.725,81.297 A 22.5,22.5 0 1 1 281.275,81.297"/>
	<text x="263.5" y="143.5" font-family="Times New Roman" font-size="20">(a,a) → ɛ</text>
	<text x="263.5" y="168.5" font-family="Times New Roman" font-size="20">(b,b) → ɛ</text>
	<polygon fill="black" stroke-width="1" points="281.275,81.297 272.527,84.83 280.618,90.708"/>
</svg>

## Faladat 3
- L = { uu⁻¹ | u∈{a,b}⁺ }
- berakjuk a cuccokat az automatába
- ha olyan jön ami bent van, akkor kiolvasó állapotba megyünk
- onnan kezdve kiolvasgatunk

<svg width="800" height="300" version="1.1" xmlns="http://www.w3.org/2000/svg">
	<polygon fill="black" stroke-width="1" points="1,0 31,30 25,35 35,35 35,25 29,30 0,1"/>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="61.5" cy="54.5" rx="30" ry="30"/>
	<text x="51.5" y="60.5" font-family="Times New Roman" font-size="20">q0</text>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="294.5" cy="54.5" rx="30" ry="30"/>
	<text x="284.5" y="60.5" font-family="Times New Roman" font-size="20">q1</text>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="557.5" cy="54.5" rx="30" ry="30"/>
	<text x="547.5" y="60.5" font-family="Times New Roman" font-size="20">q2</text>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="557.5" cy="54.5" rx="24" ry="24"/>
	<polygon stroke="black" stroke-width="1" points="91.5,54.5 264.5,54.5"/>
	<polygon fill="black" stroke-width="1" points="264.5,54.5 256.5,49.5 256.5,59.5"/>
	<text x="147.5" y="75.5" font-family="Times New Roman" font-size="20">(a,a) → a</text>
	<text x="147.5" y="95.5" font-family="Times New Roman" font-size="20">(b,b) → b</text>
	<path stroke="black" stroke-width="1" fill="none" d="M 74.725,81.297 A 22.5,22.5 0 1 1 48.275,81.297"/>
	<text x="22.5" y="143.5" font-family="Times New Roman" font-size="20">(#,a) → #a</text>
	<text x="22.5" y="163.5" font-family="Times New Roman" font-size="20">(#,b) → #b</text>
	<text x="22.5" y="183.5" font-family="Times New Roman" font-size="20">(a,a) → aa</text>
	<text x="22.5" y="203.5" font-family="Times New Roman" font-size="20">(a,b) → ab</text>
	<text x="22.5" y="223.5" font-family="Times New Roman" font-size="20">(b,b) → bb</text>
	<text x="22.5" y="243.5" font-family="Times New Roman" font-size="20">(b,a) → ba</text>
	<polygon fill="black" stroke-width="1" points="48.275,81.297 39.527,84.83 47.618,90.708"/>
	<polygon stroke="black" stroke-width="1" points="324.5,54.5 527.5,54.5"/>
	<polygon fill="black" stroke-width="1" points="527.5,54.5 519.5,49.5 519.5,59.5"/>
	<text x="400.5" y="75.5" font-family="Times New Roman" font-size="20">#,ɛ → #</text>
	<path stroke="black" stroke-width="1" fill="none" d="M 307.725,81.297 A 22.5,22.5 0 1 1 281.275,81.297"/>
	<text x="263.5" y="143.5" font-family="Times New Roman" font-size="20">(a,a) → ɛ</text>
	<text x="263.5" y="168.5" font-family="Times New Roman" font-size="20">(b,b) → ɛ</text>
	<polygon fill="black" stroke-width="1" points="281.275,81.297 272.527,84.83 280.618,90.708"/>
</svg>


## Feladat 4
- L = { u∈{a,b}* | lₐ(u) = lᵦ(u) }
- ha nem találok semmi, akkor berakom
- ha van párja, akkor kiveszem
- egy állapot, hurokél sok szabállyal

# Gyak_4 2021.09.28

## ZH
- 2 hét múlva

## Logika
- Kétértékű logikával foglalkozunk mi
- i,h (egyéb 1,0)
- Nagy I,H mást jelent
- összetett állítás: állítás és logikai műveletek kapcsolata
- A→B, B a tágabb halmaz, A része B-nek

### Ítéletlogika leíró nyelve
- ábécé: Var={x,y,z,x₁,...} ; ¬ ; ∧ ; ∨ ; → ; ( ; ) ;

- Logikai összetettség
    - l(x)=0
    - l(¬A) = l(A) + 1
    - l(A ∘ B) = l(A) + l(B) + 1
    - hány műveleti jel van benne
- Közvetlen részformula
    - A ∨ B közv. részf.: A,B
- Részformula
    - A ∨ (B ∨ C) részf.: B,C,A ∨ (B ∨ C)
- Fő műveleti jele, fő logikai összekötő
    - Milyen típusú a formula?
    - Az ami az egész formulára hat
- Zárójel elhagyás
    - Ha a prioritása nagyobb mint a másiké
    - A → (B → (C → D))
    - ((A ∧ B) ∧ C) ∧ D

#### Feladat
- a : (((x → y) ∧ (y → z)) → (¬x ∨ z))
    - ((x → y) ∧ (y → z)) → (¬x ∨ z)
    - ((x → y) ∧ (y → z)) → ¬x ∨ z
    - (x → y) ∧ (y → z) → ¬x ∨ z
    - l((x → y) ∧ (y → z) → ¬x ∨ z) = 6
    - imp
- b : ((x → y) → (y → x))
    - (x → y) → y → x
    - l((x → y) → y → x) = 3
    - imp

#### Szemantika
- B_I(A) := I(A)

### Igazságtábla
- Bázis : ítéletváltozók sorrendje
- Táblában az összes lehetséges kombinációja a változók értékének

| x | y | z | (x→y)→z | x→(y→z) |
|:-:|:-:|:-:| :-----: | :-----: |
| i | i | i |    i    |    i    |
| i | i | h |    h    |    h    |
| i | h | i |    i    |    i    |
| i | h | h |    i    |    i    |
| h | i | i |    i    |    i    |
| h | i | h |    h    |    i    |
| h | h | i |    i    |    i    |
| h | h | h |    h    |    i    |

- két formula **ekvivalens** ha megegyezik az igazságtáblájuk, bizonyít
    - a fenti két formula nem ekviv.
    - van két eltérő sorok

### Igazhalmaz/Hamishalmaz
- Olyan interpretációk amikre i/h a formula
- ((x→y)→z)ʰ = {(i, i, h), (h, i, h), (h, h, h)}
- lesz ZH-ban

### Szemantikus tulajdonságok
- I interp. **kielégít** B formulát: I ⊧₀ B
- B **kielégíthető** ha  ∃I ⊧₀ B
- B **kielégíthetetlen** ha  ∄I ⊧₀ B
- B **tautológia** ha ⊧₀ B
- ugyanezek formulahalmazokra
- A form.-nak B form. **tautológikus következménye**: A ⊧₀ B ha I ⊧₀ A és I ⊧₀ B
- A és B **tautológikusan ekviv.**: A ~₀ B ha A ⊧₀ B és B ⊧₀ A
- ugyanez formulahalmaz és formula esetén

### Nevezetes ekviv.
- a) dupla tagadás törvénye
- b) indenpotens tul.
- c) kommutativitás tul.
- d) asszociativitás tul. (átzárójelezhetőség)
- e) disztributivitás tul.
- f) elnyelési tul. *(A ∨ B) ∧ B ~₀ B és (A ∧ B) ∨ B ~₀ B*
- g) implikáció átírása *A → B ~₀ ¬A ∨ B*
- h) De-Morgan azon. *¬(A ∧ B) ~₀ ¬A ∨ ¬B és ¬(A ∨ B) ~₀ ¬A ∧ ¬B*
- i) *A ∨ ¬A ~₀ ⊤ és A ∧ ¬A ~₀ ⊥*
- j) *A ∨ ⊤ ~₀ ⊤ és A ∧ ⊥ ~₀ ⊥*
- k) *A ∨ ⊥ ~₀ A és A ∧ ⊤ ~₀ A*
- bizonyítsa/lássa be feladatok erre épülnek

#### Feladat 
- Lássa be: ⊧₀ x → (y → x)
1. implikációtól megszabadulni 
    - x → (y → x)
    - ~₀ x → (¬y ∨ x)
    - ~₀ ¬x ∨ (¬y ∨ x)
2. többi szabály
    - ~₀ (¬x ∨ ¬y) ∨ x
    - ~₀ (¬y ∨ ¬x) ∨ x
    - ~₀ ¬y ∨ (¬x ∨ x)
    - ~₀ ¬y ∨ ⊤
    - ~₀ ⊤

| x | y | x→(y→x) |
|:-:|:-:| :-----: |
| i | i |    i    |
| i | h |    i    |
| h | i |    i    |
| h | h |    i    |


# Gyak 5 2021.10.05

## ZH
- jövőhét
- élőben papír
- online nem kell papír
- zh közben is lehet kérdezni
- első 5 gyak anyaga
- CNF, CYK, Veremautómata, Nulladrandű logika

## Logika

#### Feladat 
- Lássuk be: ¬(x ∨ (y ∧ (z → x))) ~₀ ¬x ∧ (y → z)
- Tautológikusan ekviv.
- Jó szabály: implikáció, negáció bevitel, disztribúció
- ~₀ ¬(x ∨ (y ∧ (¬z ∨ x)))
- ~₀ ¬x ∧ ¬(y ∧ (¬z ∨ x))
- ~₀ ¬x ∧ (¬y ∨ ¬(¬z ∨ x))
- ~₀ ¬x ∧ (¬y ∨ (z ∧ ¬x))
- ~₀ ¬x ∧ ((¬y ∨ z) ∧ (¬y ∨ ¬x))
- ~₀ ¬x ∧ (y → z) ∧ (¬y ∨ ¬x)
- ~₀ ¬x ∧ (¬y ∨ ¬x) ∧ (y → z)
- ~₀ (¬x ∧ (¬y ∨ ¬x)) ∧ (y → z)
- ~₀ ¬x ∧ (y → z)
- kijött

## Konjunktív és diszjunktív normál forma
- Literál
    - Prímformula vagy negáltja (x, ¬x). Alapja: x
    - Komplemens párja, a negáltja
- Elemi konjungció  ∧
    - különböző alapú literálok konjungciója
- Elemi diszjunkció (klóz) ∨
    - különböző alapú literálok diszjunkciója
- Teljes ha a bázis minden változója benne van
- DNF - elemi konj. diszjunkciója
- KNF - elemi diszj. konjunkciója
- KKNF, KDNF - kitűntetett, összed elemi cucc teljes

### Feladat
- a. x → y                          - semmi
- b. ¬z                             - literál, elemi dis/kon, KNF/DNF
- c. x ∧ ¬y ∧ z                     - teljes elemi kon, KNF/KDNF
- d. (x ∨ ¬y) ∧ z                   - KNF
- e. (x ∧ y ∧ ¬z) ∨ (¬x ∧ y ∧ z)    - KDNF

## Ítélettáblából lehet DNF/KNF-et csinálni
- Most kimarad

### Feladat - KNF-re hozás
- x → y → ¬(x ∧ ¬y)
- ¬(¬x ∨ y) ∨ ¬(x ∧ ¬y)
- (x ∧ ¬y) ∨ (¬x ∨ y)
- (x ∧ ¬y) ∨ ¬x ∨ y <-> DNF
- (x ∨ ¬x ∨ y) ∧ (¬y ∨ ¬x ∨ y) <-> KNF
- (⊤ ∨ y) ∧ (⊤ ∨ ¬x)
- ⊤ ∧ ⊤
- ⊤

## Rezolúció
- Tét.: F ⊧₀ ϕ akkor és csak akkor ha F∪{¬ϕ} kielégíthetetlen.
- Rezolóció klóz halmazról eldönti, hogy kielégíthetetlen-e
- Rezolúciós levezetés lényege, hogy kijöjjön az üres klóz
- Komplemens literálpárt ki kell venni
- res(x ∨ z, ¬y ∨ z) = x ∨ z

S={¬x∨y, x, ¬y}
|   |        |
|:-:| :----: |
| 1 |  ¬x∨y  |
| 2 |    x   |
| 3 |res(1,2)|
| 4 |  ¬y    |
| 3 |res(3,4)|

### Feladat
Igazold, hogy {A1, A2, A3} következménye B
- Változók
    - P : elmegyünk Pécsre
    - H : elmegyünk Hévízre
    - K : elmegyünk Keszthelyre
- A1 - Ha elmegyünk Pécsre, akkor Hévízre és Keszthelyre is.
    - P → H ∧ K
- A2 - Ha nem megyünk Keszthelyre, akkor elmegyünk Hévízre.
    - ¬K → H
- A3 - Ha elmegyünk Keszthelyre, akkor Pécsre is.
    - K → P
- B  - Tehát elmegyünk Hévízre
    - H

- Írélettábla
    - Ha az előzmények teljesülnek, akkor a következmény is teljesül

| P | H | K |   | P → H ∧ K | ¬K → H | K → P |   | H |
|:-:|:-:|:-:| - |:---------:|:------:|:-----:| - |:-:|
| i | i | i |   |   **i**   | **i**  | **i** |   | **i** |
| i | i | h |   |     h     |   i    |   i   |   | i |
| i | h | i |   |     h     |   i    |   i   |   | h |
| i | h | h |   |     h     |   h    |   i   |   | h |
| h | i | i |   |     i     |   i    |   h   |   | i |
| h | i | h |   |   **i**   | **i**  | **i** |   | **i** |
| h | h | i |   |     i     |   i    |   h   |   | h |
| h | h | h |   |     i     |   h    |   i   |   | h |

- Rezolúció
    - A következmény tagadását hozzávesszük az előzményekhet
    - Normálformára hozás
    - És-enként szét lehet szedni

S = {P → (H ∧ K), ¬K → H , K → P , ¬H}  
S = {¬P ∨ (H ∧ K), K ∨ H , ¬K ∨ P , ¬H}  
S = {(¬P ∨ H) ∧ (¬P ∨ K), K ∨ H , ¬K ∨ P , ¬H}  
S = {(¬P ∨ H), (¬P ∨ K), K ∨ H , ¬K ∨ P , ¬H}  
|   |        |     |
|:-:| :----: | :-: |
| 1 |   ¬H   |     |
| 2 | K ∨ H  |     |
| 3 |res(1,2)| = K |
| 4 | ¬K ∨ P |     |
| 5 |res(3,4)| = P |
| 6 |(¬P ∨ H)|     |
| 7 |res(5,6)| = H |
| 8 |res(1,7)|= ▭ |


# Gyak 7 2021.10.19

## Elsődrendű logika - Predikátumkalkulus
- Nulladrendű az állítások belselyével nem foglalkozik
    - Halmazokkal nem foglalkozik, része, nem része
- Szimbólumhalmaz:
    - Pred - predikátumszimbólum
    - Func - függvényszimb.
    - Cnst - konstanszimb. (aritás = 0)
    - Ind - indivídumváltozó (nincs aritás)
    - {¬,∧,∨,→,∀,∃}
    - ( ) ,
    - Aritás: mennyi argumentuma van s ∈ Pred ∪ Func ∪ Cnst
- Termek
    - Term ami Ind vagy Cnst vagy Func ami neki megfelelő számú Term argumentummal van ellátva
- Elsőrendű formula
    - Pred kell a formulához, zárojelébe termeket teszek
    - **atomi formula** : pred amiben termek vannak 
    - kvantor hatásköre a teljes formulára kihat akkor fő logikai összekötő -> kvantált formula
- Precedencia:
    - ∀,∃,¬,∧,∨,→
- Szerkezeti fa
    - Fölogikai összekötönál lehet vágni
    - ∀xϕ -> közvetlen ... -> ϕ
    - ¬∀x(P(x,y)) → q(x) ∨ ∃xq(x)
        - ¬∀x(P(x,y))
            - P(x,y)
        - q(x) ∨ ∃xq(x)
            - q(x)
            - ∃xq(x)
                - q(x)
    - leveleiben atomi formulák

- Szemantika
    - Interpretáció és változókiértékelés adja meg
    - Interpretáció
        - I = < U , I_pred, I_func, I_cnst >
        - U - tetsz. nem üres - univerzum
        - I_pred - reláció - eredmény : i/h
        - I_func - művelet - eredmény : alaphalmazbeli elem
        - I_cnst - univerzum elemét jelenti
    - változókiértékelés
        - κ : Ind → U
    
    - példa
        - U: ℕ
        - I_pred(p)=p^I, (m,n)∈p^I ⇔ m ≥ n
        - I_pred(q)=q^I, (m,n)∈q^I ⇔ m = n
        - I_func(f)=f^I, f^I(m,n):=m + n
        - I_cnst(a)='0
        - κ(x)=5, κ(j)=3

- Értékelés
    - |x| = κ(x), x ∈ Ind
    - |c| = c^I,  c ∈ Cnst
    - term értéke a részeinek értékei és a műveletek alkalmazásai

    - |f(f(x,y),y)| = f(f(5,3),3) = f(5+3,3) = 8 + 3 = 11

- Kiértékelés variánsa
    - x-nek lehet több kiértékelése is 
- Formula kiértékelése
    - Termek kiértékelése
    - Reláció eldöntése
    - ∀ - összes variánsra igaz
    - ∃ - legalább egy variánsra igaz

    - |p(f(y,y),x)| = 3+3 ≥ 5 = i
    - | ∀x p(x,a) |  = i
    - |∀x ∃y q(f(x,y),a)| = ∀x ∃y (x+y = 0) = h
    - |∀x(∀y q(f(y,x),y)→q(x,a))| = ∀x(∀y (y+x = y → x = a)) = i 

- Ind vált. előfordulása
    - Többször is előfordulhat, de attól még egy marad
    - Kötött a változó  ha minden előfordulása kötött
    - Kötött az előfordulás ha kvantor hatáskörben van
    - Ha minden változó kötött akkor Zárt
    - Különben nyitott
    - Paraméter ha van nyitott előfordulása
    - Ha zárt a formula akkor a kiértékelése nem függ a változókiértékeléstől

- Prímformula ha atomi vagy kvantált
- Prímkomponensek:
    - szerkezetifából könnyű meghatározni
    - Prímformula és nem részformulája prímformulának
    - Az ágon a legmagasabb prím
    - _x_ -> prímformula
    - *x* -> prímkomponens

```
¬(∀x p(x,y) → ∃x r(z) ∨ r(y))
            |
  ∀x p(x,y) → ∃x r(z) ∨ r(y)
          /     \
*_∀x p(x,y)_*  ∃x r(z) ∨ r(y)
       |           /     \
_p(x,y)_  *_∃x r(z)_*   *_r(y)_*
                |
            _r(z)_

Prímkomponenses felírás
¬(A→B∨C)
Nulladrendű lesz
```

- Kielégíthető ha van Interpretáció ami kielégíti
- Logikailag igaz ha minden I kielégíti : **⊧ ϕ**
- Logikailag ekvivalens ha ugyn az az interpretáció elégíti ki
- Logikai következmény ha az I amire a halmaz i, arra a formula is i
- Quine-táblázat - igazságtábla a prímkomponenses felírásra
- Tautológikusan igaz ha a Quine-táblázatban van csupa i-s sor : **⊧₀ ϕ**
- Tautológikus erősebb mint a logikai

- Értéktábla
    - Ítélettáblához hasonlít
    - Csak a paramétereket sorolja fel
    - Oszlopba felírni
    - A paramétert az univerzum minden elemén vizsgálni kell

- Nulladrendű törvények Elsőrendűek is 
    - x ∉ Par(ϕ) - x kötve van ϕ-ben
        - ∀xϕ ~ ϕ és ∃xϕ ~ ϕ

    - ∀x∀yϕ ~ ∀y∀xϕ
    - ¬∃ϕ ~ ∀x¬ϕ
    - x ∉ Par(ϕ)
        - kihozható a kvantor az x elé
        - ϕ ∧ ∀xδ ~ ∀x(ϕ ∧ δ)

### Feladat
- ZH-ban lehet

- U : {0,1,2}
- I_pred: P→P^I, Q→Q^I
- I_func: f→f^I
- I_cnsrt: a → 0, b → 1
- P^I = {(0,1),(0,2),(2,1),(2,2)}
- Q^I = {(0),(2)}
- f^I a mod 3 összeadás

- (∀x(P(a,y) ∨ Q(x)) → ¬∀x∃yP(x,y)) ∧ P(f(y,y),b)

y | A | B | C | A → ¬B ∧ C
--|---|---|---|------------
0 | h | h | i | i
1 | i | h | i | i
2 | i | h | h | h

### Bizonyítás h nem törvény
- ϕ ∧ ∀xδ ~ ∀x(ϕ ∧ δ)
- ϕ = p(x)
- δ = q(x)
- p(x) ∧ ∀xq(x) ~ ∀x(p(x) ∧ q(x))
- U = ℕ
- q^I := {(x) | x ∈ ℕ}
- p^I := {(x) | x páros}
- κ: x → -4
- p(x) ∧ ∀xq(x) ~ ∀x(p(x) ∧ q(x))


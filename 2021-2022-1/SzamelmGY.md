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

# Számelm GY 2021.09.14

## CYK Algoritmus
- CNF-ben kell lennie
- Eldönti a szóproblémát
    - Igen / nem a kimenete
    - Egy szó a bemente
    - Eldönti, hogy a nyelvben van
- Lentről fölfelé elemez
- **Szorgalmi a szintaxisfához**
- Mártix van
    - A részszót hogyan tudjuk előállítani
    - Sorok az, hogy milyen hosszú résszóról van szó
    - Az oszlopok meg az, hogy hanyadik betűtől
    - Minden cellában nemterminálisok vannak amiból le lehet vezetni az alatta lévó résszót
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

## Verem autómata
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
    - q állaptban vagyunk, z van a verem tetején és x-et olvasunk
    - δ(z,q,x)={(u₁,p₁),..,(uₙ,pₙ)} // uᵢ∈Z*, pᵢ∈Q
    - δ(z,q,ɛ)={(u₁,p₁),..,(uₙ,pₙ)} // uᵢ∈Z*, pᵢ∈Q

- redukció:
    - α-t β-ra redukálja az A autómata : α ⇒_A β
    - α = rzqaw
    - β = rupw
    - //r - még van valami a veremben, w - van még valami a szalagon
    - (u,p) ∈ δ(zqa)

- több lépéses redukció:
    - egy lépéses tranz. refl. lezártja
    - α ⇒* β

- elfogadó állapotta lelfogadó nyelv
    - L(A) = {u∈T* | z₀q₀u ⇒* rp, r∈Z*, p∈F}

- üres veremmel elfogadott nyelv
    - ha kiürül a verem és végigér a szón, akkor elfogadja
    - L(A) = {u∈T* | z₀q₀u ⇒* p, p∈Q}

## Feladat 1
- L = { aⁿbⁿ | n≥1 }
- ehhez a nyelvhez autómata
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
- amíg c jön addig brakom a cuccokat
- a c után nézem h ugyan az van-e a veremben

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
- berkajuk a cuccokat az autómatába
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
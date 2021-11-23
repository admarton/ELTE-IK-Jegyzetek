# Számításelmélet EA 2021.09.08

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
    A grammatika által generált nyelv osztálya megegyezik a grammatika osztályával.

    L₃ ⊂ L₂ ⊂ L₁ ⊂ L₀

- Formális nyelvek megadása  
    - Generatív grammatikával előállítható.
    - Matematikai gépek, automaták
    - Egyéb: felsorolás, regexp

- Véges automata
    - Input szalagról olvas, belső állapota változik

- 3-as típusú nyelvek
    - 3-as t. grammatikák
    - 3-as norm.f. grammatikák
    - regexp
    - determinisztikus, n.d. véges automaták

- Veremautomata
    - input szalag + verem szerkezetű memória, belső állapota + verem változik
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
    - X -> Y₁Y₂...Yₖ, k ≥ 3 szabályt helyettesítjük:
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

**Tét.:** Minden hossz-nemcsökkentő grammatika környezetfüggő nyelvet generál.
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
Eldönthető, hogy egy G₃ az üres nyelvet generálja-e.  
**Biz.:**
Szélességi keresés.

**Tét.:**
Eldönthető, hogy két G₃ által generált nyelv diszjunkt-e.

**Tét.:**
Eldönthető, hogy két G₃ ugyan azt a nyelvet generálja.

**Tét.:**
Eldönthető, hogy egy G₃ bővebb nyelvet generál-e, mint a másik.

### Szóprobléma (membership problem)
**Tét.:** G₃-nál lineáris időben eldönthető, hatékonyan.
- t a szó
- H₀ := {S}
- Hᵢ₊₁ := { A ∈ N | ∃B ∈ Hᵢ ∧ B → tᵢ₊₁A ∈ P}
- Hᵢ az i. lépésben a szó végén álló terminálisok halmaza 
- VDA-val automatizálható a H-k kiszámítása
- Ha a szavunk kisebb, mint a grammatika jóval, akkor hatékonyabb a H-k kiszámolása mint a VDA elkészítés és futtatás.


**Áll.:** G₂ generálja-e a szót eldönthető.  
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
- a pozitív elemeket felismeri
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
- Kielégíthető ha van olyan interpretáció ami kielégíti
- Tautologia ha minden interpretáció kielégíti
- tautologikusan ekvivalensek ha pontosan ugyanazok az interpretációk elégítik ki
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
    - F ⊧(\models)₀ a akkor és csak akkor ha F∪{¬a} kielégíthetetlen

- Literál : x és ¬x
- Elemi diszjunkció (klóz) : a₁ ∨ ... ∨ aₙ, aᵢ-k különböző literálok
- Konjunktív normálforma (KNF) : k₁ ∧ ... ∧ kₙ ahol kᵢ klóz
- Elemi konjunkció : hasonlóan
- Diszjunktív normálforma (DNF) : hasonlóan 

- Ítéletkalkulusbeli formulához megadható vele ekviv. DNF
    - Az igazságtábla igaz sorai adják hogy mi kell bele
- Ítéletkalkulusbeli formulához megadható vele tautologikusan ekviv. KNF
    - A hamis sorok negáltjai kellenek
    1. implikáció eliminálás
    2. negációs operátorok csak ítéletváltozók előtt legyenek
    3. disztributív szabályokkal 2 szintűvé lapítjuk

- Rezolvens
    - 1 komplemens literálpárt tartalmaz klózoknak lehet rezolvense kivesszük belőlük a komplemens literálpárt és összevagyoljuk 
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
- Kötött: ∃xϕ -> x zárt előfordulás
- Szabad: különben
- Ha ϕ minden változója kötött akkor zárt

### Szemantikus fogalmak
- Kielégíthető, kielégíthetetlen
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
- Eldöntés algoritmusnál
    - nem eredménynél nem mindig terminál akkor parciális algoritmus
- Kurt Göbel - rekurzív függvényi
- Alonso Church - λ kalkulus
- Alan Turing - Turing gép

- Church-Turing tézis
    - Minden algoritmizálható probléma megoldható Turing-géppel

# EA 5 2021.10.06

## Turing gép
M = < Q, ∑, Γ, δ, q₀, qᵢ, qₙ >
- Q - állapotok halmaza
- q_0 kezdő, q_i elfogadó, q_n elutasító állapot
- ∑,Γ - ábécé

### Konfigurációja
uqv szó
- q ∈ Q
- u, v ∈ Γ
- v ≠ ɛ
- v a maradék szó

### Kezdő konfig.
- q₀u⎵

### Számolás
- Konfiguráció átmenet
- uqav konfig van
    - δ(q,a) = (r, b, R), akkor uqav |- ubrv'
    - δ(q,a) = (r, b, S), akkor uqav |- urbv
    - δ(q,a) = (r, b, L), akkor uqav |- u'rcbv
- Többlépéses konfig. átmenet
    - az egy lépéses tranz. szim. lezártja
    - |-* 

## TG által felismert nyelv
- Azokat a szavak, amikből a kezdő konfigurációból többlépéses konfig. átmenettel elfogadó állapotba jutunk.
- Felismert nyelvben az input ábécé szavai vannak, nem a szalagábécé
- L nyelv Tring-felismerhető
- L nyelv eldönthető, ha van hozzá TG ami minden bemenetre megállási konfigurációba jut - el tudja dönteni, hogy benne van-e a nyelvben minden inputra

## RE éd R
- RE Rekurzívan felsorolható - létezik Turing gép
- R Rekurzív nyelv - eldönthető TG-vel
- R ⊆ RE
- Milyen nyelv nincs benne RE-ben
    - van olyan

## TG futási ideje
- u szóra t, ha M TG u-ból t-lépésben megállási konfigurációba lép
- ha nincs ilyen t, akkor végtelen

- f(n) időkorlátos gép, ha minden szóra max f(n) lépésben végez
    - elég egy jó aszimptotikus felső korlát

## K-szalagos Turing Gép
- Több szalagról is olvas
- Konfigurációjában összes szalagon lévő fej és szöveg
- kezdetben az első szalagon van az input, a többi üres
- egy lépéses konf. átmenet
    - Minden szalagra megtörténik az adott szabálynak megfelelő lépés
    - Nem kell ugyan abba az irányba mozduljanak a fejek
- ami több szalagosan megy az egy szalagossal is
    - egy szalagra felvesszük az összes tartalmat egymás után elválasztó karakterrel
    - külön szimbólummal jelöli h hol lenne a többi fej
    - oda vissza mászkál és csinálja
    - O(n + f(n)) egy több szalagos egy lépésének szimulálása

## Nemdeterminisztikus Touring gép (NTG)
- P(X) = {Y|Y⊆X}
- Minden ugyan az kivéve az átmenetek
- egy állapothoz valahány állapotot rendelünk
    - ilyenkor választani kell majd
- Nemdeterminisztikus számítási fa
- Eldönti, ha a számítási fa véges és minden levele elfogadó vagy elutasító
- f(n) időkorlátos, ha n hosszú szóta f(n) magas max a fa

# EA 6 2021.10.13

## Lexikografikus rendezés
- szavak rendezése

## Nemdeterminisztikus TG
- szimulálható determinisztikus TG-vel
- exponenciális teljesítmény romlással
- számítás szelectora
    - gyökér - üres szó
    - a lehetséges lépések közül sorszám minden szinten
- (input, számolás, szelektorok)
- másolgatás a szalagokon
- megszámlálhatóan végtelen, continum végtelen szó van
- túl sok halmaz
- 

# EA 7 2021.10.20

## RE és R
- RE nem zárt a komplementer-képzésre
- R zárt a komplementer-képzésre

## Számítási feladatok megoldása TG-pel
- Szófüggvények
- f : Σ* → Δ*

- **Def:** Az M=< Q, Σ, Δ, ...> TG kiszámolja az f : Σ* → Δ* szófüggvényt, ha minden u ∈ Σ* szóra megáll, és ekkor f(u) ∈ Δ* olvasható az utolsó szalagján

- **Def:** f szófüggvény kiszámítható ha van TG ami kiszámítja
- **Def:** L₁ visszavezethető L₂-re, ha van olyan f kiszámítható szófgv., hogy w∈L₁ ⇔ ...

- Ha L₁ ≤ L₂ és L₂ ∈ RE, akkor L₁ ∈ RE
- Ha L₁ ≤ L₂ és L₂ ∈ R, akkor L₁ ∈ R

- M visszavezető gép, M₂ felismeri L₂
- Ezekből építünk M₁-et ami felismeri L₁-et

- Ha L₁ ≤ L₂ és L₂ ∉ RE, akkor L₁ ∉ RE
- Ha L₁ ≤ L₂ és L₂ ∉ R, akkor L₁ ∉ R

## Turing gépek megállási problémája
- Megáll-e valaha az inputon
- Lₕ ~ Lₕₐₗₜ = {< M, w > | M megáll w bemeneten}
- Lᵤ ⊆ Lₕ

- **Tét:** Lₕ ∉ R
- **Tét:** Lₕ ∈ RE

## Rice tétel
- **Def:** P⊆RE halmaz a rekurzívan felsorolható nyelvek egy **tulajdonságának** nevezzük.
    - P triviális, ha P=∅ vagy P=RE
    - L_P = {< M > | L(M) ∈ P}
- **Rice tétele:** Ha P⊆RE egy nem triviális tulajdonság, akkor L_P ∉ R
- Bizonyítás:
    1. eset ∅ ∉ P
        - tudjuk hogy Lᵤ ∉ R, elég belátni h Lᵤ ≤ L_P
        - L ∈ P (L ≠ ∅)
        - L∈RE M_L TG, L(M_L) = L
        - < M, w > TG hez készítünk M'
            1. Szimulálja M-et w-re
            2. M nem áll meg akkor M' sem
            3. Ha megáll akkor elemzi az x szót
            4. ...
        - < M, w > ∈ Lᵤ ⇔ < M'> ∈ L_P
    2. eset
        - P komplementer = RE/P
        - L_(P komplementer) = (L_P komplementer)
        - L_(P komplementer) ∉ R
        - ezért (L_P komplementer) ∉ R
        - így L_P ∉ R

- M TG-ről eldönthetetlen, hogy 
    - csak az üres nyelvet ismeri fel
    - véges nyelvet ismer-e fel
    - környezetfüggetlen nyelvet ismer-e fel
    - elfogadja-e az üres szót
    - stb

## Post Megfeledkezési Probléma
- **Def:** Σ egy ábécé, u_1..u_n, v_1..v_n ∈ Σ⁺ (n ≥ 1)
- A D={u_1/v_1,..,u_n/v_n} halmazt **dominókészletnek** nevezzük.
- Egy dominósorozat megoldása egy készletnek, ha alul és felül ugyan az a szó van
- Megoldások véges hosszú sorozatok
- pl: (a/ab),(bc/ca),(aa/a) egy megoldás

- **Tét:** L_PMP ∈ RE
- **Tét:** L_PMP ∉ R
- Biz:
    - PMP = { < D > | D-nek van megoldása}
    - MPMP = {< D,d > | D-nek van d-vel kezdődő megoldása}
    - L_MPMP ≤ L_PMP
    - balcsillag(u): * x * x * x
    - jobbcsillag(h): x * x * x *
    - baljobbcsillag(h): * x * x * x *
    - dominók felső szavát balcsillag, alsót jobbcsillag
    - az első dominó: balcsillag/baljobbcsillag
    - utolsó dominó: *#/#
    - Ezekkel létrehozzuk a D'-t
    - < D,d_₁ > ∈ L_MPMP ⇔ < D'> ∈ L_PMP
    
## Környezetfüggetlen
- L_ECF = {< G > | G egyértelmű CF grammatika}
- P_A = {A->u₁Aa₁,..,A->uₙAaₙ,A->ε}
- P_B hasonlóan, u helyett v
- G_A = < A, {A}, Σ∪Δ, P_A>, G_B hasonlóan
- G_D = < S, {S,A,B}, Σ∪Δ, {S->A, S->B}∪P_A∪P_B>
- f: < D > -> < G_D > visszavezetés

- L(G_A) komplementer környezetfüggetlen, G_B-re is

- nem értem miről van szó

# EA 8 2021.11.03

## PMP
- Turing eldönthető
- Az igen példányoakat megadja
- Dominókból ki lehet rakni dolgokat

## Környezetfüggetlen grammatika egyértelműsége nem eldönthető
## Két környezetfüggetlen g. által generált nyelv metszete nem eldönthető
1. L(G1) ∩ L(G2) ≟ ∅
2. L(G1) ≟ L(G2)
3. L(G1) ≟ γ*  ,  γ ábécé
4. L(G1) ⊆? L(G2)
 
## Eldönthető problémák nulladrendű logikában
- Eldönthető
    - ϕ formula kielégíthető
    - ... kielégíthetetlen
    - ... tautológia
    - két formula tautologikusan ekvivalens
    - F ⊧₀ ϕ 
- Brute force módszer nem hatékony, mert n változó esetén 2ⁿ eset van

## Eldönthetetlen problémák elsőrendű logikában
- ValidityPred  := {< ϕ > | ϕ logikailag igaz elsőrendű formula} ∉ R
- UnsatPred     := {< ϕ > | ϕ kielégíthetetlen elsőrendű formula} ∈ RE -- felismerhető
- SatPred       := {< ϕ > | ϕ kielégíthető elsőrendű formula} ∉ R
- EqivPred      := {< ϕ,ν > | ϕ,ν elsőrendű formula ekvivalens} ∉ R
- ConsPred      := {< F,ϕ > | F halmazból következik ϕ elsőrendű formula} ∉ R

## 𝕃₀ és RE kapcsolata
**Tét.:** Minden G grammatikához megadható egy L(G)-t felismerő NTG.
- 3 szalag
    - első a TG bemenete
    - második a grammatika szabályai
    - jelek csak olvasva
    - harmadikon α mondatforma
- Nem determinisztikusan választ egy szabályt meg egy helyet, ha alkalmazható a szabály, akkor alkalmazza
- Ha az első és harmadik szalag megegyezik, akkor megáll

**Tét.:** Minden M NTG-hez megadható egy L(M)-t generáló G grammatika.
- Legyen G = < (Γ/Σ)∪Q∪{S,A,▹,◃}, Σ, P, S >
- P szabályok
    1. S -> ▹AqᵢA◃
    2. A -> aA | ɛ
    3. bq' -> qa, ha δ(q,a)=(q',b,R)
    4. q'b -> qa, ha δ(q,a)=(q',b,S)
    5. q'cb -> cqa, ha δ(q,a)=(q',b,L)
    6. ⎵◃->◃, ◃->ɛ, ▹⎵->▹, ▹q0->ɛ

## 𝕃₁ és R kapcsolata
- Lineárisan korlátolt automata (LKA)
- Van kezdő és vég szimbólum: ▹,◃
    - Csak közötte állhat a fej
    - Nem módosítható
    - Közöttük van a szó
**Tét.:**  
1. Minden G 1-es gramm. meg lehet adni A LKA-t melyre L(A)=L(G) 
2. Minden A LKA-hoz meg lehet adni G 1-es gramm. melyre L(G)=L(A)
- Szabályok nem kellenek a szalagra, mert a gépbe lehet építeni
- Lineáris korlátoltság miatt nem kell ⎵
**Tét.:** A LKA, akkor L(A) eldönthető.

## 𝕃₃ ⊂ 𝕃₂ ⊂ 𝕃₁ ⊂ R ⊂ 𝕃₀ = RE
- 𝕃₃ - VDA
- 𝕃₂ - Veremautomata
- 𝕃₁ - LKA
- R  - Minden inputra megálló TG
- 𝕃₀ = RE - Nem determinisztikus TG


# EA 9 2021.11.10

## Időbonyolultság osztályok, P ≟ NP
- TIME(f(n)) = 
    {L|L eldönthető O(f(n)) időkorlátos det. TG-pen}
- NTIME(f(n)) =
    {L|L eldönthető O(f(n)) időkorlátos NTG-pen}
- P=⋃_k≥1 TIME(nᵏ)
- NP=⋃_k≥1 NTIME(nᵏ)
- Korábbi tétel alapján:
    - NTIME(f(n)) ⊆ TIME(2^(O(f(n))))
- Észtevétel:
    - P ⊆ NP, mert TG lehet speciális NTG
- Sejtés:
    - P ≠ NP, de nem bizonyított

## Polinom idejű visszavezetés
- f : Σ* -> Δ* szófgv. **polinom időben kiszámítható**, ha van polinom időkorlátos TG ami kiszámítja.
- L₁ ⊆ Σ* **polinom időben visszavezethető** L₂ ⊆ Δ*-ra, ha van olyan f polinom időben kiszámítható szófgv., hogy
    w ∈ L₁ ⇔ f(w)∈L₂. Jelölés: L₁ ⩽ₚ L₂
- Ha L₁ polinom időben visszavezethető L₂-re
    - L₂ ∈ P 
        - Akkor L₁ is P beli lesz
    - L₂ ∈ NP
        - Akkor L₁ is NP beli lesz

## C-teljesség
- L nyelv C-nehéz (polinom idejű visszavezetésre nézve), ha minden L' ∈ C esetén L'⩽ₚ L.
- L C-teljes ha L ∈ C és C-nehéz.

## NP-Teljes
- NP-teljes
    - L ∈ NP
    - L NP-nehéz
- NP-beli problémák legnehezebbjei
- Nem találtunk NP teljes problémát, ami P beli is lenne

### Cook-Levin tétel
- SAT ∈ NP és NP-nehéz -> NP-teljes

# EA 10 2021.11.17

## Polinom idejű visszavezetés tranzitív
- L_1 ⫹ₚ L_2, L_2 ⫹ₚ L_3 ⇒ L_1 ⫹ₚ L_3

## NP teljes nyelvre visszavezethető NP beli nyelvek NP teljesek is

## kSAT
- KNF : konjunktív normálformájú nulladrenű formula
- SAT = {<ϕ> | ϕ kielégíthető   KNF }
- kKNF : olyan KNF, ahol minden klóz pontosan k darab különböző alapú literál disjunkciója
- kSAT = {<ϕ> | ϕ kielégíthető kKNF }

### 3SAT NP-teljes
- SAT NP-teljes
- 3SAT-á alakítható az általános SAT
- Visszavezethető

### 2SAT ∈ P
### HORNSAT ∈ P
- Horn formula : olyan KNF, amelynek minden tagja egy pozitív literált tartalmaz.
- HORNSAT = {<ϕ> | ϕ kielégíthető Horn formula }

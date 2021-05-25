# Formális nyelvek és fordítóprogramok

## Előadók
----------
- Nagy Sára saci@inf.elte.hu

## 1. Előadás
-------------

### Alapfogalmak és jelölések

**Ábécé:**  
- Ábécének nevezzük a jelek egy nem üres véges halmazát. 
- Jele: V

**Betű:**
- Az ábécé elemeit betűknek hívjuk. (a ∈ V )

**Szó:**
- A V ábécé elemeinek egy tetszőleges véges sorozatát a V ábécé feletti szónak nevezzük. (Ha V nem lényeges vagy egyértelmű, akkor szóról beszélünk.)
- Ha u egy tetszőleges szó, akkor **ℓ(u)** jelöli a szó hosszát. 
- 0 ≤ ℓ(u) < ∞ ; ℓ(ε) = 0, ahol **ε** az üres szó
- A V ábécé feletti szavak halmazát **V\***-gal jelöljük.
- A nem üres szavakét **V+**-szal.

**Nyelv:**
- V* valamely részhalmazát a V ábécé feletti nyelvnek nevezzük. 
- Jele: L 
- L ⊆ V* 

**Nyelvosztály (nyelvcsalád):**
- Nyelvek valamely összességét nyelvosztálynak hívjuk.

### Műveletek szavakon

**Konkatenáció**
- Legyenek u = t₁...tₖ és v = q₁...qₘ szavak egy V* felett értelmezve.
- Ekkor a két szó konkatenáltja az  
uv := t₁...tₖq₁...qₘ  
(A két szó egymás utáni leírásával kapott szó.)

- V* zárt a konkatenációra
- V* a konkatenációra egységelemes félcsoportot alkot.
- **Asszociatív:** u,v,w ∈ V* : (uv)w = u(vw)
- **Egységelemes:** ɛ és v ∈ V* : ɛv = v = vɛ

**Hatványozás**
- Legyen u egy tetszőleges szó. 
- Nemnegatív egész hatványai:  
u⁰ := ε  
u¹ := u  
uⁿ := uⁿ⁻¹u , ahol n≥1

**Megfordítás**
- Ha u egy tetszőleges szó és u = t₁...tₖ és v = tₖ...t₁, akkor v az u fordítottja, másképpen mondva a tükörképe.
- Jelölése: u⁻¹ = v

### További alapfogalmak

- **Részszó:** A v u-nak részszava, ha léteznek olyan w₁;w₂ szavak, hogy u = w₁vw₂.
- **Szó prefixe:** A v az u szó prefixe,ha van olyan w szó, hogy u = vw.   
Valódi prefix, ha v ≠ ε és v ≠ u.
- **Szó suffixe:** A v az u szó suffixe,ha van olyan w szó, hogy u = wv.   
Valódi suffix, ha v ≠ ε és v ≠ u.

### Műveletek nyelveken

**Unió**
- Legyenek L₁ és L₂ nyelvek V* felettiek.   
Ekkor az L₁ és L₂ nyelvek unióján az 
L₁ U L₂ := {u ∈ V* | u ∈ L₁ vagy u ∈ L₂ } nyelvet értjük.

- Az unió kommutatív, asszociatív és egységelemes művelet. Az egységelem az üres nyelv (üres halmaz).
- Jele: Ø
- Ø U L = L = L U Ø

**Két nyelv metszete**
- Legyenek L₁ és L₂ nyelvek V* felettiek. 
- Ekkor az L₁ és L₂ nyelvek metszetén az 
L₁ ∩ L₂ := {u ∈ V* | u ∈ L1 és u ∈ L2
} nyelvet értjük.

**Komplementer**

- Az L ⊆ V* nyelv komplementere a V ábécére vonatkozóan: L̅ := V* \ L, azaz minden olyan szó, ami nem tartozik az L nyelvbe. 
- L̅ ∩ L = Ø és L̅ U L = V*

**Tükörkép**
- Az L ⊆ V* nyelv tükörképe az a nyelv, amely a szavainak megfordítottját tartalmazza.
- Jele: L⁻¹
- L⁻¹ := {u ∈ V* | u⁻¹ ∈ L}
- Példa:  
L = {abc, aabb, acaa, baab}  
L⁻¹ = {cba, aaca, baab, bbaa}

**Konkatenáció**
- Legyenek L₁ és L₂ nyelvek.
- Ekkor az L₁ és L₂ nyelvek konkatenációján az L₁L₂ := {uv | u ∈ L₁ és v ∈ L₂ } nyelvet értjük.
- A nyelvek halmaza a konkatenációra nézve egység elemes félcsoport alkot.
- Egység elem: {ε} (az üres szót tartalmazó nyelv)
- {ε}L = L = L{ε}
- ∅L = ∅ = L∅

**Hatványozás**
- Legyen L egy tetszőleges nyelv.
- Nemnegatív egész hatványai:  
L⁰ := {ε}  
L¹ := L  
Lⁿ := Lⁿ⁻¹L , ahol n≥1.

**Lezártja (iteráltja)**
- Legyen L egy tetszőleges nyelv. 
- L* := L⁰ U L¹ U L² U … az L nyelv lezártja.  
Másképpen:  
L* := ⋃ⱼ≥₀ Lʲ valamint L+ := ⋃ⱼ≥₁ Lʲ

### Reguláris műveletek:
- unió
- konkatenáció
- lezárás

### Nyelvek megadási módjai
- logikai formula
- struktúrális rekurzió
- algoritmus
- matematikai gépek
- produkciós rendszerek


## 2. Előadás
-------------

### Nyelv megadásának szabályrendszere

***Def.:*** Grammatikának (nyelvtannak) a következő négyest nevezzük:  
**G = (N,T,P,S)**
- **N** a nemterminális ábácé,
- **T** a terminálisok ábécéje,
- **P** az átírási szabályok véges halmaza,
- **S** a kezdőszimbólum.  
- N és T diszjunkt halmazok, azaz N ⋂ T = ∅.
- S Є N, kezdőszimbólum.
- A szabályok p → q alakúak, ahol p ∈ (N∪T)* N (N∪T)* , q ∈ (N∪T)* és p jelöli a szabály baloldalát, q a jobboldalát,  
→ a két oldalt elválasztó jel.
- A szabályok baloldala kötelezően tartalmaz legalább egy 
nemterminális szimbólumot.
- (N∪T)* elemeit _mondatformáknak_ nevezzük.

### Grammatika által generált nyelv
- Minden olyan szó, amely közvetetten levezethető a kezdőszimbólumból.  
- L(G) := { u ∈ T* | S ⇒ᴳ* u }

### Közvetlen levezetés
- Legyen G = (N, T, P, S) egy adott grammatika.  
- Legyen u, v ∈ (N ∪ T)* .  
- Azt mondjuk, hogy a v mondatforma közvetlenül levezethető az u mondatformából, ha létezik u₁ , u₂ ∈ (N ∪ T)* és x → y ∈ P úgy, hogy u = u₁xu₂ és v = u₁yu₂.
- Jelölése: u ⇒ᴳ v

### Közvetett levezetés
- Legyen G = (N, T, P, S) egy adott grammatika.
- Legyen u, v ∈ (N ∪ T)* .
- Azt mondjuk, hogy a v mondatforma közvetetten levezethető az u mondatformából, ha létezik olyan k ≥ 0 szám és x₀,…,xₖ ∈ (N ∪ T)* , hogy u = x₀ és v = xₖ és ∀ i ∈ [0,k-1]: xᵢ ⇒ᴳ xᵢ₊₁ .  
- Jelölése: u ⇒ᴳ* v

### Ekvivalencia
- A G1 es G2 nyelvtanok ekvivalensek, ha 
L(G1) = L(G2), azaz ugyanazt a nyelvet generálják.  
- Gyengén ekvivalensek, ha L(G1)\{ε}= L(G2)\{ε}.

### Chomsky féle grammatika típusok
***Def.:*** A G =(N,T,P,S) grammatika i-típusú (i = 0,1,2,3), ha P szabályhalmazára teljesülnek a következők:
- **i = 0:** Nincs korlátozás.
- **i = 1:** P minden szabálya u₁Au₂ → u₁vu₂ alakú, ahol u₁,u₂,v ∈ (N∪T)* , A ∈ N, és v ≠ ε, kivéve az S → ε alakú szabályt, de ekkor S nem fordul elő egyetlen szabály jobboldalán sem  
(Ezt "Korlátozott ε szabály”-nak, röviden: KES szabálynak hívjuk.)
- **i = 2:** P minden szabálya A → v alakú, ahol A ∈ N, v ∈ (N∪T)* .
- **i = 3:** P minden szabálya vagy A → uB vagy A → u alakú, ahol A,B ∈ N és u ∈ T* .

### Chomsky féle grammatika típusok
- Jelölje 𝔾ᵢ az i-típusú grammatikák halmazát.  
- A grammatikák alakjából következik, hogy  
𝔾ᵢ ⊆ 𝔾₀ , ahol i=1,2,3.  
𝔾₃ ⊆ 𝔾₂ 

### Nyelvek típusai
- Egy L nyelvet i-típusúnak nevezünk (i ∈{0,1,2,3}), ha létezik olyan i-típusú grammatika, ami az L nyelvet generálja.
- Jelölje 𝕃ᵢ az i-típusú nyelvek halmazát. 
(Nyelvcsalád.)

### Chomsky féle hierarchia
- 𝕃₃ ⊆ 𝕃₂ ⊆ 𝕃₁ ⊆ 𝕃₀   
#### Pontosabban valódi tartalmazás van
- 𝕃₃ ⊂ 𝕃₂ ⊂ 𝕃₁ ⊂ 𝕃₀
#### Grammatikákra
- 𝔾₃ ⊆ 𝔾₂ ⊈ 𝔾₁ ⊆ 𝔾₀  
A 2-es szabályban v≠ɛ nincs kikötve, az 1-esben pedig igen.


## 3. Előadás
-------------

### Nyelvtani transzformáció
- Eljárás, ami G grammatikából G' grammatikát készít.
- **Ekvivalens** transzformáció, ha **L(G)=L(G')**.

### ε-mentesítés
**Tétel:** Minden 2-es grammatikához megkonstruálható egy vele ekvivalens, amiben nincs epszilon szabály.
- G=(N,T,P,S) ---> G'=(N',T',P',S')
- (A → ɛ) ∉ P'
- kivéve ha ɛ ∈ L(G)  
ekkor (S' → ɛ) ∈ P', de S' nem szerepelhet szabály jobb oldalán.

#### Lépések:
1. Meghatározzuk, hogy mely nemterminálisokból vezethető le az üres szó.
    - H:={ A ∈ N | A ⇒ᴳ* ε}
    - Ehhez definiáljuk a Hᵢ(i≥1) halmazokat:
        - H₁ := { A ∈ N | ∃A→ε ∈ P}
        - Hᵢ₊₁ := Hᵢ U { A ∈ N | ∃A→w ∈ P és w ∈ Hᵢ*}
        - H₁ ⊆ H₂ ⊆ … ⊆ Hₖ = Hₖ₊₁ ∃k és legyen H:= Hₖ
    - ɛ ∈ L(G) ⇔ S ∈ H
2. Átalakítjuk a grammatika szabályait.
    - A → v' ∈ P'   ⇔   v'≠ɛ és ∃A → v ∈ P
    - v-ből nulla vagy több H-beli nemterminális elhagyásával kapjuk v'-t.
    - Ha **S ∈ H**
        - Hozzáveszünk még két szabályt.
        - S' → ɛ
        - S' → S
        - S' ∉ N és S' a G' új kezdőszimbóluma
    - Az átalakítás megőrzi a 2. és 3. típust.

### Nyelvosztályok zártsága a reguláris műveletekre
**Tétel:** Az 𝕃ᵢ, i = 0, 1, 2, 3 nyelvosztályok mindegyike zárt a reguláris műveletekre nézve. 

### Nyelvosztály zártsága nyelvi műveletre
- Legyen ϕ n-változós nyelvi művelet, azaz ha L₁,…,Lₙ nyelvek, akkor ϕ(L₁,…,Lₙ) is nyelv.  
- Az 𝕃 nyelvcsalád zárt a ϕ műveletre nézve, ha L₁,…,Lₙ ∈ L estén ϕ(L₁,…,Lₙ) ∈ L.

#### Unió
G=(N,T,P,S) legyen az L nyelvhez tartozó grammatika és G’=(N’,T,P’,S’) legyen az L’ nyelvhez tartozó grammatika és N ∩ N’ = Ø és G, G’ azonos típusúak.  

**i=0,2,3** esetén, legyen S₀ új szimbólum, azaz S₀ ∈ (N ∪ N’).  
Gᵤ = (N ∪ N’ ∪ {S₀},T, P ∪ P’ ∪ {S₀→S, S₀→S’}, S₀).  
Látható, hogy Gᵤ típusa megegyezik G,G’ típusával, 
és L(G) ∪ L(G’) = L(Gᵤ)

**i=1** esetén, ha ɛ ∈ (L ∪ L'), akkor nem teljesül a KES.  
Ezért tekintsük az L1 = L \ {ε} és L2 = L’ \ {ε} nyelveket, amelyeket G1 és G2 1-es típusú grammatikák generálnak. 
Készítsük el Gᵤ–t az előbbi módon, majd vezessünk be egy S₁ új kezdőszimbólumot és adjuk a szabályhalmazhoz az S₁→ε és S₁→S₀ szabályokat.

#### Konkatenáció
_(Megjegyzés: Most csak a 3-as típusra bizonyítjuk.)_  
Legyen i = 3.  
A P szabályhalmazból megkonstruálunk egy P1 szabályhalmazt úgy, hogy minden A → u alakú szabályt felcserélünk egy A → uS′ alakú szabályra, a többi szabályt változatlanul hagyjuk.  
A Gc = (N ∪ N′, T, P1 ∪ P′, S) grammatika 3-as típusú és generálja az L(G)L(G′) nyelvet.

#### Lezárás
_(Megjegyzés: Most csak a 3-as típusra bizonyítjuk.)_  
Legyen i = 3.  
Legyen S0 új szimbólum, azaz S0 ∈ N.
Definiáljuk a P1 szabályhalmazt úgy, hogy minden A → u alakú szabályt felcserélünk egy A → uS0 alakú szabályra és ezek legyenek a P1 elemei.  
G∗ = (N ∪ {S0}, T, P1 ∪ P ∪ {S0 → ε, S0 → S}, S0) grammatika generálja az L* nyelvet.

### A 3-as nyelvcsalád nyelveit leírhatjuk
- 3-as típusú grammatikával,
- reguláris kifejezéssel,
- véges determinisztikus automatával,
- véges nemdeterminisztikus automatával.

Bizonyítható, hogy  
- 𝕃₃ = 𝕃_(reg) = 𝕃_(VDA) =𝕃_(VNDA).  

_Megjegyzés: A programozási nyelvek lexikális egységei a 3-as nyelvcsaládba tartoznak._

### Reguláris nyelvek (rekurzív definíció)
- az elemi nyelvek: Ø, {ε}, {a} , ahol a ∈ U, 
azaz egy tetszőleges betű
- azon nyelvek, melyek az elemi nyelvekből 
az unió, a konkatenació és a lezárás 
műveletek véges számú alkalmazásával 
állnak elő;
- nincs más reguláris nyelv

### Reguláris nyelvek 
**Tétel:** Minden L reguláris nyelvhez megadható egy G 3-as típusú grammatika,amelyre L=L(G). (𝕃_(reg) ∈ 𝕃₃)
**Bizonyítás:**
Elemi nyelvekhez adható 3-as típusú grammatika.
- G=( {S}, {a}, {S→aS}, S)   L(G)=Ø
- G=( {S}, {a}, {S→ε}, S)    L(G)={ε}
- G=( {S}, {a}, {S→a}, S)    L(G)={a}

Az 𝕃₃ nyelvcsalád zárt a reguláris műveletekre, így az elemi nyelvek grammatikáiból kiindulva reguláris műveletekkel megkonstruálható bármilyen 3-as grammatika.

### Reguláris kifejezések:
**Definició:**
- az elemi regularis kifejezesek: Ø, ε, a , ahol a ∈ U
- ha R1 es R2 és R regularis kifejezesek akkor 
    - (R1 | R2);
    - (R1R2);
    - (R)* is reguláris kifejezések.
- a reguláris kifejezések halmaza a legszűkebb halmaz, 
melyre a fenti két pont teljesül.

Jelölje L_R az R reguláris kifejezéshez tartozó nyelvet.  
- L_Ø = Ø, L_ε = {ε}, L_a = {a}

Ha Q és R reguláris kifejezések, akkor
- L(Q|R) = L_Q ∪ L_R unió
- L(QR) = L_QL_R konkatenáció
- L(R)* = (L_R)* lezárás

A műveletek prioritási sorrendje növekvően:  
- unió, konkatenáció, lezárás.  

A zárójelek elhagyhatók a reguláris kifejezésekből a 
prioritásoknak megfelelően.

### 3-típusú grammatikák normál formája
**Tétel:** Minden 3-as típusú, nyelv generálható egy olyan grammatikával, amelynek szabályai
- **A → aB**, ahol A, B ∈ N és a ∈ T vagy
- **A → ε** alakúak, ahol A ∈ N.

_Megjegyzés: A 3-as normál forma alakítható majd át könnyen automatává._

### 3-as típusú grammatikák normálformára hozása 
Legyen G=(N,T,P,S) 3-as típusú grammatika.
Megkonstruálunk egy G’=(N’,T,P’,S) 3-as normál formájú grammatika, melyre L(G)=L(G’).

**Lépesei:**
1. hosszredukció
2. befejező szabályok átalakítása
3. láncmentesítés

#### Hosszredukció
Elhagyjuk az **A→a₁…aₖB** alakú szabályokat, ahol k≥2 és ∀i ∈ [1,k]: aᵢ ∈ T és A ∈ N, B ∈ N vagy B=ε.
Helyettesítjük a következő szabályokkal:
- **A →a₁Z₁** ,ahol Z₁∉N, azaz új nemterminális,
- **Z₁ →a₂Z₂** ,ahol Z₂∉(N ∪ Z₁)
- **…**
- **Zₖ₋₁ →aₖB**

_Megjegyzés: Minden szabályra új nemterminálisokat vezetünk be._

#### Befejező szabályok átalakítása
Elhagyjuk az **A→a** alakú szabályokat, ahol a∈T és A∈N.  
Legyen E egy új nemterminális. 
_(Ez lehet közös minden befejező szabály esetén.)_  
Vegyük fel P’-be az **A→aE** és a **E→ε** szabályokat az előbbiek helyett.

_Megjegyzés: A 3-as normál forma alakítható majd át könnyen automatává._

#### Láncmentesítés
Elhagyjuk az **A → B** alakú szabályokat P-ből, ahol A, B ∈ N.
Első lépésben meghatározzuk minden A ∈ N esetén a
- H(A):={ B ∈ N | A ⇒ᴳ* B} halmazokat.

Ehhez definiáljuk a Hᵢ (i≥1) halmazokat:
- H₁(A)={ A }
- Hᵢ₊₁(A)=Hᵢ(A) ∪ { B ∈ N | ∃C ∈ Hᵢ(A) és C→B ∈ P}
- H₁(A) ⊆ H₂(A) ⊆ … ⊆ Hₖ(A)= Hₖ₊₁(A) ∃k és legyen H(A):= Hₖ(A).

Ezután P’-be felvesszük az **A → X** szabályokat, ha ∃B ∈ H(A) és B → X ∈ P, ahol X∈(T U N)* és X nem csak egyetlen nemterminális.

### Véges determinisztikus automata (VDA)
**Definíció:** A = (Q, T, δ, q0, F) rendezett ötöst véges determinisztikus automatának nevezzük, ahol
- Q az állapotok nem üres véges halmaza,
- T az input szimbólumok ábécéje,
- δ: Q × T → Q leképezés az állapot-átmeneti függvény,
- q0 ∈ Q a kezdőállapot,
- F ⊆ Q elfogadóállapotok halmaza.

Véges determinisztikus automata estén a δ: Q × T → Q állapot-átmeneti függvény ∀(q,a) párra értelmezett, ahol (q,a) ∈ Q × T és egyetlen olyan p ∈ Q állapot van, amelyre δ(q,a) = p.

## 4. Előadás
-------------

### Alternatív jelölés az állapot-átmenetre
- δ(q, a) = p állapot átmenet jelölhető egy
- qa → p    szabállyal is.

### Közvetlen redukció
Legyen A = (Q, T, δ, q0, F) egy véges determinisztikus automata és legyenek **u, v ∈ QT\*** .   
_(Konfiguráció: aktuális állapot, input hátralévő része.)_  
Azt mondjuk, hogy az A automata az u konfigurációt a v konfigurációra redukálja közvetlenül (jelölés: u ⇒_A v), ha van olyan qa → p szabály (azaz δ(q, a) = p) és van olyan w ∈ T* szó, amelyre u = qaw és v = pw teljesül.

### Redukció
**Definíció:** Az A = (Q, T, δ, q0, F) véges automata az u ∈ QT* konfigurációt a v ∈ QT* konfigurációra redukálja (jelölés: u ⇒_A* v), ha vagy u = v, vagy van olyan z ∈ QT*, amelyre u ⇒_A* z és z ⇒_A v teljesül.

### Automata által elfogadott nyelv
**Definíció:** Az A = (Q, T, δ, q0, F) véges automata által elfogadott nyelv alatt az L(A) := {u ∈ T*| ∃q0u ⇒_A* p és p ∈ F} szavak halmazát értjük.

_Megjegyzés: Ez azt jelenti, hogy van olyan működése az automatának, hogy a **kezdőállapotból** indulva végig olvasva az inputot **elfogadóállapotba** jut._

### Véges nemdeterminisztikus automata (VNDA)
**Definíció:** A = (Q, T, δ, **Q0**, F) rendezett ötöst véges **nemdeterminisztikus** automatának nevezzük, ahol
- Q az állapotok nem üres véges halmaza,
- T az input szimbólumok ábécéje,
- δ: Q × T → **P(Q)** _(a Q részhalmazaiba képez)_
- Q0 ⊆ Q a kezdőállapotok halmaza,
- F ⊆ Q elfogadó állapotok halmaza.

_Megjegyzés: VNDA a VDA általánosítása_

### 3-as típusú nyelvek kapcsolata a véges automatákkal
**Tétel:** Minden 3-as típusú L nyelvhez megadható egy véges nemdeterminisztikus automata, és fordítva, minden nemdeterminisztikus automata 3-as típusú nyelvet ismer fel.
- (𝕃₃ ⊆ 𝕃_(VNDA) , 𝕃_(VNDA) ⊆ 𝕃₃)

_Megjegyzés: Már láttuk, hogy 𝕃\_(reg) ⊆ 𝕃₃, így a reguláris kifejezésekhez (lexikális egységekhez) építhető automata._

**Bizonyítás vázlat:**
- G grammatikából A nemdeterminisztikus autómata.
    - Az input szimbólumok ábécéje a terminálisok.
    - Rendelünk minden nemterminálishoz egy állapotot.
        - q_A ⟺ A ∈ N
    - A kezdőállapot megegyezik a kezdő nemterminálishoz rendelt állapottal.
    - Állapot-átmemeteketek a levezetési szabályok alapján.
        - δ(q_A,a)=q_B ⟺ A → aB ∈ P
        - q_A ∈ F ⟺ A → ɛ ∈ P
    - Ha **S ⇒\* u** (G szerint), akkor **q_S ⇒\* u** (A szerint)
- Autómatából grammatikát hasonló eljárásokkal kapunk.

#### Nemdeterminisztikus automaták determinisztikussá tétele
**Tétel:** Minden A=(Q,T,δ,Q0,F) nemdeterminisztikus automatához megadható egy A’=(Q’,T,δ’,q0’,F’) véges determinisztikus automata, hogy L(A’)=L(A).
(𝕃_(VNDA) ⊆ 𝕃_(VDA))

#### Determinisztikus automata megkonstruálása:
- Legyen Q’:= P(Q) ,azaz Q összes részhalmazainak halmaza, azaz hatványhalmaza.  
- Legyen a δ’: Q’ × T → Q’ a következőképpen definiálva:
    - δ’(q’,a):= ⋃_(q∈q') δ(q,a), ahol q’∈Q’ és a∈T.
    - Állapotok helyett halmazok.
    - pl.: {A,B}a → {C,D} // Aa→C, Ba→D ∈ δ
- Legyen q0’:=Q0 és F’:={q’ ∈ Q’|q’ ∩ F≠∅}.

### Kleene tétele
**Tétel:** 𝕃₃ = 𝕃_(reg)  
Minden reguláris nyelvhez adható 3-as típusú grammatika, és fordítva minden 3-as típusú nyelv felépíthető az elemi reguláris nyelvekből a reguláris műveletek véges sokszori alkalmazásával.

**Bizonyítás vázlat:**
1. 𝕃_(reg) ⊆ 𝕃₃
2. 𝕃₃ = 𝕃_(VDA)
3. 𝕃_(VDA) ⊆ 𝕃_(reg)

## 5. Előadás
-------------

### Minimális véges determinisztikus automata
**Definíció:** Az A véges determinisztikus automata minimális, ha nincs olyan A′ véges determinisztikus automata, amely ugyanazt a nyelvet ismeri fel, mint A, de A′ állapotainak száma kisebb, mint A állapotainak száma.

**Tétel:** Az L reguláris nyelvet felismerő minimális véges determinisztikus automata az izomorfizmus erejéig egyértelmű.

**Tétel:** Az L reguláris nyelvet felismerő minimális véges determinisztikus automata (VDA) az izomorfizmus erejéig egyértelmű.  
**Bizonyítás lépései:**
1. Automata összefüggővé tétele
2. Ekvivalens állapotok meghatározása

#### Összefüggő véges determinisztikus automata

**Definíció:** Az A = (Q, T, δ, q0, F) véges determinisztikus automata q állapotát **elérhetőnek** mondjuk, ha ∃u∈T* szó, hogy q0u ⇒* q.
(Gráfos ábrázolásban ez azt jelenti, hogy van irányított út q0-ból q-ba.)

**Definíció:** Az A = (Q, T, δ, q0, F) véges determinisztikus automatát **összefüggőnek** mondjuk, ha minden állapota elérhető a kezdőállapotból.

Elérhető állapotok meghatározása:
- H halmaz tartalmazza az elérhető állapotokat.
    - Legyen H0={q0},
    - Hᵢ₊₁=Hᵢ ∪ {r∈Q | δ(q,a)=r, q∈Hᵢ, a∈T} és i≥0.
    - ∃k≥0 : Hₖ = Hₘ , ahol m≥k. Legyen H=Hk.
- A’ legyen az A azon részautomatája, ahol Q’=H.
- (A Q\H nemelérhető állapotok elhagyhatók.)

#### Ekvivalens állapotok meghatározása
**Definíció:** q ~ p (q és r ekvivalens állapotok), ha ∀ u∈T* szóra igaz, hogy qu ⇒* r és pu ⇒* r’ esetén r∈F akkor és csak akkor, ha r’∈F.
- (Minden szóra igaz, hogy az automatát q-ból indítva vagy p-ből indítva, vagy mind kettő esetben elfogadja a szót, vagy mind kettő esetben elutasítja.)

**Állítás:** Ha q és p ekvivalens, akkor qa→s és pa→t
esetén s és t is ekvivalens állapotok ∀ a ∈ T betűre.

**Definíció:** q ~𝒊 p (q és r i-ekvivalens állapotok), ha ∀ u∈T* szóra,ahol l(u)≤ i igaz, hogy qu ⇒* r és pu ⇒* r’ esetén r∈F akkor és csak akkor, ha r’∈F.
- (Legfeljebb i hosszú szavak esetén a két állapot nem megkülönböztethető.)

**Lemma:** q ~𝒊+1 p akkor és csak akkor, ha ∀a ∈ T-re qa→r és pa→t esetén r ~𝒊 t.

**Lépések:**
- Tegyük fel, hogy az A automata **összefüggő**.
0. q ~0 p ⇔ q,p ∈ F ∨ q,p ∈ Q\F
    - Első lépésben szétválasztjuk az elsfogadó és nem elfogadó állapotokat.
    - Q = B₁ ∪ B₂, B₁=F, B₂=Q\F
1. q ~i p ⇔ ∀a∈T : qa→r ∧ pa→t : r,t ∈ Bᵢ
    - A szavak hossza szerint finomítjuk a partíciókat.
    - q és p akkor marad együtt, ha minden inputra ugyanabba az állapothalmazba/partícióba mennek át, különben szét kell bontani.
    - Ha az előző lépés szerint mindig ugyanoda képeznek, akkor q ~(i+1) p.
    - Addig folytatjuk amíg van változás.

#### Minimális automata megadása
- A’ = (Q’, T, δ’, q0’, F’)
- Q’= {az előző eljárással nyert Bᵢ partíciók}
- q0’= a q0-t tartalmazó partíció.
- F’ =az F-ből keletkezett partíciók.
- δ’(Bᵢ,a)= Bⱼ, ha δ(q,a)=p és q ∈ Bᵢ és p ∈Bⱼ

### Szükséges feltétel 3-as típusú nyelvekre
**Tétel:** (Kis Bar-Hillel lemma) 
Minden L ∈ 𝕃₃ nyelvhez van olyan n≥1 nyelvfüggő konstans, hogy ∀u ∈ L , ahol l(u) ≥ n szó esetén van u-nak olyan u = xyz felbontása, amelyre 
- l(xy) ≤ n, 
- y≠ε, 
- ∀i ≥ 0 egész esetén x(y^i)z ∈ L.

**Bizonyítás vázlat:**
- L-hez adható minimális véges determinisztikus autómata.
- Ha az autómatának n állapota van és nézünk egy n hosszú szót akkor legalább egy állapotot kétszer kell érinteni.
- Gráfos ábrázolásnál ez azt jelenti, hogy teszünk egy kört.
- A kör során érintett szórészletet bárhányszor "bepumpálhatjuk" és L-beli szót kapunk.

### Nyelv maradéknyelvei
**Definíció:** Legyen L egy T ábácé felett értelmezett nyelv.  
Az L nyelv egy p∈T* szóra értelmezett maradéknyelve a következő:
- Lp :={ u∈T* | pu ∈ L}

### Myhill-Nerode tétel
**Tétel:** L ∈ 𝕃₃ akkor és csak akkor, ha az L-hez tartozó maradéknyelvek száma véges, azaz |{Lp|p ∈ T*}|<∞.

_Megjegyzés: A szavakon egy osztályozást végzünk az 
adott nyelvtől függően._

**Bizonyítás vázlat:**
1. Ha véges sok maradéknyelve van, akkor azokkal lehet VDA-t készíteni, amire L(A)=L.
Az autómata pedig átírható 3-as grammatikává.
2. Ha L 3-as, akkor van hozzá 3-as grammatika, amihez van autómata.
Az autómata állapotaihoz rendelhető egy-egy maradéknyelv.
Ezek között vannak megegyezők.
Milyen az állapotok száma is véges, így a maradéknyelvek száma is véges.

### VDA előállítása maradéknyelvekből
Határozzuk meg a szavak hossza szerint haladva a lehetséges maradék nyelveket!  
Legyen p1,p2,…,pn az egyes maradék nyelvek egy-egy reprezentáns szava!  
Feleltessük meg az állapotokat a maradék nyelveknek, azaz legyen 
- Q:={Lpᵢ| n≥i≥1} és
- δ(Lp, a):=Lpa ∀a ∈ T;
- q0:=Lɛ;
- F:={Lp|ε ∈Lp}.

### Backus-Naur forma (BNF)
A BNF lényegében egy 2-es típusú grammatika.
- Szabályok véges halmaza, ahol a szabályok bal- és jobb oldalát a **::=** jel választja el.
- A bal oldalon egy fogalom (egy nemterminális) szerepel.  
**< fogalom >** (A < > jelek közé tetszőleges szöveg írható.)
- A jobb oldalon a bal oldal kifejtése szerepel. Ha több alternatíva is van, akkor az alternatívákat | jel választja el.
- A terminálisokat nem kell semmilyen jel közé tenni.
- Egy alternatíva terminálisok és nem terminálisok sorozata.

### Szóprobléma
- Szintaktikusan helyes-e az egy kifejezés?
- Ha levezethető a <kifejezés> fogalmából, akkor igen.

### Levezetési fa (szintaxisfa)
**Definició:** Legyen G = (N,T,P,S) tetszőleges 2-es típusú grammatika.  
A t nemüres fát G feletti levezetési (szintaxis) fának nevezzük, ha
- pontjai T ∪ N ∪ {ε} elemeivel vannak címkézve;
- belső pontjai N elemeivel vannak címkézve;
- ha egy belső pont címkéje A, a közvetlen leszármazottjainak címkéi pedig balról jobbra olvasva  
X1, X2, …, Xk, akkor A → X1X2…Xk ∈ P.
- az ε -nal címkézett pontoknak nincs testvére.

**Tétel:** Ha adott G grammatika esetén u ∈ L(G) akkor és csak akkor, ha u-hoz megadható egy szintaxisfa.

_**Megjegyzés:** Az u-hoz tartozó szintaxisfa gyökere S és a leveleit balról jobbra összeolvasva az u szót kapjuk._

**Állítás:** Minden szintaxisfához megadható egy levezetés és fordítva.
- Legbal levezetés: A legbal levezetés olyan levezetés, hogy ha a levezetés folyamán a mondatforma i. betűjén helyettesítés történik, akkor a korábbi pozíciókat (1., … , i-1.) a levezetés a további lépesekben már nem 
érinti, azok változatlanul maradnak.

Egy G 2-es típusú grammatika egyértelmű, ha minden u ∈ L(G) szóhoz egyetlen szintaxisfa tartozik.
- **Ellenpélda:** S → a | S + S u = a + a + a //két fát is meg tudunk adni


## 6. Előadás
-------------

### 2-típusú grammatikák normál formája
**Definíció:** Egy G=(N,T,P,S) környezetfüggetlen grammatikát Chomsky normálformájúnak mondunk, ha szabályai
- A → a, ahol A ∈ N és a ∈ T vagy
- A → BC alakúak, ahol A,B,C ∈ N.
- S → ε, de ekkor S nem fordul elő egyetlen szabály jobboldalán sem.

### Chomsky normál forma
**Tétel:** Minden környezetfüggetlen grammatikához megkonstruálható egy vele ekvivalens Chomsky normálformájú grammatika.

**_Megjegyzés:_**
- _A 2-es típusú grammatikák Chomsky normálformára hozásának algoritmusa nem a tananyag része._
- _Chomsky normálformájú grammatikákhoz megadható olyan elemző program, amely O(n³) időben eldönti a szóproblémát (Cocke-Younger-Kasami algoritmus)._
- _Bizonyos állítások bizonyítását elég elvégezni a normálformájú grammatikákra._

### 2-es típusú grammatikák redukálása
A grammatikák transzformálása közben keletkezhetnek olyan szabályok, amelyek egyetlen szó levezetésében sem használhatóak.  
A grammatikában lehetnek olyan nemterminálisok, amelyekből 
1. nem lehet csupa nem terminálisból álló sorozatot előállítani; (zsákutcák)
2. nem érhetők el a kezdőszimbólumból.

### Hasznos/ nem hasznos nemterminálisok
**Definició:** 
- **Aktív** nemterminálisok halmaza egy adott G=(N,T,P,S) környezetfüggetlen grammatika esetén:
    - A := { X ∈ N | X ⇒* u és u ∈ T*}.
- **Inaktív** (zsákutca) nemterminálisok: N \ A.

**Definició:** 
- **Elérhető** nemterminálisok halmaza:
    - R := { X ∈ N | S ⇒* uXw és u,w ∈ (T ∪ N)*}.
- **Nemelérhető** nemterminálisok: N \ R.

**Definició:** Egy nemterminálist **hasznosnak** mondunk, ha **aktív** és **elérhető**.

**Definició:** Egy környezetfüggetlen grammatika redukált, ha **minden nemterminálisa hasznos**, azaz a grammatika **zsákutcamentes** és **összefüggő**.

**Tétel:** Minden 2-es típusú grammatikához megkonstruálható egy vele ekvivalens **redukált grammatika**.

**Bizonyítás:**
1. Zsákutcák meghatározása és minden olyan szabály elhagyása, amiben inaktív nemterminálisok szerepelnek.
2. Az S-ből nem elérhető nemterminálisokhoz tartozó szabályok elhagyása, azaz a grammatika összefüggővé tétele.

#### 1. Zsákutcák elhagyása
- A₁ = { X ∈ N | X → u ∈ P és u ∈ T*}
- Aᵢ₊₁ = Aᵢ ∪  { X ∈ N | X → w ∈ P és w ∈ (Aᵢ ∪ T)*} , ahol i ≥ 1.
- ∃k : ∀m > k : Aₖ = Aₘ
    - Ekkor Aₖ a grammatika aktív nemterminálisainak halmaza.
- Az N\Aₖ inaktív (zsákutca) nemterminálisokat elhagyjuk a grammatikából és minden olyan szabályt is, amiben szerepelnek.

#### 2. Összdefüggővé tétel
- R₁ = { S }
- Rᵢ₊₁ = Rᵢ ∪ { Y ∈ N | X → uYw ∈ P, X ∈ Rᵢ, u,w ∈ (N ∪ T)*} , ahol i ≥ 1.
- ∃k : ∀m > k : Rₖ = Rₘ
    - Ekkor Rₖ a grammatika elérhető nemterminálisainak halmaza.
- Az N \ Rk nem elérhető nemterminálisokat elhagyjuk a grammatikából és minden olyan szabályt is, amiben szerepelnek.

### Bar-Hillel lemma (pumpáló lemma)
Minden L környezetfüggetlen nyelvhez megadható két nyelvtől függő természetes szám p és q úgy, hogy
- ∀ u ∈ L szóra, ha l(u) > p, akkor u felírható **u = vxwyz** alakban, ahol v, x, w, y, z ∈ T* és
    - l(xwy) ≤ q, 
    - xy ≠ ε,
    - v(x^i)w(y^i)z ∈ L, ∀ i ≥ 0 esetén.

_**Megjegyzés:** A lemmát nem bizonyítjuk, de a bizonyításhoz szükséges, hogy a 2-es típusú nyelvekhez létezik Chomsky-normálformájú grammatika._

### Szóprobléma eldöntése
**Tétel:** Minden G=(N,T,P,S) környezetfüggetlen grammatika esetében eldönthető,hogy egy tetszőleges u ∈ T* szó benne van-e a G grammatika által generált nyelvben vagy sem.  
Másképpen u ∈ L(G) igaz-e?

**Bizonyítás:**
- Feltesszük, hogy G Chomsky normál formában van.
- A nyelvben van üras szó ha S→ɛ ∈ P
- u levezethető k=2*l(u)-1 lépésben G-ben.
- A k lépésben levezethető szavak halmaza véges, így eldönthető, hogy u ∈ L(G) vagysem.

### Veremautomata
**Definíció:**
- A = (Z, Q, T, δ, z0, q0, F) rendezett hetest veremautomatának nevezzük, ahol
    - Z a verem szimbólumok ábécéje,
    - Q az állapotok nem üres véges halmaza,
    - T az input szimbólumok ábécéje,
    - δ: Z × Q × (T ∪ {ε}) → P(Z* × Q) leképezés az állapot-átmeneti függvény, ahol δ véges részhalmazokba képez,
    - z0 ∈ Z a kezdő veremszimbólum,
    - q0 ∈ Q a kezdőállapot,
    - F ∈ Q elfogadó állapotok halmaza.

### Veremautomata állapot-átmenete
Egy lépésben mindig kell egy jelet olvasni a verem tetejéről és csak egy jelet lehet elérni. Az input szalagról is egy jelet lehet olvasni, de nem kötelező.
Megváltoztatható az automata aktuális állapota, illetve a verem teteje. Egy lépésben egy egész sorozatot is beírhatunk a verembe.
Példák:
- δ(#,q0,a) = {(#a,q0)}
    - Jelentése: Ha # van a verem tetején és 'a' betű jön az inputon, akkor tegyük be 'a'-t a verembe.
- δ(#,q0,a) = {(ε,q0)}
    - Jelentése: Ha # van a verem tetején és 'a' betű jön az inputon, akkor töröljük #-t a veremből.
- δ(#,q0,a) = {(#,q0)}
    - Jelentése: Ha # van a verem tetején és 'a' betű jön az inputon, akkor ne változtassuk a verem tartalmát.
- δ(#,q0,ε) = {(#bb,q0)}
    - Jelentése: Ha # van a verem tetején és nem olvasunk az inputról, akkor tegyünk a verembe két 'b' betűt.

### Veremautomata - alternatív jelöléssel
- Ha δ(z,q,a) = {(w₁,r₁),…,(wₖ,rₖ)} , akkor ezt a leképezést a következő szabályhalmazzal is jelölhetjük:
    - zqa → wᵢrᵢ,ahol 1≤i ≤k.
- Ha δ(z,q,ε) = {(w₁,r₁),…,(wₖ,rₖ)} , akkor ezt a leképezést a következő szabályhalmazzal is jelölhetjük:
    - zq → wᵢrᵢ,ahol 1≤i ≤k.
- Tehát a szabályok baloldala ZQT vagy ZQ alakú és a jobboldala Z*Q alakú.

### Konfiguráció
Legyen A = (Z, Q, T, δ, z0, q0, F) egy veremautomata és legyen α ∈ Z*QT* . 
Azt mondjuk α az A veremautomata egy **konfigurációja**. 
- A konfiguráció a veremautomata egy pillanatnyi állapotát írja le. 
- Ha α=zqu, ahol z ∈ Z* és q ∈ Q és u ∈ T* és z=z1…zk és u=u1…um, akkor z1 a verem alján és zk a tetején lévő karakter és u az input szöveg még el nem olvasott része, ahol u1 a soron következő karakter.
- Kezdő konfiguráció: z0q0w ,ahol w ∈ T* az elemzendő szó.

### Közvetlen redukció - definíció
Legyen A = (Z, Q, T, δ, z0, q0, F) egy veremautomata és legyenek α, β ∈ Z*QT* konfigurációk. 
- Azt mondjuk, hogy az A veremautomata az α konfigurációt 
a β konfigurációra redukálja közvetlenül (jelölés: α ⇒_A β), 
ha van olyan z ∈ Z, q,p ∈ Q, a ∈ T U {ε} és r,u ∈ Z*, w ∈ T* 
szó, hogy zqa → up egy szabály és
- α = rzqaw és β = rupw teljesül.

### Redukció - definíció
Legyen A = (Z, Q, T, δ, z0, q0, F) egy veremautomata és legyenek α, β ∈ Z*QT* . 
- Azt mondjuk, hogy az A veremautomata az α konfigurációt a β konfigurációra redukálja (jelölés: α ⇒* β, α ⇒_A* β), ha vagy α=β vagy létezik α₁,…,αₖ konfiguráció sorozat, hogy
- α₁ = α és αₖ = β és αᵢ ⇒ αᵢ₊₁ (1≤i≤k-1).

### Veremautomata által elfogadott nyelv
**Elfogadó állapottal felismerhető nyelv:**
- **L(A)** := { u ∈ T*| ∃ z0q0u ⇒* wr és r∈F és w∈Z*}.

_**Megjegyzés:** Ez azt jelenti, hogy van olyan működése a veremautomatának, hogy kezdő konfigurációból indulva végig olvasva az inputot elfogadóállapotba jut._

**Üres veremmel felismerhető nyelv:**
- **N(A)** := { u ∈ T* | ∃ z0q0u ⇒* r és r ∈ Q }.

_**Megjegyzés:** Ez azt jelenti, hogy van olyan működése a veremautomatának, hogy kezdő konfigurációból indulva végig olvasva az inputot teljesen kiüríti a vermet._

### Determinisztikus veremautomata
Egy veremautomatát determinisztikusnak mondunk, ha minden α ∈ Z+QT* konfiguráció esetén egyetlen konfiguráció vezethető le közvetlenül α -ból.

_**Megjegyzés:** Ez azt jelenti, hogy nincs két olyan szabály, amelynek azonos a baloldala, valamint, ha zq egy baloldal, akkor nincs zqa baloldal egyetlen terminálisra sem._

### Determinisztikus és nemdeterminisztikus veremautomaták kapcsolata
A determiniszitikus autómatákkal felismerhető nyelvek családja **szűkebb** mint a nemdeterminálisoké.  
Pl. a szimmetrikus szavak nem ismerhetőek fel determinisztikussal.

### A kétféle elfogadás kapcsolata.
**Lemma1:** Bármely A veremautomatához megadható A’ veremautomata úgy, hogy N(A’)=L(A). 
**Lemma2:** Bármely A veremautomatához megadható A’ veremautomata úgy, hogy L(A’)=N(A).

_**Megjegyzés:** Ez azt jelenti, hogy ha egy nyelvhez építhető elfogadó állapottal felismerő veremautomata, akkor építhető üresveremmel felismerő veremautomata és fordítva._

### A 2-es nyelvcsalád és a veremautomaták kapcsolata
**Tétel:** Ha L ∈ 𝕃₂, akkor megadható egy A veremautomata úgy, hogy L=N(A), azaz 𝕃₂ ⊆ 𝕃1V .

**Bizonyítás:** Legyen G=(N,T,P,S) egy környezetfüggetlen (2-es típusú) 
grammatika, amelyre L=L(G).  
Ekkor A=(T∪N,{q0},T,δ,S,q0,∅), ahol δ a következő:
- Xq0 → w⁻¹q0 akkor és csak akkor, ha X → w ∈ P, X∈N, w∈(T∪N)*;
    - Ha nemterminális van a verem tetején, akkor valamelyik rá vonatkozó szabály jobb oldalára cseréljük.
- aq0a → q0 akkor és csak akkor, ha a ∈ T.
    - Ha terminális van a verem tetjén, akkor ha ugyan az van az inputban akkor tovább lépünk az inputban és kivesszük a veremből.
- A veremmel a szó legbal levezetését szimuláljuk.

_**Megjegyzés:** A egy egyállapotú üresveremmel elfogadó automata._

**Tétel:** Minden A veremautomatához megadható egy környezetfüggetlen G grammatika úgy, hogy L(G)=N(A), azaz 𝕃1V ⊆ 𝕃₂ .

_**Megjegyzés:** A fordított tételt nem bizonyítjuk._



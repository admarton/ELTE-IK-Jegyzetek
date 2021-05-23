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
- **Egységelemes:** ϵ és v ∈ V* : ϵv = v = vϵ

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
A 2-es szabályban v≠ϵ nincs kikötve, az 1-esben pedig igen.


## 3. Előadás
-------------


## 4. Előadás
-------------


## 5. Előadás
-------------


## 6. Előadás
-------------


## 7. Előadás
-------------


## 8. Előadás
-------------


## 9. Előadás
-------------


## 10. Előadás
--------------


## 11. Előadás
--------------


## 12. Előadás
--------------



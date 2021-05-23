# Formális nyelvek és fordítóprogramok

## Előadók
- Nagy Sára saci@inf.elte.hu

## 1. Előadás

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



## 3. Előadás



## 4. Előadás



## 5. Előadás



## 6. Előadás



## 7. Előadás



## 8. Előadás



## 9. Előadás



## 10. Előadás



## 11. Előadás



## 12. Előadás




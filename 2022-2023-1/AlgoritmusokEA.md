# Algoritmusok tervezése és elemzése Ea

# 2.EA 2022.09.20

## Gale-Shapley algoritmus helyessége

### Állítás:
1. GSA befejeződik az n²+1 nap alatt
2. Teljes párosítást ad
3. Stabil párosítást ad

### Bizonyítás:
1. Ha bármelyik nap nem felyeződött be az algoritmus, akkor van olyan lány akinek az erkélye alatt legalább két fiú ólálkodik, ... az egy neki való ..., a többiek kosarat kapnak, és ... a ... ..., röviden egy ... nap legalább egy lánynál áthúzhatunk kérőt.


    1. Ha lett párja...
    2. Ha egy fiúnak nem lett párja, akkor mindenkinél próbálkozott és mindenkitől kosarat kapott.
    3. Ha egy lánynak van uvarlója akkor párja is lesz.
    4. Ha egy lánynak van udvarlója valamikor, akkor a végsőkig válogatja a legjobbat.

2. Indirekt tfh. h egy fiú minden háznál próbálkozott és mindenkitől kosarat kapott. De ha egy lánynak volt udvarlója, akkor végül lett párja. Minden lánynak lett párja, akkor minden fiúnak is kellene legyen. Különben ellentmondás.

3. Indirekt tfh. a párosítás stabil és léteznek olyan (f,l) és (f',l') párok ahol, l-nek jobban tetszik f' és f-nek jobban tentszik l' mint a párja.  
A protokoll szerint f először l'-nél próbálkozik, majd l azután jön (valamikor), ha l-nél kosarat kap. Igen ám, de l'-nek az udvarlói közül a legjobbat kell választania. Ellentmodás lenne.

### Optimalitás
- Kinek kedvez a GSA?
    - Azokra az elrendező párokat fogjuk vizsgálni, ahol a fiúk és lány párba kerül egy stabil párosításban. 
    Mondjuk azt, hogy egy fiú és egy lány szóba jönnek egymás számára ha van olyan stabil párosítás, amiben ők egy párt alkotnak.
    
#### Állítás
4. A fiúk a számukra legjobb szóbajövő lányt kapják.
5. A lányok a számukra legkedvezőtlenebb szóbajövő fiút kapják.

#### Bizonyítás
4. Indirekt tfh. van olyan fiú akinek nem a számára szóbajövő lányok közül nem a legjobban tetsző lesz a párja végül. A protokoll szerint ez a fiú udvarol valamikor a számára szóba jöhető lányok közül a legjobbnak és kosarat kapott. 
Tekintsük az első olyan napot, amikor ilyen szomorú dolog történt. (egy fiú ... kap a számára szóba jövő lányok közül a ... legjobbat ...)
Legyen f egy olyan fiú, l a ... lány, f' pedig az a fiú akit l szívesen látna.  
Mivel ez az első alkalom ezért ...  
Jelölje l* az f' számára a legjobbat.  



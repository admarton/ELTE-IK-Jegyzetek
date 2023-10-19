# 1.EA

Jung András  
Canvas-ban fent vannak a diák  
Teszt online  
30 kérdés  
Utolsó órán meg lesz adva, hogy melyik diáról lesz kérdés  

Távérzékelés, hiperspektrális, növények és talaj  
Multiszenzor, dron és fúzió részleg  

GNSS
- GPS az amerikai nav rendszer
- Ez a globális hivatalos neve
- Glonas az oroosz
- Galileo lesz az európai

Vector - Raszter
- Régen elkülönültek
- Mostanra már szinte mindegyik tud mindent

Technológiát mi csak követjük.  
Jelenleg nagyon drága egy jó felbontású műholdkép.  
Nagy időbeli és térbeli felbontást nehéz produkálni

# 2.EA

## Raszteres vagy Vektoros
Emberek és szoftverek is az egyiket válasszák

## Vetületek
Föld föld alakú, a vetület pedig 2D
fentrol.hu
GNSS alapú rendszert használ mindenki
Változásokat meg lehet nézni a képek alapján.
Olyan föld vetület kell ami jól viszonyul a képekhez.

## Tematikus rétegek
Térbeli integritás
Minden réteg más információt tartalmaz

## Koordináta rendszerek
Derékszögű kis területeken jó lehet, de csak kis terülten.
Nagyobb területen nagyobb hibát ad.

## Attribútumok
Nominális
- Szín
Rendezett
- Rangsorolható
Numerikus
- Operátorok alkalmazhatóak
- Magasság

## Adatmodellek
Diszkrét objektumok vektorosan.
Földmérő 50-60 centiméterrel nem foglalkozik, a földhivatal hibahatárán belüliek.
Görögországban nagyon rossz a földhivatal.
Fotogrammetria
- Mérnöki tudomány
- Fénykép alapján geometrikus információ gyűjtés
- Raszter -> Veckor
- Ortofotó alakítás - sugárirányú torzulást el kell távolítani
- Ezt kiegészíti a drónos fotózás

## Drónozás
Gábor Dénes - Drón technológia szakirány és konferencia

# 3.EA

Szkenneléses és snapshot felvétel  
Szkennelés - mint a sima szkenner - soronként olvas be  
Snapshot - Egy pillanatban csinálja az összes pixel a képet  

Infravörösben (762 nanométer) lehet látni az ereket és visszereket, 262~ nanométeren lehet látni a véroxigén szintet

## Raszteres adatmodell

Adat mintavételezés egy mátrixot ad.  
Mintavételezés sűrűsége számít, méréspontok között interpolálni vagy extrapolálni lehet.  
Térbeli, időbeli, spektrális és radiometriai felbontás  
Térbeli felbontás nagyon irányfüggő.
Radiometria = bitmélység = dinamika tartomány
- 8 bit a legtöbb kép, mert az ember nem lát többet
- De a kép nagyobb bitmélységgel készül, amikor analóg jelből digitális jelet csinálok

Geo-referált kép
- Be kell rakni egy képet egy vetületbe
- Koordináta a kép közepéhez tartozik és onnan kell kiszámolni a többit

## Raszter kihívások

Pontszerű helyeket hogyan lehet raszteres világba vinni.  
Ha sok pont esik egy raszterbe akkor adatot veszíthetünk.  
Nagyobb térbeli felbontás segíthet -> milyen kihíváshoz milyen felbontás szükséges.
Zöld kerületek egyre kevésbé zöldek, a magára hagyott területek növelik a zöld értékeket.  
Könnyen eltűnhetnek információk.  
Képfeldolgozás lényege, hogy osztályozzuk a pixeleket és tematikus információkat veszünk ki belőle. Pixelből ki lehet keverni sub-pixeles információkat.  
Kézi földmérési munka sokszor kiváltható raszteres adatok feldolgozásával.  
3D városmodellek -> mobile mapping.  

# EA - 2023.10.18

## GIS Műveletek

### Térbeli analízis
- Vizuális programozási módszerekkel modellek építése
- MATLAB-ban csinálnak programot a rapid prototyping idejében, utána ha termék lesz, akkor kell rendes programot írni
- Nehéz a valóságot automatizálni, mert sok empirikus dolog van, amit nehéz reprodukálhatóan megcsinálni.

### Réteges adatok vannak  
- Műveletnél számítanak a bemeneti rétegek száma és a kimeneti rétegek száma
- Egy inputból lehet több output
	- pl infravörös képen könnyen elkülöníthető a növényzet és a vízfelszín
		- ebből lesz egy víztérképem és egy növény térképem
- Több inputból egy output
	- pl indexek, képletek amik összehoznak információkat
		- termális felvétel és vegetációs index
			- termális képen látszik a növényzet és a beton/aszfalt
	- pl NDVI - növényi vegetációs index
	- CIR ábrázolás - Color-Infra-Red
		- B (400-500), G (500-600), R (600-700), NIR - near infra red (700-1000 nm)
		- Eltolás B->X, G->B, R->G, NIR->R
		- ekozmu.hu
		- Precíziós növénytermesztésben használják ezeket

### Agrárinformatikai tárgy is van

### Lekérdezések
- Nem térbeli adatokat az attribútum táblákban tudjuk kezelni
- Térkeli lekérdezés és térbeli válasz
	- Szőlős, domborzati minta -> 3D modell -> van-e még ilyen hely a földön
	- Borvidék hasonlóságok -> esetleg minőségi következtetések

### Halmazalgebra  

### Klasszifikáció

- Parlagfű kiválasztása a repce mezőkön.
- Bináris képek tulajdonság kiemelésére.
	- Maszkokat lehet csinálni
	- Csak a maszkolt részeket kell tovább vizsgálni



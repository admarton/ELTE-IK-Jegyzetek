# Térinformatika Gyakorlat

# 1.GY

## Elérhetőség
kerkovits@map.elte.hu
mercator.elte.hu/~kerkovits
Hétfő, kedd, szerda, É7.75

## Követelmény:
- Katalógus lesz
- 3x lehet hiányozni
- Jegyek
	- Beadandók
	- 4db * 20pont = 80pont
	- Min 8 pont kell
	- Min 45 összesen
Honlapon több infó
Honlapon a gyak tervezett menete
Két oktatónál teljesen más lehet
Utolsó óra egy beszámoló  
- Kiselőadás az utolsó beadandóból
- 10 pont
Beadandó késés
- -0.5 pont / nap / beadandó
- Ékezetes fájlnév ne legyen
	- Ékezetenként 0.5 pont levonás

## Oktató:
Térképészetből doktorált
Vetülettan
Bringás és túrázó
Evangélikus templomban orgonál

## Szoftver:
- qgis.org
- szokott fagyni a program
- Fájlformátumok
  - Térkép az egy adatbázis
    - Rekord hol van a térben
  - Külön tároljuk, hogy hogyan néz ki
- GPKG
  - sqlite adatbázisra épül
  - Adattípus:
    - Pontszerű
    - Vonal szerű
    - Felület szerű
  - Egy táblában csak egy típusú lehet
- shp, dbf, shx fájlok mind kellenek
  - táblánként új dbf kell
  - mezőnév max 8 karakter, ékezetes karakter nem megy
- cpg
  - dbf-ben milyen karakterkódolás van
- prj
  - milyen koordináta rendszerben vannak a koordináták
- qpj 
  - koordináta rendszer plusz adatok
- lehetnek további kiegészítő fájlok, de azok nem kötelezőek
- shp
  - ARCGIS natív formátuma
  - Régebbi nagyobb szoftver
- Megjelenítés
  - qgz - QGIS
  - myd - ARCGIS
- QGZ
  - Igazából egy zip fájl
  - QGD és QGS
  - QGS - XML van benne

MO.gpkg
- Minden réteg egy tábla

QGIS
- 2D-3D megjelenítés
- Görgetés a legjobb navigáció a térképen

Raszteres formátumok
- tiff a legnépszerűbb, veszteségmentes tömörítés

Méretarányok, vetületek számítanak

Vetületek:
- Területtartó
- Szögtartó
- Távolságtartó vetület nem létezik
- Általános torzulású 
  - se nem egyik se nem másik
  - jobb eredményeket adhat
- QGIS alapból meridiánban értelmezett négyzetes hengervetületet használ
- Közelítő elipszoid - WSG 84 általában, HD72 magyarországi ingatlannyilvántartás
- Koordináta rendszer
  - Földrajzi: fokban, szélesség-hosszúság
  - Vetületi: méterben
- Külön adat koordináta rendszer és külön térkép koordináta rendszer
- EOV - egységes országos vetület Magyarországon 
  - szögtartó
  - segéde egyenlítő az ország közepén - ebből hengervetület
  - Gellérthegyi kezdő meridián
  - Ez a kezdő koordináta el lett tolva
    - Függőleges koordináta kisebb mint 400km
    - Vízszintes koordináta nagyobb mint 400km

Geodéziai dátum
- Dátum - latinul adat
- Nincs köze a naptári dátumhoz

# 2.GY

Vonal
- 0.2-0.5 mm a vékony vonal

Marker
- Kör, négyzet, rombusz, háromszög, vonal, kereszt, csillag

Betű
- Minimális méret 5-6 pont

SVG
- Minimum 3×3 mm

Folyó
- 1-2-3 mm

## Utak ábrázolása

Vonalvastagsággal lehet hangsúlyozni, színnel és összetettséggel
Egyvonalas elem, vagy szaggatott - burkolat nélküli, nem kiépített
Kétvonalas elem - aszfaltos út, főút
Háromvonalas elem
Színek:
- Autópálya teljesen más színű mint a többi (kék, zöld, lila)
- Erős szín (piros) fontosabb mint a gyengébb színek (fehér)

# 4.GY

## Első beadandó

Három térképet kell csinálni
Tematikus megyetérkép
A4-es lapon nyomtatási kimenet
Térképnek van:
- Cím
- Jelmagyarázat
- Méretarány
- Stb
Tematikus térkép részei:
- Háttértérkép
	- Közigazgatási egységek, bel- és külterülethatárok
	- Ez lefedi a megyét
	- Vízhálózat (folyók, patakok, tavak)
	- Út és vasúthálózat
- Tematikus adatok
	1. Települések kategorizált megjelenítése
	2. Lakosság összetétele, kördiagram
	3. Hulladéklerakónak hely keresés
Ebből 3 PDF és a geopackage és a projektfájl.

np_tk a környezetvédelmi cuccok
mo -ból nem kell
- Országhatár
- Járás
- Patak

Anyaghoz új geopackage
Export/Save selected features as

Felesleg levágása:
Vector/Geoprocessing Tools/
- Clip vágás
- Intersection
- Buffer - sávot hagy
- Difference - kivonás átfedés eldobás
- Dissolve - Érintkező elemek egyesítése
- Union - megmaradnak a külön elemek, de csoportosítja

Jelek tervezése
- Méret
- Színek (2-4)
- Alakzat (Csillag, négyzet > kör)
- Összetettség
- Scale range - milyen nagyításnál látszik

# GYAK 11.08

Topology checker
Processing toolbox / Fix geometry
Invalid geometry:
- Egy helyen két csomópont
- Önmetszés
- Vonalszerű
[Sentinel 2 adatok](https://dataspace.copernicus.eu)

# GYAK 11.15

## Vetületek

A felhasználáshoz kell megfelelő vetületet választani. 
Gömb vagy forgási elipszoid és azt vetítjük valahogy síkra.

### Szögtartó

- Topográfiai
- Tájékozódásra használjuk
- A térképen a szög és a valóságban a szög megegyezik
- Nagy méretarányú térképeken

### Területtartó

- Térképen mért terület és valós terület arányos
- Kis méretarányú térképeken

### Általános torzulású

- Mindkét torzulást próbálja minimalizálni
- Hasznos lehet

### Hossztartó vonalak

- Egyenlítő, szélességi körök

### Pólus pont vagy vonal

- Hogyan vetül, google maps pl pólus vonalas

### Fontos vetületek

#### Négyzetes hengervetület

- Ez a legelterjedtebb vetület, pl QGIS,
- Meridiánokban hossztartó
- Négyzetrácsos

#### Marcator vetület
- Google
- Hengervetület
- Szögtartó

## Geodéziai dátum

Az elipszoidot a földhöz hova rakjuk
Hol fogja jól közelíteni a földfelszínt

## GPS

WGS84 - 4326 
Ez a GPS alapja és a legtöbb vetületnek
GPS magasság az elipszoid feletti magasságot adja meg, több méter eltérés is lehet

## GEOTIFF

- TIFF header-ben vetületi adatok
- Sarokpont, sorok és oszlopok száma
- Pixelek mérete, méretarány
- Vetület
- Lehet több csatorna a pixelértékekhez
	- RGB
	- Más fény hullámhossz
	- Magasság adat

## Domborzat modellek

- SRTM magasság feltérképezése
	- Űrsiklóról sztereó mérés
- Semi-global
- 30m-es felbontás



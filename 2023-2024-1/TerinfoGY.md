# Térinformatika Gyakorlat

# 1. Gyak

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
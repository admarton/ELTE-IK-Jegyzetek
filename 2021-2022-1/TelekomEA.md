# Telekommunikációs hálózatok EA 2021.09.08

Interneten csomagok mennek. Kis kapacitású élhez sok csomag megy, akkor várakozás. Ha túl sok várakozó, csomagok eldobása.

Az internet mennyire megbízható? Vannak kiesések!  
Rout leaking, egy routert rosszul konfigurálnak és olyan mintha a csomagokat egy fekete lyukba dobálnánk.

## Elérhetőség

lakis@inf.elte.hu  
https://lakis.web.elte.hu

## Cél
Hogyan működik az internet?  
- Címzés
- Rétegek
- Forgalomirányítás
- Megbízhatóság
- Erőforrás megosztás

## Számonkérés
- Vizsga
    - Teszt : 20 kérdés, min 11 pont
    - Esszé : 5 kérdés, kifejtős (algoritmus, összehasonlítás)
- 50% -> 2
- 85% -> 5

## Hálózat
- Végpontok vannak összekötve, pl.: Linux szerver, okos TV, stb.
- Switchek és routerek vannak az végpontok között
    - Otthoni kb 1Gbps
    - ToR kb 1,8-6,5 Tbps
    - Internet Core kb 12,8 Tbps (Claster upto 927 Tbps)
- Linkek:
    - Végpont <-> Router
    - Router <-> Router
    - Lehet 
        - réz 
        - optikai - 2/3 fénysebesség
        - vezetéknélküli
            - lehet rádiós vagy fény(lézer)
- További fogalmak
    - Hálózati host
    - Átviteli csatorna/médium/fizikai közeg

## Mértékegységek
- bit / másodperc - b/s
- 1000 a váltószám, SI mértékegység

## Internet
Hálózatok hálózata
- DSL - telefon vonalakon keresztül, telefon volt már
    - Letöltési : Ez a legnagyobb
    - Feltöltési : 
    - Két-irányú : Ez a telefon pl
- CATV - kábeltévé megoldás, réz koax kábel
    - Letöltés
    - Feltöltés
    - DSL-nél saját kábel, TV-nél közös vezetékek osztott használata
- Eternet - hálókártya, UTP kábel
- Modil - okosteló
- Műhold
- FTTH 
- Optika
- Infiniband - HPC klaszter - háttértárt is szerveren kell elérni

## Topológiai elvárások:
- Hibatolerancia
    - Több útvonal a végpontok között
- Rugalmasság
    - Költséghatékony infrastruct
    - Bővíthető
    - Max link szám
- Megfelelő csomópont-kapacitás
    - Min link szám

## Topológiák
- Teljesen összekötött
    - Nem megvalósítható
- Lánc, gyűrű
    - Kis méretekben
    - Nem túl hibatoleráns
    - Terhelések nem egyenlően oszlanak meg
- Busz
    - Ha busz sérül akkor szétesik a gráf

- Kompromisszumos megoldás az Internet
    - Van redundancia, de minimalizált
    - Terheléseknek megfelelő bővítés
    - Döntés kell, hogy merre továbbítódik, komplex routerek kellenek
        - Útvonaltervezés
        - Erőforrásmegosztás
        - terhelésfelmérés

## Erőforrások kezelése
- Előre foglalásos
    - Hálózatnak előre bejelentés
    - Lefoglalás
    - Küldés
    - Felszabadítás
    - **Folyam szintű multiplexálás**
- Igény szerinti
    - Kis csomagok
    - Címzés
    - Küldés
    - Minden hálózati pont döntéseket hoz, hogy tudja-e küldeni vagy eldobja
    - **Csomag szintű multiplexálás**
- Csúcs és átlagos ráták
    - Flow, folyam rendelkezik
        - Csúcsrátával (peak rate): P
        - Átlagos ráta: A
    - Előre foglalásnál P-hez kell foglalni
        - A/P kicsi, akkor sok a veszteség
    - Igény szerintiben nagyobb kihasználtságot lehet elérni
- Melyik jobb?
    - Nehéz eldönteni, helyzettől függ
    - Ha P/A kicsi (csúcs közel az átlaghoz), akkor előre foglalás
        - pl telefon ilyen, folyamatos adatátvitel telefonálás közben
    - Ha P/A nagy, akkor az előre foglalás pazarlás
        - Az adat általában BURSTY-löket szerű ezért a csúcs sokkal több mint az átlag
        - Az internet általában igény szerinti
- Megvalósítás
    - Áramkörkapcsolt:
        - telefonálás, központban kapcsolták a kábeleket
        - előre foglalás
        - Resource Reservation Protocol
            - Swichek lefoglalják az útvonalakat, áramköröket
            - Végén bontjuk a foglalást
        - csak azt az útvonalat lehet használni
            - ha sérül
            - akkor új útvonalat kell foglalni
        - előnyök:
            - kiszámíthatóság
            - stabilitás
        - hátrányok:
            - alacsony kihasználtság
            - hiba érzékenység
            - kis adatnál több idő a hálózat kezelése
    - Csomagkapcsolt
        - csomagok, címinformáció
        - löketek kezelésére bufferek
        - igényszerinti

# Telekom EA 2021.09.15

## Csomagkapcsolt hálózatok
- Az adatátvitel egyedi csomagokban történik
- Minden csomagba kell extra info: célállomás
- Ha a csomópont túlterhelt, akkor csomagok eldobódnak
- Ha pontosan egyszerre jönnek, akkor pufferba kerül
- Pufferkezeléz
    - Löketszerű viselkedést kezelni kell.
- Hiba tolerancia
    - A switch hibás kapcsolat esetén másik irányba küldi
    - Végpontnak mind1 az útvonal
- Előnyök
    - Hatékonyabb erőforrásgazdálkodás
    - Egyszerű megvalósítás (nincs előfoglalás)
    - Hibatolerancia
- Hátrány
    - Kiszámíthatatlan teljesítmény
    - Puffer-kezelés és torlódás-vezérlés

## Internet hierarchikus struktúra
- Tier-1 ISP nemzetközi - Pár tucat
- Tier-2 ISP nemzeti - több ezer
- Tier-3 (Access) ISP helyi - sok

- Ezeket linkek kötik össze
- Ami nem szolgáltató-vevő között van az **peer** link
    - peer tranzakciókért általában kölcsönösen nem fizetnek
- Olyan útvonal nincs ahol nem részesülnek az adatátvitel jutalékából
- IXP - hatalmas csomópont - Internet eXchange Point
    - Mindenki behúz egy linket és ott vannak összekötve a hálózatok
    - Olcsóbb, mint mindenkit mindenkivel összekötni
    - Tier-1 és Tier-2 között létezik kb
    - Földrajzilag is egy pont (Budapest, Frankfurt)
    - Egy helyen lehet változtatni a kapcsolatokat, nem kell linkeket kiépíteni

## A kommunikáció
- Különböző folyamatok különböző host-oknál és ezek között adatot akarunk cserélni
- Résztvevők távol vannak
- A többi csak a mese hozzá
- Több autonóm rendszeren megy keresztül
- Protokollok segítik a kommunikációt
    - konvenciók, szabályok, formátumok, mind2 fél értse a dolgokat

- Gyakorlati szinten : socket API (minden nyelvben implementálva)
    - Üzenet összeállítás (bájtsorozat)
    - Küldés
    - Megkap
    - Értelmezés (bájtsorozat feldolgozása)
    - Utána aktuálisan szükséges lépések
    - Háttérben sokkal több minden történik

- Protokoll Rétegek
    1. Bitek kódolása, küldése
    2. Biztonsági réteg
    3. több ugrás
    4. Alkalmazások között
    5. ...

- Új protokoll bevezetése nehéz
    - Router-ben is implementálni kell
    - Mikrochip szinten kb 4-5 év
    - Innovációs lánc elég lassú

- Rengeteg Protokoll van
    - Együtt működnek
    - Több kell ahhoz, hogy minden működjön

- Határokat kell definiálni
    - Ne legyen spagetti kód
    - Kezelhető programot kell létrehozni
    - Modularitás
        - Részfeladatra bontás
        - Absztrakt szintek
        - implementációknak kompatibilisnek kell lennie
        - Barbara Liskov: ötlete

## Hálózatok modelljei
- Internet rétegmodelljei
    - TCP/IP
    - Arpanet-ből jön régről
    - 4 réteg van
        - Kapcsolati réteg (Link, Host to network layer)
            - Adatátvitel, helyesség, javítás
            - Vastag réteg
            - Ezt kisebb részekre kellen bontani
            - Ethernet, LAN, ARPANET
        - Hálózati réteg (Internet layer)
            - Azonosítani az eszközöket
            - Adatcsomag továbbítás
            - Bárhonnan bárhova meg találja az utat
            - IP (IPv4, IPv6)
            - Itt nem lehet több protokoll különben szétszakad az internet
        - Szállítói réteg (Transport layer)
            - Két app között legyen csomagküldés
            - Bizonyos alkalmazásoknak eltérő internet igényei vannak
            - Pl.: minden bájthelyesen megérkezzen (kép dokumentum, valósidejüség fontosabb (live video, csomagvesztést tudja kezelni)
            - TCP(biztos de sok overhead), UDP(levelezés szerű), CLIK(Google cucc)
        - Alkalmazási réteg (Application layer)
            - Minden más
            - Egyedi megvalósítások
            - Üzenetformátum, kommunikáció mintázata, stb

- Nyílt rendszer hálózatának standard modelljei
    - Open System Interconnection Reference Model
    - Általános modell, kommunikációs hálózatokhoz
    - Nem feltétlenül az internethez
    - 3 dolog kell egy réteghez
        - Szolgáltatás
        - Interface
        - Protocoll
    - 7 réteg (internet 5):
        - Fizikai
            - SZ
                - Információ két fizikai eszköz között
                - 1 bitet
                - Fizikai közegeknél máshogyan kell kódolni
            - I
                - Van egy függvény, amivel bitet lehet küldeni
            - P
                - Bit kódolásának sémája
                - Jel megfelelő dekódolása

        - Adatkapcsolati
            - SZ
                - Bitsorozat elküldés
                - Hibadetektálás
                - Hibajavítás
                - Kisebb csomagok a hosszú bitsor helyett
                - Egyszerre adást valahogy meg kell oldani
            - I
                - Keret küldése két eszköz közt
            - P
                - Fizikai cmzés ilyemi

        - Hálózati
            - SZ
                - Csomagtovábbítás
                - Switch/Routerben a keretek tovább küldés
                - A közvetlen eszközhöz küldést használja
                - Útvonalválasztás
                - Puffer kezelés
            - I
                - Csomagküldés végpontba
            - P
                - Globálisan egyedi címek
                - Routing táblák

        - Szállítói
            - SZ
                - Multiplexálás - továbbítás processhez
                - Torlódásvezérlés
                - Megbízhatóság 
            - I
                - Üzenet küldése egy célállomásnak
            - P
                - Port szám (process azonosító)
                - Megbízhatóság/hiba javítás
                - Folyamat felügyelet
        - Munkamenet (nincs az internetnél)
            - SZ
                - kapcsolat menedzsment
                - munkamenet típus meghatározás
                - Szinkronizációs pont (checkpoint)
            - I
                - ...
            - P
                - Token menedzsment
                - Checkpoint beszúrás
        - Megjelenítési (internet esetén nincs, app része)
            - SZ
                - Adatkonverzió rendszereke között
                - Encódolás, konverzió
            - I
            - P
        - Alkalmazási
            - SZ
                - Bármi
            - I
                - Bármi
            - P
                - Bármi

- Routerbe kell:
    - Fizikai, Adatkapcsolati, Hálózati
    - A többi nem kell
    - De ezek igen, hogy megtalálja a célt
- Switch-nél elég a fizikai meg adatkapcsolati réteg
- A réteget csak akkor kell implementálni, ha nem kell
- Routernek és switch-nek mindegy mi az adat a csomagban
- Tűzfalnál más a rendszer
    - Ott lehet app réteg is kell
    - Belenéz az alkalmazási adatba
- Közbenső pontoknál lehet átalakítás
    - pl.: wifi -> eternet

- Hibrid réteg
    - Az első kettő keveréke
    - 5 réteg

- Réteg homokóra
    - Fizikainál sok protokoll, sok hordozóközeg
    - Adatkapcsolatnál sok protokoll, leginkább a fizikai réteg miatt, de kevesebb mert egy prot. többet is tud kezelni
    - Hálózatinál egy IP-hogy egyben legyen
    - Szállítónál több protokoll, mert mindenhova más kell
    - App rétegnél kb végtelen protokoll szám

- Minden réteg hozzátesz az üzenethez
    - L5 App - üzenet a proccessek között
    - L4 Trans - szegmensek 
    - L3 Network - csomagok
    - L2 Link - keretek
    - L1 Phys - bitek

- Megvalósítás
    - L5-L2 software - flexibility
    - L4-L1 hardware - speed
    - Közelednek egymáshoz
        - programozható hálóeszközök (relatíve rugalmas, mégis gyors)
        - optimalizált lib-ek, driverek (sokat gyorsít, hardware jobb kihasználása)

- Réteg infók
    - App - HTTP
        - header + message
    - Trans TCP
        - 
    - Network - IP
    - Link - Ethernet


# EA 3 2021.09.22

## Hálózati karakterisztikák
- Késleltetés - delay
    - rossz felhasználó élmény
    - mennyi idő az átvitel
    - link property
        - **transmission** delay 
            - meddig tart kiírni az adatot
            - packet size [bits] / link badwidth [bits/sec] = delay [sec]
        - **propagation** delay
            - jelterjedés az adott linken keresztül
            - link length [m] / signal propagation speed [m/sec] = delay [sec]
    - traffic mix & switch internals
        - **processing** delay
            - feldolgozási idő pl.: hova kell küldeni
            - általában ez a legkevesebb ( sokszor elhanyagolható )
        - **queuing** delay
            - átmeneti túlterhelésnél várakozás
            - ha egyszerre mennének ugyan arra, akkor az egyik várakozik
            - előre nehéz meghatározni
            - arrival rate, transmission rate, 
    - ezekből jön a **total** delay
- Csomagvesztés - loss rate
    - Elveszett csomagok újra küldése vagy minőségromlás
    - mennyi csomag veszik el mennyiből
    - permanens túlterhelésnél megtelik a várakozási sor és eldobálja a maradék csomagokat
        - ha nem sikerül akkor valaki majd megoldja
        - TCP mindig teletölt egy sort
- Átvitel - throughput
    - Nagy fájloknál nagy sávszélesség kell
    - data size [bits] / transfer time [sec]
    - útvonal menti bottle neck határozza meg
        - a leggyengébb láncszem a meghatározó
        - linket használók között fel kell osztani az átvitelt
    
- Átvitel és a késleltetés fejlődik, de a terjedési sebesség nem nő
    - ezért replikák vannak és több helyen fut ugyan az a szerver
    - mindenki közelébe kerül egy kiszolgáló

## Fizikai réteg
- Villamosmérnökök terepe
- Erre épül az adatkapcsolati réteg
- semmi garancia sincs
- lehet nem az érkezik meg mint amit elküldtem
- fizikai behatások érik a jelet
- Információ átvitel a cél
- Kódolni kell a bitet

### Alapfogalmak
- számítógép digitális, diszkrét
- a valóság meg analóg
- Legegyszerűbb:
    - 1 - van feszültség vagy áramerőség
    - 0 - nincs feszültség
    - időegységbe kódolva
    - kapcsolót kapcsolgatjuk
    - érzékelő kell a másik oldalon
    - szinkronban kell lennie a két félnek
- Furier sorokkal lehet modellezni a valóságot
    - sin/cos-ok összegeikén állnap össze a jelek
    - lehet közelíteni a szögletes jelhez hullám függvényekkel
- aproximált jel érkezik meg
- periódusokat lehet ismételni
- jelek el tudnak nyelődni
    - csökken a jelerősség
    - küldési energia / vevési energia = elnyelődés [dB, deciBel]
    - nem egyenletes az elnyelődés
    - a közeg tulajdonságai meghatározzák, hogy mely frekvenciákat érdemes használni
- fázis eltolódás
    - más frekvencia más sebességgel terjed
    - ez nem túl jó
- zaj, hő, más rendszerek, ...

- bitek helyett szimbólumok vannak
    - két jelszint pazarlás lenne
    - ha négy szimbólum van, akkor több bitet is reprezentálhat - egy időben több információ megy át
    - szimbólum ráta [BAUD] nem változik
    - Adat ráta [bps] nő
    - vevő oldalon ez probléma
        - ha több szimbólum van, akkor nehezebb megkülönböztetni

### Átviteli közegek
- mágneses adathordozó
    - sávszélesség jó, késleltetés nagy (nem , on-line)
    - nagyon nagy adatmennyiségnél gyorsabb
- sodort érpár
    - ha nem sodort akkor antenna is lehet
    - nagy távolsági rendszerek
- koax kábel
    - nagy sebesség és távolság
    - nincs csavarás ezért le kell szigetelni
- fényvezető szálak
    - fény adó és vevő
    - pattog az optikai szálban
    - egy vékony szál, hajlítható, szigetelés
    - rengeteg szál össszerakva pl az óceánban
- vezeték nélküli
    - frekvencia, f [Hertz, Hz] - másodpercenkénti rezgésszám
    - hullámhossz, λ
    - fénysebesség, c, kb 3*10⁸m/s
    - rézben és üvegszálban kb 2/3-ad
    - λf = c
    - antennaméret és hullámhossznak van köze egymáshoz
    - érdekesség - "speed of light internet"

### Kiinduló feltételek
- Jelet időnként mérjük
- szinkronizálni kell mert torzult jel jön
- órajelenként egyszer lehet mintavételezni
- ha eltér az órajel, akkor többet tud mérni, vagy kevesebbet
- GPS szinkronjelekkel lehet ott, ahol ez nagyon fontos
- Kritikus időpontokban szinkronizáljuk
- Önütemező jel
    - órajel szinkronizáció nélkül is kódolható
    - nem alacsony-magas jel, hanem változások
    - a változásokat könnyebb észrevenni
- Mancheszter kódolás, ami most fontos - 10 megabitnél
    - minden bit jelszintváltozásba
    - 1 - magasról alacsonyra
    - 0 - alacsonyról magasra
    - két órajel egy bit kódolásához
    - lehetséges kapacitás felét használjuk ki
- NRZI
    - 1 - átmenet
    - 0 - ugyanaz marad
    - egy órajelciklus elég a kezeléshez
    - sok nullánál el tud csúszni
- 4-5 bit kódolás - 100 megabitnél
    - max 3 nulla lehet egymás mellett
    - veszít sávszélességet de nem túl sokat és cserébe jobb
- 8-10 kódolás gigabit-nél

### Alapsáv és szélessáv
- alapsáv fel minden frekvencián megy
- szélessáv, csak egy tartományba küld, pl ott ahol az elnyelődés egyenletes

# EA 4 2021.09.29

## PSK több szim.
- fázis eltolás könnyen felismerhető a fogadó által
## Amplitúdó több szim.-hez

## Multiplexitás
- Egy fizikai közeget többen is használnak
    - átvitelek zavarhatják egymást
    - csatorna felbontása logikai alcsatornákra
    - Küldő oldalon kell egy összefésülő eszköz : **multipexer**
    - Vevőnél demultiplexálás

- Térbeli multiplexálás
    - A legegyszerűbb
- Frekvencia multi.
    - Adott tartományban jó az átvitel
    - A tartományt is fel lehet osztani
    - Kis szünet is van a jelek között, hogy biztos legyen
    - Összefésülés
    - Egyben megy ki
- Hullámhossz
    - Optikai módon meg lehet csinálni
- Idő
    - meg van hogy ki mikor jön
- CDMA - Code Division Multiple Access
    - nincs megszorítás
    - hol a multiplex?
    - nagy zaj generálódik
    - ki lehet szűrni a sepeckó üzeneteket
    - 3G-nél jött használatba
    - minden állomás egyfolytában sugározhat
    - interferencia = lin. komb. az egyedi jeleknek
    - jeleket úgy kell kódolni, hogy ki lehessen majd olvasni
    - vektor összeg, báris, projektálás a bázisra és tá-dá csak az eredmény
    - töredék/csip vektor
    - minden állomásnak van chip
    - ezekre ortogonalitás kell, hogy vissza lehessen állítani
    - 1-et chippe kódoljuk
    - 0-t a chip komplemensével kódoljuk
    - két állomás cuccai összeadódnak
    - slotonként lesznek átfedések
        - összegvektor jelenik meg a hálózaton
        - eredő az összeg
    - dekódolásnál skalárisan szorozni kell a chippel
        - pozitivitását kell nézni
        - negatív - 0
        - pozitív - 1
        - nulla   - nem küldött semmit

- Fizikai réteghez tudni kell
    - nem biztosít semmi
    - lehet, h. rosszul értelmezi

## Adatkapcsolati réteg
- Feleadata, hogy kezelje a hibákat
- Statikus módszerek pazarolnak- erre nyújt megoldásokat
- Felkészülés löketszerűségre és változó felhasználószámra
- Keretek Átvitele
- Folyamvezérlés

### Keret képzés
- Nagy adatnál egybe küldésnél hibák lesznek
    - el kell dönteni, hogy jó-e
- Kis darabokban nem kell ez egészet újra küldeni hiba esetén
    - gyorsabb
- Nem akarjuk túlterhelni a vevőt
    - bufferba belefér
    - ha feldolgozta kor megy még keret
- Fel kell ismerni, hogy hol kezdődik és hol van vége
    - itt is lehetnek hibák
    - hol volt zaj, hol van keret
- Csomag kapcsolt hálózat
- Fajtái
    - Bájt alapú
    - Bit alapú
    - Idő alapú
- Fejlécben a keret hossza / bájt alapú
    - Annyi cucc kell
    - De ha pont az hibás akkor baj van
        - elcsúsznak a dolgok
    - szinkron elveszhet
- Bájt beszúrás
    - Flag bájt az eleje és vége
    - Kezelni kell az adaton belüli flag-szerű részeket
    - String-eknél hasonlóan működik programozási nyelvekben
    - ESC - escape
        - ESC-t is lehet ESC-elni kell
    - itt is lehet hiba
    - **teljesítmény**
        - általában legrosszabb eset
        - ha minden ESC vagy FLAG, akkor kétszer akkora lesz az adat 
- Pont-pont alapú protokollok: modem, DSL, cellular
- Bit beszúrás
    - FLAG szerű bitsorozat
    - bitminta az adatban
        - csak bit lesz beszúrva
        - kevesebb overhead
        - nagyobb hibalehetőség
    - pl HDLC protokoll
    - 11111 után be kell szúrni egy 0-t
        - 6 db 1-nél hiba van
    - **teljesítmény**
        - csupa 1-nél a legnagyobb overhead
- Óra alapúak optikai hálózatokban
    - Keret mérete fix hosszú
    - Keret küldés ideje is fix
    - 810 bájt
    - Táblázat szerű
    - Speckó kezdőminta
        - onnan tudjuk az idejét és az adat mennyiséget
    - Vége ki lesz paddelve
    - Tartalmazza hogy mennyi adat van - maradék padding
    - Elég biztonságos az optika, kevesebb hiba

## Hiba felügyelet
- Zaj kezelés
    - hogyan detektáljuk a hibát
    - hogyan állítsuk helyre
- Bithiba
    - hiba löketek vannak
    - van ami nem jó, de van ami jó
    - olyan sorozat aminek az eleje és vége hibás
    - m : védelmi övezet
    - csoportos hibán belül minimum m-nek kell jónak lenni, hogy szétszedjük két másiknak
- Naív hibadetektáló
    - adatból nem lehet eldönteni
    - kétszer kérünk egy keretet
        - ha mind2 egyenlő akkor minden jó
        - különben hiba
    - rossz ötlet
        - minden duplázva - sávszélesség feleződik
        - hiba védelem is gyenge
            - mindkettő lehet hibás
- Paritás bit
    - minden kis csoporthoz paritásbit (pl 7 bit (ASCII karakter) helyett 8)
        - az egyesek száma páros v. páratlan
    - kis overhead
    - max 1 bit hibát engedünk meg
        - nem stimmel valami
        - 2 bit hiba nem detektálható

## Hiba javítás
- Annyi extra infó, hogy helyre lehessen állítani
- Csak detektálás és újra küldés
- Melyik a jobb - nem egyértelmű
    - javítóban több extra infó, extra számolások, extra hardver igény
    - ha biztos a hálózat akkor jobb a ARQ (automatic repeat request)
    - rossz hálózaton jobb az FEC (forward error correction)
    - mobil hálózatok adaptívan működnek
        - gyenge és erős hibajavító között váltogat
    - vezetékes hálózatok inkább újra küldik
        - várni kell addig amíg van visszajelzés, hogy újra kell-e küldeni
- Hibadetektálás nélküli átvitel
    - pl hangátvitel
    - veszteséges visszaállítás

## Redundancia
- Extra infó
    - m adatbit
    - r redundáns bit
    - ki kell számolni, el kell küldeni
    - ha redundáns dolog hibásan jön akkor baj van

## Hamming távolság
- Kulcsszavak jók, a többi nem
- Hány bitben különböznek a dolgok
- Hibát akkor lehet felismerni, ha a bithibák sokasága nem állítja véletlen helyesre
- Halmaz min Ham-távát a legál és legál között lehet detektálni
    - minHam = k -> k-1 bithibát lehet detektálni
- d hiba javításásohoz 2d+1 minHam kell
    - legközellebbi jó volt az ami elromlott
    - ennek egyértelműnek kell lenni (a jó a rádiusza kisebb mint a távolsága a legközelebbi jótól)
    - ha nagyon sok romlik el akkor egy másikhoz lesz a legközelebb

- Ráta
    - S a legálisak
    - Rₛ = (log₂|S|)/n
    - Hatékonyság karakterisztikája
- Kód távolság
    - δₛ = d(S)/n
    - hibakezelési képesség karakterisztikája
    

# EA 5 2021.10.06

Az Internet törékeny  
Facebook meghalt. Nem mondtak sokat. Itt is valami router probléma volt. Nem tudta feloldani a domain-eket

## Redundancia
- Szükséges a hibakezeléshez
- Extra infó a hasznos adat mellett
- Hamming távolság használata
    - bitsorozatok távolsága
    - megfelelő távol kel lennie a jó és a rossz kulcsoknak (bitsorozatoknak)
    - hibás bitsorhoz a legközelebbi helyes bitsort vesszük
- az alatta lévő közegnek garantálni kell egy max hibaszámot, hibakorlátot
    - különben nem használható

### Hamming korlát
- C kód Hamming távolsága k
- |C| ∑_(i=0)^( ⌊(k-1)/2⌋ ) (n alatt az i) ≤ 2ⁿ

- egy X kód legfeljebb egy helyes kód van amihez (k-1)/2 távolságra van

## Hibafelismerés és javítás Hamming távolsággal
- Mekkora hiba lehet
- Ebből ki lehet számolni, hogy mekkora Hamming távolság kell a kódszavak között

## Paritás bit
- 7 bit adat, 8. bit a paritás
- Egy(páratlan) hibát tud detektálni
- Javítása:
    - Hamming kód
    - Kódszó bitjeit megszámozzuk
    - Keverjük az adat és redundáns biteket
    - Kettő hatvány pozíció az ellenőrző bit
    - Közötte az adatok
    - Paritás számítás
        - Más-más adatbitet figyel
        - átfedések is vannak
        - k=13 adatbit, ami =1+4+8 -ebbe a háromba tartozik bele
        - Ha az adott pozíción 1-es adat van akkor a bináris felbontásán növeli a paritást
    - Vevő oldalon 
        - ha a k-adik paritás nem jó akkor egy számlálóhoz adok egyet
        - ha a számláló 0 akkor jó
        - javítás:
            - k helyén a hibás cucc van
            - egy bit hiba javítható
            - kettő már nem

## Hibajelző kódok
- Netes protokollok tartalmaznak ilyet
- Vezetékes átvitel elég stabil, kevés hiba
- Kevés plusz adat
- Ha van hiba akkor újra küldjük a keretet
- CRC kód
    - Polinom kód, ciklikus redundancia
    - bitsorozat polinom, kettes maradékosztály testek felett
    - összes eszköz tudja a generátor polinomot
    - generátor polinomot nehéz készíteni
    - xᵍ*keret - elshiftelem a generátor fokával
        - xᵍ*M(x)
    - ezt leosztjuk a generátorral és a maradékot tartjuk meg
        - r(x) = xᵍ*M(x) mod G(X)
    - küldött adat a keret lesz eltolva és az előző eredménye  
        - T(x) = xᵍ*M(x) + r(X)
    - fogadó oldalon az eredmény osztható kell legyen a generátorral
        - E(x) a hiba
        - (T(x) + E(x)) mod G(x)
            - ha ez 0 akkor jó minden
    - Ha a hiba a generátor többszöröse akkor nem detektálható a hiba
        - ezért kell jó generátor
    - 1961-ben megmutatták, hogy ez harveresen implementálható könnyen
    - Ethernet 32 bites CRC
    - Más rétegben is előjön

## Folyamvezérlés, forgalomszabályozás
- Mit csinál hiba után?
- Gyors adó, lassú vevő probléma
- Engedély alapú: Vevő engedélyezi h küldjenek neki
- Sebesség alapú: mérnek és az alapján küldenek
- Rétegek üzeneteket adnak át egymásnak
- Gép hibákkal nem foglalkozunk
- Sok hibától eltekintünk
- Simplex komm. - egy irányú
- fél-duplex komm. - több irány lehet, egyszerre csak egy
- duplex komm. - szimultán két irány
    - két logikai alcsatorna, nem zavarják egymást
- Protokollok
    - Szimplex módszer
        - mindig mindenki készen áll, végtelene puffer, 0 feldolgozási idő, hiba nélkül megy
        - végtelen ciklusban küld a küldő
        - pufferba várja a vevő
        - ilyen nincs a valóságban
    - Szimplex megáll-és-vár protokoll (stop-and-wait prot.)
        - Mindig készen állnak
        - van feldolgozási idő
        - megvárja és utána küld
        - nyugta után küld újat
        - nyugta csomagot vissza kell küldeni
        - fél-duplex csatorna kell
    - Szimplex zajos csatornához
        - keretek elromolhatnak
        - küldő vár a nyugtára
        - ha nem jön akkor újra küldi
        - ha jön nyugta akkor újat küld
        - vevő hiba esetén nem küld vissza semmit
            - ezzel jelzi a hibát és újra fogja kapni
        - még ez sem old meg minden problémát
        - nyugta is meghibásodhat
            - ilyenkor kavarodás lehet
            - kétszer kapjuk meg ugyan azt a csomagot
            - duplikátumot kellene ellenőrizni - hálózati rétegben
        - csatorna kihasználtság
            - kis keretnél kicsi a kihasználtság
    - Alternáló bit protokoll (ABP)
        - egy bites számláló bevezetése 
        - keretbe is sorszám
        - alternál a sorszám
        - vevő sorszámra vár
        - ha nyugtát kap akkor másik számmal küld
        - így, ha kétszer ugyan az a számláló jön akkor a nyugta nem ment vissza
            - újra küldjük az előző nyugtát
         - Kihasználtság
            - átérés: T_packet + d
            - vissza: T_ack + d
            - össz idő hiba nélkül az előző kettő összege

            - n = T_packet/(T_packet+d+T_ack+d)
            - minnnél nagyobb csomaggal lesz jobb a kihasználtság
            
            - Javítás
                - Küldünk több keretet
                - Jönnek a nyugták
                - Több dolgot kell bufferelni
                - Pipeline teknika
                - Így lehet túlterhelés
                    - lehet max-ot bevezetni az egyben fogadható keretszámra
                    - várakozni kell
    - Csúszó ablak protokoll 
        - ennek az általánosítása az ABP
        - javítja a kihasználtságot
        - n keretet lehet egyben fogadni
        - küldő max n keretet küldhet nyugtázatlanul
        - több sorszám, ciklikusan nő
        - nyugtákban is számít a sorszám
            - kumulatív nyugta is lehet
                - az összes annál kisebb sorszámú megjött
                - ha nyugta elveszik akkor a következő ezt helyettesíti
                - nyugta sorszám az, ami még nem jött meg
        - Az ablak tolódik
            - ha az első elveszik akkor újra kell küldeni az összeset a kumulatív nyugta miatt
            - olyan nyugtát küldök, ami még nincs meg
            - majd akkor küldöm a nagyobbat, ha a hiányzó is megjön
            - ami megjött azt megtartja a fogadó és egyszerre nyugtázhatja az egészet, ha megjön a hiányzó
            
# EA 6 2021.10.13

## Adatkapcsolati réteg és MAC alréteg

### Visszalépés N-el
- Go back N
- mennek a csomagok
- ha hiba van akkor sokat kell újra küldeni
- vételi oldalon kicsi puffer

### Szelektív ismátlás
- SRCK
- Hiba esetén jelzi, hogy mi nem volt jó és csak azt küldik újra

## Ethernet keret
- MAC azonosító, átkonfigurálható
    - lokálisan azonosítja

## Közeg hozzáférés
- Ethernet és Wifi is többszörös hozzáférés
- Közegen több résztvevő osztozik
    - Adatszórás
- Egyidejű átvitel ütközés
    - Lényegében meghiúsítja az átvitelt
- Követelmények a Media Access Control (MAC)
    - szabályok a közeg megosztásra
    - ütközések detektálása és elkerülése

## MAC alréteg
- Dinamikus felosztási protokollok
    - verseny vagy ütközés alapú protokollok (ALOHA, CSMA, ..)
    - verseny mentes protokoll (bittérkép-alapú)
    - korlátozott verseny 
- Dinamikus csatornakiosztás
    1. Állomás modell
        - N terminál/állomás
        - valószínűség, hogy Δt idő alatt csomag jön: λΔt, 
    2. Egyetlen csatorna
        - Minden állomás egyenrangú
        - Egy csatornán minden kommunikáció
        - Minden állomás tud küldeni és fogadni
    3. Ütközés feltételezés
        - Ha két keret egy időben megy akkor kiütik egymást
    4. Időmodell
        - Folytonos
        - Diszkrét
            - szlot elején lehet küldeni
    5. Vivőjel értékelés
        - El lehet dönteni, hogy valaki használja-e a csatornát
- Terhelés (G)
    - A protokoll által kezelendő csomagok száma egy időegységben
    - G>1 : túlterhelés
    - A csatorna egy kérést tud elvégezni
- Ideális eset
    - Ha G<1, S=G
    - Ga G≥1, S=1
    - Ahol egy csomag küldése egy időegység

- Tiszta ALOHA
    - hawaii egyetem 70-es évek
    - Ha van adat akkor elküldi
    - Alacsony költségű, egyszerű
    - Mindent nyugtáz
    - Vár a nyugtára, idő után újra küldi
    - Teljesítmény elemzés - Poisson eloszlás
        - Pₖ(t)=((λt)ᵏe^(-λk))/k!
        - T_f = keret-idő
        - S : sikeres átvitelek száma
        - G : összes kísérlet
        - D : küldés és vétel közötti idő
        - Feltesszük:
            - Minden keret azonos méretű
            - A csatorna zajmentes, csak ütközési hiba van
            - A keretek nem kerülnek sorokba
            - A csatorna egy Poisson folyamat
    - S = S(G) = G × (A "jó" átvitelek valószínűsége)
    - Sebezhetőségi idő : 2T_f
    - Sebezhető idő alatt más ne küldjön

- Réselt ALOHA
    - Diszkért időmodell bevezetése
    - Sebezhetőségi idő fele akkora lett
    - 0,37% kiszolgálás, egyszerre 1

- Adatszóró (bradcast) Ethernet
    - Adathordozó teknológia
    - Carriar Sense Multiple Accesss
        - belehallgat a csatornába és eldönti, hogy használhatja-e
        - 1- perzisztens CSMA protokoll
            - mindenki hallgatózhat
            - perzisztens módon várjuk, hogy mikor lesz szabad a csatorna
            - ha szabad akkor egyből küld
        - Non-perzisztesn CSMA protokoll
            - folyamatos időmodell
            - mohóság kerülése
            - mindenki hallgatózik
            - random időt vár
            - lehet, hogy felszabadul a csatorna de még vár mert random ideig kellett
        - p-perzisztens protokoll
            - Diszkrét modell
            - Kövi időrésig vár

        - CSMA/CD - collision detection
            - Nehéz dolog
            - Egymástól távoli eszközök
            - Mikor elkezdi akkor még nem használta senki, de közben elkezdte
            - Közben detektálni kell
            - minimális keretméret - hálózat hosszától függ
            - csomag legyen nagyobb, mint a propagációs késés
            - min_keret = ráta(b/s) * 2 * d(s)
                - ethernet: 64 bájt
                - 10 Mbps
                - (64B * 8) * (2 * 10⁸mps) / (2 * 10⁷) ≈ 5 km hosszú
                - de ma már nincs ütközés
            
# EA 7 2021.10.20

## Mit kell csinálni ütközés detektálásnál?
- Binary Exponential Backoff algoritmus
    - Mekkora lehet a terhelés
    - Ez az érték alapján vár és újra küld
    - Szinkronizáció megtörése állomások között
    - k ∈ [0, 2ⁿ-1], n ütközések száma
    - várunk k egységet
    - n max 10, 16 sikertelen próba után eldobja a keretet
- max_keret
    - túl nagy akkor sok hiba lehet
    - ethernet:
        - default: 1500 bájt
        - adatközpont: jumbo frame: 9000 bájt
    - infiniband
        - sokkal nagyobb teljesítmény
        - HPC-ben külön tár és számoló egység 
        - közöttük vannak infiniband-ek
        - 64 KB frame-ek

## Ütközésmentes protokollok
- Ütközések hátráltatják
- Állomások megszámozva
- Réselt időmodell
- Nem történhet ütközés
- Technikai megoldás nehezebb
- Bittérkép protokoll
    - Helyfoglalási periódus és adatküldési periódusok
    - Helyfoglalás
        - Időosztás- résztvevők száma szerint
        - Bitmap réseiben az adott időállomás jelzett-e h van igénye
        - Ezt mindenki tudja
    - Adatidőréseket a bejelentetteknek
        - Ebben az időben tudnak küldeni
    - Újra helyfoglalás és küldés
- Bináris visszaszámlálás protokoll
    - Egy időrésben több állomás is ad 
    - Ki kell használni a konstruktív interferenciát
    - Mindenki sugározza a bitjét
    - Mindig a legnagyobb azon nyer
    - kiéheztetés lehetséges
- Javítás
    - Azonosítók permutálása
    - Aki nyert az kapja a legkisebbet
    - A többi növeli
    - Azé a legnagyobb, aki a legrégebb kapott hozzáférést
    - *Mock és Ward módosítás*

## Korlátozott versenyes protokollok
- Lehet ütközés
- Feloldás: korlátozzák a küldők számát
- Ötvözi az előző két családot
- Kis terhelésnél a verseny során nincs interferencia és gyorsabb
- Adaptív fabejárás protokoll
    - Nem hálózatból jön
    - Vérvizsgálatból jön az ötlet
    - Szifilisz vizsgálat - 1943
    - Feltették, hogy nem mindenki beteg
    - Kis számú beteg
    - Költséges a teszt
    - Kevés tesztet akartak és minden beteg megtalálása
    - Embercsoportoktól vesznek mintát, összekeverik és úgy vizsgálják
    - Ha negatív akkor mindenki negatív
    - Ha pozitív akkor kisebb csoportra bontás és úgy
    - Addig amíg egy emberhez nem jutnak
    - Átment a hálózatokhoz 1971-ben
    - Minden tesztel egy időrést elbukunk
    - Állomásokat csoportosítjuk
    - Csoportot bontjuk az ütközés szerint
    - Részcsoport küldhet
    - Ha nincs ütközés akkor jó
    - ha van akkor részcsoport és ők küldenek

## Hogyan kötünk össze lanokat?
- Bridge korlátozza az ütközéseket
- Layer 2 eszközök
- Switch-ek is Bridge-ek, de Bridge többet tud
- Ütközési tartomány csökkentése
- Teljes transparencia
- Plug n play
- Funkciók
    1. Keretek továbbítása
    2. (MAC) címek tanulása
    3. Feszítőfa (Spanning Tree) Algoritmus (a hurkok kezelésére)
- Továbbító tábla 
    - MAC cím
    - Port
    - Kor
        - Dinamikusan változik
        - Jönnek mennek az eszközök
        - Ha rég nem frissül akkor elfelejtjük
- Kézi beállítás
    - Időigényes
    - Hiba lehetőség
    - Nem dinamikus
- Címek tanulása
    - Kitől honnan jön forgalom
    - Frame feladóját megnézi
    - Továbbító táblába bekerül
    - Ha nincs a táblában a cél
        - broadcart
        - minden portra kiküldi
- Körökben cirkulál a csomag, rossz irányt tanul meg
- Feszítőfa algoritmus
    - Lefed minden csomópontot
    - Nincs benne kör
    - Elosztott algoritmus
    - Egymás közötti kommunikáció
    - Gyökér hotspot
    - BPDU - config üzenet
        - BridgeID, GyökérID, Út költség a gyökérhez
        - Lehet A gyökérID-t frissíteni az út hossza a lapján
        - Kezdetben minden állomás felteszi h ő a gyökér
- Switch-nél
    - Minden port egy hosthoz
    - Vagy kliens terminál
    - Vagy másik switch
    
# EA 8 2021.11.03

- Switch-nél mindig 2.-es réteget megvalósító eszköz van összekötve
    - Így nem kell CSMA
    - Hardware is egyszerűsödik
    - Full duplex linkek
    - Feloldja a hurkokat
- Nem jól skálázható
    - Spanning tree nem jó mert 
        - a fa elágazásainál túl nagy terhelés lenne
        - a faság miatt csomó él kiesik
        - nem tesz különbséget a linkek mérete között
    - Továbbítót tábla is primitív
        - Síktopológia
        - Hatalmas méret lehet
        - Ha nincs a táblán, akkor az elárasztás nem jó technika
        - Lassú keresés
- Az IP és a Hálózati réteg oldja meg ezt a problémát

## Hálózati réteg
- Fő funkció:
    - Eszköz lehet bárhol a világon
    - Ha van nete, akkor lehet nemi csomagot küldeni
    - Forgalom irányítás
- Forgalom irányítás
    - Táblák feltöltése, útvonalkereső algoritmusok
    - Továbbítás
- Elvárások
    - Robosztus, helyes, egyszerű
- Algoritmus osztályok
    1. Adaptív
        - topológia és forgalom alapján dönt
    2. Nem-adaptív
        - offline meghatározás

### Adaptív algoritmusok
1. Honnan kap infót?
    - Szomszédok, mindenki
2. Mikor változtatja az útvonalat?

- Optimalitási elv
    - I-től K-ig optimális útvonal
    - J I és K között van akkor J-K is I-K-n lesz
    - Egy csúcsra lehet nyelőfát csinálni
    - Meg lehet határozni a legjobb útvonalat
    - Hálózat gráf ábrázolásával lehet tanult algoritmusokat alkalmazni
    - Súlyozás pozitív értékeket rendel

- Dinamikus algoritmusok két csoportja
    - distance vector routing --- távolságvektor alapú
    - link-state routing --- kapcsolatállapot alapú

- Távolságvektor alapú
    - Nincs központi irányítás
    - Táblázatokat a szomszédok alapján töltjük ki
    - Elosztott Bellman-Ford algoritmus
        - Gráfban a legrövidebb utak fája a célállomáshoz
        - Csomópontok számaszor kell végigmenni az összes élen
        - Párhuzamosan történik az élbejárás
            - Minden router bejárja a környezetét
            - Távolságvektorok cseréje
            - Minden állomáshoz az általa ismert legrövidebb út
            - Ha a szomszéd ismer rövidebb utat, akkor a szomszédon keresztül rövidebb utat találtunk
            - Ha nincs változás, akkor megáll az algoritmus
            - Addig amíg valami meg nem változik
                - Jó hír gyorsan terjed
                - Rossz hírrel sok munka van, mert észlelnie kell a rendszernek majd újra kiszámolni a legrövidebb utakat
                    - Ez a távolságvektor protokoll hibája, virtuális köröket hoz létre
                    - Leválasztásnál Végtelenig növeli
                    - Él növelésnél addig növeli körkörösen amíg a növelt lesz a legjobb
                    - Inkonzisztens állapotba kerül a rendszer
                - Megoldás a rossz hírre
                    - Tőlünk tanult rossz infót kapjuk vissza
                    - Split horizon with poisoned reverse
                        - Ha tőle tanultam, akkor végtelent küldök -- nem kell számításba venni
                        - Ha B-nek küld, akkor ahol Next az B ott végtelen súlyt küld
                    - Így gyorsabb feldolgozás
    - Routing Information Protocoll
    - Kevésbé elterjedtek

- Kapcsolatállapot alapú
    - Eltérő sávszélesség figyelembevétele
    - Dijkstra módosított változata
        - Cél prior sorba
        - Ha kiveszünk a sorból, akkor az a csúcs kész
        - Kiterjesztjük
            - Berakjuk a tőlünk vezető úttal
    - Mindig a legkisebb csúcsot terjesztem ki
    - Elosztottan nem lehetne célzottan választani
    - Adatgyűjtés elosztottan
    - Algoritmus lokálisan, nem elosztottan
    - Link-State advertisement - szétküldi mindenkinek
        - Router, környezete és költsége
        - Ebből ki lehet rakni az egész topológiát
        - Erre már mindegyik tud egy Dijkstra-t futtatni
        - Sorszámozva a csomag, minden router növeli
            - ha visszaér ugyan azzal a sorszámmal, akkor már nem küldi tovább
    - Protokollok
        - OSPF
            - Céges adatközpont
            - Nagy overhead
            - Jól konfigurálható
            - IP csomagok
            - Átfedő területekre bontás
            - Area0 a központ
        - IS-IS
            - Internet szolgáltatók használják
            - Tömörebb, kisebb overhead
            - Részhálózatokra bontható a nagy hálózat
            - Nem IP csomagok
            - 2-Szint
            - Level2 a gerinchálózat

- Két Router között többféle adatkapcsolati réteg is lehet, több eszközzel
- Falyamok vannak (Kliens - Szerver kommunikáció)

### Forgalom irányítás
- Unicast
    - Legegyszerűbb
    - Csomag két végpont között
    - Forrás cím, cél cím, IP azonosító
- Adatszórás
    - Broadcast "mindenhová"
    - A lokális csoporton belül
    - Több megoldás
        1. Kölön csomag mindenkinek, ugyanazzal a tartalommal
            - Nem igazi funkció
            - Csak elfedés
            - Ugyan azt küldök mindenkinek
            - n * csomagméret
        2. Elárasztás
            - Kétpontos kommunikáció nem használható
        3. Többcélú forgalomirányítás
            - Cél lista van egy cél helyett
            - Külön listákkal több felé is mehet
            - Listákat frissíteni kell
        4. Forrás router-hez tartozó nyelőfa használata
            - Nyelőfa visszafele használata
            - Broadcast üzenetet a forrásnak nem adja, a többinek igen
        5. Visszairányú továbbítás
- Többes-küldés (Multicasting)
    - Nem mindenkinek, de egy csoportnak küldöm
    - PL IPTV - akinek van ilyene azoknak mind elküldöm a TV adást
    - Minden élen csak egyszer megy ugyan az a csomag
        - Nem kell minden eszközhöz külön csomag
    - Dinamikusan változhat a csoport tartalma
    - Szervernek csak egyszer kell legenerálni a csomagot
    - Multicast képes router fogja tudni, hogy kinek kell a csomagot küldeni
    - Csoporthoz lehet csatlakozni, csoport azonosító kell csak
- Hierarchikus forgalomirányítás
    - Router táblázat növekedésének elkerülése
    - Hálózat szétbontása, alhálózatra
    - PL telefonszám:
        - Azonosító nem random
        - Országszám, Körzetszám, stb
        - Országon belül döntik el, hogy melyik körzetbe kell küldeni
        - Körzeten belül döntik el, hogy hova, stb
    - Interneten is ilyen hierarchia

## IPv4
- Internet alap hálózati protokollja
- Hiányosságai miatt jött létre IPv6
    - DE még nem vette át a helyét
- Fejrésze, 5*32 bit szó + option header-ek
    - Forrás cím, cél cím 
    - élettartam, protokoll, ellenőrző összeg
        - élettartam: ugrások száma
            - ha 0, akkor eldobódik a csomag
        - protokoll: mi van beágyazva a csomagba
        - ellenőrző összeg: check sum, CRC
    - azonosítás, DF, MF, darabeltolás
        - azonosítás: ip csomag darabolására használjuk
    - Verzió, IHL, Szolgáltatás típusa, (router tud jelezni, ha túlterhelődik, 2 bit), teljes hossz
- Cím is túlterhelt fogalom
    - Mi a címed? sok mindent jelenthet
- Címzési struktúra
    - Sík - Flat
        - Minden host-nak 48-bites sorozat, random
        - A routernek minden host-hoz bejegyzés kell a táblához
            - nagy, lassú, stb
    - Hierarchikus
        - Adott területre kell csak nézni
        - Cím kiosztás is lokálisan történik
        - Feladatkörök szeparálása
        - Routing táblák kezelése
            - Csak pár bit kell ahhoz, hogy a megfelelő helyre tovább küldjem
            - Az a hely meg magában tovább küldi
            
# EA 9 2021.11.17

## IP cím
- Több hierarhia szint

### IPv4
- 4 bájtos ip cím
- Decimális felírást szoktak használni
- | Hálózat | hoszt |
- Routing táblában elég a hálózat azonosító útja

#### Osztály alapú IP címeket osztogattak
- IP blokkok
- Azon belül szabadon oszthatja ki a tulajdonosa
- Blokkok méretére nem gondolták át
- Osztályok
    - A
        - | 0 | 7 bit | 27 bit |
        - Nagyon nagy címtartomány
        - 2⁷ ilyen szervezet lehet
        - Azon belöl 2²⁷-en hoszt lehet
    - B
        - | 10 | 14 bit | 16 bit |
        - több ilyen hálózat lehet
        - kevesebb hoszt, de így is sok
        - ELTE is ilyen
    - C
        - | 110 | 21 bit | 8 bit |
        - sok ilyen hálózat lehet
        - 254 host max
        - Közepes méretű cégnek ez kevés
    - D
        - multicast címek
        - | 1110 | többesküldési cím |
        - iptv, ilyesmi
- Speciálisak:
    - 0...0 - Ez egy host
    - 0..0 | host - hoszt eg yhálózaton
    - 1...1 - adatszórás helyi hálón
    - háló | 1...1 - adatszórás adott hálózaton
    - loopback
- Amíg el nem érjük a hálózat központi routerét addig elég a hálózat azonosító
- Alhálózatok kialakítása
    - kevesebb bejegyzés a központi routerbe
    - Alhálózati maszk használata

### CIDR - cyder
- Osztályok lecserélése
- C osztályú címek agragálása
- Egymás utániakat egybe osztják ki, amennyi kell
- Nem csak a háló azonosító kell hanem a maszk is
    - ez a kettő kell az azonosításhoz
- Next hop ismert
- Maszkolás és összevetés
    - ha nincs találat, akkor a leghosszabb illeszkedés feléküldi
- `Kernel IP routing table`
    - Destination - Cím
    - Gateway - next hop
    - Genmask - mask

### NAT
- IP cím nagyon gyorsan fogy
- Network Address Translation
- Otthoni routerekben van NAT
- Háztartás netforgalma egy ip-val megy majd ki
- De otthon lehet több számítógép
- 3 IP címtartomány
    - Globálisan nem routolható
    - Privát tartományokon belül
    - 10.0.0.0/8 - sok hoszt
    - 172.16.0.0/12 - közepes
    - 192.168.0.0/16 - 65536 host
        - ez szokott lenni otthon
- Nem csak az ip van,
    - Ki volt a feladaó
    - TCP vagy UDP
    - Milyen portról
    - Lecseréli a címet és a portot
    - Megjegyzi ezt az átalakítást
- Mobil hálózatban is NAT-olás van
    - nagyon dinamikusan változik
    - IP pool-ból lehet választani
- Sérti az IP architekktúrát
- De valahogy meg kell oldani az IP címek számának problémáját

## IP Fragmataion

### MTU
- Maximális csomagméret
- Heterogén hálózatot feltételeztek
- Valóságban homogénebb mint gondolták
- Általában MTU = 1500 bájt
- Szét kell darabolni a nagyobb csomagokat
- Vissza kell állítani az eredeti csomagot
- Azonos azonosító köti össze őket
- Flagaknél van utolsó csomag jelölő
- Offset - mi az eredetiben a kezdő indexe a darabkának
- Költséges módszer
- Dont Fragment Flag - eldobja ha darabolni kéne
- Felderítés - MTU discovery
    - Csükkenti a csomag méretet
    - Nem kell fregmentálni
- Adatközpontokban nagyobb - pl MTU = 9000





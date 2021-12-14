# Telekommunikációs hálózatok EA 1 2021.09.08

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
- Ethernet - hálókártya, UTP kábel
- Mobil - okosteló
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
        - Terhelésfelmérés

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
        - igény szerinti

# Telekom EA 2 2021.09.15

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
            - Pl.: minden bájthelyesen megérkezzen (kép dokumentum, valósidejűség fontosabb (live video, csomagvesztést tudja kezelni)
            - TCP(biztos de sok overhead), UDP(levelezés szerű), QUIC(Google cucc)
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
                - Fizikai címzés ilyemi

        - Hálózati
            - SZ
                - Csomagtovábbítás
                - Routerben a keretek tovább küldés
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
                - Adatkonverzió rendszerek között
                - Encoding, kódolás, konverzió
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
    - pl.: wifi -> Ethernet

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
- Fourier sorokkal lehet modellezni a valóságot
    - sin/cos-ok összegeikén állnap össze a jelek
    - lehet közelíteni a szögletes jelhez hullám függvényekkel
- approximált jel érkezik meg
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
    - Küldő oldalon kell egy összefésülő eszköz : **multiplexer**
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
    - vektor összeg, bázis, projektálás a bázisra és tá-dá csak az eredmény
    - töredék/chip vektor
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
- Feladata, hogy kezelje a hibákat
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
    - ha feldolgozta, akkor megy még keret
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
    - 1961-ben megmutatták, hogy ez hardveresen implementálható könnyen
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
            - minél nagyobb csomaggal lesz jobb a kihasználtság
            
            - Javítás
                - Küldünk több keretet
                - Jönnek a nyugták
                - Több dolgot kell bufferelni
                - Pipeline technika
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
        - Non-perzisztens CSMA protokoll
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

## Hogyan kötünk össze LAN-okat?
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
    - Ha van nete, akkor lehet neki csomagot küldeni
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
- Folyamok vannak (Kliens - Szerver kommunikáció)

### Forgalom irányítás
- Unicast
    - Legegyszerűbb
    - Csomag két végpont között
    - Forrás cím, cél cím, IP azonosító
- Adatszórás
    - Broadcast "mindenhová"
    - A lokális csoporton belül
    - Több megoldás
        1. Külön csomag mindenkinek, ugyanazzal a tartalommal
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
- Több hierarchia szint

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
        - | 0 | 7 bit | 24 bit |
        - Nagyon nagy címtartomány
        - 2⁷ ilyen szervezet lehet
        - Azon belül 2^24-en hoszt lehet
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
- C osztályú címek agregálása
- Egymás utániakat egybe osztják ki, amennyi kell
- Nem csak a háló azonosító kell, hanem a maszk is
    - ez a kettő kell az azonosításhoz
- Next hop ismert
- Maszkolás és összevetés
    - ha nincs találat, akkor a leghosszabb illeszkedés felé küldi
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
    - Ki volt a feladó
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
    - Csökkenti a csomag méretet
    - Nem kell fregmentálni
- Adatközpontokban nagyobb - pl MTU = 9000

# EA 10 2021.11.24

## Vizsga
- online vizsga
- teszt és esszé kérdés
- teszt rész min 50%, 11/20
- decemberben egy, januárban több

## Fogyó IPv4 címek
- 2^32-en a max cím ~ 4 miliárd
- IP blokkok már ki vannak osztva

## IPv6
- 1998-tól
- 128 bites cím
- 4.8 * 10^28 cím/ember
- Cím formátum
    - hexadecimálisan szokták írni, 8 csoport
    - vannak egyszerűsítések
    - kezdeti nullákat el lehet engedni, max 3
    - 0000 blokkokból álló sorozatokból egyet el lehet hagyni
        - 20:0:0:0:32 -> 20::32
- Lokál cím, loopback cím
    - ::1
- Fejléc - IPv4 kétszerese
    - Version
    - DSCP/ECN
    - Flow Label
    - Datagram Length
    - Next Header - belső protokoll
    - Hop Limit
    - Sourse IP address
    - Dest IP address
    - hiányzik
        - fejléc hossza hiányzik - nect header láncolás miatt nem kell
        - checksum - nem igazán hasznos
        - identifier, flags, offset
            - nincs fregmentáció
            - MTU felderítés
- Internet súlypontjai megváltoztak
    - Hálózatok sokkal homogénebbek, mint gondolták
    - A routing költsége domináns
    - Source Routing
        - A küldő határozza meg az útvonalat
    - Mobil IP
        - Az állomások magukkal vihetik az IP címüket más hálózatba
        - Forrás routing használata a csomagok irányításához
- Az átálláshoz a routereknek is át kell állni
- Tunnelek
    - A tunnel elején becsomagoljuk a az IPv6 csomagot IPv4-be
    - A végén meg ki
    - Előtte/utána mehet IPv6-ként

## Internet Routing
- Első szint - autonóm rendszer, belső üzemeltetés, felügyelet
    - Belső routing egyszerűbb
    - Legkevesebb hop általában a jó
    - Link state is jó
- Második szint - interdomain szint
    - itt már nem működnek az egyszerű módszerek
    - BGP router
        - belső és külső router is
        - Határ router
    - Más belső hálózatán menő forgalomért fizetni kell
    - El lehet rejteni a belső hálózatok szerkezetét
    - AS szám 
        - autonóm rendszerek azonosító száma
    - rugalmas útvonalválasztás
        - változik az optimális útvonal
    - protokollok
        - path vector routing
        - distancce vector fejlesztése kb

### BGP
- eltérő célok
- fogalom korlátozás
- hálózatok
    1. csonka hálózat
        - perem hálózat
    2. Többszörösen bekötött hálózat
        - alkalmas átmenő hálózatként
        - de nem engedélyezett
        - inkább stabilitási okok miatt van
    3. Tranzit hálózatok
        - harmadik fél csomagjait vezetik
        - összekötik az autonóm rendszereket
- TCP protokollokat használnak
- Útvonal hirdetések
- Megoldja a count to infinity problémát
- Customer - Provider kapcsolat
    - Customer fizet a providrenek
    - Szolgáltatón kersztüli forgalom
- Peering viszony
    - Egymásnak küldeni
    - kb egyenrangúak
    - Bérmentve cserélnek forgalmat
    - hálózatban, vagy ügyfelében generálódik a forgalom
    - minden szereplő ki lesz fizetve, vagy szolgáltatást kap
    - több peer-en nem megy keresztül
        - a közbenső peer-ek nem kapnának pénzt
            - csak terhelést
        - emiatt peering linkek csak kettő pper között van
        - ha ilyenre lenne szükség, akkor van mégy egy nagyobb provider
    - a legfelső szinten minden peer között van kapcsolat
        - Tier-1 ISP peering
- Routing táblában prefix és milyen útvonalon érhető el

## Path vector protocol
- AS útvonalak
- útvonal vektorok
- döntés, hogy melyik szomszédnak milyen útvonalat hirdet meg
- Legrövidebb út nem egyértelmű
    - Legrövidebb autonóm rendszer útvonal nem biztos, hogy fizikailag is a legrövidebb
- Hot potato routing
    - gyorsan továbbadja a csomagot valaki másnak
    - kisebb hálózatnak jobb
    - ne terhelje a rendszert
- Cold potato routing
    - minél tovább maradjon a saját hálózatán
    - nagy szolgáltatónak ez jobb
- Szabályok importálása
    - mindenhonnan van cucc
    - provider, peer, belső
- Exporting routes
    - Customereknek minden
    - Peereknek a belső dolgokat
    - Providerekenk is a belsőket
- eBGP
    - külső 
- iBGP 
    - hálózaton belüli kapcsolata a BGP-knek
- BGP Routing tábla
    - nagyon nagy
    - bizonyos routerekben már nem fért el a tábla
    - szerencsére ezt orvosolni tudták

## Protokollok, amik Alkalmazási rétegben vannak de inkább Hálózati dolgok
- ICMP
    - elérhetetlen cél
    - időtúllépés 
        - erre csak korlátozottan van példa
        - traceroute ezt használja
    - paraméterprobléma
    - ping
        - visszhang küldése
        - válaszidő és elérhetőség mérése
- **ARP**
    - Ez köti össze a MAC címet az IP címmel
    - linux - arp paranccsal ki lehet listázni az arp táblát
    - ha nincs a táblában
        - arp üzenet
        - megkérdezi a lokális hálózaton, h kié az ip
            - visszaküldi a MAC címét
        - feladó tudni fogja, berakja a tálájába
        - ha kívül van az ip cím
            - next hop router címét rakja a táblába
- DHCP
    - az elején egy csomó konfig üzenet megy
    - Subnet, netmask, statikus ip
- VPN
    - több különböző helyszín összekötése mintha egy hálózat lenne
    - bérelt vonalak kihúzása
        - dedikált vonal
        - drága
        - más nem éri el
    - virtuális linkek
        - nem tudja értelmezni, hogy mi megy ott
        - titkosított forgalom
        - tunnel
            - tunnel végpontok
            - otthon lehet a helyi eszköz is 
            - telephelyen a fő router
            - végpontok tovább csomagolják a csomagot
            - az is benne van, hogy melyik tunnel végpontba megy
            - a belsejét titkosítja
            - kriptográfia
            - IPSEC
                - NEW IP header
                - ESP header
                - titkosított rész
                    - Old IP
                    - TCP
                    - Payload
                - Authentication (HMAC)
            - megbízható
            - nehezen feltörhető
        - olcsóbb

- Jövőhét - szállítói réteg
- Utolsó hét - milyen lesz a vizsga

## EA 11 2021.12.01

## Szállítói réteg
- Adatfolyamok demultiplexálása
- Hosszú élettartamú kapcsolat
- Jó kihasználtság
- Megbízható adatátvitel

### Multiplexálás
- Datagram hálózat
    - nincs áramköri kapcsolás
- A kliensek számos alkalmazást futtathatnak
- IP fejléc "protokoll" mezője kicsi
- Demultiplexálás megoldása a szállítói rétegben
- Port szám lesz az egyedi azonosító
    - Az alkalmazás azonosítója
- Egy szerver számos klienssel kommunikálhat
- Végpontok azonosítása , kapcsolat azonosítás
    - < src_ip, src_port, dest_ip, dest_port, protocol >
    - five_tuple

### UDP protokoll
- Egyszerű
- 8 bájtos fejléc
- Forrás port, cél port, adat hossz, kontrollösszeg
- semmilyen garancia arra, hogy átment a csomag
    - nem biztos, hogy átment
    - hibák saját kezelése
    - pl video átvitel, ha nem megy át minden csomag, akkor lehet helyettesíteni, csak rosszabb lesz a minőség
        - valós idejű alkalmazásoknál
- TCP javításai az alkalmazási rétegben
    - Google::QUIC protokoll
        - UDP, alkalmazási rétegben csinálja meg a csomagok újra küldését, hiba kezelést
    - RTMP - pl videó
- TCP után vezették be
    - TCP-nél fájlok küldése volt
    - ott nem fért bele a hibás átmenetű

### TCP
- 20 bájtos fejléc + options fejléc
    - forrás port, cél port
    - sequence number
    - acknowledgement number - mindent nyugtázni kell
    - hlen, flags, advertised window - vevő megmondhatja, hogy hány bájtot fogadhat
    - checksum, urgent pointer
    - options
    - soronként 32 bit
- Először kapcsolat kiépítés van
    - sorszám random számról indul
    - three way handshake
    - kliens kezdeményez: SYN < SeqC, 0 >
    - Szerver válaszol: SYN/ACK < SeqS, SeqC+1 >
    - Kliens nyugta: ACK < SeqC+1, Seq+1 >, ez már szállíthat adatot
        - pl http get request
- Flagek, fontosabbak
    - SYN - szinkronizáció, kapcsolat felépítésénél fontos
    - ACK - ez nyugta-e
    - FIN - kapcsolat lezárása
- Kapcsolat építési problémák
    - zavar, ezért kell a random kezdés idő
    - hamisítás, jó random kell hozzá
    - állapot kezelés
        - minden SYN helyet foglal a szerveren
        - Alapból 2 percig tart egy kapcsolatot, he nincs több kapcsolat
        - Meg lehet tölteni a szerver memóriáját
            - SYM flout, DOS támadás
            - Megoldás pl coocke sym szám
                - csak akkor foglal memóriát, ha kliens ack is megvan
        - kapcsolat bontásnál van a memória felszabadítás
        - maradhat félig nyitott kapcsolat
            - kliens fin
            - server ack
            - server data
            - kliens ack
            - server fin
            - kliens ack
            - teljesen async processek
- TCP-ben van újra küldési mechanika
- Sorszámok tere
    - absztrakt bájtfolyam
    - 32 bites érték, körbe fordulhat
    - bájtfolyamot segmens-ekre bontjuk, tcp "csomag"
    - Max Segment size bemásolja
    - Úgy kell beállítani, hogy ne legyen szegmentálás
    - Szegmenseknek is egyedi sorszám
        - adat kezdetének jele
        előző szegmens hosszával növelődik
- Kétirányú kapcsolat
    - tudjuk, hogy mit várunk és mit küldünk
- Folyam vezérlés
    - ne terheljük túl a fogadót
    - hálózatot se terheljük túl
    - puffer méret jelezhetjük az advertised window-al
    - hány nyugtázatlan bájtot lehet küldeni
    - csúszóablak
    - advertised window időben változhat
    - egyszerre küldhető több szegmens
    - nyugta csúsztatja az ablakot
- Átviteli idő
    - függ az ablak mérettől és az átfordulási időtől
- Nyugta
    - Minden csomagra
    - Kumulált
    - Negatív - NACK
    - Szelektív - SACK
    - tcp-nél kumulált alapból, és SACK szokott még lenni
        - SACK TPC
        - újra küldések számát lehet csökkenteni
        - most már alapból be van kapcsolva
- Buta ablak szindróma
    - kis adat, nagy fejléc
    - több erőforrás a header-ökre mint az adatra
    - emiatt egy pufferbe gyűjtjük az adatokat, és ha elég sok, akkor van elküldve
    - Nagel algoritmus
        - ablak ≥ MSS és adat ≥ MSS
            - küldés
        - különben, ha van nem nyugtázott adat
            - várakozás
        - ha nincs nyugtázatlan csomag, akkor elküldjük a kisebb adatot is
    - Ha azonnal kell küldeni, akkor ezt ki lehet kapcsolni
- Hiba detektálás
    - ip, tcp és adat-re checksum CRC
    - sorszámok segítik a sorrendhelyes átvitelt
        - duplikáltak eldobása
        - hiányzók jelzése
    - elveszett csomagok detektálása
        - időtúllépés
        - szükséges RTT becslés (fordulási idő, késleltetés)
        - RTO alul becsülve
            - felesleges újra küldés, pazarlás
        - RTO felülbecslés
            - túl sok várakozás a nyugtára
            - kevésbé rossz mint az alábecslés
        - new_rtt = α(old_rtt)+(1-α)(new_rtt)
            - nem fog hirtelen megugrani
            - α : 0.8 - 0.9 
            - simított
        - Karn-elv az újra küldési mintákat ne vegyük figyelembe
- Torlódás vezérlés
    - hálózat néha terhelt, néha üres
    - ne legyen router túlterhelve
    - torlódás csomagvesztést okoz
    - várakozást okoz, rtt-vel arányos is tud lenni
    - túlterhelés észlelésnél növelni kell a várakozási időt
        - rendszert hagyni kell fellélegezni
    - könyökpont környékén kell mozogni
    - szirt pontot el kell kerülni
    - az ablakok méretét is lehet módosítani ezért
    - küldési ráta módosítás
    - torlódási ablak is az advertised ablak mellett
    - cwnd - állítása az eldobott csomagok alapján
        - nyugta nem jön
        - duplikált nyugta
            - valami elveszett
    - túlterhelést lassan lehet észre venni, megjavulást gyorsan
    - Három változó
        - cwnd
        - adv_wnd
        - ssthresh: vágási érték
    - küldésnél: wnd = min(cwnd, adv_wnd)
    - vezérlés két fázisa
        1. Lassú indulás
            - ssthresh = adv_wnd
            - amíg jön nyugta addig növeljük az ablakot
            - exponenciális növekedés
        2. Torlódás elkerülése
            - ha cwnd ≥ sstresh
                - ha nyugta akkor cwnd növelés
                - he nincs nyugta akkor csökkentés

# EA 12 2021.12.08

## Szállítói réteg
### Lassú indulás
- Gyorsan el akarjuk érni a könyökpontot
- Azért nem olyan lassú, mert exponenciális a növekedése
- Csomagvesztésig, vagy küszöbig csináljuk ezt

### Torlódás elkerülés
- Itt már nem kell gyorsan növelni, mert nem akarunk senkit túlterhelni
- Itt már csak lineáris növekedés
- Ha hamar van csomagvesztés, akkor ez a rész nagyon hosszú
- **TCP Tahoe** algoritmus
    - 80-as évek
    - Nagyon fűrészfogas
        - ugrál
    - Csomagvesztés után visszamegy a SlowStart-ba
        - Nulláról indul

- **TCP Reno**
    - Megkülönböztet két torlódást
    - Gyors újra küldés
        - Kumulált nyugta duplikátumok kihasználása
        - 3 duplikátum, még csak kevésbé súlyos torlódás
        - Ha nem jön nyugta egyáltalán, akkor SlowStart
    - Gyors helyreállítás
        - Nem nullára ugrunk, csak egy kisebb értékre
        - Lineáris szakaszba lépünk

- TCP mindig növeli a rátát és így mindig lesz csomagvesztés
    - kikényszeríti

- **TCP NewReno**
    - Minden egyes duplikált nyugtára újra küldés
    - Gyorsabban szabályozza magát
    - Hibás sorrendben küldésnél egy duplikált nyugta véletlen is előfordulhat

- **Compound TCP** (Windows)
    - Reno alapú
    - Késleltetés alapú ablak
        - RTT csökkenésnél gyorsítja a küldést
    - Win10 előtti rendszerekben
    - wnd = min(cwnd + dwnd, adv_wnd)
        - dwnd - késleltetési ablak
        - Kis RTT -> dwnd növelés
        - Nagy RTT -> dwnd csökkentés
- **TCP CUBIC** (Linux)
    - Csomagvesztés harmadfokú egyenlete alapján állítja a dolgokat
    - Win10, linux
    - W_cubic = C(T-K)³+W_max
        - K = (W_max*β/C)^(1/3)
    - W_max - előző csomagvesztési szint
    - Legutolsó csomagdobás óta eltelt idő alapján változik
        - SlowStart-nál gyorsabb növekedés
        - W_max közelítésénél lassulás
        - Ha ezen a torlódáson túljutunk
            - Akkor megint köbös növekedés
    - SlowStartba már nem megy vissza
    - A köbös fgv határozza meg a működését

    - Torlódásvezérlés legyen fair a korábbiakkal
        - De ez nem lehetséges
        - Reno-val nem fair
            - CUBIC sokkal több sávszélességet fog szerezni

### TCP hibái
- Kis folyamok
    - ezeket nem jól kezeli
    - több erőforrás a kapcsolat létrehozása
    - SlowStartban maradunk
    - Megoldások
        - cwnd induljon 10-ről
        - TCP Fast Open - hashekkel azonosítjuk a felhasználót és a régi rátával kezdünk küldeni
- Wireless
    - Csomagvesztés nem biztos, hogy torlódás
    - De lehet, hogy itt nem is jelenik meg a csomagvesztés, csak a késleltetés lesz nagyobb
- Szolgáltatás megtagadása
    - DOS támadás
    - Szerver állapotot foglal a kliensnek
    - Sok SYN csomag elfoglalja az összes állapotot
    - SYN floud
    - DDOS - elosztott dos támadás
    - Megoldás
        - SYN cookie
        - SYN/ACK-csomagba kódol egy cookie-t ami tárolja a fontos adatokat
            - Ha visszajött a helyes válasz, akkor foglal memóriát

## Tipikus internetes várakozási sorok
- Löketek miatt kellenek
- Túlterhelést lehet kerülgetni vele
- Nagy puffer késlekedést okoz
    - Az idő sok helyen fontos
    - Kisebb queue javítja, de így hamarabb elérheti a hálózat a max terhelését
- Alap: FIFO + DROP_TAIL
- **RED** algoritmus
    - kihasználja a TCP működést
    - Random eldobál csomagokat, ha már betelne a puffer
    - Így a küldők lassabban fognak küldeni
    - Sorhosszot nézi
    - Van két küszöb érték: min, max
        - 0-min : minden csomag mehet
        - min-max : random csomagokat eldobálgat
            - profillal lehet határozni
        - max-∞ : mindent eldob
    - nem lesz túltöltve a puffer, kisebb késleltetés
    - Active Queue Management Algorithms
- Csomagdobás vagy ECN küldés
    - RED feleslegesen dobál, ehelyett lehetne jelzést is küldeni
        - ECN - csomagdobás helyett egy FLAG 
        - Nem kell újra küldeni
        - Megjött a jelzés
        - Gyorsabban is megérkezik a jelzés
            - 1 RTT, nem pedig valami random várakozási idő
            - Csomagdobás 2 RTT idő
    - ECN-hez speckó router kell
        - nem mindenhol van ilyen
    - Végpont és router támogatás is kell
        - ECN 2 bit
            - 00 - Nem ECN képes
            - 01, 10 - ECN képes
            - 11 - Ha a végpont ECN képes, akkor ezt rakhatja

- DCTCP - Data Center TCP
    - Adatközpontban működik, máshol nem
    - Aggregátor a külvilág felé
    - Workerek belül
    - Sok alternatív útvonal a szerverek között
    - Lehet sokféle üzenet
        - Kis, gyors - Query
            - késleltetés érzékeny
        - Kis, lassabb - Coordination
            - késleltetés érzékeny
        - Nagy, lassú - Large flow
            - sávszélesség érzékeny

    - Incast probléma
        - Kis üzenetek lemennek
        - Válaszok nagyok, csomagvesztés
        - Újra küldés
    - ECN-el lehet ezt valamennyire kezelni
        - Küszöbérték utáni csomagokat megjelöli
        - TCP nagyon mozgatja a küldési rátát
            - itt csak kisebb változás kell
        - Jelölt csomagok száma alapján csökkenti a rátát

## Internetes alkalmazások fejlődése
- Manapság minden használ internetet
- DNS segítette a net elterjedését
    - Nem kell IP-t megjegyezni
    - ember számára megjegyezhető nevek
    - domain nevek szervezeti struktúrát tükrözik
- Régen fájlban tárolták
    - Linux: /etc/hosts
    - Windows: C:\Windows\System32\drivers\etc\hosts
    - Ha ebben nincs, akkor DNS szerverben kell keresni
        - manapság van hogy ezt nem is nézik
    - nem jól skálázható
- DNS
    - hatáskörök létrehozása
    - alnevek lokális menedzselése
    - elosztott adatbázis
    - udp kliens-szerver architektúra
        - rövid kérés, válasz
    - hierarchikus névtér
        - com -> google.com -> mail.google.com
    
## Vizsga
- online vizsga
- minden használható
- canvas modul, két rész
- 8-12 idősávban, de nem 4 óra van rá, kevesebb mint egy óra van rá
- teszt - 20 pont
    - 20 kérdés, 20 perc, szekvenciális
    - min 11 pont
- kifejtős - 25 pont
    - sikeres teszt után
    - 5 kérdés 30 perc, tetszőleges sorrend
    - 5 pontos kérdések
    - megértés a lényeg, nem a diák másolása
    - jó gondolatmenet legyen, copy-paste nem ér sokat
    - kérdésekre figyelni kell
    - Rövid bekezdésnyi szöveg kell kb 

# EA 13 2021.12.15

## TCP
## Lassú indulás
- Internetet sokan használják
- Router csak adott mennyiséget tud küldeni
- Ha több jön, akkor túlterhelés lehet
- Ezért kell kis küldési rátáról indulni
- "Lassan növeljük"
    - 1-et küld
    - 1 nyugta jön -> 2-t küldök
    - 2 jön -> 4-t küldök
    - exponenciális növekedés
    - el kell érni a könyök pontot gyorsa
        - akkor lesz a hálózat kihasználtsága a legjobb
- Két módon fejeződik be ez a rész
    - Elérjük az sstesh-t
        - Innentől a másik szakaszba lépünk
    - Csomag eldobás történik
        - Túlterheltünk egy pontot
        - sstesh-t a cwnd felére állítjuk
        - vagy megint slow sart vagy egyéb
- Küszöb érték elérése után nem akarjuk elérni a könyökpontot

## Additiv increase
- Minden nyugtázott csomaggal 1/cwnd-vel növeljük csak
    - ez már egy lassabb növekedés
    - lineáris növekedés
    - keressük a maximális kapacitást

## TCP Tahoe
- az eredeti TCP
- Frank Jacob -  80-as évek
- ez a megoldás most már nem elég jó
- túl sok visszalépés 0-ra

## TCP Reno
- újabb megoldás
- ez volt a kezdeti népszerű megoldás
- van benne gyors újraküldés
- 3 duplikált nyugta
- ez még nem a szirtpont
    - ezért még lehet növelni
    - fast recovery, gyors helyreállítás
        - csak a küszöb felére ugrunk vissza
        - onnan additiv incraese
        - nem kell slow start
        - AIMD - additiv increase, multiplikativ decrease
        - fűrészfogas
            - de nem kell visszamenni 0-ra
- TCP mindig növel és mindig csomagvesztést kényszerít ki

## TCP new RENO
- javítja az újraküldést
- minden duplikált nyugtánál visszaugrik
- ilyen lehetett sorrend csomag cserék ami ilyet okozhat
    - de kicsi a valószínűsége

## Vegas
- késleltetés alapú 
- ha megnő a késleltetés, akkor torlódás

## TCP manapság
- nagy sávszélesség
- jobb kihasználás kell  

### Compound TCP
- RENO alapú
- késleltetés és csomagvesztés alapú egyben
- két ablak, egymástól függetlenek
- wnd = min(swnd+dwnd, adv_wnd)
- cwnd - csomagvesztés alapján
- dwnd - gyorsítási/lassítási faktor
- dwnd állítás
    - ha nő az RTT, akkor csökkent a dwnd
    - RTT csökken, dwnd nő
- agresszívan reagál az RTT-re    

### TCP CUBIC
- harmadfokú egyenlet alapján állítja az ablakot
- nem használ két ablakot, de AIMD-t se
- kigyorsítás gyorsabb
- ez előző torlódási szint közelében lassul
    - ott érzékenyebb a növelés
    - óvatosan próbálkozik
    - remélhetőleg nem terheli megint túl
    - ha ott nincs csomagvesztés
        - akkor mehet megint egy kigyorsítás
        - egészen addig amíg új torlódás lesz
- ez kevesebb pazarlás
- többször lesz maxon a kihasználás
- ez nagyon agresszív
- ha egy rendszeren van CUBIC és RENO is
    - akkor a CUBIC jobban használja a rendszer
    - a másikat elnyomja

## TCP problémák
- kis folyamok problémát okoznak
    - kapcsolat építés sokáig tart
    - kis idő a csomag szállítás
    - kapcsolat lezárás is sok az adathoz képest
    - slow startban használjuk kb mindig
    - általában kis folyamok mennek
    - megjegyezhetjük utoljára milyen ablak max volt - onnan kezdjük
- wireless
    - csomagvesztés sokszor lehet torlódás miatt is
    - ilyenkor nem kellene visszaugrani
    - késleltetés alapú ilyenkor jobb lehet
        - de utána a rendes netren már nem olyan jó
    - jelzőbit bebillentés
- támadási felület
    - DOM - syn flood
    - kapcsolat építés sokszor
    - kernel pánikkal összeomlik a rendszer
    - SYN coocke használata
        - valódi kapcsolat jobb megállapítása
        - csak a harmadik kézfogás lépésnél lesz erőforrás foglalás

## Kitekintés
- Várakozási sorok is lehetnek különbözőek
- RED algoritmus
    - random csomag eldobás a betelés előtt
    - így kicsit visszavesz a küldő
    - ECN flag - nem tényleges eldobás, csak olyan jelzés
        - itt ECN részletesebb rész
        - előző jegyzetben

## DNS - ebben lesz új anyag
- Híváshoz is telefonkönyv
- neveket könnyebb megjegyezni egy embernek
- név alapján
    - lehet a hozzánk közelebbi szervert vagy a kevésbé terhelt szervert elérni
- DNS biztosítja a nevek és ip címek összekötését
- DNS előtt egy hosts fájlban tároltuk
    - akármi lehetett a domain
    - nem skálázható
    - nevek megkülönböztethetősége
- DNS - app az internet felett
- elosztott adatbázis szerű
- UDP-t használ, mert nagyon rövid üzenetek
- hierarchikus névtér
    - a domain vége a legfontosabb
    - előrefelé haladva vannak az alrészek
    - adatbázis struktúrát is meghatározza
        - valaki felel egy adott részért
        - nem kell központi felügyelet
- Megvan, h ki melyik részért felel
    - zónája domain rekordjait tárolja
    - de van redundancia-robosztusság
    - hierarchia miatt csak az egyel alatta lévő szervert kell ismernie
- ROOT - ICANN
    - a->m-ig 
    - root szervertől meg lehet tudni az ip-t a fa végigkeresés alapján is
- szolgáltató ad otthon lokális névszervert
    - cash-eli a neveket
    - ha nincs meg lokálisan, akkor fordul a root-hoz
- a cash alapján át lehet ugrani szinteket
- lehet a rekurzív vagy iteratív
    - rekurzívnál sok erőforrás kell
        - nagy terhelés a szervereken
    - iteratívan
        - sorba kérdezi egyre lejjebb
        - nem kell minden szervert leterhelni
        - csak azt aki végigiterál
- ha veszünk domain nevet akkor mi lesz
    - megtörténik a bejegyzés
    - van ahol azonnal elérhető
    - van ahol több idő kell
    - DNS propagonation - elterjedés 
        - ez lehet lassú
        - cash-elés élettartama miatt lehet sok idő
        - 72 óra a legnagyobb általában
            - max 72 órát kell várni az új oldalra

## Vizsga
- Itt vannak a példák, infók
- Voltak az utolsó órán is
- másolást nem szeretik, egymásról sem
- 30-40 perc a második részben




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
    - Hálózati hoszt
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
    - Kölcséghatékony infrastruct
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
    - Dontés kell, hogy merre továbbítódik, komplex routerek kellenek
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
        - CSúcsrátával (peak rate): P
        - Átlagos ráta: A
    - Előre foglalásnál P-hez kell foglalni
        - A/P kicsi, akkor sok a veszteség
    - Igény szerintiben nagyobb kihasználtságot lehet elérni
- Melyik jobb?
    - Nehéz eldönteni, helyzettől függ
    - Ha P/A kicsi (csúcs közel az átlaghoz), akkor előrefoglalás
        - pl telefon ilyen, folyamtos adatátvitel telefonálás közben
    - Ha P/A nagy, akkor az előrefoglalás pazarlás
        - Az adat általában BURSTY-löket szerű ezért a csúcs sokkal több mint az átlag
        - Az internet általában igény szerinti
- Megvalósítás
    - Áramkörkapcsolt:
        - telefonálás, központban kapcsolták a kábeleket
        - előrefoglalás
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
    - Csomagkapcsolalt
        - csomagok, címinformáció
        - löketek kezelésére bufferek
        - igényszerínti

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
    - Kiszámíthatatln teljesítmény
    - Puffer-kezelés és torlódás-vezérlés

## Internet hierachikus struktúra
- Tier-1 ISP nemzetközi - Pár tucat
- Tier-2 ISP nemzeti - több ezer
- Tier-3 (Access) ISP helyi - sok

- Ezeket linkek kötik össze
- Ami nem szolgáltató-vevő között van az **peer** link
    - peer tranzakciókért általában kölcsönösen nem fizetnek
- Olyan útvonal nincs ahol nem részesülnek az adatátvitel jutalékából
- IXP - hatalmas csomópont - Internet eXchange Point
    - Mindenki behúz egy linket és ott vannak összekötve a hálózatok
    - Olcsóbb mint mindenkit mindenkivel összekötni
    - Tier-1 és Tier-2 között létezik kb
    - Földrajzilag is egy pont (Budapest, Frankfurt)
    - Egy helyen lehet változtatni a kapcsolatokat, nem kell linkeket kiéoíteni

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

- Rnegeteg Protokoll van
    - Együtt működnek
    - Több kell ahhoz hogy minden működjön

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
    - Általános modell, komminikációs hálózatokhoz
    - Nem feltétlenül az internethez
    - 3 dolog kell egy réteghez
        - Szolgáltatás
        - Interface
        - Protocoll
    - 7 réteg (internet 5):
        - Fizikai
            - SZ
                - Információ két fizikai eszköt között
                - 1 bitet
                - Fizikai közegetnél máshogyan kell kódolni
            - I
                - Van egy függvény amivel bitet lehet küldeni
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
                - CSomagtovábbítás
                - Switch/Routerben a keretek továbbküldés
                - A közvetlen eszözhöz küldést használja
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
                - Magbízhatóság 
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
- A réteget csak akkor kell implementálni ha nem kell
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
    - roszz felhasználó élmény
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
    - Elveszett csomagok újraküldése vagy minőségromlás
    - mennyi csomag veszik el mennyiből
    - permanens túlterhelésnél megtelik a várakozási sor és eldobálja a maradék csomagokat
        - ha nem sikerül akkor valaki majd megoldja
        - TCP mindig teletölt egy sort
- Átvitel - throughput
    - Nagy fájloknál nagy sávszélesség kell
    - data size [bits] / transfer time [sec]
    - útvonal menti bottle neck határozza meg
        - a leggyengébb láncszem a meghatározó
        - linket hsználók között fel kell osztani az átvitelt
    
- Átvitel és a késleltetés fejlődik, de a terjedési sebesség nem nő
    - ezért replikák vannak és több helyen fut ugyan az a szerver
    - mondenki közelébe kerül egy kiszolgáló

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
    - ha négy szimbólum van, akkor több bitet is reprezentáhat - egy időben több információ megy át
    - szimbólum ráta [BAUD] nem változik
    - Adat ráta [bps] nő
    - vevő oldalon ez probléma
        - ha több szimbólum van, akkor nehezebb megkülönböztetni

### Átviteli közegek
- mágneses adathordozó
    - sávszélesség jó, kéleltetés nagy (nem , on-line)
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
- GPS szinkronjelekkel lehet ott ahol ez nagyon fontos
- Kritikus időpontokban szinkronizáljuk
- Önütemező jel
    - órajel szinkronizáció nélkül is kódolható
    - nem alacsony-magas jel, hanem változások
    - a változásokat könnyebb észrevenni
- MAncheszter kódolás ami most fontos - 10 megabitnél
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
- 4-5 bit kódólás - 100 megabitnél
    - max 3 nulla lehet egymás mellett
    - veszít sávszélességet de nem túl sokat és cserébe jobb
- 8-10 kódolás gigabit-nél

### Alapsáv és szélessáv
- alapsáv fel minden frekvencián megy
- szélessáv, csak egy tartományba küld, pl ott ahol az elnyelődés egyenletes


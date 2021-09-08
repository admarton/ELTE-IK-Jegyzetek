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
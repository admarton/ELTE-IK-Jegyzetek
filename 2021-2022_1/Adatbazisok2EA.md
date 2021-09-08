# Adatbázisok 2 EA - 2021.09.07

inf.elte.hu/

## Ismétlés
1. Adatbázis-kezelő rendszerek - Fontos
2. A relációs adatmodell - Fontos
3. Az SQL nyelv részei
4. Adatmodellezés

## Adatbázis kezelés
- Háttértáron rögzített nagy mennyiségű adat kezelése
- Adatmodell támogatás
- Adatbázis kezelő nyelvek
- Több felhasználó kezelése
- Tranzakció-kezelés *
- Helyreállíthatóság *
- Ügyfél-kiszolgáló felépítés
- Adatvédelem, adatbiztonság

## Adatmodellek
- Hálós, hierarchikus adatmodell (apa-fiú kapcsolat gráfja)
- Relációs adtmodell (táblaszerű kezelés)
- Objektum-orientált adatmodell (háttérben relációk is lehetnek)
- Logiakai modell (tények és szabályok, tény + szabály -> új tény)
- Félig struktúrált (XML, gráfos)

## Adatbázis-kezelő nyelvek
- DDL - adatdefiniáló nyelv (sémák...)
- DML - Adatkezelő nyelv (beszúrás, törlés,...)
- QL  - lekérdező nyelv
    - Deklaratív (SQL, kalkulus)
    - Procedurális (relációs algebra)
- PL/SQL - programozási szerkezetek + SQL
- Programozási nyelv beágyazás
- 4GL nyelvekű

## Több felhaználó
- Felhasználói csoportok
- DBA - ab rendszergazda
- Jogosultságok (írás, olvasás, jogok továbbadása, visszavonása)
- Jogok tárolása is táblákban (lekérdezhető)

## Tranzakció-kezelés
- **Tranzakció**: adatkezelő műveletekből álló sorozat
- **Cél**: tranzakció párhuzamos végrehajtása
    - Műveleteket össze kell fésülni
    - Egyik fél se várakozzon
    - Az eredménynek olyannak kell lennie mintha sorosan lenne végrehajtva
- Tranzakció kezelő biztosítja:
    - Atomosság (egységben lefut vagy sem, ne maradjon félállapotban) Atomiciti
    - Következetesség (nem rontja el az adatbázist) Consistenci
    - Elkülönítés (mintha egyedül kezelné az AB-t) 
    - Tartósság (commit után megmarad az állapot, hiba esetén is)

### Zárolások (Lock, Unlock)
Egymásra várnak a tranzakciók.

### Kétfázisú protokoll

### Tranzakció érvényesítés

### Ütemező
Végrahajtás sorrendjét adja meg.

### Szerializálhatóság
Ekvivalens tranzakciók egymás utáni végrehajtása.

## Helyreállíthatóság
- Szoftver vagy hardverhiba esetén utolsó jó pont visszaállítása
- Rendszeres mentések
    - Statikus adatb (nem gyakori)
    - Dinam (gyakori)

## Ügyf. - Kisz.
- **Kiszolgáló**:
    - Nagy tárhely, gyors
    - Optimalizált párhuzamos végrehajtás
- **Ügyfél**:
    - Formázás
    - Kérés küldése

## Adatvédelem
- Jogok kezelése (grant, revoke)
- Nézettáblákra is
- Titkosítani lehet az edatokat vagy a hálózati kapcsolatot

## AB-kezelő felépítése
- Lekérdezés feldolgozó
    - Szintaktika ellenőrzés
    - Táblák léteznek
    - Jogok ellenőrzése
    - Lek. opt. átértelmezése
    - Végrehajtási tervek készítése
    - Legjobb költségő kiválasztása
- Tranzakció-kezelő
    - Párhuzamos végrahajtást biztosít
    - (ACID)
- Tárkezelő
    - memóriába töltés
    - előre létrehozott indexek, nézettáblák,...
    - bonyolultabb lekérezések gyorsítása

## Adatb-kezelő felépítése
Alkalmazás  Lekérdezés              Sémaleírás
        \       /                       |
    Lekérdezés-feldolg.             Sémafordító
                    \               /
                Adatb-lezelő motor
                        |
                Állománykezelő

## Szintek
- Sémák és előfordulások
- Fizikai, logiaki, alkalmazások
  
- Fizikai adatfüggetlenség
    - A réteg módosítása ne látszódjon a felsőbb rétegekben

- Logikai függetlenség
    - Logiaki bővítésnél az alkalmazásokat nem kell újraírni

## Relációs adatmodell
### Edgar Frank Codd 12 szabálya
1. Egységes megjelenésű információ - táblázatokban
2. Garantált lokalizálhatóság szabálya - adatmodellnek megfelelően kell hivatkozni az adatra, Tábla,Sor,Oszlop egyértelműen meghatároz
3. A NULL értékek egységes kezelése - típusfüggetlen
4. A relációs modell alapján aktív online katalógust kell üzemben tartani - rendszertáblák is megvannak, SQL-el olvashatóak
5. A teljes körű "adatnyelv" szabálya - interaktív, appba élítve, kül. a lekérd. és az adatmódósító műv., lehessen tranzakció
6. A nézet frissítésének szabálya - nézettáblák használata, autómatikus frissítés
7. Mahgas szintű beszúrás, törlés, módostás
8. Fizikai adatfüggetlenség
9. Logikai adatfüggetlenség
10. Jóság (integritás) függetlensége - constraintek definiálása, ellenőrzése
11. Elosztástól való föggetlenség - alkalmazói szinten nem látszik, hogy elosztott az adatbázis, redundancia
12. Megkerülhetetlenség szabálya - ne hessen közvetlenől belenyúlni, csak a kezelővel lehessen módosítani

## Relációs adatmodell
- Relációsáma: R(A1,A2,...,An)
    - R - relációnév
    - Ai - attr.-, tul.-, oszlop név
    - Dom(Ai) - lehetséges értékek halmaza
**!!??????????????????!!**

- Jelölések:
    - t ∈ r esetén t sor (angolul: tuple - n-es)
    **!!??????????????????!!**

## SQL lekérdezés módostása
Structured Query Language  
Összetett lekérdezés felbontása, és külön optimalizálás.
- Egyzserű SQL
    - Kiválasztás
    - Többtábla
    - Halmazművelet
    - Átnevezés
    - 

## Relalg műveletek
1. ÚNIO, R ⋃ S, R,S azonos sáma, sorok halmaza
2. KÜLÖNBSÉG, R - S,  
3. DIREKT SZORZÁS, R × S, két tábla sémája nem egyezhet meg, átneveződik, nincs kétszer ugyan az az oszlop
4. PROJEKCIÓ, SELECT, Πₐ(R), SELECT a FROM R
5. KIVÁLASZTÁSOK, SZŰRÉS, oszlop összehasonlítása, σₕ(R), SELECT * FROM R WHERE h  
    - σ_A∧B(R) ⩳ σ_A(σ_B(R))
    - σ_A∨B(R) ⩳ σ_A(R) ∪ σ_B(R)
6. ÁTNEVEZÉS, ρ_S(A,B)(R) az R át lesz nevezve S-re és az oszlopai is

Részkifejezésekből nézettáblák -> azokon lekérdezése = összetett lekérdezés felépítése  
```SQL
 CRATE VIEW T1 AS SELECT ... FROM ... WHERE ...;
 ```

Ilyen műveletek sorozata a relációs algebra.

Él táblából Út tábla. Tranzitív lezárt.  
Nem triviális rekurzió.  
**Tétel:** Nem lehet relációs algebrával megoldani.  
*Teljes nyelv* ha mindent tud amit a relációs algebra. 

## Származtatott műveltek
- Metszet
- Összekapcsolások
    - Téta : |X|_A=B  
        A szabály olapján kell összekapcsokólni
    - Természetes : |X|  
        Közös oszlop alapján összekapcsolás
    - Félig-összekapcsolás: |X  
        Az elsőből csak azok kellenek amihez van a másodikban
    - Külső összekapcsolás : |X|^O (Outter)  
        Mindent szeretnénk látni, ezért NULL párokkal bekerülnek a hiányzó dolgok (nem teljesen relációs művelet)


    - séma egyezzés r|X|s=r∩s
    - séma nem egyezzik r|X|s=r×s
- Osztás, hányados
- Monotonitás - sorok hozzáadásával növekedni fog.
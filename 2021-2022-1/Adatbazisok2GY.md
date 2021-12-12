# Adatbázisok 2 GY 2021.09.09

https://people.inf.elte.hu/branyi/ora/gyak2/  
https://branyi.hu

## Jegy
- 2 * 2 * 45 perc (papíros, gépes)
- 4 jegy átlaga
- mind min 2
- 8 alkalom javítás - egy alkalom 2 zh-t lehet javítani
- javításnál csonkolás van, nem kerekítés

## Tananyag
1. ZH 
    - Papíros
        - B+ fa rajzolás, nem az mint a sima B+ fa
        - Lineáris hasító index
        - ...
    - Gépes
        - Rendszergazdai dolgok
        - Rendszertáblák
2. ZH
    - Papíros
        - Naplózás
        - Megelőzési gráf
        - Költségszámítás
    - Gépes
        - Mit csinál a gép
        - Hintek

# Nevezés
- Oracle nagybetűsít
- LiteSQl nem foglalkozik ilyesmivel
- x név ≠ "x" név


```SQL

SELECT * 
FROM DBA_OBJECTS;

SELECT * 
FROM ALL_OBJECTS;

SELECT * 
FROM USER_OBJECTS;

CREATE TABLE X(A NUMBER);

SELECT * 
FROM DBA_OBJECTS
WHERE OBJECT_NAME='X'
ORDER BY 9 ASC;

CREATE TABLE "x"(A NUMBER);

-- 1.
SELECT OWNER TULAJDONOS
FROM DBA_OBJECTS 
WHERE OBJECT_NAME='DBA_TABLES' AND OBJECT_TYPE='VIEW';


SELECT 1+1 FROM x;
-- SEMMI

SELECT 1+1 FROM DUAL;
-- 2

SELECT 1+1 FROM DOLGOZO; -- NEM ÜRES TÁBLA
-- 2 ANNYISZOR AHÁNY SOR VAN


```

- DUAL EGY SIMA EGY CELLÁS TÁBLA, MERT ORACLE-BAN MINDEN LEKÉRDEZÉSHEZ KELL EGY TÁBLA
- HA VAN OLYAN NEVŰ OBJ, AKKOR AZT HASZNÁLJA; HA NINCS, AKKOR A PUBLIC-OT HASZNÁLJA
- HA SZINONÍMA VAN, AKKOR ARRA HIVATKOZIK

# GYAK 2021.09.16

```SQL
SELECT DISTINCT OBJECT_TYPE "object_type" FROM DBA_OBJECTS WHERE OWNER="ORAUSER";

-- MILYEN TÍPUSU OBJ-K VANNAK A DB-BEN
SELECT DISTINCT OBJECT_TYPE FROM DBA_OBJECTS;

-- HÁNY OBJ TÍPUS VAN A DB-BEN
SELECT COUNT(DISTINCT OBJECT_TYPE) "darab" FROM DBA_OBJECTS;
-- 47

-- KINEK VAN TÖBB MINT 10 FÉLE
SELECT OWNER, COUNT(DISTINCT OBJECT_TYPE) FROM DBA_OBJECTS GROUP BY OWNER HAVING COUNT(DISTINCT OBJECT_TYPE) > 10;
-- SYS CSAK 44

-- KINEK VAN NÉZETE ÉS TRIGGERE
SELECT DISTINCT OWNER FROM DBA_OBJECTS WHERE OBJECT_TYPE = "VIEW"
INTERSECT
SELECT DISTINCT OWNER FROM DBA_OBJECTS WHERE OBJECT_TYPE = "TRIGGER";

-- MIN 40 TABLE, MAX 37 INDEX
SELECT DISTINCT OWNER FROM DBA_OBJECTS WHERE OBJECT_TYPE="TABLE" GROUP BY OWNER HAVING COUNT(*)>40
INTERSECT
(SELECT DISTINCT OWNER FROM DBA_OBJECTS WHERE OBJECT_TYPE="INDEX" GROUP BY OWNER HAVING COUNT(*)<37
UNION
(SELECT USERNAME FROM DBA_USERS
MINUS
SELECT OWNER FROM DBA_OBJECTS WHERE OBJECT_TYPE="INDEX"));

SELECT DISTINCT OWNER FROM DBA_OBJECTS WHERE OBJECT_TYPE="TABLE" GROUP BY OWNER HAVING COUNT(*)>40
MINUS
SELECT DISTINCT OWNER FROM DBA_OBJECTS WHERE OBJECT_TYPE="INDEX" GROUP BY OWNER HAVING COUNT(*)>37;
```

- DBA_TABLE táblákat mutat
- all_tables, user_tables

# GYAK 3 2021.09.23

```sql
-- Oszlopok tulajdonságai
select * from dba_tab_columns;

-- Fordító eszköz - megadja az oszlopokat és a típusaikat, meg hogy lehet-e null
desc dual;
```

- Ha olyan típust ad meg az ember, ami nincs de ansi-ban van, akkor azt is feldolgozza
    - smallint  -> number, 0 tizedes jegy
    - int       -> number, 0 tizedes jegy
    - float     -> float, 126 jegy
    - real      -> float, 63 jegy
    - varchar   -> varchar2
- Típusok
    - char      -> kitölti a maradékot szóközzel a fix hosszhoz (trim, ltrim, rtrim)
    - varchar2  -> max hosszt lehet megadni, nem tölti ki szóközzel
    - nchar     -> kétszer annyi hosszt felvett mint amennyit megadná

```sql
-- Tábla tulajdonos és nevÉT AMINEK VAN Z-VEL KEZDŐDIK NEVŰ OSZLOPA
SELECT DISTINCT OWNER, TABLE_NAME FROM DBA_TAB_COLUMNS WHERE COLUMN_NAME LIKE 'Z%';
SELECT DISTINCT OWNER, TABLE_NAME FROM DBA_TAB_COLUMNS WHERE SUBSTR(COLUMN_NAME,1,1) = 'Z';
SELECT DISTINCT OWNER, TABLE_NAME FROM DBA_TAB_COLUMNS WHERE INSTR(COLUMN_NAME, 'Z') = 1; -- JÖVŐHÉTEN EZZEL LEHET MEGOLDANI EGY FELADATOT

-- TÁBLÁK AMIBEN MIN 8 DÁTUM TÍPUSÚ CUCC VAN
SELECT OWNER, TABLE_NAME FROM DBA_TAB_COLUMNS 
WHERE DATA_TYPE="DATE" 
GROUP BY OWNER, TABLE_NAME
HAVING COUNT(TABLE_NAME) >= 8;

-- TÁBLA AMIBEN  AZ ELSŐ OSZLOP VARCHAR2
SELECT DISTINCT TABLE_NAME FROM DBA_TAB_COLUMNS
WHERE DATA_TYPE = 'VARCHAR2' AND COLUMN_ID=1;

-- TÁBLA AMIBEN  A NEGYEDIK OSZLOP VARCHAR2
SELECT DISTINCT TABLE_NAME FROM DBA_TAB_COLUMNS
WHERE DATA_TYPE = 'VARCHAR2' AND COLUMN_ID=4;

-- TÁBLA AMIBEN  AZ ELSŐ ÉS NEGYEDIK OSZLOP VARCHAR2
SELECT DISTINCT TABLE_NAME FROM
(SELECT DISTINCT OWNER, TABLE_NAME FROM DBA_TAB_COLUMNS
WHERE DATA_TYPE = 'VARCHAR2' AND COLUMN_ID=1
INTERSECT
SELECT DISTINCT OWNER, TABLE_NAME FROM DBA_TAB_COLUMNS
WHERE DATA_TYPE = 'VARCHAR2' AND COLUMN_ID=4);

-- SZEKVENCIA VÁLTOZÓ
CREATE SEQUENCE NAME 
START WITH 1
NOCYCLE;
-- .CURVAL, .NEXTVAL
-- EGYEDI AZON KIOSZTÁSA
```

### Kövi óra
- Mindkét adatbázisba be fogunk lépni
- Nézettábla

# Gyak 4 2021.09.30

## Csatlakozás adatbázishoz
```sql
CREATE DATABASE LINK aramis_link CONNECT TO felhasználónév IDENTIFIED BY jelszo
USING 'aramis.inf.elte.hu:1521/aramis';

SELECT * FROM USER_DB_LINK;
SELECT * FROM DBA_DB_LINK;

SELECT * FROM SZERET;
SELECT * FROM SZERET@aramis_link;

CREATE OR REPLACE SYNONYM ORSZAGOK FOR NIKOVITS.VILAG_ORSZAGAI; 
CREATE OR REPLACE SYNONYM FOLYOK FOR NIKOVITS.FOLYOK; 

SELECT TLD,NEV
FROM ORSZAGOK
WHERE (
    SELECT ORSZAGOK 
    FROM FOLYOK
    WHERE NEV=''
) ...;

SELECT * FROM DBA_VIEWS;
CREATE VIEW NÉV AS ALLEKÉRDEZÉS;
```
- LEHET ADATOT BEVINNIN A NÉZETTÁBLÁBA?
    - LEHET, DE NEM MINDEGYIKBE
    - AZ ADAT AZ EREDETI TÁBLÁBA KERÜL

- MIT RAK AZ ÜRES HELYEKRE,
    - HA NINCS SEMMI AKKOR NULL
    - HA VAN DEFAULT AKKOR AZ
    - HA MEG VAN ADVA AZ INSERT-NÉL AKKKOR AZ

- BE LEHET-E RAKNI SELECTES VIEW-BA
    - A TÁBLÁBA RAKJA

- MUNKÁS TÁBLÁBA SZÚRÁS
    - HA NINCS DEFAULT ÉS NOT NULL AKKOR NEM ENGEDI A NEMMEGHATÁROZOTT BESZÚRÁST
    - MEGSZORÍTÁSOK - CONSTRAINT
        - GÁTOLHAT BESZÚRÁST

- DISTINCT VIEW-BA NEM LEHET BESZÚRNI
- GROUP BY-OS VIEW-BA SEM LEHET BESZÚRNI
- ÖSSZEKAPCSOLÁSOS VIEW-BA SEM LEHET
- EREDMÉNY OSZLOPOT TARTALMAZÓ VIEW-BA SE LEHET

- CSAK LEÍRÁST TARTALMAZ

# Gyak 5 2021.10.07

## Merevlemez
- Egy szektor: 512 bájt
- formázás
    - Boot sector
        - itt van a boot program
        - lemez elején van - legkülső sávban
        - floppynál lyuk van
        - vinyónál meg a motornak van 0-s állapota
        - Master Boot Recod
    - foglaltsági táblázat
        - lemez minden szektorát nyilvántartotta
        - ebből baj lesz
    - főkönyvtár
        - fix méretű
        - x darab fájlt lehet csak belerakni
        - alkönyvtárak bővíthetőek

## Oracle
- Lemez blokkok
- Adatbazis blokkok, fix méretek, itt vannak a konkrét adatok
- Extets - részek, változó méretek
- Segments - az adattábla, index, cluster
- Tablespaces - táblaterek, az azonos célra használt táblákat összecsoportosítja, ebben vannak a szegmensek, jogokat leht hozzárendelni

## Adatbázis blokkok
- Van blokk header
- Vannak sorok
- Közöttük van hely a növekedéshez 10% megmarad
- Ha 40% felszabadul akkor lesz megint használható a felszabadítás után
- `dba_data_files` és `dba_TEMP_file` listázza fájlokat, ahol a blokok vannak
- user verzió nincs, mert oracle-ben nem tud saját táblateret csinálni

## Szegmensek
- `dba_segments` 
- hány extens van benne
- Melyik partíción

## Extensek
- `dba_extents`
- melyik fájlban van

## Üres helye
- `dba_free_space`

## Jövőhét
- papír kell majd

# Gyak 6 2021.10.14
- PAPÍRON

# Gyak 7 2021.10.21

## Spec táblák
### Partícionált tábla
- Egy tábla túl nagy akkor partícionált
- Tábla részeit megmondhatjuk h melyik táblatérre
- Fájlt nem lehet megmondani
- Táblateret csak rendszergazda tud csinálni
- Rendszergazda engedélyezhet adattárolást
- Partíciókkal lehet optimalizálni a lekérdezéseket
- Alábbiakat lehet kombinálni
    - érték szerinti után hash-es
    - 3 érték bontás, azon belül 3 hash = 9 partíció
- RANGE -> LESS THAN MAXVALUE
    - minden nagyobb kerüljön ide
- LIST -> VALUES DEFAULT
    - minden, ami nincs egyik listában sem

```SQL
PARTITION BY RANGE (<COLUMN NAME>)
    (PARTITION <PARTITION NAME> VALUES LESS THAN (<VALUE>) SEGMENT CREATION IMMEDIATE STORAGE (INITIAL 0K NEXT 0K) TABLESPACE <NAME>,
    (PARTITION <PARTITION NAME> VALUES LESS THAN (<VALUE>) SEGMENT CREATION IMMEDIATE STORAGE (INITIAL 0K NEXT 0K) TABLESPACE <NAME>,
    (PARTITION <PARTITION NAME> VALUES LESS THAN (<VALUE>|MAXVALUE) SEGMENT CREATION IMMEDIATE STORAGE (INITIAL 0K NEXT 0K) TABLESPACE <NAME>,);

PARTITION BY HASH (<COLUMN NAME>)
    (PARTITION <PARTITION NAME> SEGMENT CREATION IMMEDIATE TABLESPACE <NAME>,
    (PARTITION <PARTITION NAME> SEGMENT CREATION IMMEDIATE TABLESPACE <NAME>,
    (PARTITION <PARTITION NAME> SEGMENT CREATION IMMEDIATE TABLESPACE <NAME>,);

PARTITION BY LIST (<COLUMN NAME>)
    (PARTITION <PARTITION NAME> VALUES (<VALUES LIST>) SEGMENT CREATION IMMEDIATE STORAGE (INITIAL 0K NEXT 0K) TABLESPACE <NAME>,
    (PARTITION <PARTITION NAME> VALUES (<VALUES LIST>) SEGMENT CREATION IMMEDIATE STORAGE (INITIAL 0K NEXT 0K) TABLESPACE <NAME>,
    (PARTITION <PARTITION NAME> VALUES (<VALUES LIST>) SEGMENT CREATION IMMEDIATE STORAGE (INITIAL 0K NEXT 0K) TABLESPACE <NAME>,);
```

- rowid
    - hol van az adatbázisban
- dba_part_tables - partícionált táblák
    - főpartíció és alpartíció típusa
- partíció szabályának lekérdezése
    - dba_tab_partition
    - hash-nél nem mondja meg a szabályt (null)
    - partíciók neve is benne van
    - dba_tab_subpartition
- melyik oszlop alapján csinálta a partíciót
    - dba_part_key
        - főpartíció oszlopa
    - dba_subpart_key
        - alpartíció oszlopa
- hol tárolja az adatokat
    - dba_segments

### Index szervezett tábla
- rowid van hogy megtalálja
- rowid helyett iot-ben az adat van
    - row header
    - kulcs oszlop
    - nem kulcs oszlop
    - ha túl sok adat akkor muató a maradékra
- indexek
    - dba_indexes
- indexelt oszlopok
    - dba_ind_columns
    - sys szám$ - függvény
- függvény magyarázat
    - dba_ind_expressions
    - oszlop desc - olyan mint egy függvény mert számolni kell

- index szervezett tábla
```SQL
CREATE TABLE <NAME> (<COLUMNS>)
ORGANIZATION INDEX
PCTRESHOLD <VALUE> INCLUDING <COLUMN>
OVERFLOW TABLESPACE <TABLESPACE NAME>;
```
- iot oszlopból lehet tudni h index szervezett
- fel lesz véve a kicsorgó rész táblaként
- az iot nincs tárolva - a túlcsorgóban van
- dba_objects -> data_object_id -nál null van - nem tartalmaz adatot
    - segmense sincs
        - a túlcsordulásának és az indexének van

### Clustered table
- Összekötéshez nem kell ide oda rakni
- Össze vannak rakva egy fájlba az összekötött adatokat
- Oszlop érték alapján lehet összekötni táblákat
```SQL
CREATE CLUSTER <NAME> (<SHARED SPACE> <TYPE>) SIZE <x>K;

CREATE TABLE <NAME> (...)
CLUSTER <CLUSTER NAME> (<COLUMN>);

--SEGÍTENI KELL AZ ADAT MEGTALÁLÁST
-- INDEX VAGY HASH
CREATE INDEX <NAME> ON CLUSTER <CLUSTER NAME>;
CREATE CLUSTER <NAME> (<SHARED SPACE> <TYPE>) SIZE <x>K HASHKEY ...;

```
- Minden táblából van egy elsődleges adat, ami egy helyen van
    - a többi megegyező is egy blokkba kerül, de nem ugyan abban az adatban
- dba_clusters
- melyik tábla van a clusterben
    - dba_tables -> cluster_name nem null
- mi a közös
    - dba_clu_columns
    - table_name, table_column_name
- hash függvény
    - dba_cluster_hash_expression
- hol tárolódik az adat
    - dba_objects
        - a beépített tábla ott tartja az adatát a cluster adatban
    - dba_segments
        - egy szegmensben vannak
        - a cluster szegmensében

## ZH
- első 5 hét feladatai lesznek
- gépeshez mindent lehet használni
- szünetben lehet tanulni

# GYAK 8 2021.11.04

gyakII_9.sql

emp, dept tábla kell

## Hogyan hajt végre utasításokat
- utlxplan.sql - branyi
- expl.txt - nikovits
- Create table PLAN_TABLE
`expalin plan for select ... from ...`
- Utasítások bekerülnek a plan_table-ba
- Plan_id és id szerint sorban
- Statement_id - név ha adunk
    - set statement_id='név'
- Plan_ID - minden lekérdezés kap új sorszámot
- Operation - 
- Parent_id - melyik utasítás szülte ezt 
- Access_Predicate - milyen feltétel van
- Cost - milyen költséggel jár
- Cardinality - hány sort kellett átnéznie
- Bytes - mennyi memória volt ez
- Projection - hány oszlopot látott a végrehajtás során

- `select plan_table_output from table(dbms_xplan.display("plan_table",null,"basic"));`
- `select plan_table_output from table(dbms_xplan.display());`
- `select plan_table_output from table(dbms_xplan.display("plan_table",null,"all"));`

### Megjelenítés
Példa a `gyakII_9.sql` fájlban
SQL Developer-ben van gomb, ami grafikusan kijelzi -> Explain Plan

### Hintek, tippek
- `select /*+ use_nl(emp,dept) */ from ...` - nested loop join
- `select /*+ use_merge(emp,dept) */ from ...` - sort merge join
- `select /*+ use_hash(emp,dept) */ from ...` - hash join
- `no_use_hash(...)` - akkor azt a módszert választja, ami a következő legolcsóbb megoldás
- `/*+ no_use_hash(...) no_use_merge(...) no_use_nl(...) */` - ha hülyeséget kérdezek akkor visszatér az eredeti állapothoz, de nem jelez hibát

- Oracle oldalán fent van az összes hint a manual-ban

- Ne használjon indexet: `no_index(< tábla név >), full(< tábla név >)`
- Megmondhatom melyik indexet használja, választhat: `index(< tábla név > < index név >,< index nevek >)` 

### ZH-ban 
- 3 ilyen feladat
- serial van megadva, abból kell a lekérdezést megadni
- ahány sor annyi pont + a feltételek 

# Gyak 12 2021.12.02

## explain plan for select...
- distinct
    - hash unique
    - sort unique

- avg, count, sum
    - Sort aggregate az összesítés
    - áltaghoz a count-ot meg a sum-ot használja

- group by
    - hash group by
    - sort group by

- havin
    - megjelenik egy **FILTER** is
    - where is van mag having is
        - akkor két * van
            - group by alatt van a where, fölötte having
            - a `TABLE ACCESS` a where
            - `FILTER` a having

- UNION
    - UNION ALL
    - megtart mindent
    - és utána van `SORT UNIQUE` -> DISTINCT
    - ha végrehajtásnál van view akkor van distinct és union all

- MINUS, INTERSECT
    - nincs MINUS ALL
    - más adatbázis kezelőben van except all
    - sort unique -olja a részeredményeket és utána minus-ozik

- IN
    - Semi join van a végrehajtásban
- NON IN, NOT EXISTS
    - anti join

- SUM termékek, ahol nagyobb a ckod mint 249
    - Használ indexet
    - kevesebb adatnál nim használ indexet
- SUM termékek, ahol nagyobb a ckod mint 250
    - nem használ indexet
    - nem csak attól függ, hogy mit kérek, hanem attól is h mennyi adat
    - sok adatnál már mindent átnéz

## Zárak
- hamarabb zárom le a kövi adatot, mint hogy elengedném az előzőt
- zárolásokból holtpont lehet
- lehet itt is megelőzési gráf, ki kire vár
    - kör holtpontot jelent
    - oracle a régebbit lezárja
    - sql developerben be lehet kapcsolni az auto commit-ot
        - minden sor után commit-ol
- Exclusive és shared lock 
    - shared-nél lehet nézni az adatot, de írni nem lehet
    - exclusive-ra más nem zárhatja le
    





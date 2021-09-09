# Adatbázisok 2 GY 2021.09.09

https://people.inf.elte.hu/branyi/ora/gyak2/  
https://branyi.hu

## Jegy
- 2 * 2 * 45 prec (papíros, gépes)
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
- LiteSQl nem foglalkozik ilyesmive
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
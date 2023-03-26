# Számítógépes grafika

# 1. EA

- Bán Róbart
- cg.elte.hu
- Két papíros ZH
    - Elméleti és számolós kérdések
- Szirmaí-Kalos László  - Háromdimenziós grafika, animáció és játékfejlesztés
- Andrew Glassner - Realtime rendering

## Számgraf

- Alkalmazott tudomány
- Mateken alapul
- Nem elég képleteket ismerni

- Vizuális anyagokat állítunk elő
    - Kép elemzés és manipulálás is
    - Képfeldoolgozás
- Modellekből képeket csinálunk
- Virtuális világot el kell tárolnunk - reprezentáció
- Meg kell jeleníteni a világot - képszíntézis, megjelenítők

## Képszintézis

- Hogyna modellezzük le a világot?
- Hogyan számítjuk ki a képet?

# 2. EA

- Koordináta rendszerek
- Descartes
    - X, Y
- Polár
    - r, szög
- Baricentrikus
    - háromszög csúcsaihoz viszonyítva
- Homogén
    - plusz egy homogén tag
    - párhuzamosoknak van homogén pontja a végtelenben

# 3. EA

- Tudjuk ábrázolni a pontokat a számítógépen
- Bonyolultabb dolgokat pontok halmazaként írjuk le
- Halmazok megadása
    - explicit: y = f(x)
    - parametrikus: p(t) = [ x(t) y(t)]^T
    - implicit: f(x,y)=0

## Egyenes megadása

- Explicit
    - y=mx+b
- Mi lesz a függőleges egyenesekkel
- Implicit
- Normálvektoros egyenlet
    - p(px, py) pont és n=[nx, ny]^T =/= normálvektor
    - x(x,y) rajta van-e
        - <x-p, n> = 0 akkor rajta van
        - <x-p, n> > 0 akkor nincs az egyenesen de az egyenesnek a normálvektor oldalán van
        - <x-p, n> < 0 akkor nincs az egyenesen de az egyenesnek nem a normálvektor oldalán van
    - implicit leírás
- Általános / homogén implicit egyenlet
    - ax + by + c = 0
- Ha normálvektor egység hosszú
    - Hesse-féle normál alak
    - Pontosan a pont és egyenes távolságát kapjuk meg
- Homogén egyenlet determináns alakja
    - p(px, py) és q(qx, qy) pontokkal adjuk meg az egyenest
    ```
    | x  y  1 |
    | px py 1 | = 0
    | qx qy 1 |
    ```
- Parametrikus egyenlet
    - p pont és v irányvektor
        - x(t) = p + tv = [px+tvx py+tvy pz+tvz]^T 
    - két pontból, p és q
        - v = q-p
        - utána ua mint előbb
        - x(t) = (1-t)p + tq // baricentrikus felírás
            - lineáris interpoláció

## Sík leírása

- Explicit
    f(x,y) = ax + by + c
- Homogén implicit
    - Normálvektor
        - P pont és normálvektor
        - <x-p, n> = 0
        - Olyan mint a síkban az egyenes
    - ax + by + cz + d = 0
        - sík általános egyenlete
    - Hesse-féle alak van itt is ha egység a normál
    - Determináns alak
        ```
        | x  y  z  1 |
        | px py pz 1 | = 0
        | qx qy qz 1 |
        | rx ry rz 1 |
        ```
- Parametrikus
    - Itt két paraméter van
    - x(s,t) = p + su + tv
    - Ez lehet egy ponttal és két iránnyal
    - vagy lehet 3 ponttal
    - Baricentrikus felírás

## Transzformációk

- Virtuális világunk kisebb alakzatokból áll össze
- Ezeket majd a helyükre transzformáljuk
    - Vagy mozogniuk kell
- Végén egy képet is létre kell hoznunk

### Elvárások

- Minden pontot tudjunk transzformálni
- Pont képe pont legyen, egyenesnek egyenes, síknak sík
- Illeszkedés tartása
- Legyen egyértelmű és egyértelműen megfordítható
- Pontokat koordinátarendszerben tároljuk ezért a koordinátákon kell függvényeket megadni
    - Pontok helyett a helyvektorukat tároljuk
        - Igy az origóra nézzük a forgatásokat, méretezéseket
- Lineáris leképzések lesznek
    - Additív és homogén
    - g(a+b) = g(a) + g(b)
    - g(l * a) = l * g(a)
    - Ezeket fel lehet írni mátrixokkal

### transzformációk

- Ideális síkkal kibővített euklideszi tér
- Affin transzformáció ha az ideális pontok nem keverednek az euklideszi pontokkal
- Asszociatív transzformációk
    - Csoportosíthatóak
- Létezik egység elem
    - Helybenhagyás transzformáció
- Legtöbb transzformációnak van inverze is
- Nem kommutatív
- Összes affin transzformáció leírható egy lineáris transformációval és egy eltolással
    - f(x) = Ax + b
    - A a mátrix és b az eltolás
    - Ezt a kettőt összerakhatjuk
        ```
        +-         -+
        |    A    b |
        | [0,0,0] 1 |
        +-         -+
        ```
    - Az összes affin transzformációt felírhatunk egy mátrixxal
    - Ez jó mert össze tudunk többet rakni szorzásokkal
    - A baricentrikus koordináták affin invariánsak

- Affin transzformáció megadása
    - n dimenzióban n+1 pont kell a transzformációhoz
- Projektív transformáció
    - Nem garantálható hogy a homogén alak megmarad

## Összes transzformáció

- Affin
    - Egybevágósági
        - Egység
            - semmi
        - Forgatás
            - Orikó körüli forgatás
        - Eltolás
    - Momzgásokat ezzel lehet modellezni
    - Hasonlósági
        - Izotróp Léptékezés, skálázás
            - Minden irányba egységgesen
            - Origótól megint
    - Lineáris
        - Transzláción kívül az összes
        - Léptékezés
        - Tükrözés
            - Speciális léptékezés
        - Nyírás
- Projektív
    - Perspektív
        - Középponti perspektíva
    
## Eltolás

- Egy vektorral leírható
```
| 1 0 0 dx |
| 0 1 0 dy |
| 0 0 1 dz |
| 0 0 0 1  |
```
- Neve általában T
- Kommutatív részcsoport
- Inverze az ellentétes irányú eltolás

## Forgatás

- Z tengely körül
    - x' = xcost - ysint
    - y' = xsint + ycost
```
| c -s 0 0 |
| s  c 0 0 | = Rz
| 0  0 1 0 |
| 0  0 0 1 |

|  c 0 s 0 |
|  0 1 0 0 | = Ry
| -s 0 c 0 |
|  0 0 0 1 |

| 1 0  0 0 |
| 0 c -s 0 | = Rx
| 0 s  c 0 |
| 0 0  0 1 |

c = cos(theta)
s = sin(theta)
```
- Kommutatív részcsoport az azonos tengely körüli forgatás
- inverz transzformáció a vissza forgatás - minusz theta
- Itt ha több van azt jobbról-balra kell olvasni
- Tetszőleges tengely szerinti forgatás
    - Eltolás
    - Ráforgatás az egyik tengelyre
    - Ráforgatás a másik tengelyre
    - Így a harmadik tengellyel meg lehetcsinálni a forgatás
    - Utána a felkészítő dolgokat visszafelé kell megcsinálni
- Yaw, pitch, roll
    - függőleges-, kereszt-, hossztengely

## Méretezés

- x,y,z tengely mentén skálázunk
```
| sx  0  0 0 |
|  0 sy  0 0 | = S
|  0  0 sz 0 |
|  0  0  0 0 |
```
- Ha valamelyik nulla akkor abban az irányban kilapítjuk
    - Nincs inverze a mátrixnak
    - Nem lehet visszacsinálni
- Ha valamelyik negatív akkor tükrözés van
    - Ha kettő is negatív akkor tengelyes tükrözés
    - Sodrásirányt is megfordítja

## Nyírás

- Pakli kártya elferdítése
- X tengely eltolása függ az y tengely értékétől
```
| 1 a b 0 |
| 0 1 c 0 | = N
| 0 0 1 0 |
| 0 0 0 1 | 
```





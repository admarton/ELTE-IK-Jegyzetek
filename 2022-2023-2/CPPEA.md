# Haladó C++

# 1. EA

- Porkaláb Zoltán
- http://gsd.web.elte.hu/multi/
- Multiparadigmális programozás
- C++ a lényeg
- Dupla EA lesz, nincs gyak
- 2 órás vizsga
  - teszt és programozás
  - jelenléti, géptermi
- 17:45 kezdés
- 19-kor kb szünet

## Kivételkezelés és hibakezelés

- Errno
  - Statikus változó, C11-óta thread statikus
  - Makro, implementációfüggő
  - Sok **if**
  - Kód nagyobbik része a hibakezeléssel foglalkozik
  - Ezen a logikai szinten tapasztalom a hibát, de nem tudom eldönteni, hogy milyen komoly a hiba
- IOstream
  - exception előtt fejlesztették
  - flag-eket állít be
  - bad, failed, eof
    - ha bármelyik igaz akkor nem good
  - failed-nél nem vesztettünk információt, újra lehet próbálni
  - bad egy nem visszaállítható hiba
  - nem kötelelző a flag-eket figyelembe venni
    - ha bármelyik bebillen, akkor az összes többi művelet SKIP lesz
    - flag-et vissza kell állítani ha tovább akarom használni (clear)
  - a bitekre lehet exceptiont kötni
  - stream bool konverzió is hibát jelezhet
- assert
  - kényelmes
  - prekondíció, postkondíció
  - abortál
  - c++11 óta static_assert
    - fordítási idei feltételek

### Célok

- Detektált problémát nem biztos, hogy kezelni tudom
- Át akarom adni a vezerlést és minnél több infót akarok adni
- Ha nem használom akkor ne legyen hatékonysági következménye
  - Ilyen nem létezhet
- Különböző hibát különböző helyen lehessen kezelni
  - De csoportosan is lehessen
  - Inheritance
- Multithread-en is működjön
- Különböző nyelveken is működjön
  - Általában nem működik

### Exception

- Fortran óta van
- PL1 óta van explicit exception
- Nem keveredtek a nyelv többi elemével
- ML -> OcamL
  - Kitalálta hogy sima típusu objektumokat el lehessen dobni hibaként
- C-ben volt valami exception szerű (C85)
  - setjmp, longjmp
  - jmp_buf
  - setjmp
    - makró
    - stack állapotát menti a visszagörgetéshez
  - longjmp
    - throw
    - visszaadja a vezérlést a setjmp-hez és visszaállítja az állapotot
- C++
  - try,catch,throw
  - nem kapásból ugrik vissza, hanem visszagörget és lefutnak a destruktorok
  - Az eldobott objektumot ki kell menteni egy statikus területre
    - ha nem másolható vagy move-olható, akkor nem lehet eldobni
  - Ha referenciaként veszem át a catch-ben akkor a statikus memórát
    - pl ha nem ref és alosztályt kapok el őssel, akkor slice-ing van
      - elvesznek a plusz adatok és a virtual függvények
  - Ki kapja el?
    - Ha a típus megegyezik, akkor egyértelmű
    - Ha egyértelmű leszármazás van vagy a pointer leszármazás egyértelmű
    - Ezek közül az első kapja el
      - Ha a base alatt van a leszármazott, akkor mindig a base kapja el
  - Többszörös öröklődés
    - Interface öröklődés érdemes
    - pl file_error és net_error a nfs_error-ban
  - re-throw
    - következő catch nem számít, feljebb megy a láncon
  - nem kötelező a függvénybe beírni hogy milyen hibát dob
    - de hasznos lehet
    - futási időben ha más jön, akkor abort-ol a program
    - ha azt mondom h dobok std::bad_exception-t akkor azt adja a többi helyett
    - Mostani divat:
      - csak azt mondjuk, hogy dob valamit vagy sem
      - C++11 - noexcept
        - specifier mint a const
          - nem dob vagy abortálom ha mégis jönne
          - egy fordítási időben eldöntött expression lehet benne
        - operator mint sizeof()
          - fordítási időben megmondja hogy a kapott függvény dob-e hibát
          - pl.:
            ```c++
            template <typename T>
            void f() noexcept(noexcept(T::g())) {
                T::g();
            }
            ```
  - destruktorok
    - ne dobjenak hibát
    - Exception közben egy új exception az undefined behavior
      - pl Stach unwinding
  - Exception safety
    - Meglepő végrehajtási ágak lehetnek
    - Meglepő hibalehetőségek lehetnek
    - Olyan sorrendbe kell raknom a műveleteket, hogy bármikor exception dobódik akkor ne vesszen el semmi
    - STL exception safety
      - Basic guaranteee
        - Bármire igaz az stl-ben, hogy nem lesz memory leak hiba esetén
      - Strong guaranteee
        - Atomi lehet egy-egy művelet
        - pl.: vector::push_back nem teszi korruptá a vectort
      - Nothrow guaranteee
        - Garantáltan nem dob hibát
        - pl.: vector::pop_back, swap, erase
  - C++11 dolgok
    - Nesting exception
      - Be lehet ágyazni hibákat kibákba és együtt dobni

### Optional

- Maybe monad
- std::pair<T,bool>
- deafult vagy std::nullopt_t ha nincs benne

### Expected

- C++23
- olyan mint egy variant
- lehet void és error is

# 2. EA

## C++ céljai

- Típus biztonság - C-hez képest
- Erőforrás biztonság - RAII
- Hatékonyság ellenőrzés
- Megjósolható viselkedés
  ```c++
  struct Base {
      virtual void f(int i=1) {cout<<"B "<<i;}
  };
  struct Der : public Base {
      void f(int i=2) override {cout<<"D "<<i;}
  };
  Base *bp = new Der{};
  bp->f();
  ```
  - Mi fog kiíródni?
    - "D 1"
    - D mert leszármazott
    - 1 mert a def param nem a függvény része hanem a környezet része
      - hívó kód adja be a paramt
      - a hívó bázisnak ismeri
  - Le kell vezetni a szabályokat és úgy már egyértelmű
- Olvashatóság
- Könnyen tanulható

## Konstans biztonság

- std::endl - 20% overhead
- "%d"-be double-t írni nem lesz jó
- istream-be nem lehet beírni
  - típusrendszer nem engedi
- Konstansság fordítási idejű ellenőrzése
- Const literal
  - char t[] vagy char \*s
  - tömb és az adatai az enyém
  - pointernél csak a pointer az enyém, az adatok egy közös helyen lehetnek
    - lehet hogy ua a szöveg több helyen is kap pointert
    - postfix-eire is rakhat pointert a fordító
    - ha nem const akkor futási hiba lehet módosításnál
- Named constants
  - forítási és futási idejű konstansok
  - VLA - variadic length array
    - Nem jó
    - A local változó nem tudjuk milyen messze van a bázis pointertől
    - Memória foglalás jelzi a sikerességét (malloc return vagy new exception)
      - VLA lefoglalás nem ad hibát
  - Jó esetben nem kell memóriát foglalni a compile time const-nak
    - fordító kioptimalizálja
    - kivéve ha használom a címét
      - `&` operátor valid címmel kell visszatérjen
        - ezért le kell foglania
- Optimalizáció
  - const_cast undefined behavior
  - const_cast-al leszedem a const-ról a const-ot
    - a kapott pointeren keresztül módosítunk akkor a memóriában módusil az érték
    - de a const használatnál az eredeti érték lesz felhasználva
    - volatile azt jelenti, hogy ne optimalizálja ki a konstanst
- Const correctness
  - const param azt mondja hogy e függvény nem módosítja
  - const param / ref használatával el lehet kerülni a `==` / `=` felcserélés hibákat
  - Yoda condition
    - x == 0 --> 0 == x
    - hibákat el lehet kerülni
    - Star Wars lesz ennél a kérdésnél a válasz
  - const része a típusrendszerek
    - const int* nem lehet értékül adni egy int*-nak
  - pointer is lehet const
    - pointert nem lehet változtatni de az értéket igen
    - `int * const a` - const pointer
    - `int const * a` - const-ra mutató
    - `const int * a` - const-ra mutató
    - `const int * const` - const-ra mutató const pointer
- Pointer ugrás
  - pointerekkel átugorjuk a tulajdonságot
  - `const int ** a = &(int **b)` - nem lehet mert átugrana egy constot
  - Két leszármazottnál nem lehet két pointerrel a base pointeren keresztül elveszíteni a leszármazott típust
- Const member function
  - const objektumra csak const függvényt lehet meghívni
  - const method const típusú this-t kap
  - mengled névben benne van a const-ság
- Overloading on const
  - mangled név különbözik
  - lehet túlterhelni
- Const adattag
  - nem mindegyik objectben lesz ugyanaz, de nem nem változtatható
  - fordítási idejű garanciát kaphatok
  - inicializáló listában tudom megadni az értékét
  - ha az osztály definícióban értéket adok, akkor az olyan mintha az inicializációs listába tenném
- `mutable` adattag
  - akkor is írható ha az object const
  - cache-elés, számlálás, optimalizálás ilyesmikre használjuk
  - nem kell const_cast
  - lock-oláshoz is használjuk
    - `mutable std::mutex`
- `static const`
  - minden objektumban ugyanaz és soha sem változtatható
- STL is konstansbiztos
  - ha konstans iterátort adok, akkor a find is constanst ad

## Constexpr object

- C-ben is volt konstans kifejezés
  - ha valamit tudott a fordító, akkor már fordítási időben megcsinálta
  - user defined függvényre és operátorra nem működött
- `constexpr`
  - fordítási időben kiszámítható
  - elején csak egy return lehetett benne - MACRO kicserélésére született
    - volt ?: és rekurzió => touring teljes
  - C++14-től szinte bármit lehet csinálni
  - nem kell két verzió
    - ha megy akkor fordítási időben csinálja
    - ha nem akkor futási időben
  - Osztálynak is lehet constexpr metódusa
    - nem csak const lehet
  - template metaprogramozással trükközést lehet kiváltani
  - C++17 constexpr lambda
  - C++20 constexpr union, try-catch, dynamic_cast, allocation, virtual call
    - fordítás idejű vector és string
    - tranziens és nem tranz. allokáció
      - tranziens ha van new és delete is
      - nem tranziens - más hívja meg a deletet, nem én

## Consteval

- csak fordítási időben fusson le
- consteval variable - garantáltan csak fordítási időben

## Constinit

- fordítási időben inicializálódik
- ha nem tudja inicializálni fordítás közben, akkor hibát kapok

## Static if

- `if constexpr`
- fordítási időben eldől és csak a megfelelő ág fordul le
- pl variadic fgv termináló ága lehet ilyen if-ben
- pl fibonacci is lehet fordítási időben

# 3. EA

- Invariánsokat a programozónak kellett fejben tartani és annak helyesen programozni
- Továbblépés a Rekord és Struct dolgoktól az osztályokra
- Konstruktor, Destruktor, Operátorok

## Konstruktor

- Létrehozza az objektumot
- A lényege, hogy az invariánsokat beállítja
  - Ha nem tudja akkor ne engedje létrehozni
- Speciális memeber függvénye
- Factory függvények is lehetnek
  - Statikusak
  - Nagyon komplex inicializációnál szokták használni
- Konverziós konstruktor
- Ideiglenes, névnélküli objektum létrehozása

## Destruktor

- Felszabadítja az erőforrásokat
- iostream egy rossz példa

## Inicializációs szekvencia

- Default, value, zero
- Van-e ezeknek konstruktor lépése az egy másik kérdés
- Global változó
  - Először zero utána default inicializáció
  - zero
    - lefoglalod a memóriát és kinullázod
- Stack változók
  - default inicializáció
  - default
    - lefuthat konstruktor
  - C++11 óta
    - Kapcsos zárójel -> érték inicializáció
  - `T k = T()`
    - érték inicializáció
    - névtelen változóval value inicializálom
  - `T m();`
    - függvény deklaráció
  - Heap-re is inicializálhatok
    - `new` van használva
- Adattag
  - Alapból minden adattagot default inicializálom
  - Ha van inicializáló lista akkor value inicializácio

## Default inicializáció

- Osztályszerűnél
  - A default konstruktort hívja
- Tömb
  - Mindegyikre hívja a def konstruktort
- Ha egyik sem akkor memóriaszemét

## Value init

- Osztályszerű
  - Default init
    - Ha nincs user-defined akkor zero is
  - Ha nem lehet akkor Zero
- Tömb
  - Összesre ua.

## Zero init

- Változó a program végéig kitart
  - Zero lefut
  - Nullázza a memóriát

## Quiz

```c++
#include <iostream>

struct foo {
    foo() = default; // foo() nem felhasználói
    int a;
}

struct bar {
    bar(); // bar() felhasználói - mert a header fordító nem látja a konstruktort
    int b;
}

bar::bar() = default; // bar() még mindig user-provided

int main() {
    foo a{}; // zero then value inited
    bar b{}; // value inited
    std::cout << a.a << ' ' << b.b; // 0 undefined
}
```

- A legjobb ha nem fordul
- Másik legjobb a mindig rossz
- Általában fut de néha rossz
- Default konstruktor
  - noncs param
  - minden paramra van default
- Azért nem zero minden előtt mert van saját logikája hogy feltöltse
  - Nem kell fizetni a felesleges nullázásért

```c++
int i; //default
int i{}; //value
static int i; //zero
static int i = constexpr_fun(); //constant

int i{42}, int j(42);   //direct
int i = 42, j = i;      //copy
int i = {42};           //copy list
int i{42};              //direct list

int iarr[3] = {0,1};    //aggregate iarr[2]==0
                            // nagyobb nem lehet
                            // kisebbnél a maradékot value inicializálja
int iarr[3] = {.1=2};   //aggregate c11,c++20
const int $iref = 42;   //reference

// static: zero- or const
// dynamic: non static
// unordered: dynamic init. of class template static member
// ordered: dynamic init. other non-locals with static life
// implicit: default or value
```

## Dátum típus

```c++
class date {...};

main() {
    date exam{2019, 12, 15};
    date semester{2022,2};
    if ( exam < date{2020}){...} // 2020.1.1
    else if ( exam < date{} ){...} // today
    date exam2{"2019.12.15"}; // construct from string
}
```

- 3 konstruktorral ezt meg lehet oldani
- Lehetnek default értékek
- Egyparaméteres konstruktornál ki lehet írni az `explicit` kulcsszót
  - különben konvertálja a beadott értéket
- Explicit konverzio nem fordulhat le implicit helyen

## Operátorok

- a + b

  - a.operator+(b)
  - operator+(a,b)

- only member

  - a = b
  - a[b]
  - a(b,b,b)
  - a->

- Hova kell írni
  - ostream kiírást nem lehet egy sztream member-nek rakni
  - ha nem member akkor nem fér hozzá a privát dolgokhoz

```c++
class date {
    bool operator<(const date& rhs);
};
...
date today;
if (today < 2016) //works
if (2016 < today) //not work, operator< is member, int not have that operator
```

```c++
class date {};
bool operator<(const date& lhs, const date& rhs);
...
date today;
if (today < 2016) //works
if (2016 < today) //works
```

- Ha a header-be írom, hogy ne kelljen DLL, akkor legalább legyen `inline`
  - ha ezt nem akarom akkor egy cpp-ben lehet body-ja, vagy DLL
  - Ez az inline azt jelenti, hogy lehet több definíciója is

## Subobjects

- Ahhoz hogy éljen az objektum, élnie kell a részobjektumainak
- `member initializer expression`
  - adattag neve
  - érték amire inicializálni szeretném
  - a sorrend nem számít mert az osztály def szerint hajtja végre
  - de ha függenek egymástól akkor baj lehet
    - ha egy későbbitől függök akkor memóriaszemetet kapok
- Header-be is írhatom a member mellé az inicializációt
  - Konstruktor body előtt megtörténnek az értékadások
- Ha van mind2, akkor a konstruktor erősebb

## Destructor

- Élettartam végén
  - heap delete
  - scope végén
  - global a main végén
- Ha leszármaznak az osztályból

  - akkor `virtual` destruktor kell

- `Base* bq = new Der[5];`
  - `delete [] bq;`
  - hiba mert 5 Base-nyi memóriát töröl

## Deep copy

- Polimorf vektor
  - deep-copy ősből kellene leszármazottakat létrehozni
  - dynamic_cast megoldás lehet, de drága
    - de minden leszármazot esetet le kell kezelni
  - clone függvényt kell megadni
    - virtual, const, pure virtual az abstract osztályban
    - clone függvényt kell hívni a deep_copy-nál
    - visszatérési érték nem overload
  - copy assignment operator
    - defaultból létezhet, és memberenkénti értékadás
    - sima értékadás pl exception safty pl std::vector
    - copy-swap
      - másolat az rhs-ből és swap-olom az adatokat
    - assignment value-t kap
      - nem const ref
      - és abból a másolatból már swap-olok
    - override base-re
      - default jobban match-el
      - deafult meghívja a base értékadását is mert subobject

## Nem akarom másolhatóvá tenni

- régen priváttá tetted
  - de osztályon belül lehetett használni
- c++11 óta
  - `*speckó_tagfüggvény* = delete`
  - publikusan kijelentem hogy nincs
  - megkérheted hogy csináljon default-ot

## Delegálás

- member inicializáló listába írhatok másik konstruktort
  - így tovább delegálom
  - utána nem lehet body

## Injektált

- használhatom a bázis cuccait
  - `using Base::Base`
  - de adhatsz új overload-ot
    - nem virtuális, hanem overload

## Inicializáló lista

- lehet egymásba rakni amíg a konstruktor kitalálja
- ilyet nem szép írni
  - fordító majd csinálja
  - read-onlynak hozza létre

## Konstruktor hiba

- lehte function try-t csinálni

```c++
class C {
    C (int x, int y)
    try
        : x(x), y(y)
    {}
    catch(...)
    {
        if(...)
            throw ...;
    }
    ...
}
```

- hibát dobó destruktor nem jó

## Complex init

- Azonnal végrehajtódó lambda
  - névtelen osztály zárójel operátrral

## std::launder

- optimalizációs firewall
- nem optimalizálja ki a const cuccokat

## 4. EA

## Move semantics

## Arrays

- Folyamatos memóriadarab

## Array decay

- Pointerként adódik át
- Ha referenciaként veszem át akkor nem válik pointerré
  - `int (&a)[6]`
  - `template <typename T, int N> ... param: T (&a)[N]`
  - Ha ismerni akarjuk a tömb méretét

## Pointerek

- Memóriaterület címét azonosítják
- Minden memóriaterületre tud hivatkozni
  - Global, heap, local, static
  - Pascalban ilyen nem volt
- `nullptr`, régen `NULL`
  - tudjuk, hogy nem mutat sehova
  - A nem null az igaz

## Pointer aritmetika

- Csak tömbökön szabad használni
  - Csak akkor ha az eredmény is a tömbbön belül marad
- Két pointer távolsága elemszámban a különbség
- Pointerre lehet tömbös indexelést használni
  - Kényelmi szolgáltatás
- A tömb és pointer kb ugyanúgy használható
  - De a fordító két külön típusként használja
  - Más assembly lesz a t[1] és a p[1]

## Memeber pointer

- Típus szelektor
- Member változót vagy függvényt lehet kiválasztani
  - Adat member pointer
    - This-hez képesti eltolás
  - Függvény
    - Virtuális táblába is mutathat
    - Menüpont kiválsztja a member fgv.t és egy ok végrehajtja

## Nullptr

- nullptr nem konvertálódik int-re mint a 0
  - biztonsági is elegancia dolog

## Reference

- Nem új fogalom
- Több név egy tárterülethez
- Neveknek van scope-ja
  - tárterület élettartama nem feltétlen egyezik meg a név élettartamával
- Tárterülethez rendelt név

## Pointer vs referencia

- Pointernél van nullptr
  - Referenciánál ilyen nincs
  - Ha null-t akarunk beadni, akkor az hibát dob
    - vagy megállítja valahogy a vezérlést

## Paraméter átadás

- Címszerinti átadás referenciával
  - Ugyan azt a területet piszkálom, nem másolom le
- Inicializáció szerinti paraméter átadás
  - egy type meg egy reftype máshogy inicializálódik

## Referencia kötés

- Referencia nem köthető bármihez
- int\*-nak be lehet adni double-t
  - de int&-nek nem tudok
- ref-t csak balértékhez tudok kötni
  - literálhoz nem tudok
- const ref-t tudok kötni temp értékhez és literalhoz

## Ref return

- Lokális változó referenciát veszélyes visszaadni, mert már megszűnt
- Láncoláshoz használható
- Prefix ++ láncolható, postfix ++ nem adhat referenciát mert az már lokális érték
- Mátrix getter ref-el térhet vissza
  - Összeadás viszont új mátrixot ad vissza

## Jobb és balérték

- Mindkét oldalon lehet összetett kifejezés
- c-ben lvalue és rvalue
- c++-ban
  - lvalue - módosítható memóriaterület
  - xvalue - pl temp változó
  - prvalue - pl 7

## Value semantics

- C++ value szemantika van
  - Az értékek átíródnak a memóriában
  - Java-ban csak a váltózó átállítódik az értékadásnál

## Move semantics

- Temp értékre is írhatunk függvényt
  - T&&
  - allokációt spórolhatok
- Temp értéket akarok másolni, akkor az értékadásban el lehet lopni a memóriaterületet
- Erőforrásokat ellopok és így allokációkat és másolásokat spórolok
- lval-ref - T&
  - nem köt temporálishoz
- rval-ref - T&&
  - nem köt névvel ellátott változóhoz
- const-lval-ref - const T&
  - Tud kötni mindenhez de alacsonyabb a precedencia mint az rval-ref
- Visszafelé kompatibilitást próbálták megőrizni, de hatékonyság növekedést akartak
  - Rulo-of-3 -> rule-of-5
- Naiv swap copy-zik
  - mert mindegyik változó balérték
  - ilyenkor lehet az std::move függvényt használni
    - jobbérték konverziós függvény
    - kikényszerítem a move-ot
    - rval ref cast
- Unique_ptr nem másolható de move-olható
  - std::stream, std::thread
- A lopott cucc destruálható állapotba kell kerüljön
- Const nem move-olható
- Most vexing parse
  - -Wvexing-parse
- Megfelelő fordítási hibáért kézzel törölni kell a const move ctor-t
  - `MyClass(const MyClass&&)=delete;`
  - Erre jobban illeszkedik mint a copy ctor-ra
    - de hibát ad, mert törölve van
- Leszármazásnál a move konstruktor csapda
  - `Derived(Derived&& rhs) : Base(rhs)`
  - Ez az ős copy ctor-t hívja mert neve van
  - `Derived(Derived&& rhs) : Base(std::move(rhs))`
    - Ez a helyes
- Vector push_back strong garanciás
  - ezért copy-zza az elemeket
  - Ha noexcept a move akkor move-olja az elemeket
- `std::move(s1.begin(), s1.end(), s2.begin())`
  - std::algorithm
  - olyan mint a copy csak move-ol
- Initialization_list-ből mindig copy van
- set bonyolult mert van invariánsa
  - interátor const_ref-et ad vissza
- constansságon és r-lval-on is lehet túlterhelni
  - objektum fel tudja ismerni magát

## RVO

- Move szemantika lassíthat
- Return Value Optimalization
  - Lokális változóbol átmásolok
  - Ezt ki tudja optimalizálni
- De ha std::move-olok akkor nem lesz RVO és a fordított program lassabb lesz
  - ha nem írok semmit akkor RVO vagy move lesz a return-nél
  - csak akkor működik ha local változót return-ol

## Forwarding / Universal reference

- T&&
- Constructor problem
  - Factory függvény, templateként
  - T&& nem jobbérték ref hanem továbbítás/forwarding/universal
    - Úgy adom tovább ahogy kell
    - Egy jelöléssel leírom az összes lehetőséget
- Forwarding csak
  - T&&
  - auto&&
  - Többi esetben nem az
    - pl const, volatiole
  - és típusdedukció kell
- Kell hozzá std::forward<T>
  - std::move ha jobbérték
  - különben nem
  - T típusától függ
- decltype(auto)
  - a visszatérési értéket is a legfinomabb típusban kell visszaadni
  - const volatile lval-ref is lehet ez

# 5. EA

## Lambda

- Lambda kifejezés -> lambda functor típus -> closure object
- El lehet tárolni auto-ba vagy std::function-ben
  - std::function
    - egy hívható az objektum
    - adott paraméter és visszatérési érték
    - fgv pointer, lambda, functor, egyéb
- ki lehet írni a visszatérő értéket
  - de nem kell
- blokkban szinte akármi lehet
  - ajánlott h rövid legyen
  - kivétel az std::thread
- `v.erease( remove_if (v.begin(), v.end(), [x,y](int a){return x < a && y > a} ) );`
  - lemásolja az x és y-t és azt használja a lambda
  - Capture by ref
    - `[&sum](int a){ sum += a; }`
  - ref adattagot const member függvényben is módosíthatok
  - `[&sum, x, y](int a) mutable { sum += a; }`
    - nem const member függvény a functor-on belül
    - módosíthat ja x,y-t is
- Capture
  - Csak a lokális nem statikus változókat lehet
  - Globálisak nem lesznek elkapva
- Functor
  - Jól tudja inline-olni a fordító
- `this`-t érték szerint kell capture-elni
  - `this->s` helyett csak `s` kell
    - de ha van `s` is akkor nem
  - `[=]` ha használom a `this`-t is akkor azt is hozza
  - `*this` is elkapható
    - ez lehet null ptr
- Capture value snapshot létrehozáskor van, hiába hívom később
- Paraméterlista elhanyagolható
- Capture nélküli lambda convertálható egy fgv pointerre
- Függvénypointer sokkal olcsóbb mint a std::function
- `f(..., +[](int i){...})`
  - a `+` miatt függvényre mutató ptr lesz belőle
- IIFE - Immediately Invoked Function Expression
  - Constanst létre lehet hozni a egy ilyen függvénnyel
- Init capture
  - meg tudom adni az értéket
  - olyat is el tudok kapni ami eddig nem is volt
- Lehet `constexpr`
- `*this` a teljes objektumot lementi

## Memóriakezelés

- Storage class
- String literals - readonly szegmens
- Automatikus lokális változók
  - stack
- Global
  - Statikus
  - Data szegmens, elf
- Local static
  - Ott vannak mint a namespace változók
- new, delete, malloc, free
  - ezek ua memóriából dolgoznak
- Több heap is lehet
  - shared object-nek saját heap-je van
    - Ilyenkor jó lehet egy shared_ptr
- Tömbök és agregátumok
- Temporálisok
  - kifejezés kiértékelésekor jön létre
  - teljes kifejezés végéig él utána destruktor
  - const ref név egy temp-re
    - meghosszabítja az élettartamát amíg a név élete tart
    - **lifetime extension**
  - static const ref név a main végéig tart
    - nem a stack-en van a temp
    - lifetime extension nem tranzitív
  - ha adattagra állítok lifetime extension-t, akkor a teljes objektumot életben tartom
- `new`
  - Lefoglalja a tárt
    - bad_alloc ha nincs tár
  - try-t csinál
  - azon belül konstructor
  - catch
    - ha hiba volt a konstruktorban akkor felszabadítja a memóriát
  - van olyan `new` ami `nullptr`-t ad vissza
    - `new (x,y) Z{}`
      - `void* operator new(sizeof(Z), x, y)`
  - mi a `delete nothrow_t`
    - a `new nothrow_t` párja
    - mindig párban kell definiálni
- `placement new`
  - nem allocál
  - csak a konstruktort futtatja le
  - utána explicit destruktorhívás kell
  - ki lehet vinni a memóriafoglalást a ciklusból
    - nem kell mindíg újat foglalni és felszabadítani, elég a konstruktor és a destruktor
- `static void* operator new()`
  - memeber new és delete
- Alignment
  - new a maximális alignment-et nézte
    - utána bármilyen objektum létrejöhet
  - `alignof(T)`
  - `class align(32) MyClass {};`
  - van malloc és new is align-nak megfelelően
- Ki lehet kényszeríteni azt hogy minden a heap-ben jöjjön létre
  - private destruktor nem engedi a globális vagy lokális létrehozást

# 6.EA

## RAII

- Ha a konstruktor dob exception-t akkor a destruktor nem hívódik meg
  - Memóriaszivárgás lehet

## Smart pointers

- Hogyan kezeljük a birtoklást?
  - Owner
    - Birtokolja az erőforrást
    - Lehet egy vagy több
    - Single ownership - unique_ptr, lock_guard
      - Csak egy valaki felelős
    - Multiple ownership - shared_ptr
      - Reference counting
  - Observer
    - Nem birtokol
    - Nekik fel kell ismerni az hogy nem létezik az erőforrás
  - Példa
    - std::string - std::string_view
    - std::shared_ptr - std::weak_ptr
    - std::vector, std::array, stb...
- Auto pointer
  - Single ownership
  - Nyers pointer beburkolva
  - Destruktor felszabadítja a tárat
  - Másolásokat nem kezelte jól, mert a másolat destruktora elrontotta a főobjektumot
  - Tömbökre nem működött
  - Depricated majd törölt
- Unique pointer
  - Egy birtokosa van
  - Nem lehet másolni vag yértékül adni, csak move-olni
  - Deleter-t meg lehet adni
  - Van tömbös verziója
    - Tömb nem polimorfikus
  - Const-ból nem lehet ki-move-olni
  - Van szimulált upcast
    - leszármazottból az ősbe
    - A konstruktorban
    - Ha egy bázis unique_ptr derived-ra mutat, akkor virtual destruktor kell
      - shared_ptr-nél nem kell
        - Olyan mintha a deleter másolódna
        - Tudja melyik heap-ből jött és jó helyen törli ki
  - unique_ptr gyors kell legyen
    - empty base optimalization
    - a deleter-t ki lehet optimalizálni és olyan lesz mint egy pointer
    - Ha nem default deleter akkor ezt nem lehet megcsinálni
  - make_unique-nál nem lehet deletert adni
  - downcast operátor nincs
  - ezt kell használni
    - ha több tulajdonos is van akkor jön a shared_ptr
- Shared pointer
  - reference_countin
  - érdekes megvalósítás
    - owner-er egy körbe felfűzve
    - akkor vagyok az utolsó ha mindkét szomszédom önmagam
  - van tömbös verzió is
    - nem keveredik a kettő
  - létrehozás:
    - memóriafoglalás
    - shared_ptr ráállítás
    - továbbiakat az eddigi shared_ptr-ből kell csinálni
      - nem a memóriaterülwtből mert akkor elromlik a ref count
- Weak pointer
  - Nem tudja elérni az objektumot
    - threadsafety miatt
    - lekérdezés és használat között megszűnhet
  - ellenőrizni tudja, hogy él e még az objektum
  - lock
    - shared_ptr-t csinál
    - ha sikerült akkor már más nem fogja kiszedni alólam mert én életben tartom
    - ha nem sikerül akkor ez van, már nincs
  - így működik a unix fáljrendszerben
    - ha meg van nyitva a fájl és töröljük, akkor refcount miatt csak bezárásnál lesz valóban törölve
  - Sharing group
    - közös referenciaszámlálót használó shared és weak ptr-ek
- Implementáció
  - Objektum létrehozás
  - Shared_ptr csinál egy control objektumot
  - shared_ptr mutat az objektumra és a kontrollra
  - weak_ptr mutat a kontrollra
  - kontrolban:
    - shared_count
    - weak_count
    - object\*
    - deleter
    - allocator
  - weak_ptr a controll blokkot életben tartják és tudják a shared_count-ból hogy él-e még az objektum
- Shared ptr from this
  - Objektum tudjon adni magáról shared_ptr-t pl.: Callback világban
  - class Y : public std::enable_shared_from_this< Y >
    - így Y egy Y-ra mutató weak_ptr-t tartalmaz
- Make függvények
  - new-t se kell mondani
  - nem lehet így kiadni a pointert
  - perfect forwarding
  - de nem tudok deleter-t állítani
  - a legfontosabb hogy hatékonyabb
    - egy helyre kerül az objektum és a kontroll blokk (információs terület)
      - heap hozzáférés relatíve lassú
      - így csak egy kell
  - make_shared hátránya
    - ha van még weak_ptr akkor az objektum memóriarész nem tud felszabadulni
    - úgy viselkedik mint egy memory leak
    - általában nem nagy gond
      - de lehet probléma
  - mikor nem használhatjuk
    - custom deleter
    - custom allocator
    - sokáig élő weak_ptr van
    - false sharing több szálnál
      - minden processor saját cache
- aliasing ctor
  - shared_ptr egy objektum részeire
  - nem törölhetik ki a objektumot amíg én tartom egy részét
    - jelezni kell nekik
    - közös referenciaszámláló, de külön pointer a célra
      - erre jött létre az aliasing shared_ptr
        - meg leeht adni h melyik shared_ptr kontroll blokkal legyen összekötve
  - lifetime extension szerű dolgok mint a referenciákkal
  - void shared_ptr-el csak egy értesítést kapok arról, hogy élnie kellene még
    - és lifetime extension

# 7.EA

## Template történelem

- Először azt hitték, hogy nem kell mert ott vannak a makrók
- Generikusok (Öröklés, interfészt implementál), öröklődés, "with func"
- CPP-en nem ilyenek vannak
- Csak az van ellenőrizve, hogy sikerül-e megcsinálni vagy sem
  - ha minden függvény és member megvan akkor lefordul
- C++20-tól concept-ek
  - Előírások a templatekre
  - Hamarabb és tisztább hibaüzenetek
- Sablon-szerződés modell
  - Milyen típusparaméterek elfogadhatóak
- Java-ban
  - Generic lefordul és Object típuson működik
  - Minden konvertálódik Object-re
  - Egy típus/függvény jön létre
  - Kisebb kód lesz
  - Nem tudok specializációt írni
  - Típus törléssel van megoldva
- C++
  - Külön legenerálódik a kód az összes típusra
  - Nagyobb lesz a program
  - Tudok specializációt írni
  - Minden típushoz példányosul
  - Template függvény nem fordul le - példányai fordulnak le
  - Nem template függvény hanem függvény template
- Megnézi az összes templtet, ha nem talált egy megfelelőt sem de van nem template akkor megpróbál konvertálni
- Példák lesznek a `swap` és a `max`
  - Max int és double működik
    - Visszatérési értékkel már baj van
    - Ha intet adok vissza, akkor double értéke elveszik
  - Max int és string nem működik, de csak akkor derül ki ha már az összehasonlításnál tart a fordító.
    - Csúnya hibaüzenet
- Ritkén lehet visszatérő értéken túlterhelni
  - Azért mert a típus az AST részvája alapján számolja ki
  - Lehet a template egy részét megdni
    - A visszatérési értéket megadom a templateben, a többi típus meg kijön a függvény paraméterekből
- `std::common_type<S,T>`
  - Kihozza a legjobb típust
  - Legkisebb közös őst vagy valami konvertálható típust ad
  - Vagy szintaktikai hiba pl int,long,string esetén
  - C++14 óta `auto` is jó mert itt is általában jót talál ki
- Lehet túlterhelni típusszámra is
  - Egy típusos speciálisabb mint a két típus paraméteres
  - Speciálisabbra jobban match-el
  - Meg lehet adni az összes típust
- Különbség az összes template megadó függvény és a nem template függvény között
  - Nem template mindenképp lefordul, template csak akkor ha használják
  - Templates nem vesz részt a konverziókban
- Template class
  - Minden függvénye template függvény lesz
  - This a template
  - Ha nem hivatkozok egy template-re akkor nem példányosul
    - Csak azok a member-függvények generálódnak ki amik meg vannak hívva
  - Részleges specializáció
    - char és T a paraméter
    - Lehet teljesen más a specializáció törzse

## Template

- Dependent types
  - néha random helyekre oda kell írni hogy `typename`
  - Először csinál AST-t és tudnia kell h valam itípus vagy member
    - Azt feltételezi alapból h member
    - Ha típus akkor oda kell írni a `typename`-t
  - Van ahol más a default
    - Öröklődés az típus
    - Using az típus
    - Értékadás az érték
    - Függvény deklaráció az típus és érték
  - Kiderül a hiba fordítási időben, de sokkal később és csúnyább a hibaüzenet
- Two phase lookup
  - Egyszer csinált AST-t és utána példányosít és fordít
  - Template class specializációnak még a publikus interface-t sem kell betartania
  - Template derived nem látja a bázis template függvényeit
    - De a `this->func()` már jó
- Mixins
  - Olyan osztály ami a saját template paraméteréből származik
  ```c++
  template <class Base>
  class Mixin : public Base {...};
  ```
  - Magam alá injektálok egy bázis osztályt
  - Strategy design pattern
  - Liskov substitution principle
    - Nem működik a Mixin<Base> és a Mixin<Derived> között
- Curiously Recurring Template Pattern

  ```c++
  template <class T>
  struct Base {...};

  struct Derived : public Base<Derived> {...};
  ```

  - enable_shared_from_this
  - Ős megcsinálja a comperáló műveleteket a kisebb alapján
    - Leszármazottnak csak a kisebbet kell megírja

- Static polymorphism
  - Virtuális függvények lassuak
    - Pointer a virtuális táblára
    - Onnan fgv pointer
    - Arra függvény hívás
    - A meghívás is lassú, mert nem lehet inline-olni
      - Inline jó mert
        - 5x gyorsabb mint a virtuális fgv
        - Nem kell paramétert átadni
- Variadic template
  - Tetszőleges számú és típusú paraméter
  - Template paramater pack
  - Function parameter pack
  - Ha tovább hívok akkor a pont-pont előtti álló rész ismétlődik
    - `g(args...); -> g(arg1, arg2, ...)`
    - `g(++args...); -> g(++arg1, ++arg2, ...)`
    - `g(++args)...; -> g(++arg1), g(++arg2), ...`
    - `h(g(const_cast<const Ts>(&args))...); -> h(g(c_c<T1>(&arg1)), g(c_c<T2>(&arg2)), ...)`
- Class Template Argumentum Deduction
  - Konstruktornál auto találja ki az osztály template-ját
  - Lehet írni guid-okat
- Mixin-el össze lehet ragasztani bárhány osztályt
  ```c++
  template <class... Mixins>
  class X : public Mixins... {
  public:
    X(const Mixins&... mixins) : Mixins(mixins)... {...};
  };
  ```
  - std::visit az std::variant-okhoz
    - Van egy olyan osztályom amiben van egy f függvény minden típusra
      - A visit a megfelelő f függvényt hívja meg
      - overloaded lesz ez a speciális osztály
- Fold expression
  - `arg && ...` - fordító kibontja `arg1 && arg2 && ...`

## Példák

- Initializer list-et lehet csinálni az arg-okkal
- `template<typename ...T> auto avg(T... t) { return (t + ...)/sizeof...(t); }`

# 8. EA

## STL

## Expression problem

- Osztályhierarchiával sok mindent szépen le lehet modellezni
- Inkrementálisan bővíthető
- Ha egy ősben új művelet van, akkor elromlik a inkrementalitás
  - Minden osztályt újra át kell nézni
- Ez az expression problem
- Visitor patter - injektál műveleteket
  - De utána nehéz új osztályt belerakni
- Szimmetrikusan bővíthető rendszer kellene
  - Konstant költséggel
- Erre találták ki a standard template library

## STL megoldás

- Nincs osztályhierarchia
- Nincs öröklődési kapcsolat az adatszerkezetek között
- Az algoritmusok nem metódusok
  - nem tudják, hogy milyen kontéren dolgoznak
- Segédosztályokon keresztül tudnak az algoritmusok dolgozni
  - PL iterátor
  - Ezeknek van közös interface-e

## Implementáció

- End az utolsó utáni elem
  - Így elég csak az egyenlőség operátor
- Ha nincs valami a konténer iterátorban akkor nem fordul le
- Reverse iterator
  - rbegin, rend
  - nem definiálunk műveletet
    - insert, erase nem működik
  - base()
    - sima iterator ad vissza
    - egyel tovább mutat
    - azért mert az első előtti elem nem lehet, de az utolsó utáni igen
    - rend()-re nem lehet base()-t hívni
- Iterátor const biztos
  - cbegin, cend
    - nem constansból is lehet constans iterátort kérni
- find_if
  - predikátum kell neki
- Generikus programozás a szép neve
  - Szimetrikusan bővítünk
  - Addig generalizálunk, amíg nincs veszteség
- back_insert_iterator
  - olyan az interface mint egy sima iterator
  - `*` és `++` nem csinál semmit, `==` push_back-et hív
  - adapter design pattern
  - front_inserter, inserter
  - ugyan az a kód lesz belőle mint a ha kézzel push_back-el megírnád
- stream iterator
  - istream_iterator
    - konstruktor olvas
    - üres konstruktor az eof
    - `*` visszaadja, `++` újat olvas
  - ostream_iterator
    - outputra ír
    - plus elválasztó karakter is kiírhat

## Vector vs Associative containers

- Vector sokszor jobb lehet a folytonos adattárolás miatt
  - Kevesebb cache miss
- Ha az algoritmikus komplexitás nem véltozik, akkor a vector általában jobb
- Ha nagyon sokszor van ua elem, akkor a set gyorsabb
  - Az adatokat is kell ismerni
- Deque - "Deck"
  - Elöl-hátul növelhető

## Memória karaktrisztika

- Vektor duplázóda nő
- Deque chunk-onként nő vagy csökken
- Linked list - elemenként ad-vasz, de plusz memória

## Vector size and capacity

- c++17 - shrink_to_fit
- előtte temp-vector.swap

## Iterátor invalidáció

- Vector puch_back
- insert - mözötteseket invalidálja
- delete - mutatott elem iterátora invalid lesz
- hash_map - adott elem törlése vagy újra kell hash-elni az egészet

## std::array

- típus meg egy méret
- nem drágább a sima tömbnél
- tudja a méretét, vannak iterátorok, algoritmusok

## std::forward_list

- Csak előre mutató pointere van
- insert_after, erease_after, stb
  - csak mögé tud
- before_begin - ha az első elemet akarod beszúrni
- nincs reverse iterátor, size, back() és push_back()

## unordered_map

- Hash-tábla
- [] oerátor létrehozza ha nincs benne
- Lehet saját hash függvény
- Hash-tábla akkor hatékony ha egy bucket-ban kevés az elem
  - tipikusan lineárisan felfűzzük
- Load-factor = elemek száma / bucket-ek száma
  - ha jó a hash függvény
  - STL load-factor 1-re törekszik
  - max_load_factor - be lehet állítani
  - rehash - előre megmondom, h hány bucket lesz
    - ha load_factor nagyobb lesz a max-nál akkor újra hash-el a rendszer
      - insert, max_load_factor csökkentés vagy rehash
- bucket-ek száma legyen prím
  - hash függvény mintáját lehet a prímekkel elkeverni
- rehash nagyon drága
  - Újra szét kell osztani az össze elemet
  - Mozgatni nem kell, de újra kell láncolni
- Egyező kulcsú elemek egy bucket-ba kerülnek

## Paralell STL

- Intel's Threading Building Blocks az alapja
- legbal paraméter, execution polici
  - seq, par, par_unseq, unseq
- SIMD - Single Instruction Multiple Data
- Kis vektoron nem indít szálakat
- Bővíhető készlet
- Minimális elvárás, hogy forward iterátor legyen
- Felosztod az intervallumot részekre
- Nem kell de ajánlott a random_access_iterátor
- Programozó biztosítja, hogy ne legyen deadlock és race condition
  - Nem lehet blokkoló szinkronizáció
- vektorizáció
  - legtöbb cpu több értéket is össze tud adni egyszerre
- std::reduce -> map_fold
  - Egy functorral minden lépésben azt használja
    - map-nél és fold-nál is
  - Kommutatív és asszociatív functor kell
    - különben undefined behavior
- std::transform_reduce -> map_reduce
  - transformálom az elemeket -> majd reducolom
  - Két functor-t adok, egyiket hajtja végre az intervallumokon, majd a másikat az intervallumok eredményén

# 9.EA

## Template metaprograms

- Csak a D nyelvben van még ilyen
- Erwin Unruh - 1994
  - Nem forduló program
  - Hibaüzeneteket adott a fordító
  - Prímszámokat sorolt fel a hibaüzenetekben
- Fordítási időben algoritmusok végrehajtása
- Template példányosít
  - Példányosítás példányosítást indíthat
    - Olyan mint egy hívási lánc, szekvencia
    - Rekurzió is lehet
    - Pattern matching-el elágazások
    - Funkcionális prgramozásban ez Turing teljes
- Turing teljes nyelv
- Mi értelme van?
  - Expression template-ek
    - Szintaxisfa objektumot csinál
    - Adattárolókon elemenként hajtja végre a műveletet
  - DSL nyelvek beágyazása template metaprogramokkal
    - pl.: boost::expressive
      - regexp lib
      - template metaprogramokból áll
      - gyakran fordítási időben ismert
      - parser-t generál
    - Megkötést jelent a c++ és template szintaxis is
      - Azok betartásával lehet varázsolni
      - Ezért sokszor a szintaxis csúnya
    - Van olyan parser ami fordítási időben egy szebb szintaxist c++ helyesre parsol
- Nehéz írni, megérteni és debug-olni
  - ELTE-n kb 10 év alatt írtak debuggert
  - Meg profiler-t
  - Pár év alatt bekerül a clang-ba
- Factoriális
  ```c++
  template<int N>
  struct Factorial {
    enum { value = N * Factorial<N-1>::value };
  }
  template<>
  struct Factorial {
    enum { value = 1 };
  }
  int main() {
    const int fact5 = Factorial<5>::value;
    std::cout << fact5 << std::endl;
    return 0;
  }
  ```
  - Lesz 5 osztáylom
  - Ki tudja optimalizálni a használt osztályokat ha máshova nem kellenek.
- Constexpr vs template
  - Meglévő típusokat használ a constexpr
  - Template fordítási időben tud típúsokat csinálni
  - Funkcionális programozásra hajaz
  - Nem lehet típusokat később módosítani
- Haskell-ből is csináltak c++ metaprogramot
- Elágazások
  ```c++
  template<bool condition, class Then, class Else>
  struct IF {
    typedef Then RET;
  }
  template<class Then, class Else>
  struct IF<false, Then, Else>{
    typedef Else RET;
  }
  ```
  - Fordítási idejű feltételekre működik
- Függvény elsőrendű odjektum
  - Metaprogram átadható metaprogramnak
- Előnyei
  - Hatékonyság
  - Nyelv kiterjesztése
  - Új jelölést lehet bevezetni
- Típusok közötti firewall
  - Run-time
  - Compile-time - template instantiation
  - Template design time
    - Írhatok olyan típust ami fordítási időben kiértékelődik
- Specializáció
  - lehet írni specilizációt ami optimalizált
  - De sok specializáció jöhet létre
  - Erre találták ki a "trait"-eket
    - gyorsabb lesz mint a virtuális leszármazás
    - pl.: char_traits< Ch >
    - Még minidg nem tökéletes, de kiscit struktúráltabb
    - Csak a trait-et kell átírni és minden működik tovább
  - Magasabb szintje a Policy
    - Még egy template paraméter, hogy megkülönböztessem a típusokat
    - Csak deklarálni kell, hogy melyikbe tartozik a típusom
      - nem kell függvényeket másolni
- Typelist
  - Adatszerkezetek és algoritmusok
  - Adattárolás template metaprogramokban
  - Funkcionális lista ami típusokat tartalmaz
- Nagyon lassú fordítás és borzalmas hibaüzenetek lehetnek
- SFINAE
  - Substitution failur is not an error
  - Legspeciálisabb példányosítással kezdi
    - utána megy az általánosabbra
    - Hibakezelésre lehet használni
    - Logiaki értéket kapjak ha a példányosítás nem sikerül
- Run-time vs Compile-time
  | Run-time | Compile-time |
  | :-: | :-: |
  | Function | Metafunctio(type) |
  | Value, literal | Const, enum, contexpr |
  | Data structure | Typelist(type) |
  | If/else | Pattern matching |
  | Loop | Recursion |
  | Assignment | Ref. Transparency |
  | May depend on input | Deterministic |
  | ---- | ---- |
  | Imperative | Pure functional |
  | Object-orineted | - |
  | Genarative | - |
- Végtelen rekurzióra van egy limit
  - Ha a limitet átállítom túl nagyra, akkor kifagyhat a fordító
  - Templight - template metaprogram debugger
    - trace lesz
    - más programmal lehet nézegetni az eredményt

## Egyéb c++ funkciók c++11/14/17

- Auto
  - T&& forwarding reference - típus dedukció
  - auto - típus dedukció
  - ha az auto-t dekorálom akkor megszűntetem a forwarding-ot
  - auto&& - prefect forwarding
  - decltype(auto)
    - int i = 0;
    - decltype(változó_név)
      - int - decltype(i)
    - decltype(kifejezés)
      - int& decltype((i))
    - perfect vissza forwarding-ot akarok
- RAnge for
  - Összes elemen végigmegy
  - Mitől függ?
  - begin, end
- Enum class
  - Enum nem csinált saját névteret
  - enum class saját névteret csinál
  - konverziók szigorúbbak
  - meg lehet adni a reprezentációt
    - lehet forward deklarálni
- Initilizer list
  - valahol lementek egy tömböt
  - constans tömb
    - readonly memóriába is mentheti
    - initilizer list csak egy proxy
    - copy konstruktorral inicializálódik
    - nem lehet move-olni
- Default and delete függvények
- User defined literals
  - erős típusosság
  - pl.: std::chrono
  - `myValue operator"" _my(myValue val)`
  - túlterhelhető
- using
  - typedef egy teljes típus szinonímája
  - template típusra is lehet használni
- Structured binding
  - párokra, tuple-re
  - párhuzamos értékadás
  - Fajtái
    - tömb
      - tömb elemek
      - érték szerint alapból
      - lehet referencia szerint is
    - tuple
    - osztály
      - publikus adattagokra
      - csak a nem statikusakra lehet
- Nested namespace
- Attribútumok
  - szabványosították
  - pl.: [[depricated]], switch-ben [[fallthrough]], [[nodiscard]] a függvény visszatérés
- Filesystem
  - Gáz volt hogy nem volt
  - path, exists, stb.
  - path /= "cucc.txt"
- Any
  - olyan típus ami bármi lehet
  - python változó
  - Van egy kis reflection
    - type id operator
    - típus nevét ki leht írni
  - van .type() és .name()
  - any_cast< T >
  - működik saját típussal is
  - has_value
- Optional
  - maybe monad
  - nem kell kimenni a heap-re
  - Előre tudom a max méretet
  - std::nullopt_t
  - bool konverzio
  - operátor\*
- Variant
  - type-safe union
  - tagged union
  - default-ból az első típust csinálja
  - egy típus lehet benne töbször is
  - std::visit
    - kibontja a típust ami benne van
    - visitor-t hívja meg a paraméterrel
- String_view
  - nem bitrokol
  - invalidálódhat
  - substr-nél lehet egy ilyen
  - span - tetszőleges range-re hasonló

## 10.EA

# Multi-threading

- Nem lett gyorsabba cpu ezért fogtunk többet
- De problémák vannak
- Ha 5% nem párhuzamosítható, akkor 20 processzor fölött nem lesz gyorsabb
- C++93-ban nem volt szó párhuzamos végrehajtásról
  - Nem volt párhuzamos memóriamodell
- C++11 memóriamodell
- Java és JVM sem volt felkészülve
  - 1.2 -> 1.3 bekerült a párhuzamosítás
  - Nincs szabványbizottság, ezért gyorsabb lehet
- C++ csak akkor léphet ha minden fele a bizottságnak elfogadja

## Miért kell az új memóriamodell?

- [Epic c++ cég](https://www.think-cell.com)
- Nagyon sok optimalizáció
  - Fordító
    - Szinte teljesen átírhatja a kódot
  - CPU
    - Out of order végrehajtás
      - különböző részek, különböző feladatokat hajthatnak végre egy idő alatt
      - Overlap-elhető utasításoknál lehet ilyen
      - Instruction cache
        - ha nem lesz különbség akkor megcserélhetnek műveleteket
    - Brench prediction
      - Meg se nézi a feltételt és kiszámolja, mejd amikor gazdaságos akkor megnézi
        - ha nem volt jó akkor visszacsinálja
  - Cache
    - Proseccor a cache-be ír, nem tudni mikor kerül ki a memóriába
    - Nem biztos, hogy minden szál ugyan azt látja
    - Hardver is nagyon számít
    - Intel (x64) erős cache koherencia
      - Ha olyan memóriaterületet módosít amit más processor is használ akkor szól a másiknak, hogy invalidálja a cache-ét
    - Arm, alpha
      - Nincs így
      - Intelnél sem tudjuk meddig lesz így mert költséges
  - Messze kerülhet a valóság a kódtól
    - Kódbeli trükközés nem biztos, hogy megjelenik majd a végrehajtásban
- Olyan nyelvi definíciót kell adni ami minden hardveren jól működik
  - Olyanon is amit még ki se találtak
- RR, andu v undo
  - debugger
  - úgy futtatod, hogy trace-el
  - minden eseményt nyomkövetnek
  - Tudsz időben visszafelé lépkedni
  - Azokat az eseményeket log-olják, amik változtatnak a program futásán
- C++ 98
  - Observable bahavior
  - Blackbox a generált program
  - Ha megfigyelem, akkor azt kell kiadnia mint amit a kódban kértem
  - IO műveletnél vagy a volatile változó olvasás és írásnál lehet megfigyelni
    - Volatile egymás közötti sorrendet meg kell tartani a fordítónak
    - Volatile és nem volatile sorrendje felcserélhető
- Firewallok
  - Ami elatta van nem lehet felő vinni
- Cache is jól működjön
  - Memory banger
  - Minden oprendszerben van ilyen
  - C++98-ban ezek nem szabvényos dolgok voltak
- C++11 memory model
  - Thread-ek közötti interakciókat meghatározza
  - Korlát a fordítóprogramokra
  - Egy szerződés a programozó és a rendszer között
    - Programozó data-race mentes kódos csinál
    - Cserében a fordító sequentiol-consistent programot generál
  - A nem blokkolt thread-ek előbb utóbb továbbhaladnak
  - Thread-ek garantálják
    - hogy ha írok egy változóba akkor előbb utóbb a többi thread is értesül róla
  - Happens-before relationship
    - A a B előtt ha
      - Egy thread-ben vannak és egymás előtt
      - Két thread-ben vannak és van közöttük szinkronizációs pont
  - Memory location
    - scalar
    - bitfield egyben van amíg 0 hosszú bitfield nem jön
    - Egy struct-ban két char az külön memory location
      - eddig ez lehetett egyben is
  - Data race
    - Két thread egy memory location-t akar elérni
    - És legalább az egyik nem atomikus
    - És nincs happens before a két művelet között
    - Ha van, akkor undefined behavior
  - Sequential consistency
    - szekvenciát szekvenciálisan hajtom végre
    - de az összes többi thread-ben is ebben a sorrendben látom
  - Több szint közül lehet választani
    - Legszigorúbb - sequential consistenci
    - Leggyengébb - memory_order_relaxed
  - Relaxed memory model
    - Lock-free algoritmusok
    - Compare-exchange
      - hardverben van atomikus swap
      - ha tudom én növelem, akkor true, ha más elállította, akkor false és nem írom felül rossz értékkel
      - addig próbálgatom amíg nem sikerül
  - Release memory order
    - memory_order_release
    - memory_order_aquire vagy memory_order_consume (jelenleg nem ajánlott)
      - elsőnél a release előtti dolgok hamarabb vannak mint az aquire utániak
      - másodiknál csak azok között van happens_before amik függenek a szinkronizált változótól
        - ha nem látja az adatfüggést, akkor nem frissíti
        - nem kell mindenki újraolvasnia a cache-ben

## Eszköztár

- std::thread
  - id, native_handle
  - Konstruktor
    - csinál objektumot de nem allokál az op-rendszerben
      - erőforrás burkoló objektum ez is
      - ebbe lehet majd move-olni
    - move konstruktor
    - leggyakoribb
      - függvényszerű végrehajtható valami
      - a cucc paraméterei, variadik, perfect forvarding
      - Ekkor lefoglalja az op-rendszer szálat és végrehajtja a függvényt
  - Nem másolható és értékadható
  - Swap-elhető
  - Hardware_concurency
    - visszaad valami számot
  - joinable
    - igaz ha nem volt join vagy detach
  - join
    - megvárja, hogy a szál befejeződjön
  - detach
    - mehet tovább
    - lemondok arról, hogy a szülője vagyok
  - ha nincs szülője amikor befejeződik - az system exception
    - ha nem engedtem el és meg se várom az veszélyes
    - kiránthatom a memóriát a gyerek alól
  - referencia paraméter mindig átmásolódik a thread-local memóriába
    - nem másolható és move-olható típust nem adhatok paraméternek
    - std:ref = pointer
  - scoped_thread, jthread
    - default join-ol a blokk végén
  - Berakható konténerbe
  - std::for_each
    - std::mem_fn
      - functor ami elmenti a member pointert
      - operator() a member pointerre meghívja a megadott függvényt
- Mutex
  - std::mutex
    - szemafor szerű
    - egyszerű
    - try_lock
      - nem lock-ol
      - lefoglal vagy hamissal tér vissza
  - std::recusive_mutex
    - sima mutex rekurzióban dead_lock
    - ez nem ad rekurzív függvényre dead_lock-ot
  - std::timed_mutex
    - try_lock_for
      - addig vár
      - utána mindenképp visszatér
    - try_lock_until
  - RAII a mutex zárolásra és feloldásra
    - std::lock_guard
      - nem másolható és move-olható
      - block-al tudok területi lock-ot csinálni
    - segéd függvény
      - std::lock
        - variadik
        - lock-olható mutex szerű cuccot lehet belerakni
        - vagy az összeset lerakja vagy egyiket se
        - vár amíg az összeset le tudja rakni
      - std::try_lock
        - visszatér és elmondja, hogy hanyadik lock nem sikerült
        - -1 ha sikerült lerakni
    - C++17
      - variadik lock
      - scoped_lock
    - std::unique_lock
      - olyan mint a lock guard
      - csak van saját unlock fgv-nye
      - move-olható
    - std::shared_lock
      - reader
      - std::shared_timed_mutex-re
      - std::lock_guard a writer lock
- std::once_flag
  - gyorsan le lehet kérdezni az állapotát
  - std::call_once
    - bebillenti a flag-et
    - és meghívja a megadott függvényt
    - ha be van billentve akkor már nem hívja meg a függvényt
- loac static thread safe inicializált
- Spin lock
  ```c++
  bool falg;
  std::mutex m;
  void wait_for_flag() {
    std::unique_lock<std::mutex> lk(m);
    while (!flag) {
      lk.unlock();
      std::this_thread::sleep_for(std::chrono::milliseconds(100));
      lk.lock();
    }
  }
  ```
- Condition variable
  - szóljanak ha fel kell kelnie a thread-nek
  - std::conditional_variable
    - notify_one
    - notify_all
    - wait
      - van egy mutex-e, unique_lock
      - és van egy predikátum függvény
        - thread_safe végrehajtom a pred-et
        - ha hamis akkor feloldom és elalszok
      - ha notify van akkor megint lock és pred ellenőrzés van
      - ha igaz lesz a pred, akkor kilépek a wait-ből
  - notification stateless
    - pl SIGNAL implementáció
    - pl consumer-producer
      - ha nincs egy consumer se akkor notification elveszhet
      - curious wakeup is lehet
    - fontos a predikátum helyes megírása
- Future - Promise
  - 76-77-ben már létezett ilyen
  - shared_future
  - hasonló mint a GO-ban
    - GO-ban nagyon jó a konkurencia
  - promis-ból lehet future-t kérni
    - promisra lehet set-et hívni
    - csak utána lehet a future-ből get-elni
  - std::async
    - csinál magában egy promis-t
    - azonnal visszaadja a future-t
    - kód továbbfuthat
    - közben a megadott függvényt egy másik szálon végrehajtja
    - ha kész a függvény akkor a future.get vissza tud téreni, addig várakozik
    - 0. paraméter
      - std::launch::async
        - egyből új szál indul
      - std::launch::deferred
        - csak a future get-nél fut csak le az f, nem indul szál
      - alapból optimalizál a rendszer és választ valamit
    - get be tud fagyni (van wait is)
      - lehet poll-ozni a future.wait_for-al
  - Exception átjön a promisból a future-ba
    - promise.set_value() - írok egyszer
    - prommise.set_exception() - hibát is adhatok
- Paralell STL
  - std::async-al meg lehetne csinálni
  - de így egyszerűbb
- C++20
  - continuation-monad-ok
    - task listák létrehozása
    - elvileg C++23
- Még mindig nem tudjuk, hogyan kell jó konkurens programot csinálni

# 11. EA

Compiling, linking

## Header file

- Interface és implementáció szétválasztása
- C-ben jobb mint C++-ban
- Privát és protected dolgokat nem kellene megosztani a header-ben
  - De ez technikai okok miatt kell
    - Mekkora hely kell az objektumnak
  - OO megsértése
- Körkörös függőségeket meg lehet szakítani
- Fel lehet bontani a kódot fordítási egységekre
  - Kell include, de le lehet fordítani, nem kell egyszere több dolgot fordítani
- Template
  - Gyártási eljárás
  - Headerben kell lennie
  - STL header only
    - Ha használom akkor parsolni kell ezeket a nagy header-eket
  - Fordítási idő meg tud nőni
    - PreCompiled header
  - Módisítás a függőségek miatt sok újrafordítást eredményezhet
- Baj ha sok include van a fájlban
  - Mindenki aki használja az is mindent include-ol
  - Header guard tud segíteni
- `#include <iosfwd>`
  - Minden iostream osztályt forward deklarál
  - 6-8 órás build-et lehet egy 45 perces unity build-et csinálni
- PIMPL
  - bináris kompatibilitás
  - szabvány erről ne beszél
  - shared object vagy dll van használva manapság
    - high frequncy trading-nél ez nem olyan jó
    - de lehet patch-elni a programot
    - Ha a DLL vagy SO-ban a header-t is módosítom akkor nem biztos, hogy megmarad a bináris kompatibilitás
      - statikus adattag lehet
      - nem virtuális member-t hozzá lehet adni
      - Könnyű hibázni, mert nincs hozzá rendes szabályozás
  - Pointeren keresztüli implementáció
    - Osztály deklaráció ami nem változik
    - Implentációra mutató pointer van csak
  - Van FAST PILMPL
    - Egy karakter tömbben tárolom el a PIMPL heap-es adatait
    - Alignment-re figyelni kell

## Template

- Nem csak az a baj, hogy az OO elveket megsérti, hogy a template implemetáció a header-ben van
- Az is baj, hogy minden példányosításhoz új kód generálódik
  - Nagyobb lesz a kódom minden új példányodításnál
  - Base osztály amiben a template független kódok vannak
    - Template leszármazott a függő részekhez

## C és C++ közös használat

- Nagyjából ua bináris formulára fordul le
- Virtuális dolgok máshogy fordulnak
- Mangle név C-ben nincs
- Extern C a régi C neveket generálja nem mangle nevet csinál
  - Overloading így nem lehet

## Template példányosítás helye

- Példányosításnál a template ast subtree-t másolom és behelyettesítek
  - Túlterhelés ellenőrzése ezután történik
- Elvileg jól definiált a hely, de gyakolatban ez nem így van
  - Implementációban az is lehet, hogy több helyen létrejön

## Link-elés

- Linkelés sorrendje számít
  - Lehet írni olyan kódot aminek az eredméye a link-elés sorrendjétől függ
  - Template-nél az elsőt használja, a többit eldobja
- Változónál az extern csak akkor számít ha nem inicializálom
- Inline -> weak referencia
  - Strong és strong -> hiba
  - Strong és weak -> strong
  - Weak és weak -> valamelyik
- Template is weak referencia

## Statikus inicializálás/törlés

- Ha static-ok inicializálódnak akkor minden függőségnek léteznie kell
  - Nem biztos, hogy jó a konstruálási sorrend
  - Jó lehet ha a függőség metódusát hívom (getter a változó helyett)
    - Létre kell jönnie
- Inicializálási sorrend jó lesz
  - de a destruálási sorrend rossz lesz
  - fagyással zárul a program
  - quick exit jó lehet, mert akkor nem destruál
  - Főnix pattern
    - újraéled
- Swchartz counter
  - Biztosítja, hogy az includ-oló object-ekben biztosított a statikus élettartamot

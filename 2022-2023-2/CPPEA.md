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
    - char t[] vagy char *s
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






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

        




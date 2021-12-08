# Konkurens programozás EA 2021.09.08

Egymástól független tevékenységek futnak egyszerre és néha adatokat cserélnek.  
Alkalmazás több független részből áll össze.
(Párhuzamosság hatékonyabb manapság.)

## Kommunikációs modellek
- Megosztott (shared) memória
    - több processzor ugyan azt a memóriaterületet éri el
    - Egyzerűbbnek tűnik, de könnyebb elrontani
    - Java
- Elosztott (distributed) memoria
    - Mindenkinek saját memória
    - Üzenet csatornák
    - Kevesebbet hibázik a programozó
    - Erlang, Go

## Kevesebb processzor, mint folyamat
- A processzorok váltogatnak a folyamatok között
- Mindegyiket csak kis ideig futnak
- Párhuzamosság látszata
- Ütemező
- A folyamatok ne tartsák fel egymást

## Párhuzamosság
- Végrahajtási szálak (thread)
- JVM szálakkal foglalkozunk
- Shaered memory model

## Szálak a Javában
- thread szál - folyamat a gépben
- java.lang.Thread - kezelő osztály

## Nehézség
- Nemdeterminisztikusság
- Nehéz/lehetetlen átlátni
- Kezelendő
    - ütemezés
    - interferencia - önállóan jók, de együtt összeakadnak
    - szinkronizáció
    - kommunikáció
- Probléma: tesztelés, reprodukálhatóság

## Végrehajtási szálak létrehozása
- Főprogram egy végrehajtási szál
- Továbbiak létrehozhatóak
- A Thread osztály példányosítható
- Az objektum start() metóduasival indítjuk a szálat
- A szál programja az objektum run() metódusában van (virtual)

- `(new Thread).start();`
```java  
//Saját Thread-ünk mit csinál
class MyThread extends Thread {
    @Override public void run(){
        while(true) System.out.println("Hi!");
    }
}
```
- Névtelen osztály  
```java  
class Main {
    public static void main( String args[] ){
        (new Thread() {
            @Override public void run(){
                while(true) System.out.println("Hi!");
            }
        }).start();
    }
}
```

## Nemdeterminisztikus viselkedés
- Ütemezéstől függ
- A nyelv nem tesz az ütemezőre megkötést
- Különböző platformokon máshogy működhetnek
- A VM meghatározhatja a stratégiát, de azon belül is sok lehetőség van
- Sok mindentől függ (pl.: milyen meleg van)

## Ütemezési stratégia
- Run to completion
    - Addig fut ameddig lehet (hatékonyabb)
    - pl.: embededd
- Preemptive
    - időosztésos
    - időnként elveszi a vezérlést
    - pl.: átlag gépek

# Konkurens EA 2021.09.15

## Runnable interface
- Thread leszármazás ellövi az egyszeres öröklődést
- Ezért a Runnable interface-t kell implementálni és így megmarad az öröklődés
- Kell a run() override és a Thread-et kell létrehozni Runnable-vel
```java
class Hello {
    public static void main( String args[] ) {
        new Thread(new MyRunnable()).start();
        ...
    }
}

class MyRunnable implements Runnabele {
    @Override public void run() {
        ...
    }
}
```
- java.lang csomagban van, csak run()-t tartalmaz
- lehet névtelen osztállyal is
- lambda kif. lesz a run metódus
    - run() nulla param
    - lambda nulla param
```java
class Hello {
    public static void main( String args[] ) {
        new Thread( () -> {
            //func body
            System.out.ptintln("Hi!");
        }).start();
        ...
    }
}
```

## join()
- Szálak közötti szinkronizáció
- Interrupt-al meg lehet állítani a szálat
    - Exception-ként visszajöhet a szál
```java
Thread t = new Thread( ()-> {...});
t.start()
...
try {
    t.join();
} catch ( InterruptedException e ) {
    // main has been interrupted
}
```
- példa, rendezés két szálon
    - join() várja meg, hogy kész legyen a rész rendezés
```java
public void sort ( int[] data ) throws InterruptedException {
    int middle = data.length / 2;
    int[] left = java.util.Arrays.copyOfRange(data,0,middle);
    Thread t = new Thread( () -> java.util.Arrays.sort(left) );
    t.start();
    java.util.Arrays.sort(data,middle,fdata.length);
    t.join();
    merge(data, middle, left);
}
```

## Szál életciklusa
- Létrejött állapot
- start()-al elindul a szál
- Futtatható állapotba lép
- Ha a futtató környezet úgy dönt akkor elkezdi futtatni
- Futó állapot
- Ha a run() elfogy akkor
- Véget ért állapot - vége az objektumnak
- Hosszú futásnál az ütemező megállítja - yield() metódussal lemond a futás jogáról
- Futtatható állapot
- Blokkolt állapotba juthat 
    - pl join() várakozás
        - a szál befejeződjön vagy interrupt felébressze
    - pl wait() ahonnan egy notify()-al lehet felébreszteni
    - pl sleep()-el egy ideig vár
    - pl IO várakozás, java.io blokkolt io rendszer
    - Futtathatóba juthat
- Vannak létező, de depricated műveletek
    - stop() -> Véget ért állapotba viszi mindig, 
        - kinyírja akármit is csinál, 
        - blokkolt erőforrást nem tud felszabadítani
        - van jobb megoldás
    - suspend() -> Blokkolt állapotba viszi, resume() párja
    - resume() -> Blokkoltból futtathatóba rakja, suspend() párja
        - erőforrások beragadnak
        - szálak összeakadnak
    - **holtpontgyanús metódusok**
- Thread.State enum tartalmazza a dolgokat

## Interferencia
- Két jó program zavarja egymást
- Race condition
    - El kell kerülni

# EA 3 2021.09.22

- Össze kell hangolni a folyamatokat
    - szinkronizáció
- Interferencia nem mindig működik

## Példa 1
```java
class Számla {
    int egyenleg;
    public void rátesz( int összeg ){
        egyenleg += összeg; //nem atomi művelet
        //int újEgyenleg;
        //újEyeneleg = egyenleg + összeg;
        //egyenleg = újEgyenleg;
        //Így már látszik hogy hol lehet a több szállal a probléma
    }
} 
```

- Az adatokhoz való hozzáférés szerializálása
    - Kölcsönös kizárás (mutual exclusion)
    - Kritikus szakasz (critical section)

- Többféle megoldás
    - Bináris szemafor
    - Monitor - mi most erre fogunk koncentrálni - középső megoldás
    - Író-olvasó szinkronizáció

- Monitor
    - még nem volt oop de ez már majdnem az

## Példa 1 - javítás
```java
class Számla {
    //így csak a műveletekkel lehet manipulálni a belső állapotot
    private int egyenleg;
    //így már szálbiztos - egy időben csak egy helyen futhat ez a függvény
    // a többi hívás addig vár
    public synchronized void rátesz( int összeg ){
        egyenleg += összeg;
    }
} 
``` 
- Minden objektumhoz tartozik egy kulcs (lock) és egy várakozási sor
    - kérek kulcsot, végrehajtom a szinkronizált metódust, visszaadom
    - amig nem kapok kulcsot addig bekerülök a várakozási sorba
    - az objektumnak van kulcsa, nem a metódusnak
        - az összes metódus lehet `synchronized`
## Példa 1 - javítás 2
```java
class Számla {
    private int egyenleg;
    public synchronized void rátesz( int összeg ){
        egyenleg += összeg;
    }
    public synchronized void kivesz( int összeg )
            throws SzámlaTúllépés() {
        ...
    }
} 
``` 

## Szál megállítás
- `stop()` deprecated 
- kell egy boolean flag amit figyelnie kell
- ha átbillen a flag, akkor rendet rak maga után és megáll
- a többi szál is használja a flag-eh, mert ők akarnak jelezni
```java
class MyAnim extends ... implements Runnable {
    private boolean running = false;
    public synchronized void startAnim(){
        running = true;
        (new Thread(this)).start();
    }
    public synchronized void stopAnim(){
        running = false;
    }
    public synchronized boolean isRunning(){
        return runnig;
    }
    ...
    @Override public void run(){
        while( isRunning() ){
            // one step of the animation
            try{ sleep(20); }
            catch(InterruptedException e){...}
        }
    }
    ...
}
```

## Szinkronizált blokkok
- Nem csak metódus, de utasítás is lehet szinkronizált
    - csak kisebb része kritikus
    - felesleges várakoztatás lenne a többi
    - elég csak a kritikus részt bezárni
- blokk utasításnál van ilyen extra verziója
- `synchronized(obj){...}`
    - az adott objektum kulcsát kéri
    - ha megvan a kulcs, akkor megcsinálja a blokkbeli cuccokat
- kliensoldali zárolás, ha nem szinkronizált
    - `synchronized(számla){ számla.rátesz(100); }`
    - figyelni kell, hogy minden hívásnál megcsináljam
    - ha valahol kimarad, akkor race condition lesz
- osztály zárása biztonságosabb, potenciális hiba lokálisan megoldva

- **Ökölszabály**
    - szálak közös változót használnak, akkor kell valamilyen szinkronizáció
    - így kevesebb hiba lesz
    - ezt gyakoroljuk ebben a félévben

- néha meg kell törni a monitor szemléletet
    - több helyen tárolt adatból van probléma
    - pl.: többféle erőforrás kell neki egyszerre

## Egymásba rakott dolgok
```java
class A {
    synchronized void m1(){...}
    // nem lesz holtpont, tudja, hogy nála van a kulcs
    synchronized void m2(){... m1() ...}
}
```
- nem kéri újra a kulcsot, mert már nála van
- számlálja, hogy hányszor kérte ki és csak a végén rakja vissza a kulcsot

```java
class A {
    synchronized void m1(){...}
    synchronized void m2(B b){... b.m1() ...}
}
class B {
    synchronized void m1(){...}
    synchronized void m2(A a){... a.m1() ...}
}
```
- Egyik szálban: a.m2(b)
- Másik szálban: b.m2(a)
- Nem lesz interferencia, de holtpont igen
- most túlszinkronalizált lett

# EA 4 2021.09.29

## Holtpont probléma
- Túlszinkronizálás
- Folyamatok egy halmaza kerülhet holtpontba
    - Nem tud továbblépni
- Nincs univerzális megoldás
    - Programozó dolga
- Folyamatok leállítása és így megszüntetni a holtpontot
    - Megfelelő erőforrás felszabadítással
- Detektálás, megszüntetés
- Timeout, ne várakozzon végtelenségig
    - Mondjon le az erőforrásról
    - Próbálja újra
        - Lehet végtelen újra próbálás "ciklus"
- Gráfos ábrázolásban látszódhatnak problémák
    - lassítások 
- Megelőzés
    - Figyeljünk arra, hogy ne alakuljon ki
    - erőforrások, folyamatok sorba állítása
    - Szimmetriák megtörése
    - Folyamatok súlyozása
        - Erősebb kapja meg az erőforrást hamarabb
        - Kiéheztetés veszélye
    - Erőforrások súlyozása
        - pl Oprendszereknél
        - Kisebb utána a nagyobb erőforrás
        - Általánosan holtpont elkerülő stratégia
        - Csak akkor működik ha előre lehet tudni az erőforrás szükségletet
- Központi irányítás
- Véletlen szüneteltetés

## Példa
```java
class Számla {
    private int egyenleg;
    public synchronized void rátesz( int összeg ){
        egyenleg += összeg;
    }
    public synchronized void kivesz( int összeg )
            throws SzámlaTúllépés() {
        ...
    }

    // Ha ez is sync akkor pénz cserénél holtpont
    public void átutal (int összeg, Számla másik)
            throws SzámlaTúllépés() {
        kivesz(összeg);
        másik.rátesz(összeg);
        // Fordított sorrendben elromolhat ha nincs elég pénzem
    }
} 
``` 
- Bonyolult megoldás nem jó
    - másik programozó hozzáfejleszt és elronthatja az egyedi szinkron megoldást
- Szét kell választani a monitor és a sima működéseket
    - Külön `Számla` és `Bank` osztály
    - A sima osztály szinkronságát a támaszkodó szink. osztályok biztosítják

## Példa
```java
class Bank {

    public void átutal (int összeg, Számla innen, Számla ide)
            throws SzámlaTúllépés() {
        innen.kivesz(összeg);
        ide.rátesz(összeg);
    }
    // átutalás közben kétszer számolhat egy pénz össszeget
    public long vagyon( Számla[] számlák){
        long összeg = 0L;
        for( Számla számla: Számlák){
            összeg += számla.egyenleg();
        }
        return összeg;
    }
} 
``` 
- Ha az egész bank szink. akkor nem lehet több utalás egyszerre

## Több erőforrás szinkronizált blokkokkal
- Egy közös Objektum Lock az összes erőforráshoz
- Kliens oldali zárolás
- De így nem tudnak egyszerre dolgozni

## Szinkronizált adatszerkezetek
- Alap java dolgok nem sync-ek
- ArrayList helyett java.util.Vector (szálbiztos)
- Map helyett java.util.HashTable (szálbiztos)
- java.util.Collections
    - synchronizedCollection
    - synchronizedList
    - synchronizedSet
    - csomagoló a régi objektumoknak
    - szálbiztosítás
```java
List lst = Collections.synchronizedList(new ArrayList<Integer>());
```
- ArrayList lesz használva belül
    - kívülről szálbiztos
- ArrayList-re nem szabad megtartani a referenciát
    - ne lehessen a wrapper nélkül belenyúlni
- Iterátorokkal baj lehet
    - többszálú iteráció problémás lehet
    - külön kell szinkronizálni pl sync. blokk a listára
    - igaz a `for(Integer n: lst)`-re is

# EA 5 2021.10.06

## Memoriafelhasználás
- Java a stack-et meg a Heap-et használja
- Stack-en a szálak cucca
- Heap-en a mindenki által elérhetőek
- Stack-en a run metódus kerül be
- Daemon szálak futhatnak a main után is
    - setDeamon(true)
- Erőszakos leállításnál megáll minden
- Típus alapján dől el hogy hova kerül
- A stack-re kerül egy referencia a Heap-beli cuccról
- Cache memória fontos
- egy adathoz hány szál fér hozzá a heap-ről
- Referenciák nem kell kiszökjenek a szálból
- Stack adatai biztonságban - biztos?
    - nem fér hozzá más
    - szintaktikus dolgok vannak
    - de ez át lesz alakítva
    - biztos
    
# EA 6 2021.10.13
- fial kulcsszó
    - osztály: nem lehet leszármazni
    - metódus: nem lehet felüldefiniálni
    - változó: nem lehet módosítani, nem lehet nem lokális, nem igényel szinkronizálást
        - másolatot csinál a final local-ról ha bárhova tovább adódik
        - szálaknál is másolódik
        - ha referencia típusú akkor már lehet ban
            - amire hivatkozik azt szinkronizálni kell
    - mezők: általában nincs probléma ezekkel szinkronizálás szintjén 
        - módosíthatatlanok
        - ha referencia, akkor a hivatkozott objektum is legyen módosíthatatlan vagy szinkronizált
    
- Helyes működést nem áldozzuk fel a hatékonyságért
    - helyes, egyszerű és karbantartható fontasobb mint gyors
    - kód 10% fut az idő 90%-ában
        - csak ezt kell gyorsabbra írni
        - nem kell az egészet
        - fontosabb a helyesség, olvashatóság, tesztelhetőség
    - helyesség:
        - hibás az a program ami szink. nélkül oszt meg változtatható adatokat, erőforrásokat
        - jó minta:
            - feladatok kiosztása
            - végül adatok begyűjtése
        - megosztott változó ne legyen módosítható
        - használni kell szinkronizációt

- Módosíthatatlan adatok
    - Obj. aminek minden mezője final, hivatkozott objektumok is módosíthatatlanok
    - Funkcionális stílusú programozás
    - Új értékek új objektumban jönnek létre
    - Szekvenciális programban: overhead

- Szálak gyorsítják
    - szinkronizáció lassítja
    - ezért jó a funkcionális stílus
        - több memória
        - szemétgyűjtő sokat dolgozhat
        - de még így is jobb lehet, mint a szinkronizálgatás

- Integer, String módosíthatatlanok

# EA 7 2021.10.20

## Példa végigmagyarázása
- Java Concurency In Practice könyvből egy példa
- creative commons
- Járműflotta adatai
- Funkciók
    - getLocation() -> hol van
    - setLoaction(id,x,y) -> jármű írja hogy hol jár
- MutablePoint-al tartja számon
- Monitoros megoldás
    - Belső állapot megvédése a külső dolgoktól
    - Belső adatról (Map) csak deepCopy-val kapcsolódik a külvilághoz
    - syncronized metódusok
- Collection.unmodifiableMap
    - unmodifiable wrapper osztályok
    - put, remove kivételt dob
    - get működik
    - Mély másolat + unmodifiable = biztos nem kerül ki a belső állapot
- Pontok cseréje ImmutablePointra
    - final int x, y;
- java.util.concurent.ConcurentMap
    - konkurens programban használható
    - ez nem sync
    - egyszerre többen dolgozhatnak rajta, ha nem zavarják egymást
    - java.util.concurent.ConcurentHashMap
        - tuningolt hash map
        - ugyanúgy lehet használni, mint a hash map-et
        - a háttérben más történik
- Ezekkel
    - konstruktor a kapott map-ből egy concurentHashMap-et csinál
        - ez shalow copy de nem baj mert ImmutablePoint meg String van benne, azok módosíthatatlanok
    - getLocation csak visszaad egy unmodifiableMap-et
        - nem kell copy mert nem tudják módosítani
        - Pontokról sem kell copy mert ImmutablePoint-ok
    - másolásokat lehet spórolni
    - getLocation - ImmutablePoint-ot visszaad
    - setLocation - ki kell dobni a régi pontot egy újjal

- SafePoint
    - sync set, get

- Concurent dolgok:
    - ...
    - BlockingQueue
    - BlockingDequeu

# EA 8 2021.11.03

## Feladat dekompozíció
- Párhuzamos for ciklus
    - Ciklusmagok egy időben végrehajtódnak
    - Ciklusmagban új szálak
    - Ciklus után mindenkit bevárni
    - `Array.setAll(threads, i -> new Thread(...))`
        - Ez után mindet el kell indítani
        - Majd mindet bevárni
- Több szál, mint ciklus
    - Nem segít
    - A sok szál létrehozása lassítja a dolgot
    - Le lehet kérdezni a rendelkezésre álló magok számát
        - `Runtime.getRuntime().availabelThreads()`
- Munkát jól kell kiosztani
    - Minden szál ugyanannyi feladattal
    - Ne maradjanak üres járatban
    - Ha a részfeladatok nehézsége változó, akkor nehezebb elosztani
    - Feladatok tudjanak választani és ha kész vannak, akkor újakat kapjanak
    - Feladat mérete kritikus
        - túl nagy, akkor nem lehet rendesen párhuzamosítani
        - túl kicsi, akkor versengés, ütemezési overhead
    - Feladatok és szálak explicit összekapcsolása: skálázási probléma
        - Ha nem explicit, akkor több magos gépen jobb lesz
    
### Executor Interface
- Runnable - paraméter nélküli, visszatérés nélküli, exception nélküli run függvény
- Executor - Runnable paraméterű, RejectedExecutionException-t dobó execute függvény
    - sok féle executor lehet
    - okosabb megoldás
    - Thread pool-t használ általában
- Factory: Executors
    - newCachedThreadPool()
        - semmittevő szálnak adja, vagy indít
    - newFixedThreadPool(int nThreads)
        - fix db szálnak adogatja, amikor van végzett szál
    - sewSingleThreadExecutor()
        - egy szál dolgozik
- WebServer
    - Ha szekvenciálisan van kiszolgálva, akkor várakozni kell a többi klienshez
    - Ha jön kliens, akkor egy szál kiszolgálja
        - jó amíg nincs túl sok egyszerre
    - Ha sok kliens jön, akkor executor-ban fix szálon sorban feldolgozom
        - N darab szálat adok az executor-nak
            - ha nem a cpu a korlát, pl io (internet, disk)
                - akkor lehet több szál mint mag
        - neki bedobom a feladatokat
        - ő majd kiosztja az adott szálaknak
        
#### Életciklus kezelés - ExecutorService
- shutDown()
    - az eddigieket befejezi
    - de újat nem fogad
- shutDownNow()
    - a futókat megvárja
    - ami nem kezdődött el azt nem indítja el
    - újat nem fogad
- isShutDown()
- isTerminated()
- awaitTermination(long, TimeUnit) throws InterruptedException
    - vár egy bizonyos ideig, hogy minden leálljon
    - utána lelövi
- sunmit
    - Future < T > - ez eredményt tud tartalmazni, amint végez
    - várakoztat amíg nem készül el
    - get()
    - Általában Callable cuccot adunk
        - call() - van return meg exception
- invokeAll
- invokeAny

# EA 9 2021.11.10

## Életciklus kezelés
- stop függvény
- Nem lehet egy komponenesben sem végtelen várakozás
    - elrontja a többit is

## Future
- Más nyleveken hasonló a `Promise`
- Future-el meg lehet várni az eredméynt
```java
BigInteger compute(BigInteger input){...}
...
ExecutorService exec = ...
...
Future<BigInteger> asyncResult = exec.submit(()->compuet(input));
...
BigInteger result = asyncResult.get();
// Itt várni fog a szálra és az eredméynére
```
- Feature of Unknown
    - `Future<?>`
    - Várakoztatásra lehet használni
    - Runnable elemeknél hasonlíta join-ra

 # EA 10 2021.11.17

 ## Termelő-Fogyasztó feladat
 - Egyik lépést az egyik, másik lépést a másik csinálja
 - Randevú
    - a kommunikációhoz bevárják egymást
    - várakozások vannak
- Más processzoron lehet más feladatot csinálni
    - cél feladatot cél eszközön
    - hatékonyabb munkamegosztás
- Termelő fogyasztó
    - egy helyen gyűjti a kész dolgokat
    - abbol a pool-ból szedeget feladatot a másik
    - van középen egy buffer
    - jobb kihasználtságot eredményezhet
    - minnél nagyobb a buffer
        - annál aszinkronabbak lehetnek a feladatok
    - sor adatszerkezetben adják át az adatokat
- Van ahol a randevú is jó
- Lehet bármennyi termelő és fogyasztó
- Lehet több buffer is
- Megfelelő sor lehet
    - `BlockingQueue`
    - `take` - üresnél vár
    - `put` - telinél vár
    - `java.util.concurent.ArrayBlockingQueue`
    - `java.util.concurent.LinkedBlockingQueue`
- Be kell hangol ni a dolgokat
    - ne legyen túl sok erőforrás lekötve
    - ne kelljent sokat várni egyik folyamatnak sem

| Throws exception | Spacial value | Block | Times out |
| :---: | :---: | :---: | :---: |
| add(e) | offer(e) | put(e) | offer(e,time,unit) |
| remove() | poll() | take() | poll(e,time,unit) |
| element() | peek() | - | - |

- Első a szekvenciális megoldás
- Harmadik a konkurens
- Második egyszerűbb mint a exception
- Negyedik csak egy ideig blokkol

- BlockingQueue helyett vannak más módszerek is
    - Egy termelő - egy fogyasztónál
        - `java.io.stream`
        - PipedInputStream, PipedOutputStream
        - PipedReader, PipedReader
        - buffer implementálva
        - blokkolások implementálva
        - available(), ready()
            - meg lehet nézni hogy blokkol-e a művelet
        - Az egyik konstruktorában meg kell adni a másikat
        - `DataOutputStream` - alap típúsoknál megvalósítja az átalakításokat
        - write-ok után `flush` kell, hogy tényleg átmenjen az adat
    - lehet ebből kétirányú kommunikáció is
    - socket alapú kommunikáció is ilyen
        - a processek lehetnek bárhol az interneten
        - socket.getInputStream()
        - socket.getOutputStream()
        - client:
            - s = new Socket("ip",port)
        - server:
            - ss = new ServerSocket(port)
            - Socket s = ss.accept();

# EA 11 2021.11.24

## Wit/notify
- Jelzésig várakoztatni egy folyamatot
- Thread.yield() átengedheti a vezérlést, de lehet nem csinál semmit
- wait(), notify() régót a java-ban van
- pattern
```java
synchronized in() {
    obj.notify();
}

synchronized out() {
    while(...) {
        obj.wait();
    }
}
```
- a wait azt a kulcsot engedi el amire meghívtuk
    - a többit nem
    - wait-set-be kerül
- notify csak egy wait-et ébreszt fel
- a wait várhat a végtelenségig
    - meg lehet neki adni időkorlátot
- notify csak egy szignál
    - ha nem vár semmi, akkor nel lesz baj
- ha a telit is nézzük, akkor a berakás is várakozhat
- notifyAll - mindenkit felébreszt
    - lehet, hogy sok újra wait-el
    - de valaki tovább tud menni

- ki lehet egészíteni lock-okkal és lock.newCondition()-el
    - condition-re lehet .await()-el várakozni
    - .signal()-el lehet jelezni, hogy mehet tovább

# EA 12 2021.12.01

## Megszakítás
- Szálbiztos flag-el lehet hesználni és a hosszú műveletbe lehet ezt viszgálni a megálláshoz
- java.util.concurrent.atomic.AtomicBoolean
- volatiole változó
    - ha egy szál beleír, akkor a többi szál is látja
    - nem tud annyit mint az Atomic, de könnyebb
    - ilyen flag-nél ez kb elég is
- Interrupt mehanizmus
    - belső flag
    - bool check helyett Thread.interrupted()
        - futtató szálat kérdezi le
        - nem csak lekérdezi, false-re is állítja
        - obj.isInterrupted() csak lekérdezi
            - Thread.currentThread().isInterrupted()
    - megállítás: .interrupt()

## Explicit zároló
- Lock jobb mint a synchronized
- Nehezebb mint a nyelvi megoldás
    - de többet tud
- tud tryLock()-ot
    - Lehet várási időt is megadni
- Több metódushíváson keresztül is lehet lock
    - Lehet egy hívott függvényben az unlock
- Olvasás-írás kürön lock
    - olvasást eleleht engedni hamarabb

## Vizsga
- Canvas-en minden info

# EA 13 2021.12.08

## Félbeszakítás
- Jelezhetjük, hogy álljon meg vagy induljon tovább
- Future.cancel() - olyan mint az interrupt
- ExecutorService - shutdown, shutdownNow
- InterruptedExceptiont dobó függvények felkészültek az interrupt-ra

## CountDownLatch
- .countDown()
- .await()
- másik szinkronizációs megoldás
    - késleletetni lehet dolgokat

## GUI programozás
- GUI egy szálon tud rendesen működni
- java -> egy szál ami kezeli a gui-t
    - event dispatch thread
    
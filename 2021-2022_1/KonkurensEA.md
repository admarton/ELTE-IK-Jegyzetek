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
- Ütememző
- A folyamatok ne tartsák fel egymást

## Párhuzamosság
- Végrahajtási szálak (thread)
- JVM szálakkal fogakozunk
- Shaered memory model

## Szálak a Javában
- thread szál - folyamat a gépben
- java.lang.Thread - kezelő osztály

## Nehézség
- Nemdeterminisztikusság
- Nehéz/lehetetlen átlátni
- Kezelendő
    - ütememzés
    - interferencia - önállóan jók, de együtt összeakadnak
    - szinkronizáció
    - kommunikáció
- Probléma: tesztelés, reprodukálhatóság

## Végrehajtási szálak létrehozása
- Főprogram egy végrahajtási szál
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
- A VM meghatározhatja a stratégiát de azon belül is sok lehetőség van
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
- Vannak létező de depricated műveletek
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
- Nem csak metódus de utasítás is lehet szinkronizált
    - csak kisebb része kritikus
    - felesleges várakoztatás lenne a többi
    - elég csak a kritikus részt bezárni
- blokk utasításnal van ilyen extra verziója
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

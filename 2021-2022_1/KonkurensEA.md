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
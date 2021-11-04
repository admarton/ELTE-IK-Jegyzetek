# Konkurens Programozás GY 2021.09.09

## Számonkérés
- Lovarda vizsga
- 1 beadandó, nincs jegy

## Tanagyag
- Párhuzamos problémák megoldása
- Nem biztos, hogy előjön a hiba.

## Jövőhéten 5-kor lesz óra

```java
package hu.elte.konkurens;

public class Fo {
    public static void main(String args[]) {
        if(args.length == 0) {
            System.out.println("ASD");
        } else {
            for(int i=0; i<args.length; ++i){
                System.out.println(args[i]);
                System.out.println(factor(args[i].length()));
            }
        }
    }

    private static long factor(long n) {
        if(n ==0){
            return 1;
        }
        return n * factor(n-1);
    }
}

```

# GYAK 2021.09.16

- Az állapot átmenet a problémás
- Bárhány szál jól tud működni ameddig nem kell egymással kapcsolatba lépniük
- Szál a java jelenlegi verziójában minden szálhoz, ami a JVM-en fut akkor Windows-ban is annyi szál fut
    - Dockerben is látja a host az összes szálat
- Szál objektum létezik
- Szál csak start-nál jön létre
- Szál neve: Thread.currentThread().getName()
- A főszál a main
- `native` futási időben natív libből kapja az implementációt

```java
package hu.elte.marci;

public class Szalak {
    public static void main(String[] args) {
        Thread t0 = new MyThread();
        t0.start();
        //t0.run();
        System.out.println("hello from  " + Thread.currentThread().getName();
    }

    private static class MyThread extends Thread {
        @Override
        public void run() {
            System.out.println("hello from " + Thread.currentThread().getName());
            //Szalak.main(null);
        }
    }
}
```
- Thread-et nem szabad kiterjeszteni
    - új osztály kell és implementáljuk a `Runnable` interface-t
    - Készíts egy osztályt, ami külön szálon lehet futtatni az ezt jelenti
```java
package hu.elte.marci;

public class Szalak {
    public static void main(String[] args) {
        Thread t0 = new Thread(new MyRunnable());
        t0.start();

        Thread t1 = new Thread(new Runnable() {
            public void run(){
                MyRunnable.printHello();
            }
        });
        t1.start();

        MyRunnable.printHello();
    }

    private static class MyRunnable implements Runnable {
        @Override
        public void run() {
            printHello();
        }

        public static void printHello() {
            System.out.println("hello from "+Thread.currentThread().getName());
        }
    }
}
```

- Functional interface
    - egy darab absztrakt metódusa van
    - be lehet az osztály helyére egy darab függvényt adni
    - pl lambda függvényt
```java
Thread t = new Thread(() -> {
    System.out.println("fib("+j+") = "+fib(j));
});
```

- Final int kell neki mert megváltozhat ameddig elindul a szál
    - `int j = i` után j jó lesz mert effective final, nem változik meg a j értéke
```java
for (int i = 0; i < 100; ++i){
    int j = i;
    Thread t = new Thread(() -> {
        System.out.println("fib("+j+") = "+fib(j));
    });
    t.start();
    threads.add(t);
}
```

# GYAK 3 2021.09.23

- InterruptedException vizsgálat
- szinkronizáció alapjai
- Csak a main szál exception számít a program végén
- `Thread.interrupted()` -> törli ezt az állapotot
- `Thread.currentThread().isInterrupted()` -> nem törli elsőre
- `synchronized` mutex-el egy objektumra
- Random-ot tesztelésnél seed-el kell használni
- Minden szál aludjon min 300 sec max 500 sec
    - arra gondolnak h Random(200)+300

- két beadandó
    - 15/15 pont
    - zh 20 elm
    - zh 30 gyak
- 51-ponttól 2-es, 85 ponttól 5-ös

```java
package hu.elte.marci;

import java.util.Random;

public class Gy3 {
    public static void main(String[] args) throws InterruptedException {
        Random randomGenerator = new Random();
        for (int i = 0; i < 10; i++) {
            System.out.println("random: "+randomGenerator.nextInt(100));
        }
        Object o = new Object();
        Thread.sleep(1);
        Thread t = new Thread(() -> {
            synchronized (o) {
                try {
                    for (int i = 0; i < 50_000; i++) {

                        System.out.println(i);
                        if (Thread.interrupted())
                            throw new InterruptedException("counting was interrupted");
                    }
                    System.out.printf("Finnished");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
        // t.start();
        Thread.sleep(50);
        synchronized (o) {
            t.interrupt();
            System.out.printf("Interrupted");
        }

    }
}
```

- 100 szál, random szám 1000 és 5000 között, tökéletes szám-e, osztóinak összege a szám kétszerese
```java
package hu.elte.marci;

import java.util.Random;

public class Gy3 {
    public static boolean IsPerfect(int num){
        int sum = 1;
        for (int i = 2; i < num; i++) {
            if(num%i==0){
                sum += i;
            }
        }
        if(sum == num){
            return true;
        }else{
            return false;
        }
    }

    public static void main(String[] args) throws InterruptedException {
        Random randomGenerator = new Random();
        Object o = new Object();
        int[] eredmeny = {-1};

        for (int i = 0; i < 100; i++) {
            Thread t = new Thread(() -> {
                while(eredmeny[0]==-1){
                    int num = randomGenerator.nextInt(1000)+8000;
                    boolean p = IsPerfect(num);
                    System.out.println("Current num: "+num+(p?" is perfect":" is not perfect"));
                    if(p){
                        synchronized (o) {
                            eredmeny[0] = num;
                            System.out.println("A végeredmény: "+eredmeny[0]);
                        }
                    }
                }
            });
            t.start();
        }
    }
}
```

# GYak 4 2021.09.30

```java
package hu.elte.marci;

import java.util.Random;

public class WaitNotify {
    private static boolean t1Has = true;

    public static void main(String[] args) {
        Object o = new Object();
        Thread t1 = new Thread(() -> {
            synchronized (o) {
                while(true){
                    if(t1Has){
                        sleepRandom();
                        System.out.println("t1 is running");
                        t1Has = false;
                        o.notify();
                        try {
                            o.wait();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        });
        Thread t2 = new Thread(()->{
            synchronized (o) {
                while(true){
                    if(!t1Has){
                        sleepRandom();
                        System.out.println("t2 is running");
                        t1Has = true;
                        o.notifyAll();
                        try {
                            o.wait();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        });

        t1.start();
        t2.start();
    }

    public static void sleepRandom() {
        try {
            Thread.sleep(new Random().nextInt(10));
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

# Gyak 5 2021.10.07

- ctrl+alt+shift+L a formázás inteliij

## Konkurencia kezelés, kizárásbiztosítás
- szemafor
```java
import java.util.concurrent.Semaphore;
Semaphore semaphore = new Semaphore(1);
try {
    semaphore.acquire();
    //munka
    semaphore.release();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```
- Lehet több permitet is kérni, adni, lefoglalni
- Drain Permits -összeset lekéri
    - Összeset visszaadja ami van szabadon
- availablePermits()
- acquireUninterruptibly()
- tryAcquire() - ha nincs akkor false, ha true akkor lefoglalta
- tryAcquire(2,10, TimeUnit.MILLISECONDS) - ez várhat
- kiéheztetés ellen lehet fair semaphore 
    - ezzel jobb mint a sima sync

```java
package hu.elte.marci;

import java.util.Random;
import java.util.concurrent.Semaphore;
import java.util.concurrent.TimeUnit;

public class semaphorMain {
    public static void main(String[] args) {
        Semaphore semaphore = new Semaphore(3, true);
        for (int i = 0; i < 3; i++) {
            int j = i;
            new Thread(() -> {
                while (true) {
                    try {
                        if (j == 2) {
                            semaphore.acquire(3);
                        } else {
                            semaphore.acquire();
                        }
                        try {
                            System.out.println(Thread.currentThread().getName() + "\tsays Hi!");
                            Thread.sleep(new Random().nextInt(200) + 100);
                        } catch (InterruptedException e) {
                            throw new IllegalStateException("cannot sleep", e);
                        } finally {
                            if (j == 2) {
                                semaphore.release(3);
                            } else {
                                semaphore.release();
                            }
                        }
                    } catch (InterruptedException e) {
                        throw new IllegalStateException("cannot get permit", e);
                    }
                }
            }).start();
        }
    }
}
```
## Feladat 
- szálnak azonosító, 
- 10 szál
- 2 semafor mehet a területre
- ha mindkettő páros akkor counter növelés
- páratlan eset hasonló
- amelyik eléri a 100-at írja ki h győztem

Megoldásom
```java
package hu.elte.marci;

import java.util.concurrent.Semaphore;

public class semaphorMain {
    public static int checkInSemaphore(boolean inSemaphore[]){
        int pr = 0;
        int pt = 0;

        for (int i = 0; i < 10; i++) {
            if(inSemaphore[i]){
                if(i%2==0){
                    ++pr;
                }else if(i%2==1){
                    ++pt;
                }
            }
            if(pr>=2)
                return -1;
            if(pt>=2)
                return 1;
        }
        return 0;
    }

    public static void main(String[] args) {
        Semaphore semaphore = new Semaphore(2, true);
        boolean inSemaphore[] = {false, false, false, false, false, false, false, false, false, false};
        int race[] = {0,0};
        for (int i = 0; i < 10; i++) {
            int j = i;
            new Thread(() -> {
                int myNum = j;
                while (true) {
                    if(race[0]>=100 || race[1]>=100)
                        return;

                    try {
                        semaphore.acquire();
                        inSemaphore[myNum] = true;

                        int n = checkInSemaphore(inSemaphore);
                        if(n == -1){
                            race[0]++;
                        }else if (n == 1){
                            race[1]++;
                        }

                        if(race[0]>=100){
                            System.out.println("Paros nyert");
                        }else if(race[1]>=100){
                            System.out.println("Paratlan nyert");
                        }

                        inSemaphore[myNum] = false;
                        semaphore.release();

                    } catch (InterruptedException e) {
                        throw new IllegalStateException("cannot get permit", e);
                    }
                }
            }).start();
        }
    }
}
```

Tanári megoldás
```java
package hu.elte.pp.semaphore;


import java.util.HashSet;
import java.util.Set;
import java.util.concurrent.Semaphore;

/**
 * 10 threads, with ids from 1 to 10
 * synchronise with semaphore
 * 2 threads can be active at the same time
 * each thread mark their id in a common storage
 * if both thread is even, increase an even counter
 * if both is odd, increase odd counter
 * in case even / odd reaches 100 print "I won! " + id
 */
public class SemaphoreRace {
    public static void main(String[] args) {
        Semaphore semaphore = new Semaphore(2);
        IdRegistry registry = new IdRegistry();

        for(int i =0; i<10; ++i) {
            new Thread(new Racer(i+1, registry, semaphore)).start();
        }
    }

    private static class Racer implements Runnable{

        private final int id;
        private final IdRegistry registry;
        private final Semaphore semaphore;

        public Racer(int id, IdRegistry registry, Semaphore semaphore) {
            this.id=id;
            this.registry=registry;
            this.semaphore=semaphore;
        }

        @Override
        public void run() {
            while(!registry.isFinished()) {
                semaphore.acquireUninterruptibly();
                try {
                    registry.register(id);
                    registry.deregister(id);
                } finally {
                    semaphore.release();
                }
            }
        }
    }

    private static class IdRegistry {
        private static final int MAX = 2;
        private final Set<Integer> ids = new HashSet<>();
        private int oddCounter = 0;
        private int evenCounter = 0;

        public synchronized void register(int id) {
            if(isFinished()) {
                return;
            }
            ids.add(id);
            if(ids.size() == MAX) {
                int sum = ids.stream().mapToInt(i-> i%2).sum();
                if(sum == MAX) {
                    ++oddCounter;
                } else if(sum == 0) {
                    ++evenCounter;
                }
            }
            if(isFinished()) {
                System.out.println("I won! "+id);
            }
        }

        public synchronized void deregister(int id) {
            ids.remove(id);
        }

        public synchronized boolean isFinished() {
            return oddCounter >= 100 || evenCounter >= 100;
        }
    }

}
```

# Gyak 7 2021.10.21
- assert-hez 
    - VM option -ea
    - java -ea < class name >

- Lock
    - semaphore-al ki tudja zárni magát az ember
    - még bonyolultabb eszköz, könnyebb használni, lassabb
    - szálon belül lehet lock-olni akárhányszor
    - számolja egy szál lock-jait
        - ha nincs unlock 
    - lock() - nem megszakítható
    - lockInterruptibly() - megszakítható
    - tryLock()
    - ReentrantLock lehet fair vagy unfair
        - fair kicsit lassabb
    
# Gyak 8 2021.11.04
- Kajáló filozófusok
- Több megoldás is
- Szimmetria megtörés
- tryLock - lock helyett
- Szinkronalitás megtörés
- Live lock nagyon veszélyes
    - Úgy kerül lock-ba, hogy közben dolgozik
    - Így nem tűnik fel, hogy elakadt
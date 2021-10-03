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
- Szál a java jelenlegi verziójában minden szálhoz ami a JVM-en fut akkor Windows-ban is annyi szál fut
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
    - Készíts egy osztályt ami külön száloon lehet futtatni az ezt jelenti
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

## Feladat
- 
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
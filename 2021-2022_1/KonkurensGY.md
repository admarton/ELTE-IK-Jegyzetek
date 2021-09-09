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

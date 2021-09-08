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
        //new Thread {
        //@Override public void run(){
        //    while(true) System.out.println("Hi!");
        //}
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




# Telekommunikációs hálózatok 2 GY 2021.09.07
vzoli@inf.elte.hu
tms.inf.elte.hu

## Követelmény
- 5 beadandó, 5 csomag
- 1-4 lesz egy beadandó, az utolsó a másik
- 3 számonkérés
    - Socket ZH (min 50%) - python
    - Mininet nagyproj. - routing, tűzfal, IP cím beáll.
    - Python, socket házi feladatok (kb. 4) - TMS rendszerben

- ZH a félév két harmadánál, őszi szünet után 2 hét
    Jelenlétiben kellene megírni.
- % = házi% * 0,33 + mininet% * 0,33 + ZH% * 0,33

## Témakörök
- Py alapok
- Mininet
- Wireshark
- stb

## Python tulajdonságok
- egyszerű
- szóközzel elválasztott

## Python cuccok:
- Lista
- Tuple - immutable
- Set
- Dictionary
- Elágazás, ciklus
- függvények: map, filter
- file kezelés
- osztályok
- JSON fontos (XML is van, de JSON lesz órán)
    - import json,

## Szorgalmi
- három feladat jó megoldása email-ben, kövi gyakig
- nagy ZH-nál 1-2% bónusz pont

# Telekom GY 2021.09.13

1. feladat csomag határidő október első hétfő
2. feldat csomag határidő október második hete hétfő

## Ha nem kell output
```py
import subprocess
subprocess.call(['dir', '/B'], shell=True)
```

## Ha kell output
```py
import subprocess
p = subprocess.Popen(['echo', "Hello world"], stdout=subprocess.PIPE, shell=True)

print(p.communicate()) # eredménye egy tuple(stdout, stderr)
```

## Láncolás
```py
import subprocess
p1 = subprocess.Popen(['echo', "Hello world"], stdout=subprocess.PIPE, shell=True)
p2 = subprocess.Popen(['grep', "hda"], stdin=p1.stdout, stdout=subprocess.PIPE)

p1.stdout.close()

print(p1.communicate()) # eredménye egy tuple(stdout, stderr)
```

## Parancsok
- `p.poll()` process állapot lekérdezése
- `p.wait()` várakozik a process

## Trace
- Linux - traceroute
- Windows - tracert

## Hálózati entitások / node
- ipconfig /all
- kapcsolódnia kell egy átviteli közeghez
- szükséges szoftverek telepítve vannak
- célgéé hálózatát majd a gépet kell elérni
- fel kell paraméterezni a gépet
- Alap paraméterek
    - Physical Address, MAC address -  hálózati kártya azonosítója
    - IPv4 Adress, IPv6 Address - szofveres cím, telepítés során kapja
    - Subnet Mask - bitenkéti éselés az IPv4-el visszaadja a hálózat IPv4 címét
    - DNS server is be van konfigurálva min 2-3
- arp protocol (arp -a)
    - A hálózatomon belüli MAC address-eket sorolja fel
    - Broadcast csomag megy ki, mindenkinek szól
        - csupa 1-es a bradcast
        - ha ismeri az ip címet akkor belerakja a MAC addressét és visszaküldi
- ha nem a local hálón van a cél akkor egy kitüntetett gép kell aki kiküldhet a hálón kívülre - router
- addig meg routerről routerre a csomag ameddig eljut a helyi hálózatáig és ott meg lesz a MAC address
- ping - hálózati csomópont elérhetőségének tesztelése
    - localhost - hálókártyának szól
    - kölső cím
        - damain név (ip címhez rendelik, beszédesebb)
            - osztott adatbázis rendszer amiben kikresik a domain-hez az ip-t
            - DNS rendszer
    - összeállít egy teszt csomagot és elküldi
    - ha megkapta akkor visszaküldi
    - Reply - ha időn belül visszajön
    - Corrupted - jön de sérült csomag
    - Timeout - időn belül nem jött
    - TTL=%n -> ha router tovább dobja akkor csökkenti, hány "hopp"-nyira van
- tracert
    - ping-ben anomália van akkor jön a tracert
    - ping-hez hasonló csomag de a TTL=1 el indul
    - kijelöl egy router útvonalat
    - vannak válaszidők
    - meg lehet találni a probléma helyét


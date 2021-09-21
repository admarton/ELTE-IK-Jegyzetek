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

# GYak_3 2021.09.21

- TMS működik
- Milyen csomagok mennek?
- szerver imitálás  
    `nc -l -p 1234`
- kliens imitálás  
    `nc destination_host 1234`
- Tutorial a ppt-ben
- ilyet tudunk majd írni a félév végére
- enkapszuláció
    - egymásra épülő rétegek, saját burkolatba csomagolják a dolgokat
- tcpdump - hálózati forgalomfigyelés
    - elemezni lehet
    - forgalmat ki lehet menteni
    - host és port szűrés
        - teljes csomagot szed ki, nem csak egy részét
    - mentés pcap file-ba
- WhireShark ennek egy modernebb verziója
    - adat kiírása - hexa kód
    - logikai kiírás - szintek leírása
        - Frame - 1.szint
        - Ethernet - 2.szint
            - honnan, hova, beágyazott struktúra típusa (pl.: IPv4)
            - mindenki megnézi az elejét és megnézi hogy neki szól-e
            - csak akkor olvassa vágig ha neki szól
            - broadcast üzenetet mindenki megnézi
        - IPv4 - 3.szint
            - 4 biten a verzió
            - 4 biten h hány bájt lesz a header
            - Dolgok...pl.:
            - Protocol: pl.:UDP
        - UDP - Transport - 4.szint
            - Source port, dest port
            - checksum (extra védelem)
            - UDP payload (x bytes) - mennyi adat van
        - DATA (x bytes)
    - csomagok kiírása
        - sorban a dolgok
        - honnan, hova, protocoll, stb....
    - általános filter kifejezés
        - protocoll azonosító
            - arp - ip alapján MAC kérés
            - reverse arp - tudom a MAC címem és kérem az ip-m
                - dhcp - dinamikus ip kérés és háló konfig lekérés
                    - ip cím, netmask, default gateway, stb...
        - fejléc mező
        - fejléc almező
        - összehasonlító operátor
        - elvárt étrék
        - Ezek összekapcsolása operátorokkal
        - pl.: tcp.flags.ack==1 and tcp.dstport==80
            - ack nyugta flag - valameddig megkapt, azt visszaküldi

    - follow stream -el lehet az egész kommunikációt követni

- nem a hálózathoz kell jogosultság, hanem a géphez
    - az egész hálózatot tudom figyelni
    - általában
    - Keretinformációk nincsenek titkosítva
        - sok mindent ki lehet olvasni

- python dolgok
- `import socket`
    - socket unix erőforrás
    - két független program tudjon egymásnak üzenetet küldeni (nem pipeline, külső file, stb)
    - két task tudjon kommunikálni -> majd online is
- `gethostname()`
    - hol fut a py program host nevét
- `gethostbyname(), gethostbyname()_ex, gethostbyaddr()`
    - domain lekérés, ilyesmi
- portok használata 
    - port : short int
        - 1024 alattiak az ismertek
        - ismert porton a megfelelő program induljon
        - 22 - ssh
        - 23 - telnet
        - 80 - http
        - ftp, ftp_data, stb
        - etc/services file-ban benne van
    - `getservbyport(22)` milyen service tartozik, ha tartozik
- Little edian, big edian
    - high, low fele milyen sorrendbe van tárolva
    - hálózati formára kell transformálni - hálózati forma a rendes sorrend
    - htons(), htonl() - host to network short/long
    - ntohs(), ntohl() - network to host short/long

- TCP
    - server
        - socket()
            - oprendszer erőforrás
            - ezen keresztül kommunikáció
            - itt kötődik össze a task és az op-rendszer
            - network socket-et kér
            - socket descriptort ad amit a bind, listen, accept, és close használja
            - `sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)`
        - bind()
            - kinek szóló adatot akar megkapni
            - milyen portot akar
            - port hozzárendelés
            - `sock.bind(server_address) #server_address = ('localhost',10000)`
        - listen()
            - várakozási sor állítás
            - listen queue-ba kerülnek a várakozó kliens
            - továbít a megfelelő szerverhez
            - `sock.listen(1)`
        - windows-on settimeout(mp-ig)
        - 2. accept()
            - várakozók kiszolgálása
            - újabb connect a sorba áll
            - kliens ip címét és portszámát megkapja - hova kell visszaküldeni
            - visszaad egy kapcsolat azonosítót
            - socket descreptor - recv és send ezt használja
            - `connection, client_address = sock.accept()`
        - 4. recv()
            - `data = connection.recv(16).decode()`
        - 5. send()
            - `connection.sendall(data.encode())`
        - 7. close()
            - `connection.close()`
    - client
        - socket()
        - 1. connect()
            - mit kell elérni
            - ip, port
            - `sock.connect(server_address)`
        - 3. send()
        - 6. recv()
        - 7. close()
    
- UDP a kövi gyakon
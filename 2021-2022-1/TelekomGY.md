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
- nagy ZH-nál 1-2% bónuszpont

# Telekom GY 2021.09.13

1. feladat csomag határidő október első hétfő
2. feladat csomag határidő október második hete hétfő

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
- célgép hálózatát majd a gépet kell elérni
- fel kell paraméterezni a gépet
- Alap paraméterek
    - Physical Address, MAC address - hálózati kártya azonosítója
    - IPv4 Address, IPv6 Address - szoftveres cím, telepítés során kapja
    - Subnet Mask - bitenkénti éselés az IPv4-el visszaadja a hálózat IPv4 címét
    - DNS server is be van konfigurálva min 2-3
- arp protocol (arp -a)
    - A hálózatomon belüli MAC address-eket sorolja fel
    - Broadcast csomag megy ki, mindenkinek szól
        - csupa 1-es a broadcast
        - ha ismeri az ip címet akkor belerakja a MAC addressét és visszaküldi
- ha nem a local hálón van a cél akkor egy kitüntetett gép kell, aki kiküldhet a hálón kívülre - router
- addig meg routerről routerre a csomag ameddig eljut a helyi hálózatáig és ott meg lesz a MAC address
- ping - hálózati csomópont elérhetőségének tesztelése
    - localhost - hálókártyának szól
    - kölső cím
        - damain név (ip címhez rendelik, beszédesebb)
            - osztott adatbázis rendszer, amiben kikresik a domain-hez az ip-t
            - DNS rendszer
    - összeállít egy teszt csomagot és elküldi
    - ha megkapta akkor visszaküldi
    - Reply - ha időn belül visszajön
    - Corrupted - jön, de sérült csomag
    - Timeout - időn belül nem jött
    - TTL=%n -> ha router tovább dobja akkor csökkenti, hány "hopp"-nyira van
- tracert
    - ping-ben anomália van akkor jön a tracert
    - ping-hez hasonló csomag, de a TTL=1 el indul
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
            - csak akkor olvassa végig ha neki szól
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
        - honnan, hova, protokoll, stb....
    - általános filter kifejezés
        - protokoll azonosító
            - arp - ip alapján MAC kérés
            - reverse arp - tudom a MAC címem és kérem az ip-m
                - dhcp - dinamikus ip kérés és háló konfig lekérés
                    - ip cím, netmask, default gateway, stb...
        - fejléc mező
        - fejléc almező
        - összehasonlító operátor
        - elvárt érték
        - Ezek összekapcsolása operátorokkal
        - pl.: tcp.flags.ack==1 and tcp.dstport==80
            - ack nyugta flag - valameddig megkapta, azt visszaküldi

    - follow stream -el lehet az egész kommunikációt követni

- nem a hálózathoz kell jogosultság, hanem a géphez
    - az egész hálózatot tudom figyelni
    - általában
    - Keret információk nincsenek titkosítva
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
    - hálózati formára kell transzformálni - hálózati forma a rendes sorrend
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
            - továbbít a megfelelő szerverhez
            - `sock.listen(1)`
        - windows-on settimeout(mp-ig)
        - 2. accept()
            - várakozók kiszolgálása
            - újabb connect a sorba áll
            - kliens ip címét és port számát megkapja - hova kell visszaküldeni
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

# Gyak_4 2021.09.28

## Házik
- Ezen a héten nyílik
- kb 3 hét lesz rá
- Okt ? - a harmadik
- Nov 1 - a negyedik

## ZH
- Nov 2 ⨀ 9 
    - külön: ⨀ = és
    - egyben: ⨀ = vagy
- Gépteremben váltott héten
- Vagy Canvas feladat

## Szerializálás
- Binárissá alakítás
```py
import struct
value = (int("1"), "ab".encode(), 2.7)
packer = struct.Struct('I 2s f') # int, char[2], float
packet_data = packer.pack(*values)
```
- Üzenet visszaállítás
```py
import struct
unpacker = struct.Struct('I 2s f')
data = client.recv(unpacker.size)
unp_data = unpacker.unpack(data)
```

## Feladat 
- Kliens-szerver app
- küld két számot és egy operátort - struktúrában
- visszakapja az eredményt
- `x = eval(str(unp_data[0])+unp_data[2].decode()+str(unp_data[1]))`
- `client.send(str(x).encode())`
- `client, addr = server.accept()`
    - `print('Csatlakozott:'+addr)`
    - a loop elején accept van, nem kell explicit close(), de a kliens nem tudja, hogy bezárt


## Socket
- ipv4: AF_INET
- tcp: SOCK_STREAM
- `connect`-re kell hibakezelés
- szerveren kell: `settimeout(4.0)`
- nonblocking mode:
    - timeoutig vár, ha nincs semmi akkor megint vár
- blocking mode:
    - olvas a socket-ra
    - ha nincs semmi akkor várja h jöjjön valami
    - ha kliens küld valamit akkor csinál valamit
    - az is valami ha bezárja a kapcsolatot
        - `data = client_socket.recv(n)`
        - ha data null
            - `client_socket.close()`
    - ha a protokoll megengedi akkor a szerver is bonthat kapcsolatot
- except:
    - timeout
    - KeyboardInterrupt

## Server párhuzamosítása
- select()
```py
inputs = [server]
output = []
timeout=1
readable,writable,exceptional = select.select(inputs, outputs, inputs, timeout)
...
for s in readable:
    if s is server: # új kliens
        client, addr = s.accept()
        inputs.append(client)
    else:
        ... # kliens kezelése pl recv
```
- select-et lehet többféle erőforrásra használni //socket, fájl, stb.
- select() 1.param - van-e olvasható erőforrás
- select() 2.param - van-e írható erőforrás
- select() 3.param - van-e sűrgős adat - hálózat specifikus //nem sokat használjuk még
- select() 4.param - timeout
- select beállítja az olvasható, írható és hiba dolgokat
- readable dolgokra lehet read jellegű dolgokat hívni //lehet olvasni, accept, recv
- ha egy output benne van a writable-ban akkor lehet write jellegű folyamat //send
- close hiányosságokat pótolni kell

- server.setsockopt(SOL_SOCKET, SO_REUSEADDR, 1)
    - SO_REUSEADDR
        - adott oprendszer nem szabványosan felszabadított erőforrást még nem oszt ki másnak
        - 3-4 percig foglalt lesz a port 

# Gyak 5 2021.10.05

## Beadandók
- Ne utolsó pillanatban

## ZH
- Hibridben
    - két egymás utáni héten, a bentiek írnak
    - jövőhéten kitűzzük
    - lehet választani h mikor tud jönni
- Gépes ZH
    - Lehet akár canvasos is
    - Min 50% kell legyen

## Jobb input pythonhoz
- Fent van VZoli oldalán
- Non blocking, van egy timeout-ja
    - Tovább lép ha nincs semmi
- Non ascii karaktereket nem kezelik
    - Coding utf-8-at be kell állítani

## Chat kliens
- set timeout-al nem befagyós lesz
- két párhuzamos dolgot kell csinálnia, akkor duplázódik
- mindenkitől jöhet válasz
- bármikor kell tudni üzenetet küldeni
- végtelen ciklus, két try blokk, input és hálózat figyelés
- kvázi paralel server <-> select
- read mellett a write is legyen select-elve
- mindenkinek el kell küldeni akitől nem kaptam
- üzenetek egy queue-ba kerülnek
- majd küldésnél kiüríti
- kulcs adat párokat küld a kliens
- client.settimeout(1.0)
- két try blokk
- server socketet mindig meg kell különböztetni a többitől
- 

## UDP - Hasznos skeleton
- Kvázi paralel - select-el
- ZH-feladat lehet
    - UDP autentikáció -> token
    - Tokennel tud TCP server-hez kapcsolódni
    - két féle működés
- Minden TCP előtt Kell UDP kulcs
- Vagy kap egy címet meg portot amivel tud kapcsolódni
- min 3 feladat amiből egy több protokollt használ

# Gyak 6 2021.10.12

## CRC
- Generáló bitsorozat
- Generáló polinomból ki lehet számolni a nem detektálható hiba polinomokat
- `import binascii`
- `import zlib`
- `import hashlib`

## UDP
- sendto(), recvfrom()
- servernél kell bind()
- select-et lehet használni
- függetlenül jönnek a csomagok
    - nincs akkora szükség a kvázi paralel működésre
    
# Gyak 7 2021.10.19

## ZH
- Szünet után B hét lesz
- Ők írnak először
- A hetesek a második gyakon írják
- Akinek nem kell bejárni az választhat
- Indokkal lehet választani
- ZH alatt az otthoniak telepítik a mininet cuccokat
- Mindent tudunk a ZH-hoz
- Socket programmozási feladat lesz
- Több részfeladat
- NetCopy házi olyan volt mint a zh
- Futtatni kell mind3-4 komponenst, működnie kell
    - Ez a magfelelt/nem felelt meg
    - Ha el van fogadva akkor legalább kettes megvan
- A maradék jegy ezután jön
- Forrásokat kell elküldeni
- 50-100% között döntenek
- Minden socket fel legyen szabadítva
- Szabványos legyen a hálózati pufferkezelés, kódolás, encódolás

## Órai
- UDP calc -> TCP calc
- Üzleti logikát egy tcp-vel alrébb raktuk
- Valamitől függően udp/tcp között vált, egy programban
- Le kell kérdezni egy UDP szervertől, hogy ezután milyen szervert, milyen porton, milyen protokollal kell elérnie
- Connect után küldés kell
    - Nem szabad kisajátítani a szervert
- Kliensnél is lehet select, de nincs sok haszna
- UDP-nél leginkább akkor van értelme a select-nek ha nem ismerem a klienst, pl rosszindulatú kliens


## Proxy
- Vonal elvágás 
- Fizikailag a szállítási rétegben egy szűrés
- Lehet cím szerint filterezni
- Tartalmi szűrés - bizonyos kérések kimehetnek, bizonyosak nem
- **ZH-n** lesz szűrés, uh valszeg proxy lesz, elszólta valszeg magát
- Valamilyen funkciója van az életben - órai példában nincs
- Sokszor naplózásra használják
    - logolja a kérést és tovább küldi
    - logolja a választ és tovább
    - **tipik ZH feladat**, pl json-ba
- Gyakorlás
    - Filterezés
    - Naplózás
    
# Gyak 9 2021.11.16

## Mininet
- Kell a mininetes szarhoz
    - sudo dhclient
    - sudo service sshd restart

- Néha az Xauthority-ben meg kell újítani a dolgokat
    - xauth add ... //vzoli oldalán
    - sudo xhost +

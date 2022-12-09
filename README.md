# Jarkom-Modul-5-F11-2022

### Kelompok F11

| **No** | **Nama** | **NRP** | 
| ------------- | ------------- | --------- |
| 1 | Ryo Hilmi Ridho  | 5025201192 | 
| 2 | Moh. Ilham Fakhri Zamzami | 5025201275 |
| 3 | Putu Andhika Pratama | 5025201132 |

## A. Topologi
![topologi](https://user-images.githubusercontent.com/100068648/205689037-1cc0d455-080f-42e1-a0e8-645fcab38057.png)

![subnetm5](https://user-images.githubusercontent.com/100068648/205700026-5435aa5b-b177-42b2-9c56-fe62189ba9ee.png)

## B. Subneting (VLSM)

### Tree
![tree5](https://user-images.githubusercontent.com/100068648/205799802-44f6a840-7da8-4de7-9193-986a29c25385.png)

### Config Node

- Strix (Router)
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
    address 10.34.0.5
    netmask 255.255.255.252

auto eth2
iface eth2 inet static
    address 10.34.0.1
    netmask 255.255.255.252
```

- Ostania (DHCP Relay)
```
auto eth0
iface eth0 inet static
address 10.34.0.6
    netmask 255.255.255.252
    gateway 10.34.0.5

auto eth1
iface eth1 inet static
    address 10.34.2.1
    netmask 255.255.254.0

auto eth2
iface eth2 inet static
    address 10.34.1.1
    netmask 255.255.255.0

auto eth3
iface eth3 inet static
    address 10.34.0.25
    netmask 255.255.255.248
```

- Westalis (DHCP Relay)
```
auto eth0
iface eth0 inet static
address 10.34.0.2
    netmask 255.255.255.252
    gateway 10.34.0.1

auto eth1
iface eth1 inet static
    address 10.34.4.1
    netmask 255.255.254.0

auto eth2
iface eth2 inet static
    address 10.34.0.129
    netmask 255.255.255.128

auto eth3
iface eth3 inet static
    address 10.34.0.17
    netmask 255.255.255.248
```

- Eden (DNS Server)
```

auto eth0
iface eth0 inet static
    address 10.34.0.18
    netmask 255.255.255.248
    gateway 10.34.0.17
```

- WISE (DHCP Server)
```
auto eth0
iface eth0 inet static
    address 10.34.0.19
    netmask 255.255.255.248
    gateway 10.34.0.17
```

- Garden (Web Server)
```
auto eth0
iface eth0 inet static
    address 10.34.0.26
    netmask 255.255.255.248
    gateway 10.34.0.25
```

- SSS (Web Server)
```
auto eth0
iface eth0 inet static
    address 10.34.0.27
    netmask 255.255.255.248
    gateway 10.34.0.25
```

- Forger (Client)
```
auto eth0
iface eth0 inet dhcp
```

- Desmond (Client)
```
auto eth0
iface eth0 inet dhcp
```

- Blackbell (Client)
```
auto eth0
iface eth0 inet dhcp
```

- Briar (Client)
```
auto eth0
iface eth0 inet dhcp
```

## C. Routing

### Strix
Dapatkan hwaddress dengan `ip a`

![hwaddress](https://user-images.githubusercontent.com/100068648/205817234-a1262bf6-c78e-4ebe-8988-d6c7b152c6ee.png)

Edit config node Strix agar ipnya tidak berubah
```
auto eth0
iface eth0 inet dhcp
hwaddress ether a6:4c:e1:85:b9:19

auto eth1
iface eth1 inet static
    address 10.34.0.5
    netmask 255.255.255.252

auto eth2
iface eth2 inet static
    address 10.34.0.1
    netmask 255.255.255.252
```

Kemudian lakukan routing.
```
route add -net 10.34.0.16 netmask 255.255.255.248 gw 10.34.0.2
route add -net 10.34.0.128 netmask 255.255.255.128 gw 10.34.0.2
route add -net 10.34.4.0 netmask 255.255.254.0 gw 10.34.0.2
route add -net 10.34.0.24 netmask 255.255.255.248 gw 10.34.0.6
route add -net 10.34.1.0 netmask 255.255.255.0 gw 10.34.0.6
route add -net 10.34.2.0 netmask 255.255.254.0 gw 10.34.0.6
```

## D. DHCP

### WISE (DHCP Server)

Install DHCP Server

```
apt-get update
apt-get install isc-dhcp-server -y
```

Lalu edit interface pada file `/etc/default/isc-dhcp-server` tambahkan

```
INTERFACES="eth0"
```

Edit file `/etc/dhcp/dhcpd.conf`

```
# Forger (A2)
subnet 10.34.0.128 netmask 255.255.255.128 {
    range 10.34.0.130 10.34.0.254;
    option routers 10.34.0.129;
    option broadcast-address 10.34.0.255;
    option domain-name-servers 10.34.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}

# Desmond (A3)
subnet 10.34.4.0 netmask 255.255.252.0 {
    range 10.34.4.2 10.34.7.254;
    option routers 10.34.4.1;
    option broadcast-address 10.34.7.255;
    option domain-name-servers 10.34.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}

# Blackbell (A6)
subnet 10.34.2.0 netmask 255.255.254.0 {
    range 10.34.2.2 10.34.3.254;
    option routers 10.34.2.1;
    option broadcast-address 10.34.3.255;
    option domain-name-servers 10.34.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}

# Briar (A8)
subnet 10.34.1.0 netmask 255.255.255.0 {
    range 10.34.1.2 10.34.1.254;
    option routers 10.34.1.1;
    option broadcast-address 10.34.1.255;
    option domain-name-servers 10.34.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}

# Eden & WISE (A1)
subnet 10.34.0.16 netmask 255.255.255.248 {
}

# Garden & SSS (A7)
subnet 10.34.0.24 netmask 255.255.255.248 {
}
```

Lalu restart DHCP Server `service isc-dhcp-server restart`

### Ostania & Westalis (DHCP Relay)

Install DHCP Relay

```
apt-get update
apt-get install isc-dhcp-relay -y
```

Edit file `/etc/default/isc-dhcp-relay`

```
# What servers should the DHCP relay forward requests to?
SERVERS="10.34.0.19"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth0 eth1 eth2 eth3"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
```

Kemudian restart DHCP Relay `service isc-dhcp-relay restart`

### Testing pada client

![ipfo](https://user-images.githubusercontent.com/100068648/205834859-6bf79f09-fb90-4524-bfb7-9dc3d9efe600.png)

![ipdesmond](https://user-images.githubusercontent.com/100068648/205834440-c130af4c-aec6-49c4-b437-cb600b2502fd.png)

![ipblackbell](https://user-images.githubusercontent.com/100068648/205834517-e7f89dc7-0a29-4f93-a0c7-6df15f1f063e.png)

![ipbriar](https://user-images.githubusercontent.com/100068648/205834537-58174013-360b-41a5-89fc-8c0bf024b36f.png)

## Soal 1
### Soal
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Strix menggunakan iptables, tetapi Loid tidak ingin menggunakan MASQUERADE.

### Jawaban
Pada node Strix
```
iptables -t nat -A POSTROUTING -s 10.34.0.0/21 -o eth0 -j SNAT --to-source 192.168.122.108
```

Pada node lain
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
```

Coba ping google

![wiseping](https://user-images.githubusercontent.com/100068648/205835669-f3846cec-6ef7-448e-890e-69c2c35c3230.png)

## Soal 2
### Soal
Kalian diminta untuk melakukan drop semua TCP dan UDP dari luar Topologi kalianpada server yang merupakan DHCP Server demi menjaga keamanan.

### Jawaban
Pada node strix jalankan perintah
```
iptables -A FORWARD -p tcp -d 10.34.0.19 -i eth0 -j DROP
iptables -A FORWARD -p udp -d 10.34.0.19 -i eth0 -j DROP
```

Coba ping google pada DHCP Server WISE

![wiseping](https://user-images.githubusercontent.com/100068648/206632761-c0b1e95a-f987-499c-8467-8891dbff7273.png)

## Soal 3
### Soal
Loid meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 2 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

### Jawaban
Pada DHCP (WISE) dan DNS Server (Eden)

```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 2 --connlimit-mask 0 -j DROP
```

Lalu coba ping dari 3 client berbeda ke ip DNS Server (Eden)

![pinglimitforger](https://user-images.githubusercontent.com/100068648/206634278-663871eb-3575-48d3-b211-b7c9b6bdca2f.png)

![pinglimitbriar](https://user-images.githubusercontent.com/100068648/206634300-d4c849cf-5287-45c0-a35e-1e4626cd3f30.png)

![pinglimitdesmond](https://user-images.githubusercontent.com/100068648/206634316-706c153b-aebf-4db9-bf1f-8c61b8c0c333.png)

Coba juga ping dari 3 client berbeda ke ip DHCP Server (WISE)

![forgerlimit](https://user-images.githubusercontent.com/100068648/206635089-542e95d0-1844-429a-b574-ce606a32ccec.png)

![desmondlimit](https://user-images.githubusercontent.com/100068648/206635116-012d0bcc-8ea5-4eb8-a854-4886ebb5f329.png)

![briarlimit](https://user-images.githubusercontent.com/100068648/206635124-5244417a-2579-4b7d-8954-b53a2db733b6.png)

## Soal 4
### Soal
Akses menuju Web Server hanya diperbolehkan disaat jam kerja yaitu Senin sampai Jumat pada pukul 07.00 - 16.00.

### Jawaban
Pada node Web Server (Garden dan SSS)
```
iptables -A INPUT -j REJECT
iptables -A INPUT -m time --timestart 07:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
```

Coba ping dari client menuju web server Garden

![ws2ping](https://user-images.githubusercontent.com/100068648/206640168-a0116897-9ef2-4765-8f2b-2a47ce393d70.png)

Coba juga ping dari client menuju web server SSS

![ws1ping](https://user-images.githubusercontent.com/100068648/206640260-f16d9ad0-b868-44f5-9b9d-c6c55b9474b3.png)

## Soal 5
### Soal
Karena kita memiliki 2 Web Server, Loid ingin Ostania diatur sehingga setiap request dari client yang mengakses Garden dengan port 80 akan didistribusikan secara bergantian pada SSS dan Garden secara berurutan dan request dari client yang mengakses SSS dengan port 443 akan didistribusikan secara bergantian pada Garden dan SSS secara berurutan.

### Jawaban

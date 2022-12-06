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

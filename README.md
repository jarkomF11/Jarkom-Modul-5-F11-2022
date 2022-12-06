# Jarkom-Modul-5-F11-2022

### Kelompok F11

| **No** | **Nama** | **NRP** | 
| ------------- | ------------- | --------- |
| 1 | Ryo Hilmi Ridho  | 5025201192 | 
| 2 | Moh. Ilham Fakhri Zamzami | 5025201275 |
| 3 | Putu Andhika Pratama | 5025201132 |

## Topologi
![topologi](https://user-images.githubusercontent.com/100068648/205689037-1cc0d455-080f-42e1-a0e8-645fcab38057.png)

![subnetm5](https://user-images.githubusercontent.com/100068648/205700026-5435aa5b-b177-42b2-9c56-fe62189ba9ee.png)

## Subnet (VLSM)

### Tree
![tree5](https://user-images.githubusercontent.com/100068648/205799802-44f6a840-7da8-4de7-9193-986a29c25385.png)

### Pembagian IP
![subnetip5](https://user-images.githubusercontent.com/100068648/205801710-5d59f6eb-79be-48c3-bfd2-9800be84589c.png)

#### Eden
```
auto eth0
iface eth0 inet static
address 10.34.0.18
netmask 255.255.255.248
gateway 10.34.0.17
```

#### WISE
```
auto eth0
iface eth0 inet static
address 10.34.0.19
netmask 255.255.255.248
gateway 10.34.0.17
```

#### Westalis
```
auto lo
iface lo inet loopback

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

#### Forger
```
auto eth0
iface eth0 inet static
address 10.34.0.130
netmask 255.255.255.128
gateway 10.34.0.129
```

#### Desmond
```
auto eth0
iface eth0 inet static
address 10.34.4.2
netmask 255.255.254.0
gateway 10.34.4.1
```

#### Strix
```
auto lo
iface lo inet loopback

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

#### Ostania
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.34.0.6
netmask 255.255.255.252
gateway 10.34.0.5

auto eth1
iface eth1 inet static
address 10.34.2.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 10.34.1.1
netmask 255.255.255.0

auto eth3
iface eth3 inet static
address 10.34.0.25
netmask 255.255.255.248
```

#### Blackbell
```
auto eth0
iface eth0 inet static
address 10.34.2.2
netmask 255.255.252.0
gateway 10.34.2.1
```

#### Garden
```
auto eth0
iface eth0 inet static
address 10.34.0.26
netmask 255.255.255.248
gateway 10.34.0.25
```

#### SSS
```
auto eth0
iface eth0 inet static
address 10.34.0.27
netmask 255.255.255.248
gateway 10.34.0.25
```

#### Briar
```
auto eth0
iface eth0 inet static
address 10.34.1.2
netmask 255.255.255.0
gateway 10.34.1.1
```

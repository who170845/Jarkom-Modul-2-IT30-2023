# Jarkom-Modul-2-IT30-2023

# Nomor 1
- Pertama, buat dulu topologi sesuai dengan topologi no.8
  ![Screenshot (392)](https://github.com/who170845/Jarkom-Modul-2-IT30-2023/assets/113872836/ebaeb8e2-00fd-460e-a7b2-b8100cb38342)
- Lalu Ketikkan iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s [Prefix IP].0.0/16 pada router
- atur configurasi ip setiap node
- Ketikkan  echo nameserver 192.168.122.1 > /etc/resolv.conf pada setiap node selain router
- apt-get update dan apt-get install bind9 -y pada ArjunaLoadBalancer, WerkudaraDNSSlave dan YudhistiraDNSMaster

Router
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.168.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.168.2.1
	netmask 255.255.255.0
```

Nakula Client
```
auto eth0
iface eth0 inet static
	address 192.168.1.2
	netmask 255.255.255.0
	gateway 192.168.1.1
```

SadewaClient
```
auto eth0
iface eth0 inet static
	address 192.168.1.3
	netmask 255.255.255.0
	gateway 192.168.1.1
```

AbimanyuWebServer
```
auto eth0
iface eth0 inet static
	address 192.168.1.4
	netmask 255.255.255.0
	gateway 192.168.1.1
```

PrabukusumaWebServer
```
 auto eth0
iface eth0 inet static
	address 192.168.1.5
	netmask 255.255.255.0
	gateway 192.168.1.1
```

 WisanggeniWebServer
```
 auto eth0
iface eth0 inet static
	address 192.168.1.6
	netmask 255.255.255.0
	gateway 192.168.1.1
```

 YudhistiraDNSMaster
```
auto eth0
iface eth0 inet static
	address 192.168.2.4
	netmask 255.255.255.0
	gateway 192.168.2.1
```
WerkudaraDNSSlave
```
auto eth0
iface eth0 inet static
	address 192.168.2.3
	netmask 255.255.255.0
	gateway 192.168.2.1
```
ArjunaLoadBalancer
```
auto eth0
iface eth0 inet static
	address 192.168.2.2
	netmask 255.255.255.0
	gateway 192.168.2.1
```

# Nomor 2
Buat website arjuna.it30.com di node ArjunaLoadBalancer
dengan cara ###nano


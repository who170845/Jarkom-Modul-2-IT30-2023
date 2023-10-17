# Jarkom-Modul-2-IT30-2023

# Nomor 1
- Pertama, buat dulu topologi sesuai dengan topologi no.8
  ![Screenshot (392)](https://github.com/who170845/Jarkom-Modul-2-IT30-2023/assets/113872836/ebaeb8e2-00fd-460e-a7b2-b8100cb38342)
- Lalu Ketikkan ```iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s [Prefix IP].0.0/16``` pada router
- atur configurasi ip setiap node
- Ketikkan  ```echo nameserver 192.168.122.1 > /etc/resolv.conf``` pada setiap node selain router
- ```apt-get update``` dan ```apt-get install bind9 -y``` pada ArjunaLoadBalancer, WerkudaraDNSSlave dan YudhistiraDNSMaster

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
dengan cara nano ```/etc/bind/named.conf.local```
masukkan
```
zone "arjuna.it30.com" {
	type master;
	file "/etc/bind/arjuna/arjuna.it30.com";
};
```
kemudian buat direktori mkdir /etc/bind/arjuna
copy file --> ```cp /etc/bind/db.local /etc/bind/arjuna/arjuna.it30.com```
kemuadian ```nano /etc/bind/arjuna/arjuna.it30.com```
masukkan 
```
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     arjuna.it30.com. root.arjuna.it30.com. (
                            30          ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                         2419200        ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      arjuna.it30.com.
@       IN      A       192.168.2.2
www     IN      CNAME   arjuna.it30.com.
@       IN      AAAA    ::1
```

cname untuk www

```service bind9 restart```

kemudian coba di client Nakula dan Sadewa dengan ketik ```nano /etc/resolv.conf```
masukkan ```nameserver 192.168.2.2 (IP-nya arjuna)``` 

maka bisa di ```ping arjuna.it30.com``` coba juga dengan www

# Nomor 3

Buat website arjuna.it30.com di node ArjunaLoadBalancer
dengan cara ```nano /etc/bind/named.conf.local```
masukkan
```
zone "abimanyu.it30.com" {
	type master;
	file "/etc/bind/arjuna/abimanyu.it30.com";
};
```
copy file --> ```cp /etc/bind/db.local /etc/bind/arjuna/abimanyu.it30.com```
kemuadian ```nano /etc/bind/arjuna/abimanyu.it30.com```

masukkan 
```
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.it30.com. root.abimanyu.it30.com. (
                            30          ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                         2419200        ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.it30.com.
@       IN      A       192.168.1.4         ; IP Abimanyu
www     IN      CNAME   abimanyu.it30.com.
@       IN      AAAA    ::1
```
cname untuk www

```service bind9 restart```

kemudian coba di client Nakula dan Sadewa dengan ketik ```nano /etc/resolv.conf```
masukkan ```nameserver 192.168.1.4 (IP-nya abimanyu) ```

maka bisa di ```ping abimanyu.it30.com``` coba juga dengan www

# Nomor 4

buat subdomain dengan dns yudhistira 
```
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.it30.com. root.abimanyu.it30.com. (
                            30          ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                         2419200        ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.it30.com.
@       IN      A       192.168.1.4         ; IP Abimanyu
www     IN      CNAME   abimanyu.it30.com.
parikesit   IN  A       192.168.2.4         ; IP Yudhistira
@       IN      AAAA    ::1
```
```service bind9 restart```

coba di Nakula dan Sadewa ```ping parikesit.abimanyu.it30.com```

# Nomor 5

Buar reverse untuk abimanyu di node arjuna dengan cara ```nano /etc/bind/named.conf.local```
masukkan
```
zone "122.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/arjuna/1.168.192.in-addr.arpa";
};
```
```cp /etc/bind/db.local /etc/bind/arjuna/1.168.192.in-addr.arpa```
kemuadian ```nano /etc/bind/arjuna/1.168.192.in-addr.arpa```

masukkan 
```

; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.it30.com. root.abimanyu.it30.com. (
                            30          ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                         2419200        ; Expire
                         604800 )       ; Negative Cache TTL
;
1.168.192.in-addr.arpa.       IN      NS      abimanyu.it30.com.
4                             IN      PTR     abimanyu.it30.com.
```
```service bind9 restart```

masuk terminal client nakula dan sadewa ```apt-get update``` lalu apt-get ```install dnsutils```
kemudian ```host -t PTR 192.168.1.4 (IP-nya Abimanyu)```

# Nomor 6

tambahkan di ```named.conf.local``` arjuna
```
zone "arjuna.it30.com" {
	type master;
    also-notify { 192.168.2.3; }; 
    allow-transfer { 192.168.2.3; };
	file "/etc/bind/arjuna/arjuna.it30.com";
};
```
kemudian restart bind9

masuk ke WerkudaraDNSSlave
```nano /etc/bind/named.conf.local```
masukkan
```
zone "arjuna.it30.com" {
    type slave;
    masters { 192.168.2.2; }; 
    file "/var/lib/bind/arjuna.it30.com";
};
```
restart bind9

coba ```ping arjuna.it30.com``` di nakula atau sadewa maka akan berhasil






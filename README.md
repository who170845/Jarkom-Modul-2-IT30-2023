# Jarkom-Modul-2-IT30-2023

# Nomor 1
- Pertama, buat dulu topologi sesuai dengan topologi no.8
  ![Screenshot (392)](https://github.com/who170845/Jarkom-Modul-2-IT30-2023/assets/113872836/ebaeb8e2-00fd-460e-a7b2-b8100cb38342)
- Lalu Ketikkan iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s [Prefix IP].0.0/16 pada router
- atur configurasi ip setiap node
- Ketikkan  echo nameserver 192.168.122.1 > /etc/resolv.conf pada setiap node selain router
- apt-get update dan apt-get install bind9 -y pada ArjunaLoadBalancer, WerkudaraDNSSlave dan YudhistiraDNSMaster

# Nomor 2
Buat website arjuna.it30.com di node ArjunaLoadBalancer
dengan cara 
///
nano
///

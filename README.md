# B2-tp1-reseaux

## 0. Etape préliminaires

* Le `curl google.fr` me connecte a internet
* Presence d'une carte reseaux privé
* Connection SSH ok avec putty
* Droit sudo ok  

## I. Gather informations

* enp0s3 :   
adresse ip : `10.0.2.15/24`   
adresse mac : `10.0.2.255`  
* enp0s8 :  
adresse ip : `192.168.125.4/24`  
adresse mac : `192.168.125.255`  

* Ip en dhcp   
`inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3`.  
Le dynamic veut dire que la carte réseaux à récupéré une ip en DHCP  

* Pour afficher la table ARP on fait un `ip neigh show` et pour afficher la table de routage on fait `ip route` ou `ip route show`.

* Pour récupérer la liste des ports sur écoute sur la machine TCP on fait `ss -t` et sur la machine on fait `ss -u`  
Après l'avoir fait on obient :   
```
[root@localhost antoine]# ss -ltunp
Netid State   Recv-Q  Send-Q           Local Address:Port    Peer Address:Port  
udp   UNCONN  0       0                    127.0.0.1:323          0.0.0.0:*      users:(("chronyd",pid=726,fd=6))
udp   UNCONN  0       0         192.168.125.4%enp0s8:68           0.0.0.0:*      users:(("NetworkManager",pid=756,fd=22))
udp   UNCONN  0       0             10.0.2.15%enp0s3:68           0.0.0.0:*      users:(("NetworkManager",pid=756,fd=19))
udp   UNCONN  0       0                        [::1]:323             [::]:*      users:(("chronyd",pid=726,fd=7))
tcp   LISTEN  0       128                    0.0.0.0:22           0.0.0.0:*      users:(("sshd",pid=773,fd=6))
tcp   LISTEN  0       128                       [::]:22              [::]:*      users:(("sshd",pid=773,fd=8))
```

*   

* Pour afficher l'état du firewall on fait `firewall-cmd --state`  


## II. Edit configuration  

### 1. Configuration carte réseau 

* enp0s8 est bien configuré : 
```root@192.168.125.2's password:
Last login: Wed Oct  2 08:05:40 2019
[root@localhost ~]# ipa
-bash: ipa: command not found
[root@localhost ~]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:d9:26:d6 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 85239sec preferred_lft 85239sec
    inet6 fe80::c5ef:e3b3:3aaf:a441/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:fe:6c:83 brd ff:ff:ff:ff:ff:ff
    inet 192.168.125.2/24 brd 192.168.125.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fefe:6c83/64 scope link
       valid_lft forever preferred_lft forever
```
* Le nouveau réseau est crée :   
```3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:fe:6c:83 brd ff:ff:ff:ff:ff:ff
    inet 192.168.125.2/24 brd 192.168.125.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fefe:6c83/64 scope link
       valid_lft forever preferred_lft forever
4: enp0s9: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e4:87:65 brd ff:ff:ff:ff:ff:ff
    inet 192.168.246.2/24 brd 192.168.246.255 scope global noprefixroute enp0s9
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fee4:8765/64 scope link
       valid_lft forever preferred_lft forever
```  

### 2. Serveur SSH  






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




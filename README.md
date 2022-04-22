# SAE21
Configuration des routeurs:

interface FastEthernet 0/1.1
ip address 192.168.2.1  255.255.255.0
no shut
interface FastEthernet 0/1.2
ip address 192.168.3.1  255.255.255.0
no shut
interface Fastethernet 0/1.3
ip address 192.168.4.1  255.255.255.0
no shut
 
Configuration  du serveur DHCP

service dhcp
ip dhcp pool vlan1
network 192.168.2.0  255.255.255.0
default-router 192.168.2.1
exit
ip dhcp pool vlan2
network 192.168.3.0  255.255.255.0
default-router 192.168.3.1
exit
ip dhcp pool vlan3
network 192.168.4.0  255.255.255.0
default-router 192.168.4.1
exit

  Réglage du filtrage 

    ip nat inside source list 1 interface FastEthernet0/0 overload
    access-list 1 permit 192.168.1.0 0.0.0.255
    access-list 1 permit 192.168.2.0 0.0.0.255
    access-list 1 permit 192.168.3.0 0.0.0.255


    ip access-list extended net1n
     evaluate SIback 
     deny   ip any 192.168.2.0 0.0.0.255
     deny   ip any 192.168.3.0 0.0.0.255
     permit ip any any
     
     ip access-list extended net2n
     evaluate SIback 
     deny   ip any 192.168.1.0 0.0.0.255
     deny   ip any 192.168.3.0 0.0.0.255
     permit ip any any


     

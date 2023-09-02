hostname LODZ1
no ip domain lookup
ip domain name lodz.pl

interface GigabitEthernet0/1
 ip address 172.16.40.1 255.255.255.0
 ip nat inside
 ip authentication key-chain eigrp 100 EIGRP
 standby use-bia
 standby version 2
 standby 1 ip 172.16.40.254
 standby 1 priority 120
 standby 1 preempt
 standby 1 authentication md5 key-string cisco
 standby 1 name LODZ
 
interface GigabitEthernet0/2
 ip address 18.31.192.1 255.255.255.0
 ip nat outside
 standby use-bia
 standby version 2
 standby 255 ip 18.31.192.3
 standby 255 priority 120
 standby 255 preempt
 standby 255 authentication md5 key-string cisco
 standby 255 name LODZ-OUT

ip route 0.0.0.0 0.0.0.0 18.31.192.254

key chain EIGRP
 key 0
  key-string cisco

router eigrp 100
 network 172.16.40.0 0.0.0.255
 network 10.99.0.0 0.0.0.255
 passive-interface default
 no passive-interface GigabitEthernet0/1
 no passive-interface Tunnel1

ip access-list standard NAT
 permit 172.16.40.0 0.0.0.255
ip access-list standard BGP
 deny 172.0.0.0 0.255.255.255
 deny 10.0.0.0 0.255.255.255
 deny 192.168.0.0 0.0.255.255
 permit any
ip access-list standard BGP1
 permit 172.0.0.0 0.255.255.255
 permit 10.0.0.0 0.255.255.255
 permit 192.168.0.0 0.0.255.255
 deny any

ip nat pool HA_POOL 18.31.192.4 18.31.192.4 netmask 255.255.255.0
ip nat inside source list NAT pool HA_POOL overload

route-map BGP permit 1 
 match ip address BGP BGP1

router bgp 65005
 bgp log-neighbor-changes
 neighbor 18.31.192.2 remote-as 65005
 neighbor 18.31.192.254 remote-as 65000
 address-family ipv4
  network 18.31.192.0 mask 255.255.255.0
  redistribute connected
  redistribute eigrp 100
  neighbor 18.31.192.2 activate
  neighbor 18.31.192.254 activate
  neighbor 18.31.192.254 distribute-list BGP out
 exit-address-family

--------------------------------------

interface Tunnel1
 ip address 10.99.0.1 255.255.255.0
 no ip redirects
 ip authentication key-chain eigrp 100 EIGRP
 no ip split-horizon eigrp 100
 ip nhrp authentication cisco
 ip nhrp network-id 100
 ip nhrp redirect
 tunnel source GigabitEthernet0/2
 tunnel mode gre multipoint

--------------------------------------

aaa new-model

radius server RADIUS
 address ipv4 172.16.40.10 auth-port 1645 acct-port 1646
 key Passw0rd!

aaa authentication login default local
aaa authentication login CONSOLE none
aaa authentication login RADIUS1 group radius local
aaa authorization exec default local if-authenticated 
aaa authorization exec CONSOLE none 
aaa authorization exec RADIUS1 group radius local 
aaa authorization network RADIUS1 group radius local 

line con 0
 authorization exec CONSOLE
 login authentication CONSOLE
line vty 0 4
 exec-timeout 0 0
 authorization exec RADIUS1
 login authentication RADIUS1
 transport input telnet
line vty 5 14
 exec-timeout 0 0
 authorization exec RADIUS1
 login authentication RADIUS1
 transport input telnet
line vty 15
 privilege level 15
 transport input telnet

archive
 path tftp://172.16.40.30/$h
 write-memory


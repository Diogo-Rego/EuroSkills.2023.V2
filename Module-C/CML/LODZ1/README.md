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
 standby 1 authentication md5 key-string Passw0rd!
 standby 1 name lodz
 
interface GigabitEthernet0/2
 ip address 18.31.192.2 255.255.255.0
 ip nat outside
 standby use-bia
 standby version 2
 standby 2 ip 18.31.192.1
 standby 2 priority 120
 standby 2 preempt
 standby 2 authentication md5 key-string Passw0rd!
 standby 2 name lodz-out

ip route 0.0.0.0 0.0.0.0 18.31.192.254

object-group network BRANCHES 
 host 100.10.9.5
 host 94.121.72.1
 host 18.31.192.1
 host 18.31.192.2
 host 18.31.192.3
 host 132.87.2.1
 host 65.32.147.1

key chain EIGRP
 key 0
  key-string Passw0rd! 

router eigrp 100
 network 172.16.40.0 0.0.0.255
 passive-interface default
 no passive-interface GigabitEthernet0/1

router bgp 65005
 bgp log-neighbor-changes
 neighbor 18.31.192.3 remote-as 65005
 neighbor 18.31.192.254 remote-as 65000
 address-family ipv4
  network 18.31.192.0 mask 255.255.255.0
  redistribute connected
  redistribute eigrp 100
  neighbor 18.31.192.3 activate
  neighbor 18.31.192.254 activate
  neighbor 18.31.192.254 distribute-list BGP out
 exit-address-family

ip ssh port 2222 rotary 1
ip ssh version 2
ip scp server enable
 
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
ip nat inside source static udp 172.16.40.30 69 18.31.192.4 69 extendable
ip nat inside source list NAT pool HA_POOL overload

route-map BGP permit 1 
 match ip address BGP BGP1
 
line vty 0 4
 exec-timeout 0 0
 transport input ssh
line vty 5 14
 exec-timeout 0 0
 transport input ssh
line vty 15
 privilege level 15
 rotary 1
 transport input ssh

aaa new-model

radius server RADIUS
 address ipv4 172.16.40.10 auth-port 1645 acct-port 1646
 key Passw0rd!

aaa authentication login default group radius local
aaa authorization console
aaa authorization exec default group radius if-authenticated

archive
 path tftp://172.16.40.30/$h
 write-memory
# Semi-Project_Network

## 9.18 Semi-Project 시작

### PC IP

- 인사팀1

  ```
  ip 10.10.20.10 10.10.20.254
  ```

- 인사팀 2

  ```
  ip 10.10.20.11 10.10.20.254
  ```

- 홍보팀 1

  ```
  ip 10.10.30.10 10.10.30.254
  ```

- 홍보팀 2

  ```
  ip 10.10.30.11 10.10.30.254
  ```

- 행정팀 1 

  ```
  ip 10.10.40.10 10.10.40.254
  ```

- 행정팀 2

  ```
  ip 10.10.40.11 10.10.40.254
  ```

- 감사팀 1

  ```
  ip 30.30.20.10 30.30.20.254
  ```

- 감사팀 2

  ```q
  ip 30.30.20.11 30.30.20.254
  ```

- 보안팀 1

  ```
  ip 30.30.30.10 30.30.30.254
  ```

- 보안팀 2

  ```
  ip 30.30.30.11 30.30.30.254
  ```

  

## 9.19

### VLAN

#### Switch

R3 [인사팀 SW]

```
conf t
no ip routing
in ran f1/0 - 15
sh
exit

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40
vlan 50
name v50

in ran f1/0 - 2
no sh

in ran f1/0 - 1
sw mode access
sw access vlan 10

in f1/2
sw mode trunk
sw trunk en dot1q
sw trunk allowed vlan 1,10,20,30,40,50,1002-1005
```



R4 [홍보팀 SW]

```
conf t
no ip routing
in ran f1/0 - 15
sh
exit

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40
vlan 50
name v50

in ran f1/0 - 4
no sh

in ran f1/0 - 1
sw mode access
sw access vlan 20

in ran f1/2 - 4
sw mode trunk
sw trunk en dot1q
sw trunk allowed vlan 1,10,20,30,40,50,1002-1005
```



 R5 [행정팀 SW]

```
conf t
no ip routing
in ran f1/0 - 15
sh
exit

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40
vlan 50
name v50

in ran f1/0 - 2
no sh

in ran f1/0 - 1
sw mode access
sw access vlan 30

in f1/2
sw mode trunk
sw trunk en dot1q
sw trunk allowed vlan 1,10,20,30,40,50,1002-1005
```



R13  [감사팀 SW]

```
conf t
no ip routing
in ran f1/0 - 15 
sh

in ran f1/0 - 3 
no sh

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40
vlan 50
name v50

in ran f1/0 - 1
sw mo acc
aw acc vlan 40
span portf
exit

in ran f1/2 - 3
sw mo tr
sw tr all vlan 1,40,1002-1005
exit

```



R12  [보안팀 SW]

```
conf t
no ip routing
in ran f1/0 - 15 
sh

in ran f1/0 - 3 
no sh

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40
vlan 50
name v50

in ran f1/0 - 1
sw mo acc
aw acc vlan 50
span portf
exit

in ran f1/2 - 3
sw mo tr
sw tr all vlan 1,10,20,30,40,50,1002-1005
exit

```



#### L3 Switch [미완성]

이중화 1 

```
conf t
in ran f1/0 - 15
sh

in ran f1/0 - 3
no sh

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40
vlan 50
name v50



```



이중화 2 

```
conf t
in ran f1/0 - 15
sh

in ran f1/0 - 3
no sh

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40
vlan 50
name v50


```

#### Router

인천

```
conf t
in ran f0/0 - 1, f1/0
no sh
no switchport

in f0/0.10
encapsulation dot1q 10
ip addr 10.10.20.254 255.255.255.0

in f0/0.20
encapsulation dot1q 20
ip addr 10.10.30.254 255.255.255.0

in f0/0.30
encapsulation dot1q 30
ip addr 10.10.40.254 255.255.255.0

in f1/0.40
encapsulation dot1q 40
ip addr 30.30.20.254 255.255.255.0

in f1/0.50
encapsulation dot1q 50
ip addr 30.30.30.254 255.255.255.0

in f0/0
ip addr 10.10.20.254 255.255.255.0
ip addr 10.10.30.254 255.255.255.0
ip addr 10.10.40.254 255.255.255.0
no sh

in f0/1
ip addr 10.10.10.254 255.255.255.0
no sh

in f1/0
no switchport
ip addr 1.1.1.10 255.255.255.0
no sh

```



## 9.21

### 이중화 

R13 [감사팀 SW]

```
conf t
no ip routing
in ran f1/0 - 15 
sh

in ran f1/0 - 3 
no sh

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40
vlan 50
name v50

in ran f1/0 - 1
sw mo acc
aw acc vlan 40
span portf
exit

in ran f1/2 - 3
sw mo tr
sw tr all vlan 1,40,1002-1005
exit

```

R12 [보안팀 SW]

```
conf t
no ip routing
in ran f1/0 - 15 
sh

in ran f1/0 - 3 
no sh

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40
vlan 50
name v50

in ran f1/0 - 1
sw mo acc
aw acc vlan 50
span portf
exit

in ran f1/2 - 3
sw mo tr
sw tr all vlan 1,10,20,30,40,50,1002-1005
exit

```



이중화1(L3_Sw)

```
conf t
in ran f 1/0- 15
sh

in ran f1/0 - 3
no sh

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40

in f1/0 
sw mo tr
sw tr all vlan 1,40,1002-1005
exit

in f1/1
sw mo tr
sw tr allowed vlan 1,10,20,30,40,50,1002-1005
exit

in vlan 40
ip addr 30.30.20.251 255.255.255.0
vrrp 40 ip 30.30.20.254
vrrp 40 prio 120
vrrp 40 timer advertise 5

in vlan 50
ip addr 30.30.30.251 255.255.255.0
vrrp 50 ip 30.30.30.254
vrrp 50 prio 100
vrrp 50 timer learn
exit

spanning-tree vlan 40 root pri
spanning-tree vlan 50 root sec

in f1/3
sw mode trunk
sw trunk en dot1q
sw trunk allowed vlan 1,10,20,30,40,50,1002-1005
 
in f1/2
sw mode trunk
sw trunk en dot1q
sw trunk allowed vlan 1,10,20,30,40,50,1002-1005

```



이중화2(L3_Sw)

```
conf t
in ran f 1/0- 15
sh

in ran f1/0 - 3
no sh

vlan 10
name v10
vlan 20
name v20
vlan 30
name v30
vlan 40
name v40

in f1/0
sw mo tr
sw tr all vlan 1,10,20,30,40,50,1002-1005

in f1/1
sw mo tr
sw tr all vlan 1,40,1002-1005

in vlan 50
ip addr 30.30.30.252 255.255.255.0
vrrp 50 ip 30.30.30.254
vrrp 50 prio 120
vrrp 50 timer advertise 5
 
in vlan 40
ip addr 30.30.20.252 255.255.255.0
vrrp 40 ip 30.30.20.254
vrrp 40 prio 100
vrrp 40 timer learn
exit

spanning-tree vlan 50 root pri
spanning-tree vlan 40 root sec

in f1/3
sw mode trunk
sw trunk en dot1q
sw trunk allowed vlan 1,10,20,30,40,50,1002-1005
 
in f1/2
sw mode trunk
sw trunk en dot1q
sw trunk allowed vlan 1,10,20,30,40,50,1002-1005

```



본사 1 

```
conf t
in f0/0
ip addr 30.30.20.254 255.255.255.0
no sh

in f0/1
ip addr 30.30.30.254 255.255.255.0
no sh

in f2/0
no switchport
ip addr 80.80.80.254 255.255.255.0
ip addr 90.90.90.254 255.255.255.0
no sh

in f2/1
no switchport
ip addr 2.2.2.20 255.255.255.0
no sh
exit

router ospf 1
network 2.2.2.0 0.0.0.255 area 0
exit

access-list 1 permit 30.30.20.0 0.0.0.255
access-list 1 permit 30.30.30.0 0.0.0.255
access-list 1 permit 80.80.80.0 0.0.0.255
access-list 1 permit 90.90.90.0 0.0.0.255

in ran f0/0 - 1 , f2/0
ip nat in 

in f2/1
ip nat out
```



###   Routing_OSPF

인천

```
router ospf 1
network 1.1.1.0 0.0.0.255 area 0
exit
```



본사

```
conf t 

in f0/1
ip addr 1.1.1.20 255.255.255.0
no sh

in f1/0
no switchport
ip addr 2.2.2.10 255.255.255.0
no sh

in f0/0 [모름]

router ospf 1
network 1.1.1.0 0.0.0.255 area 0
network 2.2.2.0 0.0.0.255 area 0
exit

ip route 0.0.0.0 0.0.0.0 200.200.200.254
access-list 1 permit 
ip nat inside source list 1 in f0/0

in f0/0
ip nat out
in f0/1
ip nat in
in f1/0
ip nat in


```

 

본사 1

```
in s1/0
encapsulation ppp
bandwidth 512
ip address x.x.x.x 255.255.255.0
no sh

in f0/1

in f0/0

in f2/0
no switchport 

router ospf 3
network 30.30.20.0 0.0.0.255 area 0
network 30.30.30.0 0.0.0.255 area 0
 
```

### 터널링

인천

```
int tunnel 0
tunnel mode gre ip
tunnel source f1/0
tunnel destination 2.2.2.20
ip address 3.3.3.10 255.255.255.0
exit

access-list 101 permit ip any 30.30.20.0 0.0.0.255
access-list 101 permit ip any 30.30.30.0 0.0.0.255
access-list 101 permit ip any 80.80.80.0 0.0.0.255
access-list 101 permit ip any 90.90.90.0 0.0.0.255
route-map PBR permit
match ip address 101
set ip next-hop 3.3.3.20
exit

in ran f0/0 - 1
ip policy route-map PBR
exit
```



본사1 

```
int tunnel 0
tunnel mode gre ip
tunnel source f2/1
tunnel destination 1.1.1.10
ip addr 3.3.3.20 255.255.255.0
exit
 
access-list 101 permit ip any 10.10.10.0 0.0.0.255
access-list 101 permit ip any 10.10.20.0 0.0.0.255
access-list 101 permit ip any 10.10.30.0 0.0.0.255
access-list 101 permit ip any 10.10.40.0 0.0.0.255

route-map PBR permit
match ip address 101
set ip next-hop 3.3.3.10
exit

in ran 0/0 - 1 , f2/0
ip policy route-map PBR
exit
```



### 인터페이스

#### Switch

####  


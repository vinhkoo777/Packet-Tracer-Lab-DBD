# Bài làm 

## Subnet Allocation

| Department | Network Address | Prefix | Usable Host Range | Broadcast Address |
|------------|-----------------|--------|-------------------|-------------------|
| Sales | 192.168.100.0 | /26 | 192.168.100.1 – 192.168.100.62 | 192.168.100.63 |
| HR | 192.168.100.64 | /27 | 192.168.100.65 – 192.168.100.94 | 192.168.100.95 |
| Management | 192.168.100.96 | /28 | 192.168.100.97 – 192.168.100.110 | 192.168.100.111 |

## Switch
- Tạo Vlan trên Switch

```
conf t 
hostname SW1

interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access

interface FastEthernet0/2
 switchport access vlan 20
 switchport mode access

interface FastEthernet0/24
 switchport access vlan 99
 switchport mode access
```
- Cấu hình trunk port

```
interface FastEthernet0/23
 switchport mode trunk
```

## Router 
- Sử dụng Router all a stick. Dùng để tạo các subinterface

```
conf t
hostname R1

interface GigabitEthernet0/1.10
 encapsulation dot1Q 10
 ip address 192.168.100.1 255.255.255.192

interface GigabitEthernet0/1.20
 encapsulation dot1Q 20
 ip address 192.168.100.65 255.255.255.224

interface GigabitEthernet0/1.99
 encapsulation dot1Q 990
 ip address 192.168.100.97 255.255.255.240
```

## DHCP 

### Cấu hình trên Server

**- Management dùng IP tĩnh**

<img width="762" height="316" alt="image" src="https://github.com/user-attachments/assets/56dcfebb-295c-458b-9e00-8f92e18cf2ec" />

**- cấu hình Default Gateway**

<img width="713" height="133" alt="image" src="https://github.com/user-attachments/assets/fe3c2ac0-afeb-4d79-aec1-9c05f45c1756" />

**- Tạo pool cho Sales và HR**

<img width="752" height="107" alt="image" src="https://github.com/user-attachments/assets/d058c308-392c-4452-bb7a-e40860770dbf" />

## Helper address 

```
interface GigabitEthernet0/1.10
 ip helper-address 192.168.100.105

interface GigabitEthernet0/1.20
 ip helper-address 192.168.100.105
```

## SSH 

```
ip domain name vinhlab.com
crypto key generate rsa # nhập 2048

enable secret ccna
username vinh secret ccna
ip ssh version 2
line vty 0 15
login local
exec-timeout 5 0
transport input ssh # best practice vì chỉ giới hạn sử dụng SSH thuiiii
```

## Routing 

> Trên Router ISP 

```
interface GigabitEthernet0/0
 ip address 203.0.113.1 255.255.255.252
 no shutdown

ip route 192.168.0.0 255.255.0.0 203.0.113.2
```

> Trên R1

```
interface GigabitEthernet0/0
 ip address 203.0.113.2 255.255.255.252
 no shutdown

ip route 0.0.0.0 0.0.0.0 203.0.113.1
```

## ACL

- Trong global config của **R1** thực hiện các lệnh dưới 

```
conf t 
ip access-list extended Sales

permit icmp 192.168.100.0 0.0.0.63 host 192.168.100.105
permit tcp 192.168.100.0 0.0.0.63 host 192.168.100.1 eq 22
permit tcp 192.168.100.0 0.0.0.63 host 192.168.100.105 eq 80
deny icmp 192.168.100.0 0.0.0.63 192.168.100.64 0.0.0.31
deny ip any any

int g0/1.10
ip access-group Sales in


access-list extended Management
permit ip any any 

int g0/1.99
ip access-group Management in

```

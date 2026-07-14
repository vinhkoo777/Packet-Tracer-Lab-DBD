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

## Router 
- Sử dụng Router all a stick. Dùng để tạo các subinterface

```
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

**- Tạo pool cho Sales và HR**

<img width="752" height="107" alt="image" src="https://github.com/user-attachments/assets/d058c308-392c-4452-bb7a-e40860770dbf" />

## helper address 

```
interface GigabitEthernet0/1.10
 ip helper-address 192.168.100.105

interface GigabitEthernet0/1.20
 ip helper-address 192.168.100.105
```

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

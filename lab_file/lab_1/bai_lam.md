# Bài làm 

## IP 

192.168.100.0 - 192.168.100.63 prefix /26 - Sales 
192.168.100.64 - 192.168.100.95 prefix /27 - HR
192.168.100.96 - 192.168.100.111 prefix /28 - Management

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

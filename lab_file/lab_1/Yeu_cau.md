# Lab #1 – Branch Office Deployment
⭐⭐⭐☆☆ | Build từ đầu

**Cover:** IPv4, VLSM, VLAN, Access/Trunk, Router-on-a-Stick, Static Route, DHCP, SSH, Extended ACL, CDP/LLDP

<img width="669" height="725" alt="image" src="https://github.com/user-attachments/assets/c5a3802b-ff58-43a4-8a33-45900015c4fe" />

- Thiết bị: 1 Router, 1 Switch 2960, 2 PC, 1 Server
- WAN: ISP `203.0.113.1` – R1 `203.0.113.2`

## VLAN & VLSM
LAN block: `192.168.100.0/24` -> tự chia VLSM theo host yêu cầu

| VLAN | Name | Hosts |
|---|---|---|
| 10 | Sales | 60 |
| 20 | HR | 30 |
| 99 | Management | 10 |

## Router
- Router-on-a-Stick, subinterface cho VLAN 10/20/99

## DHCP
- Cấu hình trên **Server** (không phải router)
- Cấp IP cho Sales + HR; Management dùng IP tĩnh

## Server
- Nằm VLAN 99, IP tĩnh, gateway đúng

## SSH (chỉ SSH vào Router, không Telnet)
hostname, domain-name, RSA 2048, local user, enable secret, `login local`

## Routing
- ISP có route về toàn bộ LAN; R1 có default route -> ISP

## ACL (Extended)
| | Sales | HR | Management |
|---|---|---|---|
| Ping Server | ✅ | ✅ | ✅ |
| SSH Router | ✅ | ❌ | ✅ |
| HTTP Server | ✅ | – | ✅ |
| Ping HR/Sales chéo | ❌ | – | ✅ |

## CDP
Bật CDP, verify Router thấy Switch

## Verification checklist
- [ ] PC Sales: DHCP, ping gateway/Server, SSH Router, **không** ping HR
- [ ] PC HR: DHCP, ping gateway/Server, **không** SSH Router
- [ ] Server: IP tĩnh, ping được cả 2 VLAN


# Mega Lab #1 – Enterprise Branch Infrastructure
⭐⭐⭐⭐⭐ | Enterprise Network Project

**Cover:** VLSM, VLAN, Trunk, EtherChannel, Rapid STP, Inter-VLAN Routing, OSPF, Floating Static Route, HSRP, DHCP, DNS, SSH, Syslog, NTP, NAT, ACL, Port Security, DHCP Snooping, DAI, CDP/LLDP

> Chèn con mèo béo blim blem bieakdfjanc; ở đây :33

## Thiết bị

### Headquarters
- 2 Router
- 1 Layer 3 Switch
- 2 Layer 2 Switch
- 1 Server
- 8–12 PCs

### Branch
- 1 Router
- 1 Switch
- 3 PCs

### ISP
- 1 Router

## WAN

- ISP: `203.0.113.1/30`
- HQ Edge: `203.0.113.2/30`

## VLAN & VLSM

LAN Block: `10.10.0.0/16`

| VLAN | Name | Hosts |
|------|------|------:|
|10|Sales|120|
|20|HR|60|
|30|IT|30|
|40|Server|20|
|50|Guest|80|
|99|Management|20|


## Layer 2

- VLAN
- Trunk
- Native VLAN (≠ VLAN 1)
- Rapid STP
- EtherChannel (LACP)

## Layer 3

- Inter-VLAN Routing
- OSPF Area 0
- Default Route
- Floating Static Route


## HSRP

- R1: Active
- R2: Standby
- Kiểm tra Failover


## DHCP & DNS

- DHCP trên Server
- DNS trên Server
- Sales, HR, Guest dùng DHCP
- Management dùng IP tĩnh

## SSH

- SSH trên toàn bộ Router & Switch
- Không sử dụng Telnet

## NAT

- PAT cho toàn bộ người dùng
- Static NAT cho Web Server

## ACL

| | Sales | HR | IT | Guest |
|---|---|---|---|---|
| HTTP/HTTPS Server | ✅ | ✅ | ✅ | ❌ |
| DNS | ✅ | ✅ | ✅ | ❌ |
| SSH Router | ❌ | ❌ | ✅ | ❌ |
| Ping giữa VLAN | ❌ | ❌ | ✅ | ❌ |
| Internet | ✅ | ✅ | ✅ | ✅ |

## Security

- Port Security
- DHCP Snooping
- Dynamic ARP Inspection

## Monitoring

- CDP / LLDP
- Syslog
- NTP


## Verification Checklist

- [ ] VLAN & Trunk hoạt động
- [ ] EtherChannel hoạt động
- [ ] OSPF Full
- [ ] HSRP Failover thành công
- [ ] DHCP & DNS hoạt động
- [ ] SSH hoạt động
- [ ] NAT hoạt động
- [ ] ACL đúng yêu cầu
- [ ] Port Security hoạt động
- [ ] DHCP Snooping hoạt động
- [ ] DAI hoạt động
- [ ] Syslog nhận log
- [ ] NTP đồng bộ
- [ ] CDP/LLDP hiển thị đúng

# project-7-2-corporate-network-lab
Corporate network lab upgrade (Project 7.2) with 2 routers, 4 switches, 8 VLANs, ACL configuration, DHCP, and inter-VLAN communication. Consolidation of Project 7 with extended VLANs and improved access control.


## Overview
Project 7.2 is an upgraded and consolidated version of Project 7. It simulates a corporate network environment with multiple VLANs, ACLs, DHCP configuration, and inter-VLAN routing. This lab is designed to practice real-world network configuration, access control, and troubleshooting in a Cisco environment.

## Topology
- **Routers:** 2
- **Switches:** 4
- **VLANs:** 8, with 4 PCs per VLAN

| VLAN | Purpose        | Switch |
|------|----------------|--------|
| 10   | Clients 1      | Switch 1 |
| 20   | Clients 1      | Switch 1 |
| 30   | Clients 2      | Switch 2 |
| 40   | Clients 2      | Switch 2 |
| 50   | Servers        | Switch 3 |
| 60   | Servers        | Switch 3 |
| 70   | Management     | Switch 4 |
| 80   | Management     | Switch 4 |

## ACL Configuration
- ACL applied only on VLANs 10–40.  
- Extended ACLs used to restrict traffic as required.

| VLAN | Access Allowed                 | Notes                 |
|------|--------------------------------|----------------------|
| 10   | VLAN 20–30                     | Block all others     |
| 20   | VLAN 40–10                     | Block all others     |
| 30   | VLAN 40–50                     | Block all others     |
| 40   | VLAN 70                        | Block all others     |
| 50–80| No ACL (full access)           | Functioning normally |

## DHCP Configuration
- **Router 1** handles DHCP for VLANs: 10, 20, 30, 40, 70, 80  
- **Router 2** handles DHCP for VLANs: 50, 60  
- IP helper addresses configured for inter-VLAN DHCP requests.  

## Tests and Verification
- `ping` tests performed from PCs in each VLAN to verify connectivity.  
- VLAN 50–80 communicates correctly with VLANs 30–40 and inter-router routing verified.  
- ACLs tested to ensure restricted access works as planned.  

## Key Commands (Examples)
### VLAN and Subinterface Configuration
```bash
interface g0/0.10
 ip address 192.168.10.1 255.255.255.0
 no shutdown
!
interface g0/0.50
 ip address 192.168.50.1 255.255.255.0
 no shutdown

ACL Example
access-list 100 permit ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
access-list 100 deny ip any any

interface g0/0.10
 ip access-group 100 in

DHCP Pool Example
Copiar código
Bash
ip dhcp pool VLAN10
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8

Screenshots
R1 VLANs and Subinterfaces – R1_VLANs_Subinterfaces.png
R2 VLANs and Subinterfaces – R2_VLANs_Subinterfaces.png
ACLs Configuration – ACL_VLAN10-40.png
DHCP Pools – DHCP_Pools_R1_R2.png
Ping Test Results – Ping_Tests.png
Notes
This lab is a practical simulation of corporate network design with VLAN separation, DHCP management, and ACL-based access control.
Focused on real-world scenarios for IT consultancy and networking best practices.
All VLANs are functional and inter-VLAN routing is fully tested.

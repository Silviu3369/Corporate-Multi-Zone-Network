# Corporate Multi-Zone Network  
**Enterprise-grade Network Infrastructure Documentation**

---

## 1. Overview
The **Corporate Multi-Zone Network** connects four enterprise zones through a secure, redundant dual-hub architecture built on **DMVPN over IPsec**.  
Each zone is logically segmented with dedicated VLANs, redundant gateways (**HSRP**), and centralized security via **ASA Firewalls** and **Zone-Based Firewall (ZBF)** policies.

The design ensures:
- End-to-end encrypted connectivity (AES-256 IPsec)
- High availability using dual routers and switches
- Logical segmentation with scalable VLAN structure
- Centralized management for NTP, SYSLOG, SSH, and DHCP

---

## 2. Topology Summary
| Zone | Description | Role | Connectivity |
|:--:|:--|:--|:--|
| Zone 1 | Headquarters Department | Spoke 1 | DMVPN tunnels to Hub 1 & Hub 2 |
| Zone 2 | Server Farm + DMZ | Hub 1 & Hub 2 | Centralized services + ASA perimeter |
| Zone 3 | Operations Branch | Spoke 2 | Remote users, guest/staff networks |
| Zone 4 | Finance & Marketing | Spoke 3 | Financial and sales departments |

---

## 3. Core Technologies
- **Routing:** OSPF Area 0 (single backbone)
- **VPN:** Dual-Hub DMVPN (GRE over IPsec AES-256)
- **Redundancy:** HSRP on all VLANs (.1 VIP)
- **Security:** ASA firewalls + ZBF + ACL + NAT Exempt
- **Management:** Central NTP (192.168.50.6) and SYSLOG (192.168.50.7)

---

## 4. Zone Details

### 4.1 Zone 1 – HQ (Spoke 1)
Provides IT and user connectivity at headquarters.  
Contains management, Wi-Fi, and services VLANs.  
Edge router performs DMVPN tunnels to both hubs and NAT to ISP.  
Redundant MS1/MS2 core switches handle inter-VLAN routing with HSRP.  
Distribution Switch **DS-ZONE1** connects access devices via VLAN 5/10/15/20.

---

### 4.2 Zone 2 – Server Farm + DMZ (Hub 1 & Hub 2)
Central site hosting core servers and security perimeter.  
Includes DHCP, DNS, WEB, AD, File, NTP, and SYSLOG services.  
Two ASA firewalls secure the DMZ and control inbound/outbound flows.  
MS1/MS2 core switches provide gateway redundancy; EDGE1/EDGE2 operate as DMVPN hubs.  
Distribution Switch **DS-ZONE2** interconnects DMZ, Servers, and Management VLANs.

---

### 4.3 Zone 3 – Operations (Spoke 2)
Remote operational branch for staff and guest access.  
Uses VLANs 25/30/35 for Guests, Users, and Staff, plus VLAN 60 for management.  
EDGE-ZONE3 performs NAT to ISP and encrypted DMVPN tunnels to both hubs.  
Distribution Switch **DS-ZONE3** links all local access switches.

---

### 4.4 Zone 4 – Finance & Marketing (Spoke 3)
Dedicated branch for finance, marketing, and sales departments.  
Operates VLANs 70/80/90 for business segments and VLAN 95 for management.  
Has its own local DHCP server (192.168.95.7) and dual DMVPN connectivity.  
Distribution Switch **DS-ZONE4** provides local switching and trunk links to MS1/MS2.

---

## 5. Security Overview
- **ASA Firewalls:** perimeter protection, static NAT for public services, NAT Exempt for VPN  
- **Zone-Based Firewall:** inter-zone policy enforcement (INTERNAL/VPN/MGMT/OUTSIDE)  
- **ACL Framework:** SSH-MGMT, OUTSIDE-IN, NAT-EXEMPT lists standardized across zones  
- **Defense in Depth:** layered security at edge, core, and access layers  

---

## 6. Management and Monitoring
- **NTP Server:** 192.168.50.6  
- **SYSLOG Server:** 192.168.50.7  
- **SSH Access:** Restricted to management VLANs (5, 55, 60, 95)  
- **SNMP and Syslog:** Collect device health and link status  
- **Verification Tools:** OSPF neighbors, DMVPN status, NAT translations, HSRP brief  

---

## 7. IP Addressing Table
See full addressing reference below.  
(The complete IP table can be inserted here.)

[Full IP Addressing Table](#)

---

## 8. Access Credentials
| Parameter | Value |
|:--|:--|
| **Username** | admin |
| **Password** | cisco |

---

## 9. Summary
The **Corporate Multi-Zone Network** provides a unified, secure, and scalable foundation for enterprise connectivity.  
It integrates centralized services, remote branches, and DMZ operations into a single, redundant architecture following Cisco Design Zone best practices.

---


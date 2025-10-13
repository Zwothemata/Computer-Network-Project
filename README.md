# 🖧 CMPG 325 - Computer Networks Long Project (Hybrid Topology)
### **Name:**  
### **Module:** CPMG 325 - Computer Networks  
### **Instructor:** Prof Lugayizi 
### **Year:** 2025  

---

## 📘 Project Overview

This project implements and simulates **five basic network topologies** — Bus, Star, Mesh, Ring, and Extended Star — using **Cisco Packet Tracer**.  
A **Hybrid Topology** integrates all five into one network with VLAN segmentation, IPv4/IPv6 addressing, one central **server (HTTP/DNS/DHCP)**, and a **router-on-a-stick** setup for inter-VLAN communication.

The design ensures:
- Proper VLAN segmentation and IP planning  
- End-to-end data exchange between all zones  
- Basic network security (ACLs, port security)  
- Centralized management and DHCP configuration  

---

## Hybrid Topology 

![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Screenshot%20(208).png?raw=true)


## 🧩 Network Components

| Device Type | Quantity | Description |
|--------------|-----------|-------------|
| Routers | 1 | Main inter-VLAN router (Router0) |
| Switches | 6 | Distributed across topologies |
| PCs | 20 | User devices across 5 network zones |
| Server | 1 | Provides DHCP, DNS, HTTP services |
| Access Points (optional) | 1–2 | Used for wireless mesh (Part II) |

---

##  IP Addressing Table
## 🧩 IP Addressing Table

| **Device** | **IP Address** | **Topology Zone** | **IPv6(link local address)** |
|-------------|----------------|-------------------|-----------------|
| PC0 | 198.162.1.1 | Bus | FE80::206:2AFF:FE77:4D16|
| PC1 | 198.162.1.2 | Bus | FE80::201:43FF:FE78:BC25 |
| PC2 | 198.162.1.3 | Bus |FE80::260:3EFF:FEA8:74E2 |
| PC3 | 198.162.1.4 | Star| FE80::20D:BDFF:FEEB:876C |
| PC4 | 198.162.1.5 | Star | FE80::20D:BDFF:FEEB:876C |
| PC5 | 198.162.1.6 | Extended Star | FE80::260:70FF:FE37:3205 |
| PC6 | 198.162.1.7 | Mesh | FE80::202:16FF:FE89:7A0B |
| PC7 | 198.162.1.8 | Mesh | FE80::202:4AFF:FE47:936E |
| PC8 | 198.162.1.9 | Extended Star | FE80::2D0:58FF:FE0A:1B31 |
| PC9 | 198.162.1.10 | Mesh | FE80::2E0:8FFF:FE4E:65BD |
| Server (DHCP/HTTP) | 198.162.1.1| Mesh | FE80::201:43FF:FEDE:5BAB |
| PC10 | 198.162.1.12 | Mesh | FE80::201:43FF:FE4E:CEB1|
| PC11 | 198.162.1.13 | Ring | FE80::201:42FF:FE64:B2D8 |
| PC12 | 198.162.1.14 | Ring | FE80::202:17FF:FE02:6D5D |
| PC13 | 198.162.1.15 | Ring | FE80::2D0:58FF:FE3A:2E9B |
| PC14 | 198.162.1.16 | Ring |FE80::201:97FF:FE9E:D386 |
| PC15 | 198.162.1.17 | Star | FE80::2E0:8FFF:FE59:15B2 |
| PC16 | 198.162.1.18 | Star | FE80::2D0:58FF:FEB6:65DA |
| PC17 | 198.162.1.19 | Star | FE80::2E0:F7FF:FEB8:637E |
|PC18  |198.162.1.20  |Extended Star |  FE80::2E0:A3FF:FE1B:1307 |
|PC19  |198.162.1.6   | Extended Star| FE80::20A:F3FF:FE00:E9D7 |
| Switches | Assigned Dynamically | All Zones | |

---
---

## 📑 VLAN Assignment Table

| VLAN ID | VLAN Name | Subnet | Zone | Purpose |
|----------|------------|---------|--------|----------|
| 10 | STUDENTS | 192.168.10.0/24 | Green Zone | Student devices (Star Topology) |
| 20 | STAFF | 192.168.20.0/24 | Blue Zone | Staff (Mesh Topology) |
| 30 | LAB | 192.168.30.0/24 | Pink Zone | Lab devices (Bus Topology) |
| 40 | ENGINEERING | 192.168.40.0/24 | Cyan Zone | Engineering & Research (Extended Star) |
| 50 | CORE | 192.168.50.0/24 | Yellow Zone | Core backbone between switches |
| 99 | MGMT | 192.168.99.0/24 | All switches | Management VLAN (SSH/Console) |
| 100 | SERVERS | 192.168.100.0/24 | Server Area | Server VLAN (DHCP/DNS/HTTP) |

---

## 🖥️ Device Configuration Summary

| Device | IP Address | VLAN | Function |
|---------|-------------|------|-----------|
| PC1–PC4 | 192.168.10.10–13 | 10 | Star Network PCs |
| PC11–PC14 | 192.168.20.10–13 | 20 | Mesh Network PCs |
| PC15–PC17 | 192.168.30.10–12 | 30 | Bus Network PCs |
| PC5, PC16–19 | 192.168.40.10–15 | 40 | Extended Star / Ring PCs |
| PC8–PC10 | 192.168.50.10–12 | 50 | Core VLAN PCs |
| Server0 | 192.168.100.10 | 100 | HTTP/DNS/DHCP Server |
| Router0 (Subinterfaces) | 192.168.x.1 | All | VLAN gateways |

---

## ⚙️ Configuration Notes

### 🔸 Router Configuration (Router-on-a-Stick)
```bash
enable
conf t
interface g0/0
 no shutdown

interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0

interface g0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0

interface g0/0.40
 encapsulation dot1Q 40
 ip address 192.168.40.1 255.255.255.0

interface g0/0.50
 encapsulation dot1Q 50
 ip address 192.168.50.1 255.255.255.0

interface g0/0.99
 encapsulation dot1Q 99
 ip address 192.168.99.1 255.255.255.0

interface g0/0.100
 encapsulation dot1Q 100
 ip address 192.168.100.1 255.255.255.0
exit
wr
------

enable
conf t
vlan 10
 name STUDENTS
vlan 20
 name STAFF
vlan 30
 name LAB
vlan 40
 name ENGINEERING
vlan 50
 name CORE
vlan 99
 name MGMT
vlan 100
 name SERVERS

interface range f0/1 - 4
 switchport mode access
 switchport access vlan 10

interface range f0/5 - 8
 switchport mode access
 switchport access vlan 20

interface g0/1
 switchport mode trunk

--------



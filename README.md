# 🖧 CMPG 325 - Computer Networks Long Project (Hybrid Topology)
### **Name:** Zwothe Matamela 
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

## 🧩 Network Components

| Device Type | Quantity | Description |
|--------------|-----------|-------------|
| Routers | 1 | Main inter-VLAN router (Router0) |
| Switches | 6 | Distributed across topologies |
| PCs | 20 | User devices across 5 network zones |
| Server | 1 | Provides DHCP, DNS, HTTP services |
| Access Points (optional) | 1–2 | Used for wireless mesh (Part II) |

---

## 🌐 IP Addressing Plan (IPv4 and IPv6)

| VLAN | Zone / Topology | Subnet | Gateway (Router Subinterface) | IPv6 Network | Device Range |
|------|------------------|---------|-------------------------------|---------------|---------------|
| 10 | 🟩 **Star Network (Green)** | 192.168.10.0/24 | 192.168.10.1 | 2001:db8:10::/64 | 192.168.10.10 – 192.168.10.50 |
| 20 | 🟦 **Mesh Network (Blue)** | 192.168.20.0/24 | 192.168.20.1 | 2001:db8:20::/64 | 192.168.20.10 – 192.168.20.50 |
| 30 | 🟪 **Bus Network (Pink)** | 192.168.30.0/24 | 192.168.30.1 | 2001:db8:30::/64 | 192.168.30.10 – 192.168.30.50 |
| 40 | 🩵 **Extended Star / Ring (Cyan)** | 192.168.40.0/24 | 192.168.40.1 | 2001:db8:40::/64 | 192.168.40.10 – 192.168.40.50 |
| 50 | 🟨 **Core + Server VLAN (Yellow)** | 192.168.50.0/24 | 192.168.50.1 | 2001:db8:50::/64 | 192.168.50.10 – 192.168.50.30 |
| 99 | **Management VLAN** | 192.168.99.0/24 | 192.168.99.1 | 2001:db8:99::/64 | 192.168.99.10 – 192.168.99.50 |
| 100 | **Server VLAN** | 192.168.100.0/24 | 192.168.100.1 | 2001:db8:100::/64 | 192.168.100.10 – 192.168.100.30 |

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

IP Address: 192.168.100.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.100.1
DNS Server: 192.168.100.10

DHCP Pools:
- VLAN 10: 192.168.10.10–50
- VLAN 20: 192.168.20.10–50
- VLAN 30: 192.168.30.10–50
- VLAN 40: 192.168.40.10–50

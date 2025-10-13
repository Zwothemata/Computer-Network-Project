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



# 🌐 Hybrid Network Topology – Cisco Packet Tracer

## 📘 Overview
This project demonstrates a **Hybrid Network Topology** integrating multiple topological designs — **Bus, Star, Extended Star, Ring, and Mesh** — within one cohesive network.  
It was created using **Cisco Packet Tracer** and showcases IPv4 configuration, VLAN segmentation, server connectivity, and inter-topology communication.

---

## 🖥️ Topology Components

| **Zone** | **Topology Type** | **Color Zone** | **Devices Included** | **Purpose / Notes** |
|-----------|------------------|----------------|-----------------------|---------------------|
| Zone A | **Bus Topology** | 🔴 Red | 3 PCs, 3 Switches | Demonstrates linear connection of devices using a shared backbone. |
| Zone B | **Extended Star Topology** | 🔵 Blue | 5 PCs, 3 Switches | Central switch connects multiple branches of star networks. |
| Zone C | **Ring Topology** | 🟦 Dark Blue | 4 PCs, 4 Switches | Each device connected to two others forming a logical ring. |
| Zone D | **Star Topology** | 🟢 Green | 4 PCs, 1 Switch | Centralized connection through a single switch. |
| Zone E | **Mesh Topology** | 🟡 Yellow | 4 PCs, 3 Switches, 1 Server | High redundancy and fault tolerance with multiple interconnections. |

---

## 🧩 IP Addressing Table

| **Device** | **IP Address** | **Topology Zone** | **Description** |
|-------------|----------------|-------------------|-----------------|
| PC0 | 198.162.1.1 | Bus | Workstation Node 1 |
| PC1 | 198.162.1.2 | Bus | Workstation Node 2 |
| PC2 | 198.162.1.3 | Bus | Workstation Node 3 |
| PC3 | 198.162.1.4 | Extended Star | Workstation Node 1 |
| PC4 | 198.162.1.5 | Extended Star | Workstation Node 2 |
| PC5 | 198.162.1.6 | Extended Star | Workstation Node 3 |
| PC6 | 198.162.1.7 | Extended Star | Workstation Node 4 |
| PC7 | 198.162.1.8 | Mesh | Workstation Node 1 |
| PC8 | 198.162.1.9 | Mesh | Workstation Node 2 |
| PC9 | 198.162.1.10 | Mesh | Workstation Node 3 |
| Server (DHCP/HTTP) | 198.162.1.11 | Mesh | Centralized Server for DHCP and Web Services |
| PC10 | 198.162.1.12 | Ring | Workstation Node 1 |
| PC11 | 198.162.1.13 | Ring | Workstation Node 2 |
| PC12 | 198.162.1.14 | Ring | Workstation Node 3 |
| PC13 | 198.162.1.15 | Ring | Workstation Node 4 |
| PC14 | 198.162.1.16 | Star | Workstation Node 1 |
| PC15 | 198.162.1.17 | Star | Workstation Node 2 |
| PC16 | 198.162.1.18 | Star | Workstation Node 3 |
| PC17 | 198.162.1.19 | Star | Workstation Node 4 |
| Switches | Assigned Dynamically | All Zones | Core/Access Layer Devices |

---

## 🌍 VLAN Configuration Notes
| **VLAN ID** | **Zone** | **Purpose** |
|--------------|----------|--------------|
| 10 | Bus | Isolated testing subnet |
| 20 | Extended Star | Academic/Lab connections |
| 30 | Ring | Research subnet |
| 40 | Star | Office LAN |
| 50 | Mesh | Server + Core network backbone |

---

## ⚙️ Server Configuration
**Device:** DHCP + HTTP Server  
**IP Address:** `198.162.1.11`  
**Services Enabled:**
- DHCP Pool for all VLANs
- HTTP Web Hosting
- DNS optional (if configured for internal hostname resolution)

---

## 🔄 Interconnection Links
- Each topology is linked through **core switches** using **FastEthernet** connections.  
- **Mesh zone** serves as the **core distribution** connecting all other topologies.
- Trunk links configured for VLAN intercommunication.

---

## 🧠 Key Learning Objectives
- Understand the design and function of various network topologies.
- Learn how to integrate multiple topologies into one hybrid model.
- Practice IP addressing, VLAN segmentation, and device interconnectivity.
- Configure DHCP and HTTP servers for automated IP and web service delivery.

---

## 📸 Topology Diagram
> Below is the visual representation of the Hybrid Topology (as designed in Cisco Packet Tracer):

![Hybrid Network Topology](./Screenshot%20(208).png)

---

## 🧾 Simulation Notes
- All PCs can ping the **DHCP/HTTP server (198.162.1.11)** if properly configured.  
- VLAN trunking allows devices from different zones to communicate.  
- Static routes or router-on-a-stick may be used for inter-VLAN routing.

---

## 👨‍💻 Author
**Zwothe Matamela**  
📅 *Last Updated:* October 2025  
📂 *Project File:* `HYBRID_TOPOLOGY.pkt`

---

## 🏁 How to Use
1. Open `HYBRID_TOPOLOGY.pkt` in **Cisco Packet Tracer**.  
2. Enable simulation mode and test ping between zones.  
3. View DHCP and HTTP configuration on the server.  
4. Optionally extend the network by adding wireless APs or routers.

---

### ✅ Result
A fully functional **Hybrid Network** combining multiple topology types with active communication across all zones.



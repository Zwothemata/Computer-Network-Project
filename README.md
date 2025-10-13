# 🖧 CMPG 325 - Computer Networks Long Project (Hybrid Topology)
### **Name:**  
### **Module:** CPMG 325 - Computer Networks  
### **Instructor:** Prof Lugayizi 
### **Year:** 2025  

---

##  Project Overview

This project implements and simulates **five basic network topologies** — Bus, Star, Mesh, Ring, and Extended Star — using **Cisco Packet Tracer**.  
A **Hybrid Topology** integrates all five into one network with VLAN segmentation, IPv4/IPv6 addressing, one central **server (HTTP/DNS/DHCP)**, and a **router-on-a-stick** setup for inter-VLAN communication.

The design ensures:
- Proper VLAN segmentation and IP planning  
- End-to-end data exchange between all zones  
- Basic network security (ACLs, port security)  
- Centralized management and DHCP configuration  

---
### Part I: Network Topologies



### Bus Topology
![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Bus%20topology.png?raw=true)


### Mesh Topology
![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Mesh%20Topology.png?raw=true)


### Star Topology
![picture]()


### Ring Topology
![picture]()


### Extended Star
![picture]()










## Hybrid Topology 

![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Screenshot%20(208).png?raw=true)


##  Network Components

| Device Type | Quantity | Description |
|--------------|-----------|-------------|
| Routers | 1 | Main inter-VLAN router (Router0) |
| Switches | 6 | Distributed across topologies |
| PCs | 20 | User devices across 5 network zones |
| Server | 1 | Provides DHCP, DNS, HTTP services |
| Access Points (optional) | 1–2 | Used for wireless mesh (Part II) |

---


## IP Addressing Table

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
## VLAN Segmentation
-----

##  VLAN Assignment Table

| VLAN Name | VLAN1 | Subnet | Zone | Purpose |
|----------|------------|---------|--------|----------|
| Switch0 | 10.0.0.1  |
| Switch1 | 10.0.0.2  | 
| Switch2 | 10.0.0.3  | 
| Switch3 | 10.0.0.4  | 
| Switch4 | 10.0.0.5  | 
| Switch5 | 10.0.0.6  | 
| Switch6 | 10.0.0.7  |
| Switch7 | 10.0.0.11 |         
| Switch8 | 10.0.0.10 |
| Switch9 | 10.0.0.8  |
| Switch10| 10.0.0.9  |
| Switch11| 10.0.0.11 |
| Switch12| 10.0.0.12 |
| Switch13| 10.0.0.13 |
| Switch14| 10.0.0.14 |

---

##  Device Configuration Summary

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
## ParII: Wireless Mesh Topology

![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Screenshot%20(210).png?raw=true)

##  IP Addressing Table

| **Device** | **IP Address** | **Access Points** | **Local link Address(IPv6)** |
|-------------|----------------|-------------------|-----------------|
| PC0 | 198.162.1.2 | Access Point2 |FE80::202:4AFF:FE6D:9151|
| Laptop0 | 198.162.1.3 |  Access Point1 |FE80::202:4AFF:FE6D:9151  |
| Tablet PC0 | 198.162.1.4 |  Access Point11 |FE80::201:63FF:FEB6:97DC |
| Smartphone0 | 198.162.1.5 |  Access Point0|FE80::260:3EFF:FE13:24EE  |
| Laptop1 | 198.162.1.6 |  Access Point2 | FE80::201:C9FF:FE10:5807 |
| PC1 | 198.162.1.7 |  Access Point0 | FE80::2D0:D3FF:FE49:B5DB |
| PC2 | 198.162.1.8 |  Access Point2 | FE80::209:7CFF:FEB8:BEBC |
| Tablet PC1 | 198.162.1.9 |  Access Point12 | FE80::201:C9FF:FEAE:BE07 |
| PC3 | 198.162.1.10 |  Access Point0 |FE80::2E0:8FFF:FE65:51CC |


##  VLAN Assignment Table

| VLAN Name | VLAN1 | Subnet | Zone | Purpose |
|----------|------------|---------|--------|----------|
| Switch0 | 10.0.0.1  |
|Router0  | 192.168.1.1|

### VLAN Configuration



## Configuration Notes


###  Switch Configuration 
```bash
enable
conf t
hostnane s1
interface vlan1
ip address 10.0.0.1 255.0.0.0
 no shutdown
---

### Switch password Configuratuion

## Router Configuration
```bash
enable
conf t
interface g0/0
 no shutdown

interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0



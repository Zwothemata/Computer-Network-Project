 #  CMPG 325 - Computer Networks Long Project 
 

---

##  Project Overview

This project implements and simulates five basic network topologies — Bus, Star, Mesh, Ring, and Extended Star — using Cisco Packet Tracer.  
A Hybrid Topology integrates all five into one network with VLAN segmentation, IPv4/IPv6 addressing, one central server (HTTP/DNS/DHCP), and a router-on-a-stick setup for inter-VLAN communication.

The design ensures:
- Proper VLAN segmentation and IP planning  
- End-to-end data exchange between all zones  
- Basic network security (ACLs, port security)  
- Centralized management and DHCP configuration  
-------------------------------------------------

### Part I: Network Topologies



### 1. Bus Topology

In a bus topology, all devices in the network are connected to a single central cable called the bus or backbone. This cable acts as a shared communication medium where data is transmitted from one device to all others on the network. Each computer checks the data to see if it is the intended recipient. Bus topology is simple, cost-effective, and easy to install for small networks since it requires less cabling. However, it has major drawbacks. If the main cable fails, the entire network stops working. Additionally, as more devices are added, data collisions become more frequent, slowing down the network’s performance. Bus topology is therefore best suited for small, temporary, or low-traffic networks.

![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Bus%20topology.png?raw=true)



### 2.Mesh Topology

A mesh topology connects every device to every other device directly, creating multiple paths for data to travel. This makes the network highly reliable and fault-tolerant, as even if one connection fails, data can still reach its destination through an alternate path. Mesh topology provides excellent performance and redundancy, making it ideal for networks where communication reliability is critical, such as in military, industrial, or wireless mesh systems. However, it requires a large amount of cabling and configuration, which makes it expensive and complex to install. Despite the cost, mesh topology is valued for its stability, security, and fault tolerance.

![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Mesh%20Topology.png?raw=true)



### 3.Star Topology

The star topology is one of the most commonly used network designs today. In this setup, all devices are connected to a central hub, switch, or router. The central device acts as a controller that manages and forwards data between connected nodes. If one cable or device fails, it does not affect the rest of the network, which makes troubleshooting and maintenance easier. However, if the central hub fails, the entire network becomes inoperative. The star topology is reliable, easy to expand, and provides better performance since each device has a dedicated connection. It is widely used in modern LANs (Local Area Networks) due to its efficiency and simplicity.

![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Star%20Topology.png?raw=true)



### 4.Ring Topology

In a ring topology, each device is connected to exactly two other devices, forming a closed loop or ring. Data travels around the ring in one direction (or in both directions in a dual-ring setup). Each device receives data and passes it on until it reaches the intended destination. Because the data flows in an orderly manner, collisions are rare. However, the main disadvantage is that if any single device or cable fails, the entire network can stop functioning. It can also be difficult to add or remove devices without disrupting the network. Ring topology was popular in older systems like Token Ring networks but is now less common due to advances in star and mesh designs.

![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Ring%20Topology.png?raw=true)



### 5.Extended Star

The extended star topology is an expansion of the basic star design. It connects multiple star networks together using a central hub or switch that links all the smaller stars. Each branch of the network operates as its own star segment, and all are interconnected through the main backbone switch. This design is commonly used in large organizations, schools, and campuses where multiple departments or buildings need to be connected. The extended star topology is highly scalable, reliable, and easy to maintain. However, like the standard star, it depends heavily on the central hub or switch—if the main backbone device fails, the entire network can be affected. Still, it remains one of the most practical and widely implemented topologies for large-scale networks.

![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Extended%20Star.png?raw=true)










## Hybrid Topology 

![picture](https://github.com/Zwothemata/Computer-Network-Project/blob/main/Screenshot%20(208).png?raw=true)


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
-----------------------------------------------------------------

## VLAN Configuration
###  Objective
VLANs (Virtual Local Area Networks) are used to logically segment the hybrid network for improved security, performance, and traffic management.  
Each VLAN isolates a specific group of devices while still allowing inter-VLAN communication through the router.

---

##  VLAN Assignment Table

| VLAN Name | VLAN1 | 
|----------|------------|
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
-----------------------
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

| VLAN Name | VLAN1 | 
|----------|------------|
| Switch0 | 10.0.0.1  |
|Router0  | 192.168.1.1|



## Configuration Notes


###  Switch Configuration 
```bash
enable
conf t
hostnane s1
interface vlan1
ip address 10.0.0.1 255.0.0.0
 no shutdown
-----------------------------
```
### Switch password Configuratuion
```bash
enable
conf t
enable password
exit
---------------
```
## Router Configuration
```bash
enable
conf t
interface g0/0
 no shutdown

interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
--------------------------------------
```
### Access Point Configuration

```bash
Switch(config)# interface f0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# description Connected_to_PC1
-----------------------------------------------
```
### DHCP Configuration
```bash
IP Address: 192.168.100.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.100.1
DNS Server: 192.168.100.10

DHCP Pools:
- VLAN 10: 192.168.10.10–50
- VLAN 20: 192.168.20.10–50
- VLAN 30: 192.168.30.10–50
- VLAN 40: 192.168.40.10–50
----------------------------
```
  ### SSID Configuration
 ```bash
  SSID: 
Authentication: WPA2-PSK
Passphrase: 
Channel: Auto
------------------
```
##  HTTP Server Configuration

###  Objective
The goal of this configuration is to set up an **HTTP Web Server** within the hybrid network to provide web services to all connected VLANs and wireless clients.  
This ensures that users can access a centralized internal website using a standard web browser for communication, updates, or file sharing.

---

###  Devices Involved
- **Server0** – Configured as the HTTP server (and DHCP/DNS if required)
- **Router0** – Provides inter-VLAN routing for access across all subnets
- **Switch0** – Acts as a trunk and access switch connecting VLANs
- **End Devices** – PCs, Laptops, Tablets, and Smartphones accessing the web server

---

###  Server Configuration Steps (Using Cisco Packet Tracer)

1. **Add the HTTP Server**
   - Place a **Server** device on the workspace and connect it to the switch using a straight-through cable.

2. **Assign IP Address**
   - Click on the Server → Desktop → IP Configuration.
   - Assign a static IP based on your Server VLAN (for example, VLAN 30):

     ```
     IP Address: 192.168.30.2
     Subnet Mask: 255.255.255.0
     Default Gateway: 192.168.30.1
     DNS Server: 192.168.30.2
     ```

3. **Enable HTTP Service**
   - Go to **Services Tab → HTTP**.
   - Turn **HTTP ON** (and optionally **HTTPS ON**).
   - In the “HTML” section, you can edit the homepage:
     ```html
     <html>
     <body style="background-color:#f4f4f4; text-align:center;">
     <h1>Welcome to the CPMG 325 Network Project Web Server</h1>
     <p>This is the internal website hosted on Server0.</p>
     <p>Configured by: [Your Name]</p>
     </body>
     </html>
     ```

4. **Enable Optional Services**
   - Under **Services Tab → DHCP**, configure a DHCP pool (if required) for client IP assignment.
   - Under **Services Tab → DNS**, add an entry for your web server:
     ```
     Name: webserver
     Address: 192.168.30.2
     ```

---




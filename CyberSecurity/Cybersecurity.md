# Network
1.  It is defined as medium which is responsible of transmitting a data fro one node to another
2. Network Types-Internet intranet and pan

# Topology
Toplogy - how internet are connected
## Mesh Topology
Every node is connected to each other.
Disadvantage: Expensive
# Star topology
- Nodes connected to centralised device like switches hub or router;
	Disadvantage - If central node Damaged every thing is damaged
# Bus Toplogy 
- BackBone cable running and all nodes are connected to it
CSMA CSMA/CD(collision detection)
# Ring Topology
- All nodes are circulary connected 
# Hybrid Topology 
- Combination of two or more topology

# OSI reference model
 - OSi stands open system interconnection
 - it is beveloped by iso
 - it is a 7 layer architectur
 1. Application layer - Data Generation
 2. Presentation layer -  Perform transulationn compression and encryption
 3. Sesssion layer-Managing session
 4. Transport Layer-End to end data transmission -TCP/IP
 5. Network Layer-Ip adress - routing that data
 6. DataLink layer-error free transmisssion
 7. Physical layer-Medium of transfer
 - 
# Networking protocol
## TCP vs UDP

TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) are two communication protocols used to send data over the internet.

---

## Definition

**TCP:**  
TCP is a **connection-oriented protocol** that ensures reliable and ordered delivery of data.

**UDP:**  
UDP is a **connectionless protocol** that sends data without guaranteeing delivery or order.

---

## Key Differences

|Feature|TCP|UDP|
|---|---|---|
|Connection|Connection-oriented|Connectionless|
|Reliability|Reliable (guarantees delivery)|Unreliable (no guarantee)|
|Speed|Slower|Faster|
|Error checking|Yes (error detection and correction)|Basic error checking only|
|Data order|Maintains order|Does not maintain order|
|Acknowledgement|Required|Not required|
|Header size|Larger (20 bytes)|Smaller (8 bytes)|
|Usage|Important data transfer|Fast data transfer|

---

## How they work (concept)

![Image](https://static.afteracademy.com/images/what-is-a-tcp-3-way-handshake-process-three-way-handshaking-establishing-connection-6a724e77ba96e241.jpg)

![Image](https://www.cloud4y.ru/upload/medialibrary/b74/d97dkgfm5tu0ngqu8oirrev3ltj4rqql/TCP-i-UDP.jpeg)

![Image](https://www.cloudflare.com/img/learning/ddos/glossary/user-datagram-protocol-udp/tcp-vs-udp.svg)

![Image](https://bunnyacademy.b-cdn.net/F7AJp-What-Is-UDP-how-does-it-work-and-what-are-its-benefits.png)

- **TCP:** Establishes connection → Sends data → Confirms delivery
    
- **UDP:** Sends data directly → No confirmation
    

---

## Examples

**TCP is used in:**

- Web browsing (HTTP, HTTPS)
    
- Email (SMTP)
    
- File transfer (FTP)
    
- Banking applications
    

**UDP is used in:**

- Online gaming
    
- Video streaming
    
- Voice calls (VoIP)
    
- Live broadcasts
    

---

## Simple Real-Life Example

- **TCP:** Like sending a registered post (safe, confirmed delivery)
    
- **UDP:** Like sending a normal post (fast, no confirmation)
    

---



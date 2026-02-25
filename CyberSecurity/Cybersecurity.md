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


## CIA Triad in Cybersecurity

The **CIA Triad** is a model used in cybersecurity to protect information. CIA stands for:

- **C – Confidentiality**
    
- **I – Integrity**
    
- **A – Availability**
    

It ensures that data is **secure, accurate, and accessible when needed**.

---

## CIA Triad Diagram

![Image](https://images.openai.com/static-rsc-3/5pZ3oMi_-4TJMfexGobM5yAu2fbWFLWbITbxNO8h-6vlS758MxaynnqdnIMJdfPK1v50AKdgLmmeeYyDNNADntEIxkjP_PSrEUPLXCDdTvQ?purpose=fullsize&v=1)

![Image](https://images.openai.com/static-rsc-3/uCjQ88kc9ZW_orEVzCv0TNbXxSIslyy-ZiXLqxZ6mvIO-SK7HoMdkTZLcaxBq_q84oi1DbKtyFQ4Vo6rZSvQvQzOah2uJqVETgVOZuS0keo?purpose=fullsize&v=1)

![Image](https://images.openai.com/static-rsc-3/kK7G9JOVvI3ypadEYxYIVE9HUzCP68_dThpn2L5zfQpgsi6x8ls2X87SlTux6vsN5YPtC-WyGrMdYRG0WtuJcMLROlhWYrZEgorcBi1f2SI?purpose=fullsize&v=1)

---

## 1. Confidentiality

**Definition:**  
Confidentiality means protecting data from unauthorized access.

**Purpose:**  
Only authorized users can access the information.

**Examples:**

- Password protection
    
- Encryption
    
- OTP authentication
    

**Real-life example:**  
Only you can access your email using your password.

---

## 2. Integrity

**Definition:**  
Integrity ensures that data is accurate and not modified by unauthorized users.

**Purpose:**  
Prevents data tampering or alteration.

**Examples:**

- Hash functions (SHA-256)
    
- Digital signatures
    
- Checksums
    

**Real-life example:**  
Your bank balance should not change without your permission.

---

## 3. Availability

**Definition:**  
Availability ensures that data and systems are accessible when needed.

**Purpose:**  
Ensures continuous access to information.

**Examples:**

- Backup systems
    
- Servers
    
- Regular maintenance
    

**Real-life example:**  
Accessing your college portal anytime without downtime.

---

## Summary Table

|Component|Meaning|Example|
|---|---|---|
|Confidentiality|Protect data from unauthorized access|Password, Encryption|
|Integrity|Protect data from modification|Hashing, Digital signature|
|Availability|Ensure data is accessible|Backup, Servers|

---


## 4 A’s in Security

The **4 A’s in Security** are four important principles used to control and monitor access to systems and data.

They are:

1. **Authentication**
    
2. **Authorization**
    
3. **Accounting**
    
4. **Auditing**
    

---

## Diagram of 4A Security Model

![Image](https://miro.medium.com/0%2A9WZnM_foBQEql8nh.png)

![Image](https://discover.strongdm.com/hubfs/aaa-security.jpg)

![Image](https://www.researchgate.net/publication/349829923/figure/fig1/AS%3A998067373367299%401614969213900/Structure-of-the-suggested-network-security-model.ppm)

![Image](https://img.brainkart.com/imagebk9/pfebZo6.jpg)

---

## 1. Authentication (Who are you?)

**Definition:**  
Authentication is the process of verifying the identity of a user.

**Purpose:**  
Ensures the user is genuine.

**Examples:**

- Username and password
    
- OTP
    
- Fingerprint
    
- Face recognition
    

**Example in real life:**  
Logging into your Gmail using email and password.

---

## 2. Authorization (What can you access?)

**Definition:**  
Authorization determines what resources a user can access after authentication.

**Purpose:**  
Controls permissions.

**Examples:**

- Admin can edit data
    
- Student can only view data
    

**Example:**  
Only teachers can upload marks, students can only view marks.

---

## 3. Accounting (What did you do?)

**Definition:**  
Accounting keeps a record of user activities in the system.

**Purpose:**  
Tracks user actions.

**Examples:**

- Login time
    
- Logout time
    
- Files accessed
    

**Example:**  
System records when you logged into your college portal.

---

## 4. Auditing (Checking and reviewing)

**Definition:**  
Auditing is the process of reviewing and analyzing the records to detect security issues.

**Purpose:**  
Ensures security and detects misuse.

**Examples:**

- Checking login logs
    
- Detecting suspicious activity
    

**Example:**  
Admin checking logs to detect hacking attempts.

---

## Summary Table

|A|Meaning|Example|
|---|---|---|
|Authentication|Verify identity|Password, OTP|
|Authorization|Access permission|Admin vs Student access|
|Accounting|Record user activity|Login records|
|Auditing|Review activity logs|Security checks|


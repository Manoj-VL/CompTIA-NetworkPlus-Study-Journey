# CompTIA Network+ Study Journey

Documenting my hands-on learning as I prepare
for the CompTIA Network+ exam using Jason Dion's
Udemy course and Cisco Packet Tracer labs.

---

## About Me
- Background: Mechanical Engineering
- Goal: Cloud Security Engineer (Microsoft Azure)
- Target: Network+ → Security+ → AZ-500

---


## Progress Tracker
| Day | Topics Covered | Lab Completed | Status |
|-----|---------------|---------------|--------|
| 1 | Network Components, Resources, Geography | Lab 1 — Basic Network | ✅ |
| 2 | Network Topologies - Wired,Wireless,Data Center | Lab 2 — Extended Network | ✅ |
| 3 | OSI Model - Physical,Data link | Lab 3 - Switch Mac Address Table | ✅ |
| 4 | OSI Model - Network,Transport,Session |  Lab 4 -Routing+ HTTP | ✅ |
| 5 | OSI Model - Presentation,Application,Encapsulaton|Lab 5 Data Encapuslation in Simulation Mode| ✅ |
|6-8| Break due to health issues
| 9 | Full Revision| OSI Model and Encapusalation |

-------

## Day 1 
### Topics Learned
- Network Components - Client,Server,Hub,Switch etc{Basics will go into detail later}
- Network Resources - Client/Server , Peer to Peer Model
- Network Geography - PAN,LAN,CAN,MAN,WAN

## Lab1 - Basic Network
**Topology**
PC1 → Switch → Router → PC2

**IP Addresses:**
- PC1 = 192.168.1.10 / gateway 192.168.1.1
- PC2 = 192.168.2.10 / gateway 192.168.2.1
- Router GigaEthernet0/0 = 192.168.1.1
- Router GigaEthernet0/1 = 192.168.2.1

**Problem I Hit:**
Red dots between router and all connected devices

**How I Fixed It:**
Router ports are OFF by default in Packet Tracer.
Had to manually turn them on using CLI:
```
enable
configure terminal
interface GigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
interface GigabitEthernet0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

```

**What I Learned From This:**
- Switches turn on automatically
- Routers must be manually enabled
- Routers connects two sperate networks
- no shutdown is the command to activate an interface



### Screenshot
![Lab 1 Ping]



<img width="1920" height="1080" alt="Screenshot (17)" src="https://github.com/user-attachments/assets/47b583d3-ae7e-4b43-91ee-9eba66e3a509" />

-----------

## Day 2
### Topics Learned
- Wired Topologies — Bus, Ring, Star, Mesh
- Wireless Topologies — Infrastructure, Ad Hoc, Mesh
- Data Center Topologies — Three tier, Spine and Leaf


### Key Takeaways
- Star topology is most common in modern networks
  — all devices connect to central switch
- Mesh topology is most redundant but most expensive
  — every device connects to every other device
- Spine and Leaf is standard in modern data centers
  — used by companies like Microsoft Azure


## Lab 2 — Extended Network
**Topology:**
PC1 → Switch → Router → Switch2 → PC2
                                └→ PC3

**IP Addresses:**
- PC1 = 192.168.1.10 / gateway 192.168.1.1
- PC2 = 192.168.2.10 / gateway 192.168.2.1
- PC3 = 192.168.2.20 / gateway 192.168.2.1

**What I Learned:**
- One router can manage multiple subnets
- Devices on same subnet communicate directly
- Devices on different subnets need router to communicate

### Screenshot


<img width="1920" height="1080" alt="Screenshot (18)" src="https://github.com/user-attachments/assets/62f6a7f6-da08-4004-8e34-d359fd43f308" />

-------
## Day3
### Topics Learned
- Intoduction to OSI Model
- Layer 1 Physical Layer
- Layer 2 Data-Link Layer

## Lab 3 — Switch MAC Address Table

**Topology** 
Same as lab 2

**Goal:** Observe how switches learn MAC addresses at Layer 2

**Steps Taken:**
1. Pinged PC2 from PC1 to generate traffic
2. Opened Switch CLI
3. Ran "show mac-address-table" command
4. Matched PC1 MAC address to switch table entry

**Commands Used:**
enable
show mac-address-table

**What I Observed:**
- Switch automatically learned MAC addresses
  after first ping
- Each MAC address mapped to a specific port
- Type shows "DYNAMIC" meaning switch learned it
  automatically not manually configured

**What I Learned:**
- Switches build MAC table by watching traffic
- Before first ping — switch doesn't know where devices are
- After first ping — switch remembers which port each device is on
- This is called MAC address learning

### Screenshot


<img width="1920" height="1080" alt="Screenshot (20)" src="https://github.com/user-attachments/assets/7a66656d-6a33-4dc9-8778-6808d7750274" />

--------
## Day 4
### Topics Leaarned
- OSI Layer 3 - Network Layer
- Layer 4 - Transport Layer


## Lab 4 — Routing Table + HTTP Server

**OSI Layers:** Layer 3 (Network), Layer 4 (Transport), 
Layer 7 (Application)

### Topology
```
[PC1]──[SW1]──[Router]──[SW2]──[PC2]
                  │            └──[PC3]
                  │            └──[Server]
                [SW3]
                  │
                [PC4]
```

### IP Configuration
| Device | IP Address | Subnet Mask | Gateway |
|--------|-----------|-------------|---------|
| PC1 | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| PC2 | 192.168.2.10 | 255.255.255.0 | 192.168.2.1 |
| PC3 | 192.168.2.20 | 255.255.255.0 | 192.168.2.1 |
| Server | 192.168.2.50 | 255.255.255.0 | 192.168.2.1 |
| PC4 | 192.168.3.10 | 255.255.255.0 | 192.168.3.1 |
| Router G0/0 | 192.168.1.1 | 255.255.255.0 | — |
| Router G0/1 | 192.168.2.1 | 255.255.255.0 | — |
| Router G0/2 | 192.168.3.1 | 255.255.255.0 | — |


### Router CLI Commands
```
enable
configure terminal

interface GigabitEthernet0/2
ip address 192.168.3.1 255.255.255.0
no shutdown
exit

show ip route
```

### Routing Table Output
```
C  192.168.1.0/24 is directly connected, GigabitEthernet0/0
C  192.168.2.0/24 is directly connected, GigabitEthernet0/1
C  192.168.3.0/24 is directly connected, GigabitEthernet0/2
```

### HTTP Server Setup
```
Double click Server
→ Services tab
→ HTTP → ON
→ Tested from PC1 Desktop → Web Browser
→ Entered 192.168.2.50 in address bar
→ Server webpage loaded successfully
```

### Verification Pings
```
PC1 → ping 192.168.2.10  (PC2)    → Reply ✅
PC1 → ping 192.168.2.50  (Server) → Reply ✅
PC1 → ping 192.168.3.10  (PC4)    → Reply ✅
PC4 → ping 192.168.1.10  (PC1)    → Reply ✅
PC4 → ping 192.168.2.50  (Server) → Reply ✅
```

### What I Learned
- Router maintains a routing table of all 
  connected networks automatically
- Adding a new interface adds a new route
  to the routing table instantly
- HTTP runs at Layer 7 Application layer
- HTTP traffic uses TCP at Layer 4 Transport
  meaning delivery is confirmed before
  next packet is sent
- Server serves webpages using port 80 HTTP

### Problems I Hit
- No problems where hit outside of not knowing the cli commands had to look up on google

### Screenshots
**Full Topology — All Green Dots**

<img width="1920" height="1080" alt="Screenshot (22)" src="https://github.com/user-attachments/assets/a1c65b9b-3b46-4a47-b9ed-915e066ab1d2" />


**Routing Table Output**
<img width="1920" height="1080" alt="Screenshot (26)" src="https://github.com/user-attachments/assets/d4a6dbec-0996-4801-9844-893e596022ca" />

**HTTP Webpage Loading on PC1**

<img width="1920" height="1080" alt="Screenshot (27)" src="https://github.com/user-attachments/assets/09c4ef90-bdde-4bb1-9c0e-40927daea52d" />

**Successful Ping PC1 to PC4**

<img width="1920" height="1080" alt="Screenshot (28)" src="https://github.com/user-attachments/assets/4414bea6-7069-4613-9708-25cd5bb1cb8d" />

-----------
---
## Day 5
### Topics Learned
- OSI Layer 6 Session Layer
- Layer 7 Presentation Layer
- Layer 8 Application Layer
- Encapuslation

## Lab 5 — Data Encapsulation in Simulation Mode

**OSI Layers:** All 7 layers — full stack observation

### Topology
```
Same as Lab 4 — no new devices added
Simulation Mode used to observe existing network
```

### What Simulation Mode Shows
```
Packet Tracer Simulation Mode slows down
all network traffic so you can watch
each packet travel hop by hop
across the network in real time
```

### How to Enter Simulation Mode
```
Bottom right of Packet Tracer screen
Click "Simulation" button
OR press Shift + S
```

### Steps I Followed
```
1. Switched to Simulation Mode
2. Sent ping from PC1 to Server (192.168.2.50)
3. Pressed Play to watch packet travel
4. Clicked on travelling packet
5. Opened PDU Information window
6. Observed OSI layer details at each hop
7. Watched encapsulation leaving PC1
8. Watched decapsulation arriving at Server
```

### What I Observed

**Encapsulation — Sending Side (PC1)**
```
Layer 7 Application  → Data created (HTTP/ICMP)
Layer 4 Transport    → Segment — TCP header added
                       Source port + Destination port
Layer 3 Network      → Packet — IP header added
                       Source IP + Destination IP
Layer 2 Data Link    → Frame — MAC header added
                       Source MAC + Destination MAC
Layer 1 Physical     → Bits — converted to
                       electrical signals on cable
```

**Decapsulation — Receiving Side (Server)**
```
Layer 1 Physical     → Bits received from cable
Layer 2 Data Link    → Frame — MAC header removed
                       Switch checks MAC address
Layer 3 Network      → Packet — IP header removed
                       Router checks IP address
Layer 4 Transport    → Segment — TCP header removed
                       Port number checked
Layer 7 Application  → Data delivered to application
                       HTTP webpage served
```

### PDU Names at Each Layer
| OSI Layer | PDU Name | Header Added |
|-----------|---------|--------------|
| Layer 7-5 | Data | Application data |
| Layer 4 | Segment | TCP/UDP header |
| Layer 3 | Packet | IP header |
| Layer 2 | Frame | MAC header |
| Layer 1 | Bits | Electrical signal |

### Key Takeaways
- Every layer adds its own header going DOWN
- Every layer removes that header going UP
- Router only reads up to Layer 3 IP header
  it does not care about Layer 7 content
- Switch only reads up to Layer 2 MAC header
  it does not care about IP addresses
- This is why layered networking is powerful
  each device only does its specific job

### Screenshots

**PDU Information Window — Layer Details**
<img width="1920" height="1080" alt="PDU Window  - Layer Details" src="https://github.com/user-attachments/assets/9e822700-cc37-428d-b092-0648714beb4a" />

-----

## Day 10 Ports and Protocols
### Topic Learned
- Network Fundamentals - Ports, Portocols
- TCP,UDP
- ICMP

## No Lab

-------

## Day 11 Ports and Protocols
### Topic Learned
- Web ports & Protocols (HTTP,HTTPS)
- Email Ports & Protocols (SMTP,POP3,IMAP)
- File Transfer Ports and Protocols(FTP,SFTP,TFTP,SMB)
- Remote Access Ports and Protocols(SSH,TELNET,RDP)
- Network Service Ports and Protocols (DNS,DHCP,SQL Services,SNMP,Syslog)
- Other Network Service Ports and Protocols(NTP,SIP,LDAP)


# Lab 6 - Ports in Action
## Objective
To understand how port numbers are used in network communication by observing 
HTTP and FTP traffic using Cisco Packet Tracer simulation mode.

## Topology
<img width="1920" height="1080" alt="Topology Lab 4" src="https://github.com/user-attachments/assets/898e0ed3-a576-4602-b750-a59bed9bac2e" />


## IP Addressing Table
| Device      | IP Address   | Subnet Mask   | Default Gateway |
|-------------|--------------|---------------|-----------------|
| PC1         | 192.168.1.10 | 255.255.255.0 | 192.168.1.1     |
| PC2         | 192.168.2.10 | 255.255.255.0 | 192.168.2.1     |
| PC3         | 192.168.2.20 | 255.255.255.0 | 192.168.2.1     |
| Server0     | 192.168.2.50 | 255.255.255.0 | 192.168.2.1     |
| PC0         | 192.168.3.10 | 255.255.255.0 | 192.168.3.1     |
| Router G0/0 | 192.168.1.1  | 255.255.255.0 | —               |
| Router G0/1 | 192.168.2.1  | 255.255.255.0 | —               |
| Router G0/2 | 192.168.3.1  | 255.255.255.0 | —               |

## Steps Used

### Step 1 - Verify HTTP Service
1. Enabled HTTP on Server0 → Services tab → HTTP → ON
2. Pinged Server0 from PC1 to confirm connectivity.
3. Opened web browser on PC1 → entered `192.168.2.50` in URL bar → webpage loaded successfully.

### Step 2 - Verify FTP Service
1. Enabled FTP on Server0 → Services tab → FTP → ON
2. Added login credentials on the server:
   - Username: `admin`
   - Password: `admin123`
3. Connected to FTP server from PC1 command prompt:
  ftp 192.168.2.50
4. Entered credentials — server responded with:
230-Logged in
(passive mode on)
### Step 3 - Observe Ports in Simulation Mode
1. Switched Packet Tracer to simulation mode.
2. Filtered protocols to show only HTTP and FTP packets.
3. Triggered HTTP traffic by loading the webpage from PC1 browser.
4. Triggered FTP traffic by connecting via command prompt.
5. Clicked on each packet to open PDU details and verify port numbers.

## Verification
### HTTP Web page loaded
<img width="1920" height="1080" alt="Webpage being loaded from an web server" src="https://github.com/user-attachments/assets/8396bec1-54da-4c2b-8ac1-388a20300eb5" />

### HTTP - Port 80

<img width="1920" height="1080" alt="Proof of Port 80 being used in HTTP" src="https://github.com/user-attachments/assets/e72405c3-b36f-4cbb-abc9-d3903927d501" />

### FTP Login
<img width="1920" height="1080" alt="FTP connection betwenn PC1 and Sever" src="https://github.com/user-attachments/assets/62455bc9-d23d-46fc-90f0-24292a72e949" />


### FTP - Port 21
<img width="1920" height="1080" alt="Proof of Port 21 used in FTP" src="https://github.com/user-attachments/assets/ddca13a9-5dce-4f72-891d-a2da1388d525" />


## Key Observations
- Port 80 was visible in the HTTP packet PDU, confirming HTTP operates on port 80.
- Port 21 was visible in the FTP packet PDU, confirming FTP operates on port 21.
- Port numbers operate at Layer 4 - the Transport Layer.
- IP addresses are responsible for delivering data to the correct device (Layer 3).
- Port numbers are responsible for delivering data to the correct service on that device (Layer 4).
- Both HTTP and FTP transmit data in plaintext — credentials and page content are fully 
  visible inside the PDU. This is why HTTPS (port 443) uses TLS encryption and SFTP 
  replaces FTP for secure file transfer.





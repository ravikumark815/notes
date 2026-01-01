# Networking Notes

## 📋 Table of Contents

### 🔧 **Fundamentals**
- [Terminology](#terminology)
- [Networking Devices](#networking-devices)
- [Network Types by Area](#types-of-networks-based-on-area)
- [Network Topologies](#types-of-networks-based-on-topology)
- [Signaling](#signaling)
- [Cable Types & Standards](#cable-types)
- [Data Flow & Communication Types](#data-flow-types)
- [Network Domains](#network-domains)
- [OSI & TCP/IP Models](#layered-models)

### 📊 **Layer 1 - Physical Layer**
- [Physical Media](#cable-types)
- [Ethernet Standards](#ethernet-standards)
- [Cable Categories](#cable-categories)
- [Signaling Methods](#signaling)

### 🔗 **Layer 2 - Data Link Layer**
- [Ethernet Protocol](#ethernet-protocol)
- [MAC Addressing](#mac-address)
- [CSMA/CD](#carrier-sense-multiple-accesscollision-detection-csmacd)
- [Spanning Tree Protocol (STP)](#spanning-tree-protocol-stp)
- [Link Aggregation (LACP)](#link-aggregation-lacp)
- [L2 Discovery Protocols](#l2-discovery-protocols)
- [VLAN & Trunking](#vlan--trunking)
- [802.1X Authentication](#8021x-authentication)

### 🌐 **Layer 3 - Network Layer**
- [IPv4 Protocol](#ipv4-protocol)
- [IPv6 Protocol](#ipv6-protocol)
- [ICMP Protocol](#icmp-protocol)
- [ARP Protocol](#arp-protocol)
- [Routing Protocols](#routing-protocols)
  - [RIP (Routing Information Protocol)](#rip-routing-information-protocol)
  - [EIGRP (Enhanced Interior Gateway Routing Protocol)](#eigrp-enhanced-interior-gateway-routing-protocol)
  - [OSPF (Open Shortest Path First)](#ospf-open-shortest-path-first)
  - [BGP (Border Gateway Protocol)](#bgp-border-gateway-protocol)
  - [IS-IS (Intermediate System to Intermediate System)](#is-is-intermediate-system-to-intermediate-system)
- [High Availability Protocols](#high-availability-protocols)
  - [HSRP (Hot Standby Router Protocol)](#hsrp-hot-standby-router-protocol)
  - [VRRP (Virtual Router Redundancy Protocol)](#vrrp-virtual-router-redundancy-protocol)
  - [GLBP (Gateway Load Balancing Protocol)](#glbp-gateway-load-balancing-protocol)
- [Network Address Translation (NAT)](#network-address-translation-nat)
- [Policy Based Routing (PBR)](#policy-based-routing-pbr)
- [Quality of Service (QoS)](#quality-of-service-qos)
- [SD-WAN](#sd-wan-software-defined-wide-area-network)

### 🚚 **Layer 4 - Transport Layer**
- [TCP Protocol](#tcp-protocol)
- [UDP Protocol](#udp-protocol)

### 🔐 **Layer 5-6 - Session & Presentation**
- [SSL/TLS](#ssltls-protocols)
- [IPsec](#internet-protocol-security-ipsec)

### 📱 **Layer 7 - Application Layer**
- [HTTP/HTTPS](#http-hypertext-transfer-protocol)
- [DNS](#domain-name-server-dns)
- [DHCP](#dynamic-host-configuration-protocol-dhcp)
- [SMTP/POP3/IMAP](#email-protocols)
- [FTP/SFTP](#file-transfer-protocols)
- [SNMP](#simple-network-management-protocol-snmp)
- [NetFlow/sFlow](#network-flow-monitoring-netflow)
- [Telnet/SSH](#remote-access-protocols)
- [LDAP](#lightweight-directory-access-protocol-ldap)
- [RADIUS](#radius-remote-authentication-dial-in-user-service)
- [Single Sign-On (SSO)](#single-sign-on-sso)
- [OCSP](#online-certificate-status-protocol-ocsp)
- [VoIP Protocols](#voip-protocols)
  - [SIP (Session Initiation Protocol)](#sip-session-initiation-protocol)
  - [H.323](#h323-protocol)
  - [RTP (Real-time Transport Protocol)](#rtp-real-time-transport-protocol)
- [Remote Desktop Protocols](#remote-desktop-protocols)
  - [RDP (Remote Desktop Protocol)](#rdp-remote-desktop-protocol)
  - [VNC](#vnc-virtual-network-computing)

### 🚀 **Life of a Packet**
- [What Happens When...](#life-of-a-packet-what-happens-when)

### 📡 **Wireless Technologies**
- [WLAN Protocols](#wlan-protocols)
- [Wi-Fi Standards](#wi-fi-standards)
- [Wireless Security](#wireless-security)

### 🛡️ **Network Security**
- [Firewalls & Access Control](#firewalls--access-control)
- [Email Security](#email-security)
- [Network Monitoring & Analysis](#network-monitoring--analysis)
- [Security Protocols](#security-protocols)

### 🔧 **Network Services & Management**
- [Dynamic DNS](#dynamic-dns)
- [Network Time Protocol (NTP)](#network-time-protocol-ntp)
- [Syslog](#syslog-protocol)
- [Network Troubleshooting](#network-troubleshooting)

---

## 🔧 Fundamentals

### Terminology
- **Network:** A computer network is a digital telecommunications network for sharing resources between nodes, which are computing devices that use a common telecommunications technology
- **Client:** A client is a piece of computer hardware or software that accesses a service available by a server
- **Server:** A server is a computer program or device that provides functionality for other programs or devices called clients
- **Protocol:** A set of rules used in communication between clients
- **Node:** A computing device. 
- **Bus network:** All the devices are connected on one single long cable.

### Networking Devices
- **Repeater:** A repeater is an electronic device that receives a signal and retransmits it. 
- **Hub:** A hub is essentially a multi-port repeater. Wireless Access Point is essentially a hub in the air.
- **Active Hub:** These are the hubs that have their own power supply and can clean, boost, and relay the signal along with the network. It serves both as a repeater as well as a wiring center.
- **Passive Hub:** These are the hubs that collect wiring from nodes and power supply from the active hub. They are generally used to relay signals with cleaning or boosting them.
- **Intelligent Hub:** It works like active hubs and includes remote management capabilities. They also provide flexible data rates to network devices. It also enables an administrator to monitor the traffic passing through the hub and to configure each port in the hub.
- **Bridge:** A bridge is a repeater with add on the functionality of filtering content by reading mac addresses of source and destination. It was mostly used to interconnect two LANs.
- **Transparent Bridge:** These are the bridges in which the stations are completely unaware of the bridge's existence.
- **Source Routing Bridge:** In these bridges, routing operation is performed by the source station and the frame specifies the route to follow. 
- **Switch:** A switch reads each frame and has the intelligence to transmit data to the port it is destined for based on MAC addresses. 
- **Router:** A router is a device like a switch that routes data packets based on their IP addresses. The router is mainly a Network Layer device. 
- **Wireless Access Point:** A wireless access point is a networking device that allows wireless-capable devices to connect to a wired network.
- **Wireless LAN Controller:** A WLAN controller is used to manage large scale deployments of light weight and normal wireless access points.
- **Firewall:** A firewall is a network security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. 
- **IDS:** It’s a software system that warns if there is an intrusion. They just get copies of packets that are analyzed.
- **IPS:** It’s a software system can alert you if there may be a problem and block the same. They stay inline of the network and detect and block intrusions. 
- **Email Security Appliance:** The Email Security Appliance is an email security gateway product. It is designed to detect and block a wide variety of email-borne threats, such as malware, spam, and phishing attempts.
- **Load Balancer:** A load balancer is a device that acts as a reverse proxy and distributes network or application traffic across several servers.

### Types of Networks based on Area
- **WAN:** A Wide Area Network is a telecommunications network that extends over a large geographical area for the primary purpose of computer networking.
- **LAN:** A Local Area Network is a computer network that interconnects computers within a limited area such as a residence, school and so on
- **MAN:** Metropolitan Area Network
- Wireless Local Area Network (WLAN)
- Campus Area Network (CAN)
- Storage Area Network (SAN)
- Passive Optical Local Area Network (POLAN)
- Enterprise Private Network (EPN)
- Virtual Private Network (VPN)
- Personal Area Network (PAN) 

### Types of Networks based on Topology
```
1. BUS TOPOLOGY:
   ┌────┐    ┌────┐    ┌────┐    ┌────┐    ┌────┐
   │ PC │    │ PC │    │ PC │    │ PC │    │ PC │
   │ A  │    │ B  │    │ C  │    │ D  │    │ E  │
   └─┬──┘    └─┬──┘    └─┬──┘    └─┬──┘    └─┬──┘
     │         │         │         │         │
   ──┴─────────┴─────────┴─────────┴─────────┴──
              Single Backbone Cable
   Pros: Simple, cost-effective
   Cons: Single point of failure, collision domain

2. STAR TOPOLOGY:
                    ┌────────┐
                    │ Switch │
                    │   or   │
                    │  Hub   │
                    └───┬────┘
           ┌────────────┼────────────┐
           │            │            │
       ┌───▼──┐    ┌───▼──┐    ┌───▼──┐
       │ PC A │    │ PC B │    │ PC C │
       └──────┘    └──────┘    └──────┘
   Pros: Easy to manage, fault isolation
   Cons: Central device failure affects all

3. RING TOPOLOGY:
       ┌────┐         ┌────┐
       │ PC │◄────────┤ PC │
       │ A  │         │ B  │
       └─┬──┘         └──▲─┘
         │               │
         ▼               │
       ┌────┐         ┌────┐
       │ PC │────────►│ PC │
       │ D  │         │ C  │
       └────┘         └────┘
   Pros: Equal access, no collisions
   Cons: Single break affects entire network

4. MESH TOPOLOGY:
       ┌────┐ ◄──────► ┌────┐
       │ PC │ ◄──┐  ┌─►│ PC │
       │ A  │    │  │  │ B  │
       └─┬──┘    │  │  └─▲──┘
         │       │  │    │
         ▼       │  │    │
       ┌────┐    │  │  ┌────┐
       │ PC │ ◄──┘  └─►│ PC │
       │ D  │ ◄──────► │ C  │
       └────┘          └────┘
   Pros: High redundancy, fault tolerance
   Cons: Expensive, complex management

5. HYBRID TOPOLOGY:
                ┌─────────┐
                │ Router  │
                └────┬────┘
                     │
        ┌────────────┼────────────┐
        │                         │
   ┌────▼────┐               ┌────▼────┐
   │ Switch  │               │ Switch  │
   │ (Star)  │               │ (Star)  │
   └────┬────┘               └────┬────┘
        │                         │
   ┌────┼────┐               ┌────┼────┐
   │    │    │               │    │    │
 ┌─▼─┐┌─▼─┐┌─▼─┐           ┌─▼─┐┌─▼─┐┌─▼─┐
 │PC1││PC2││PC3│           │PC4││PC5││PC6│
 └───┘└───┘└───┘           └───┘└───┘└───┘
   Pros: Combines benefits of multiple topologies
   Cons: Complex design and troubleshooting
```

### Signaling
- **Baseband Signaling:** Can only transmit a single signal at any given time. 
- **Broadband Signaling:** Can transmit multiple signals at any given time. 
 
### Cable Types
- **Coaxial Cabling:** Coaxial cable has an inner conductor that runs down the middle of the cable. This type of cabling comes in two types, thinnet and thicknet. Max Transmission Speed of 10 Mbps
- **Twisted-pair Cabling:** Has four pair of wires.  It comes in two versions, UTP (Unshielded Twisted-Pair) and STP (Shielded Twisted-Pair). Uses 8P8C/RJ45 Connector
- **Fiber-optic Cabling:** Uses optical fibers to transmit data in the form of light signals. There are two types of fiber-optic cables - Single-mode fiber (SMF) and Multi-mode fiber (MMF). Uses ST/SC Connectors

![](https://github.com/ravikumark815/notes/blob/main/images/cables.png)

### Ethernet Standards
- **10Base-T (IEEE 802.3):** 10 Mbps with category 3 unshielded twisted pair (UTP) wiring, up to 100 meters long.
- **100Base-TX (IEEE 802.3u):** known as Fast Ethernet, uses category 5, 5E, or 6 UTP wiring, up to 100 meters long.
- **100Base-FX (IEEE 802.3u):** a version of Fast Ethernet that uses multi-mode optical fiber. Up to 412 meters long.
- **1000Base-CX (IEEE 802.3z):** uses copper twisted-pair cabling. Up to 25 meters long.
- **1000Base-T (IEEE 802.3ab):** Gigabit Ethernet that uses Category 5 UTP wiring. Up to 100 meters long.
- **1000Base-SX (IEEE 802.3z):** 1 Gigabit Ethernet running over multimode fiber-optic cable.
- **1000Base-LX (IEEE 802.3z):** 1 Gigabit Ethernet running over single-mode fiber.
- **10GBase-T (802.3.an):** 10 Gbps connections over category 5e, 6, and 7 UTP cables.

### Cable Categories
Higher Categories have more twists, are less susceptible to EMIs, more stringent specifications for cross talk and system noise.
- **CAT1:** was previously used for telephones and modems.
- **CAT2:** was used for telephone and data networks up to 4Mbps.
- **CAT3:** Now generally used for telephones. Previously for data networks up to 10Mbps
- **CAT4:** Defined up to 50 MHz with speeds up to 16 Mbps.
- **CAT5:** Defined up to 100 MHz, speeds of 10/100Mbps supported longer cable runs of 1Gbps an issue. 
- **CAT5e:** Defined up to 100 MHz, speeds up to 1Gbps. 
- **CAT6:** Defined up to 250 MHZ, supports 10Gbps up to 55 m. 
- **CAT6a:** Defined up to 500 MHz, supports 10Gbps up to 100m. Good reduction in cross talks. 
- **CAT7:** Defined up to 600 MHz, supports 10Gbps up to 100m with better connectors to reduce cross talks.
- **CAT7a:** Defined up to 1000MHz, supports 100Gbps.
- **CAT8:** Supports 40Gbps. Released in March 2013, next generation.
- **CAT8.1:** Backward compatible and interoperable with CAT 6a.
- **CAT8.2:** Interoperable with CAT7

*CAT1-CAT5 are now obsolete*

### Other Cables
Direct Attachment Cable (DAC) Copper Twinax:
- Comes in various lengths with SFPs at each end.
- SFP: Hot pluggable transceiver. 
- SFPs supports various connectors and data rates up to 10Gbps. 
- Roll over cable: Special cable used in Cisco environment to connect a com port to console port.

### Ethernet Cable Forms
- **Straight-through Cable:** On a straight through cable, the wired pins match. Straight through cable use one wiring standard: both ends use T568A wiring standard or both ends use T568B wiring standard. 
- **Crossover Cable:** Crossover cable uses two different wiring standards: one end uses the T568A wiring standard, and the other end uses the T568B wiring standard. Pin1->Pin3 and Pin2->Pin6

![](https://github.com/ravikumark815/notes/blob/main/images/straight-through.png)
![](https://github.com/ravikumark815/notes/blob/main/images/crossover.png)

> **Medium Dependent Interface (MDI):** It is a type of ethernet port connection that uses twisted-pair cabling to link two network devices. MDIX (MDI Crossover) is a version of MDI that enables connection between like devices.

### Data flow Types
```
1. SIMPLEX (One-way communication):
   ┌─────────┐                    ┌─────────┐
   │ Sender  │ ──────────────────►│Receiver │
   │ (Radio) │    Data Flow       │ (Radio) │
   └─────────┘                    └─────────┘
   Examples: Radio broadcast, TV transmission

2. HALF-DUPLEX (Two-way, but not simultaneous):
   ┌─────────┐                    ┌─────────┐
   │Station A│ ──────────────────►│Station B│
   │         │    Data Flow       │         │
   └─────────┘                    └─────────┘
   
   ┌─────────┐                    ┌─────────┐
   │Station A│ ◄──────────────────│Station B│
   │         │    Data Flow       │         │
   └─────────┘                    └─────────┘
   Examples: Walkie-talkie, Hub-based Ethernet

3. FULL-DUPLEX (Two-way simultaneous):
   ┌─────────┐                    ┌─────────┐
   │Station A│ ──────────────────►│Station B│
   │         │ ◄──────────────────│         │
   └─────────┘  Simultaneous      └─────────┘
                Data Flow
   Examples: Telephone, Switch-based Ethernet
```

### Communication Types
- **Unicast:** Communication from one point to another point
- **Broadcast:** Communication from one point to all other points
- **Multicast:** Communication from one/more points to a set of other points
- **Anycast:** Communication from one to nearest. It is a network addressing and routing methodology in which a single destination IP address is shared by nodes in multiple locations.

```
1. UNICAST (One-to-One):
   ┌─────────┐                    ┌─────────┐
   │ Source  │ ──────────────────►│ Dest    │
   │192.168.1│    Single Path     │192.168.2│
   └─────────┘                    └─────────┘
   Example: Web browsing, email, file transfer

2. BROADCAST (One-to-All):
   ┌─────────┐
   │ Source  │ ────────┐
   │192.168.1│         │
   └─────────┘         │
                       ▼
   ┌─────────┐    ┌─────────┐    ┌─────────┐
   │ Dest 1  │    │ Dest 2  │    │ Dest 3  │
   │192.168.2│    │192.168.3│    │192.168.4│
   └─────────┘    └─────────┘    └─────────┘
   Example: ARP requests, DHCP discover

3. MULTICAST (One-to-Many):
   ┌─────────┐
   │ Source  │ ────────┐
   │192.168.1│         │
   └─────────┘         │
                       ▼
   ┌─────────┐    ┌─────────┐    ┌─────────-┐
   │ Member 1│    │ Member 2│    │Non-Member│
   │224.1.1.1│    │224.1.1.1│    │  (No Rx) │
   └─────────┘    └─────────┘    └─────────-┘
   Example: Video streaming, IPTV, routing protocols

4. ANYCAST (One-to-Nearest):
   ┌─────────┐
   │ Client  │ ────────┐
   │192.168.1│         │
   └─────────┘         │
                       ▼
   ┌─────────┐    ┌─────────┐    ┌────────-─┐
   │Server 1 │    │Server 2 │    │Server 3  │
   │8.8.8.8  │    │8.8.8.8  │    │8.8.8.8   │
   │(Closest)│    │ (Far)   │    │(Farthest)│
   └─────────┘    └─────────┘    └─────────-┘
   Example: DNS root servers, CDN services
```

### Network Domains
- **Broadcast Domain:** A broadcast domain is a logical division of a computer network, in which all nodes can reach each other by broadcast at the data link layer.
- **Collision Domain:** A collision domain is a network segment connected by a shared medium where simultaneous data transmissions collide with one another. 

![](https://github.com/ravikumark815/notes/blob/main/images/network-domains.png)

> **54321 Rule:**
- 5 - the number of network segments
- 4 - the number of repeaters needed to join the segments into one collision domain
- 3 - the number of network segments that have active (transmitting) devices attached
- 2 - the number of segments that do not have active devices attached
- 1 - the number of collision domains

### Layered Models
Layers and Protocol Data Units (PDUs):

**OSI Model:**
|#|Layer|PDU|
|---|---|---|
|1|Physical Layer|Bits|
|2|Datalink Layer|Frame|
|3|Network Layer|Packet|
|4|Transport Layer|Segment|
|5|Session Layer|Data|
|6|Presentation Layer|Data|
|7|Application Layer|Data|

**TCP/IP Model (4):**
|   |   |   |
|---|---|---|
|1|Physical Layer (Frame): |Physical Addresses (MAC)|
|2|Network Layer (Packet):|IP Addresses (IP)|
|3|Transport Layer (Segment)|Port Addresses (Ports)|
|4|Application Layer (Data)|Specific Addresses (Data)|

**TCP/IP Model (5 – In use by CCNA):**
|#|Layer|PDU|Address|
|---|---|---|---|
|1|Physical Layer|Bits|
|2|Datalink Layer|Frame|Physical Address (MAC)|
|3|Network Layer|Packet|IP Addresses (IP)|
|4|Transport Layer|Segment|Port Addresses (Ports)|
|5|Application Layer|Data|Specific Addresses (Data)|

**Cisco 3-Layer Model:**
1.	**Core Layer:** This layer is considered the backbone of the network and includes the high-end switches and high-speed cables such as Fiber cables. This layer of the network does not route traffic at the LAN. In addition, no packet manipulation is done by devices in this layer. Rather, this layer is concerned with speed and ensures reliable delivery of packets.
2.	**Distribution Layer:** This layer includes LAN-based routers and layer 3 switches. This layer ensures that packets are properly routed between subnets and VLANs in your enterprise. This layer is also called the Workgroup layer.
3.	**Access Layer:** This layer includes hubs and switches. This layer is also called the desktop layer because it focuses on connecting client nodes, such as workstations to the network. This layer ensures that packets are delivered to end user computers.

![](https://github.com/ravikumark815/notes/blob/main/images/cisco-3-layer.png)

### Math Review:
**Binary:**
- IPv4 addresses use Binary.
- 2 possible values per bit (Base 2): 0,1
- Total number of outcomes for a given number: 2n (For example, for 8 bits: 28 = 256) 

- 128+64+32+16+8+4+2+1 = 255

- To represent 255 in Binary

|Base|2<sup>7</sup>|2<sup>6</sup>|2<sup>5</sup>|2<sup>4</sup>|2<sup>3</sup>|2<sup>2</sup>|2<sup>1</sup>|2<sup>0</sup>|
|---|---|---|---|---|---|---|---|---|
|Binary Bit|1|1|1|1|1|1|1|1|
|Decimal|128|64|32|16|8|4|2|1|

> IPv4 has 32 bits – 4 octets. 2<sup>32</sup> = 429,49,67,296 IP addresses 

**Hexadecimal:**
- MAC addresses use Hexadecimal.
- 16 possible values per bit (Base 16): 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F
- Converting from Decimal to Hexadecimal (Ex: 224->E0):
<br>&nbsp; 224 in Binary: 1110 0000 (Divide into 4 bits each)
<br>&nbsp; 1110<sup>2</sup> = 14<sup>10</sup> = E<sup>16</sup>
<br>&nbsp; 0000<sup>2</sup> = 0<sup>10</sup> = 0<sup>16</sup>
<br>&nbsp; Result: E0

### IPv4 Addressing:
- Internet Protocol v4 is a connectionless network layer protocol. Each packet is treated independently in this protocol which allows the packets to take different paths as needed. 
- An IPv4 address is a layer 3 logical address assigned by an administrator. It is used to identify specific devices on a network and must be unique in internet.
- Private IP addresses are NATted to public address when traffic is sent onto internet.
- Format of IP address:
<br>&nbsp; • 32 bits 4 octets of 8 bits (1byte) each
<br>&nbsp; • Network Address Portion (Network ID):	Identifies a specific network. Routers look at destination of IP address and match to network address.
<br>&nbsp; • Host portion (Host ID): Identifies a specific endpoint on a network.
- Address Classes to accommodate different sizes of network and aid in classifying networks:

|Class|Range|
|---|---|
|Class A – Unicast|0.0.0.0 to 127.255.255.255
|Class B – Unicast|128.0.0.0 to 191.255.255.255
|Class C – Unicast|192.0.0.0 to 223.255.255.255
|Class D – Multicast|224.0.0.0 to 240.255.255.255
|Class E – Reserved for future|241.0.0.0 to 255.255.255.255	

- **Exceptions, Reservations and Special addresses:**
<br>&nbsp; • `0.0.0.0/8` - Default network
<br>&nbsp; • `127.0.0.0/8` – Local Loopback address. 
<br>&nbsp; • `224.0.0.X` – Link local multicasts, generally used by routing tables.
<br>&nbsp; • `224.0.0.5-224.0.0.6` - OSPF
<br>&nbsp; • Directed Broadcast address: Fill 1s in the entire host portion of the address.
<br>&nbsp; • Local Broadcast address: Fill 1s in all 32 bits. Generally used for DHCP address
<br>&nbsp; • `10.0.0.0/8` – Private IP address range (not routable on internet)
<br>&nbsp; • `172.16.0.0/12` – Private IP address range (not routable on internet)
<br>&nbsp; • `192.168.0.0/16` – Private IP address range (not routable on internet)
<br>&nbsp; • `169.254.0.0/16` – Non-routable Link Local Addresses (Automatic Private IP Addressing)

- **Subnet Masks:**
<br>&nbsp; • Used to determine network and host portion of a given IP address through AND operation.
<br>&nbsp; • Is the device remote (route through default gateway) or local (ARP)?
<br>&nbsp; • `Class A: 255.0.0.0`
<br>&nbsp; • `Class B: 255.255.0.0`
<br>&nbsp; • `Class C: 255.255.255.0`
<br>&nbsp; • Discontinuous subnet masks not supported:
`11110000.11111111.00000110.11000000 (240.244.3.191)`
<br>&nbsp; • Only contiguous subnet masks are supported.
`11111111.11110000.00000000.00000000 (255.240.0.0)`

- **Classless Inter Domain Routing (CIDR):**
<br>&nbsp; • Replaces classful IP addressing with variable length subnet mask (VLSM)
<br>&nbsp; • CIDR notation /X where X denotes number of 1’s present in binary form of a subnet mask.
<br>&nbsp; • Reduces wastage of big number of addresses.
<br>&nbsp; • Ex: `/11 = 255.224.0.0`

- **Subnetting:**
<br>&nbsp; • Work the following for a given IP address: Network address, First IP address, Last IP address, Broadcast address. 
<br>&nbsp; • Binary method to work an IP address:
<br>&nbsp; &nbsp; • Subnet address: Fill the host portion with binary 0s.
<br>&nbsp; &nbsp; • Broadcast address: Fill the host portion with binary 1s.
<br>&nbsp; &nbsp; • First host: Fill the host portion with binary 0s and set the last bit to 1.
<br>&nbsp; &nbsp; • Last host: Fill the host portion with binary 1s and set the last bit to 0.
<br>&nbsp; &nbsp; • Ex: 172.16.35.123/20:
<br>&nbsp; &nbsp; `Subnet: 172.16.0010 0000.0000 0000 = 172.16.32.0`
<br>&nbsp; &nbsp; `1st Host: 172.16.0010 0000.0000 0001 = 172.16.32.1`
<br>&nbsp; &nbsp; `Last Host: 172.16.0010 1111.1111 1110 = 172.16.47.254`
<br>&nbsp; &nbsp; `Broadcast: 172.16.0010 1111.1111 1111 = 172.16.47.255`
<br>&nbsp; • Number of hosts in a network: **2<sup>h</sup> – 2** (h = number of bits in host portion)
<br>&nbsp; • Number of networks: **2<sup>n</sup>** (n = number of bits in network portion)
<br>&nbsp; • Number of subnets: **2<sup>n</sup>** (n = number of bits in variating network octet)

### MAC Address:
-  6 bytes or 48 bits in length: 24 bits OUI (Organizational unique identifier) and 24 bits of Station Address
-  MAC addresses are unique to avoid collisions and conflicts.
-  Broadcast MAC address: FF:FF:FF:FF:FF:FF
-  OUI bits can be used to represent nature of communication as shown below:
![](https://github.com/ravikumark815/notes/blob/main/images/mac.png)

### Carrier Sense Multiple Access/Collision Detection (CSMA/CD):
-  Used to find if any other device sending traffic in a bus topology to avoid collisions in a CD. 
-  Before sending traffic, a device broadcasts if another device is communicating. If there is no response, it goes ahead and sends traffic. 
-  If a collision takes place, a backoff/jam signal is sent. 

### Data Flow in Hub, Bridge, Switch, Router:

![](https://github.com/ravikumark815/notes/blob/main/images/data-flow-topo.png)

> Hub 
-  Physical Layer Device
-  Multiport Repeater
-  Amplifies/Repeats any packet it gets in any port to all other ports.
-  When PC A sends a packet to PC D in the above topology, the device, being hub in this case would broadcast the packet to PCs B, C and D 
-  Star topology inside
-  Cable break for any spoke doesn’t affect it. 
-  Easy to extend further distances easily by just adding another hub, thereby overcoming the distance limits of various cables. 
-  A collision in any point would send a jamming signal to everyone. 
-  Very low bandwidth due to shared logical bus topology in practical applications.
-  All ports are in single collision domain and single broadcast domain.

> Bridge:
-  Datalink Layer Device
-  Maintains a MAC address table.
-  CAM Table: Content Addressable Memory – another term used for MAC address table in switching (not bridging)
-  Star Topology
-  Processing mostly done in software and hence is slow in nature. 
-  When PC A sends a packet to PC D in the above topology, the device, being bridge in this case, creates an entry for PC A in its MAC table and since it doesn’t know the MAC address of PC D, it broadcasts the received frame to all ports except PC A to create an entry for PC D. Since it is not destined to PC B and PC C, they are supposed to drop the packet. When D replies to this frame, the bridge doesn’t broadcast anything, it forwards the packet only to PC A. 
-  Each port of the bridge is in a different collision domain. 
-  All ports in a single Broadcast Domain. 

> Switch:
-  Datalink Layer Device. 
-  Processing is don’t Hardware, namely ASICs and hence is faster. 
-  No degradation performance between two devices. Wire speed in switching frames. 
-  Support many ports compared bridges. 
-  Maintains a MAC Address Table. 
-  Star Topology
-  When PC A sends a packet to PC C in the above topology and the frame arrives at the device, being switch in this case, the switch broadcasts the received frame to all ports except PC A to create an entry for PC C. When C replies to this frame, the switch forwards subsequent frames between A and C only between them.
-  Each port of the switch is in a different collision domain. 
-  All ports in a single Broadcast Domain. 
-  Broadcast addresses are not written into the MAC table. 
-  Layer 3 Switches available now. 

> Routers:
-  Network Layer Device. 
-  They make routing decisions based on IP address.
-  Router may have:
<br>&nbsp; • Serial interfaces – uses PPP and HDLC for encapsulation. 
<br>&nbsp; • Ethernet interfaces – uses MAC address and Ethernet II for encapsulation.
-  Routers populate routing table with IP addresses.
-  They use subnet masks to determine which interface the packet to be forwarded to. 
-  PCs look for MAC address for destination IP in their ARP cache, if not available, they send the packet to their default gateway, Router. 
-  Router then performs an AND operation on the IP address with subnet mask, and if the network ID is known in routing table, it forwards to the respective interface. 
-  MAC addresses change from hop to hop and not IP addresses in a packet flow unless a NAT is used.

<br>&nbsp;
## Layer 2
### Ethernet Protocol

*1. Header Structure:*

```
Ethernet II Frame Format (64-1518 bytes):
┌─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┐
│  Preamble   │     SFD     │ Destination │   Source    │  EtherType  │             │             │     FCS     │
│   (7 bytes) │  (1 byte)   │ MAC Address │ MAC Address │  (2 bytes)  │   Payload   │   Padding   │  (4 bytes)  │
│             │             │  (6 bytes)  │  (6 bytes)  │             │ (46-1500 B) │ (if needed) │             │
└─────────────┴─────────────┴─────────────┴─────────────┴─────────────┴─────────────┴─────────────┴─────────────┘
│◄─────────────────────── 64 to 1518 bytes total ──────────────────────►│

802.1Q VLAN Tagged Frame:
┌─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┐
│  Preamble   │     SFD     │ Destination │   Source    │  802.1Q Tag │  EtherType  │             │             │     FCS     │
│   (7 bytes) │  (1 byte)   │ MAC Address │ MAC Address │  (4 bytes)  │  (2 bytes)  │   Payload   │   Padding   │  (4 bytes)  │
│             │             │  (6 bytes)  │  (6 bytes)  │             │             │ (42-1500 B) │ (if needed) │             │
└─────────────┴─────────────┴─────────────┴─────────────┴─────────────┴─────────────┴─────────────┴─────────────┴─────────────┘

802.1Q Tag Breakdown (4 bytes):
┌─────────────┬─────────────┬─────────────┬─────────────┐
│    TPID     │    PCP      │    DEI      │   VLAN ID   │
│  (16 bits)  │  (3 bits)   │  (1 bit)    │  (12 bits)  │
│   0x8100    │  Priority   │ Drop Elig.  │   0-4095    │
└─────────────┴─────────────┴─────────────┴─────────────┘
```

- *Preamble:* Pattern of alternative 0s and 1s to allow sender and receiver to establish bit synchronization.
- *Start Frame Delimiter (SFD):* 1 Byte field that is always set to 10101011 to indicate that the upcoming bits are starting of the frame which destination address.
- *Destination MAC Address*
- *Source MAC Address*
- *802.1Q tag:* 4 octet field that indicates VLAN tag. The first two octets of the tag are called Tag Procol Identifier (TPID).
- *Ether Type Field:* To identify protocol carried in payload. Common Ether Types:

|Type| Description|
|---|---|
|0x0800|IPv4|
|0x0806|ARP|
|0x86DD|IPv6|
|0x22F0|Audio/Video Transport Protocol (AVTP)|
|0x22EA|Multiple Stream Registration Protocol (MSRP)|

- *Payload:* Actual data/payload from higher layers
- *CRC:* Contains 32-bit hash code generated from destination address, source address, length and data fields. If checksum computed by destination is not same as sent checksum value, data received is corrupted.  
- *Jumbo Frames:* To increase n/w throughput by reducing the overhead associated with transmitting many small frames. 

### VLAN Trunking Protocol (VTP):
- 802.1Q. Used to manage all configured VLANs consistency across a switched network
- VTP Domain: Consists of a group interconnected switches that share the same VLAN details. A Router or L3 switches defines the boundary of a VTP Domain.
- VTP Modes:
    - VTP Client: 
        - Can send and forward advertisements
        - Can synchronize VLAN configurations from VTP servers
        - Cannot add, modify or delete VLANs.
    - VTP Server:
        - Can create, modify and delete VLANs
        - Can send and forward advertisements 
        - Can synchronize VLAN configurations from VTP servers with high revision number
    - VTP Transparent: 
        - Does not participate in VTP domain
        - Does not advertise/synchronize VLAN configurations from VTP server
        - Can forward advertisements
        - Can create, modify and delete local VLANs only
- By default, all Cisco switches are in VTP Server mode.
- Revision Number: Indicates the level of revision for a VTP packet. Each time we add or remove a device from a VLAN, the revision no increments by one. 
- VTP Messages:
    - Summary Advertisement:
        - Includes current VTP domain name, revision number and VTP version.
        - Does not have VLAN configurations.
        - VTP server sends summary advertisements every 5 mins by default.
        - When switch recieves a summary advertisement, it checks for VTP domain name and if it matches, it compares revision numbers and if it is less, it synchronizes VLAN configuration.
    - Subset Advertisement:
        - Includes details of VLAN information
    - Client Advertisement Request: 
        - Request sent to VTP server to ask for VTP summary/subset advertisement.
- VTP Pruning: On enablement, a switch discards broadcast packets from another VLAN.

### 802.1Q VLAN Tagging
- **Purpose**: IEEE standard for VLAN tagging on Ethernet frames
- **Tag Size**: 4 bytes inserted after source MAC address
- **VLAN Range**: 1-4094 (0 and 4095 reserved)
- **Native VLAN**: Untagged traffic on trunk ports (default VLAN 1)

```
802.1Q Tag Structure (4 bytes):
┌─────────────────────┬────────────┬─────┬─────────────────────┐
│        TPID         │     PCP    │ DEI │      VLAN ID        │
│   (16 bits)         │  (3 bits)  │(1bit│     (12 bits)       │
│      0x8100         │  Priority  │Drop │     1-4094          │
└─────────────────────┴────────────┴─────┴─────────────────────┘

TPID (Tag Protocol Identifier):
• 0x8100: Standard 802.1Q
• 0x88A8: 802.1ad (QinQ/Provider Bridging)
• 0x9100: Legacy QinQ

PCP (Priority Code Point) - 3 bits:
┌─────┬─────────────────────────────────────┐
│ PCP │            Traffic Type             │
├─────┼─────────────────────────────────────┤
│  0  │ Best Effort (Default)               │
│  1  │ Background                          │
│  2  │ Excellent Effort                    │
│  3  │ Critical Applications               │
│  4  │ Video (< 100ms latency)             │
│  5  │ Voice (< 10ms latency)              │
│  6  │ Internetwork Control                │
│  7  │ Network Control                     │
└─────┴─────────────────────────────────────┘

DEI (Drop Eligible Indicator):
• 0: Frame eligible to be dropped in case of congestion
• 1: Frame not eligible to be dropped
```

- **VLAN Types:**
    - **Data VLAN**: Regular user traffic
    - **Voice VLAN**: VoIP traffic (often VLAN 100-199)
    - **Management VLAN**: Network device management
    - **Native VLAN**: Untagged traffic on trunk
    - **Default VLAN**: VLAN 1 (cannot be deleted)

- **Port Types:**
    - **Access Port**: Single VLAN, untagged traffic
    - **Trunk Port**: Multiple VLANs, tagged traffic
    - **Hybrid Port**: Mix of tagged and untagged VLANs

```
VLAN Configuration Example:
Switch(config)# vlan 10
Switch(config-vlan)# name SALES
Switch(config-vlan)# vlan 20
Switch(config-vlan)# name ENGINEERING

Access Port:
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10

Trunk Port:
Switch(config)# interface fa0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20,30
Switch(config-if)# switchport trunk native vlan 99
```

```
Inter-VLAN Routing (SVI - Switch Virtual Interface):
Switch(config)# ip routing
Switch(config)# interface vlan 10
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# no shutdown

Router-on-a-Stick (Inter-VLAN Routing with Router):
Router(config)# interface GigabitEthernet0/0
Router(config-if)# no shutdown
Router(config)# interface GigabitEthernet0/0.10
Router(config-subif)# encapsulation dot1q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
```

### Spanning Tree Protocol (STP)
- **Purpose**: Prevents loops in Layer 2 switched networks
- **Standard**: IEEE 802.1D (Original STP), 802.1w (RSTP), 802.1s (MSTP)
- **Port States**: Blocking → Listening → Learning → Forwarding → Disabled
- **BPDU**: Bridge Protocol Data Units used for STP communication
- **Root Bridge**: Switch with lowest Bridge ID (Priority + MAC address)
- **Port Roles**: Root Port, Designated Port, Blocked Port
- **Convergence Time**: Original STP (30-50 seconds), RSTP (1-6 seconds)

```
STP Network Example:
                ┌─────────────┐
                │   Switch A  │ ← Root Bridge
                │ Priority: 0 │   (Lowest Priority)
                └──────┬──────┘
                       │
        ┌──────────────┼──────────────┐
        │                             │
   ┌────▼────┐                   ┌────▼────┐
   │Switch B │                   │Switch C │
   │Priority:│                   │Priority:│
   │ 32768   │                   │ 32768   │
   └────┬────┘                   └────┬────┘
        │                             │
        └─────────────┬───────────────┘
                      │ ← This link BLOCKED
                      │   to prevent loop
                ┌─────▼─────┐
                │ Switch D  │
                │Priority:  │
                │  32768    │
                └───────────┘

Port States:
• Blocking: Receives BPDUs, blocks data traffic
• Listening: Processes BPDUs, prepares to forward
• Learning: Builds MAC address table
• Forwarding: Normal operation, forwards traffic
• Disabled: Port administratively shut down
```

- **STP Variants:**
    - **STP (802.1D)**: Original, slow convergence (30-50 seconds)
    - **RSTP (802.1w)**: Rapid convergence (1-6 seconds), backward compatible
    - **MSTP (802.1s)**: Multiple spanning trees, VLAN-aware
    - **PVST+**: Cisco proprietary, per-VLAN spanning tree
    - **Rapid PVST+**: Cisco rapid per-VLAN spanning tree

### Link Aggregation (LACP)
- **Purpose**: Combines multiple physical links into single logical link
- **Standards**: IEEE 802.3ad (LACP), 802.1AX (Link Aggregation)
- **Benefits**: Increased bandwidth, redundancy, load distribution
- **Modes**: Active/Active, Active/Passive, On (static)
- **Load Balancing**: Source MAC, Destination MAC, Source+Dest IP, Port-based

```
Link Aggregation Example:
┌─────────────┐                    ┌─────────────┐
│   Switch A  │                    │   Switch B  │
│             │ ── Port 1/1 ────── │             │
│             │ ── Port 1/2 ────── │             │ 
│             │ ── Port 1/3 ────── │             │
│             │ ── Port 1/4 ────── │             │
└─────────────┘                    └─────────────┘
      │                                    │
      └────── EtherChannel/Port-Channel ───┘
              (Logical 4Gbps Link)

LACP Modes:
• Active: Initiates LACP negotiation
• Passive: Responds to LACP negotiation
• On: Static bundling (no LACP protocol)
```

### L2 Discovery Protocols
- **CDP (Cisco Discovery Protocol)**:
    - Cisco proprietary, Layer 2 protocol
    - Discovers directly connected Cisco devices
    - Shares device info: hostname, IP, platform, capabilities
    - Multicast address: 01:00:0C:CC:CC:CC
    - Default timer: 60 seconds, holdtime: 180 seconds

- **LLDP (Link Layer Discovery Protocol)**:
    - IEEE 802.1AB standard, vendor-neutral
    - Discovers directly connected devices regardless of vendor
    - TLV (Type-Length-Value) format for information exchange
    - Multicast address: 01:80:C2:00:00:0E
    - Default timer: 30 seconds, holdtime: 120 seconds

```
Discovery Protocol Comparison:
┌─────────────────┬─────────────┬─────────────┐
│    Feature      │     CDP     │    LLDP     │
├─────────────────┼─────────────┼─────────────┤
│ Standard        │ Cisco Prop. │ IEEE 802.1AB│
│ Vendor Support  │ Cisco Only  │ Multi-vendor│
│ Default Timer   │ 60 seconds  │ 30 seconds  │
│ Hold Time       │ 180 seconds │ 120 seconds │
│ Power Info      │     ✅      │     ✅     │
│ VLAN Info       │     ✅      │     ✅     │
│ Security        │   Limited   │   Enhanced  │
└─────────────────┴─────────────┴─────────────┘
```

### UDLD (UniDirectional Link Detection)
- **Purpose**: Detects unidirectional links (fiber/copper) to prevent spanning-tree loops
- **Problem**: Fiber strand breaks (Tx works, Rx fails), creating a "one-way" link. STP logic fails because BPDUs aren't received, potentially causing loops.
- **Mechanism**: Layer 2 protocol (Cisco Proprietary) that uses "Echo" mechanism.
- **Modes**:
    - **Normal**: Informational. Marks port as "Undetermined" if bidirectionality fails.
    - **Aggressive**: Protective. Err-disables the port if bidirectionality fails (Recommended).

```
UDLD Echo Mechanism:
┌─────────────┐                      ┌─────────────┐
│  Switch A   │                      │  Switch B   │
│ (ID: AAAA)  │                      │ (ID: BBBB)  │
└──────┬──────┘                      └──────┬──────┘
       │                                    │
       │ 1. UDLD Hello (My ID: AAAA)        │
       │ ─────────────────────────────────► │
       │                                    │
       │ 2. UDLD Hello (My ID: BBBB,        │
       │                Neighbor: AAAA)     │
       │ ◄───────────────────────────────── │
       │                                    │
       │ 3. Bidirectional Link Detected!    │
       │    (See my ID in peer's Hello)     │
       │                                    │
```

```
UDLD Configuration:
! Global Configuration (enables on all fiber ports)
Switch(config)# udld enable           ! Normal Mode
Switch(config)# udld aggressive       ! Aggressive Mode

! Interface Configuration (Specific ports)
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# udld port aggressive

! Verification
Switch# show udld neighbors
Switch# show udld interface GigabitEthernet0/1
! Reset err-disabled ports
Switch# udld reset
```

### 802.1X Authentication
- **Purpose**: Port-based network access control
- **Components**: Supplicant (client), Authenticator (switch), Authentication Server (RADIUS)
- **EAP Methods**: EAP-MD5, EAP-TLS, EAP-TTLS, PEAP, EAP-FAST
- **Port States**: Unauthorized, Authorized, Force-Authorized, Force-Unauthorized

```
802.1X Authentication Flow:
┌─────────────┐                ┌─────────────┐                ┌─────────────┐
│ Supplicant  │                │Authenticator│                │   RADIUS    │
│  (Client)   │                │  (Switch)   │                │   Server    │
└──────┬──────┘                └──────┬──────┘                └──────┬──────┘
       │                              │                              │
       │ 1. EAP-Start                 │                              │
       │ ───────────────────────────► │                              │
       │                              │                              │
       │ 2. EAP-Request Identity      │                              │
       │ ◄─────────────────────────── │                              │
       │                              │                              │
       │ 3. EAP-Response Identity     │                              │
       │ ───────────────────────────► │ 4. RADIUS Access-Request     │
       │                              │ ───────────────────────────► │
       │                              │                              │
       │                              │ 5. RADIUS Access-Challenge   │
       │ 6. EAP-Request               │ ◄─────────────────────────── │
       │ ◄─────────────────────────── │                              │
       │                              │                              │
       │ 7. EAP-Response              │                              │
       │ ───────────────────────────► │ 8. RADIUS Access-Request     │
       │                              │ ───────────────────────────► │
       │                              │                              │
       │                              │ 9. RADIUS Access-Accept      │
       │ 10. EAP-Success              │ ◄─────────────────────────── │
       │ ◄─────────────────────────── │                              │
       │                              │                              │
       │ 11. Port Authorized          │                              │
       │ ◄══════════════════════════► │                              │

Port States:
• Unauthorized: Only 802.1X traffic allowed
• Authorized: Full network access granted
• Force-Authorized: Bypass 802.1X (always allow)
• Force-Unauthorized: Block all traffic
```

<br>&nbsp;
## Layer 3
### IPv4 Protocol

*1. Header Structure:*

```
IPv4 Header (20-60 bytes):
┌─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┐
│   Version   │     IHL     │   DSCP/ToS  │     ECN     │                        Total Length                   │
│   (4 bits)  │  (4 bits)   │  (6 bits)   │  (2 bits)   │                         (16 bits)                     │
├─────────────┴─────────────┼─────────────┴─────────────┼─────────────┬─────────────┬─────────────┬─────────────┤
│                      Identification                   │     Flags   │                Fragment Offset          │
│                        (16 bits)                      │   (3 bits)  │                (13 bits)                │
├─────────────┬─────────────┼─────────────┴─────────────┼─────────────┴─────────────────────────────────────────┤
│            TTL            │          Protocol         │                    Header Checksum                    │
│         (8 bits)          │          (8 bits)         │                      (16 bits)                        │
├─────────────┴─────────────┼───────────────────────────┼───────────────────────────────────────────────────────┤
│                                               Source IP Address                                               │
│                                                   (32 bits)                                                   │
├───────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                            Destination IP Address                                             │
│                                                   (32 bits)                                                   │
├───────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                       Options (0-320 bits, if IHL > 5)                                        │
│                                         + Padding to 32-bit boundary                                          │
└───────────────────────────────────────────────────────────────────────────────────────────────────────────────┘

Field Details:
• Version: 4 (for IPv4)
• IHL: Internet Header Length (5-15, multiply by 4 for bytes)
• DSCP: Differentiated Services Code Point (QoS marking)
• ECN: Explicit Congestion Notification
• Total Length: Header + Data (max 65,535 bytes)
• Identification: Unique identifier for fragmented packets
• Flags: Reserved(0), Don't Fragment(DF), More Fragments(MF)
• Fragment Offset: Position of fragment in original datagram
• TTL: Time To Live (hop count, decremented by each router)
• Protocol: Next layer protocol (1=ICMP, 6=TCP, 17=UDP, 89=OSPF)
• Header Checksum: Error detection for header only
```

![](https://github.com/ravikumark815/notes/blob/main/images/ip-header.png)
- `Version` (4 bits): IP Version = 4
- `IHL` (4 bits): Internet Header length. (20 bytes - 60 bytes)
- `DSCP/ToS`: Differentiated Services Code Point/Type of Service: Sets precedence for each packet. Ex. VoIP
    - Precedence: 3 Bits
    - Delay: 1 bit
    - Throughput: 1 bit
    - Reliability: 1 bit
- `Explicit Congestion Notification` (2 bit): Allows end to end notification of network congestion without dropping packets
- `Total Length` (16 bits): Entire packet size
- `Identification` (16 bits): To identify group of fragments of a single IP datagram
- `Flags` (3 bits):
    - `Reserved`
    - `Don't Fragment` (DF)
    - `More Fragments` (MF)
- `Fragment Offset` (8 bits): Specifies the offset of a particular fragment relative to the beginning of an unfragmented IP datagram.
- `Time to Live (TTL)` (8 bits): Limits a datagram's lifetime to prevent network failure in the event of a routing loop
- `Protocol` (8 bits): Defines the transport layer protocol used in the payload. 

    |Protocol No| Protocol |
    |---|---|
    |1|ICMP|
    |2|IGMP|
    |6|TCP|
    |17|UDP|
    |89|OSPF|
- `Header Checksum` (16 bits): Used for error checking of the header. The 16-bit ones' complement sum of all 16-bit words in the header is computed, with the Header Checksum field set to zero during calculation. Upon arrival at a router or destination, the checksum is recalculated. If the result is zero, the packet is valid. If not, the packet is discarded.
- `Source IP Address` (32 bits)
- `Destination IP Address` (32 bits)
- `Options`: 0 - 320 bits, padded to multiples of 32 bits


*2. Features/Functions:*
- IP Addressing
- Data Encapsulation and Packaging
- Fragmentation & Reassembly
- Routing and Indirect Delivery
- Multicasting
- Protocols: IPNAT, IPSec, MobileIP, IPv4, IPv6

*4. Options:*
- Option Type: 8 bits
- Option Length: 8 bits
- Option Data: 16 bits

*5. Fragmentation:*
- The router checks the destination address and selects the outgoing interface and its MTU (Maximum Transmission Unit). If the packet size exceeds the MTU and the Do Not Fragment (DF) bit is 0, the router fragments the packet before forwarding.

*6. Reassembly:*
- A receiver knows that a packet is a fragment, if at least one of the following conditions is true:
    - The flag more fragments is set, which is true for all fragments except the last.
    - The field fragment offset is nonzero, which is true for all fragments except the first.

**Internet Control Message Protocol [ICMP]:**
- Protocol to communicate problems with data transmission.
- RFC 792
- Connectionless protocol: One devices does not need to open a connection with another before transmission. 
- ICMP flood attack: Attacker overwhelming a target device with ICMP echo-request packets 
- Smurf Attack: Attacker sends an ICMP packet with spoofed source IP address. 
- Traceroute: Utility to know the route between two devices. 
- Header:
![](https://github.com/ravikumark815/notes/blob/main/images/icmp-header.png)

    |   |   |
    |---|---|
    Type 0| Echo Reply
    Type 3| Destination unreachable
    Type 5| Redirect Message
    Type 8| Echo Request
    Type 11| Time Exceeded
    Type 12| Parameter Problem

- Code: Carries additional info about error message and type
- Checksum: Used to check no of bits of complete message and enable ICMP tool to ensure the complete data is delivered. 
- Extended Header: Indicates problem in IP message. Byte locations are identified by the pointer which causes the problem message and receiving devices looks here for any problem. 
- Data/Payload: 576 Bytes in IPv4 and 1280 Bytes in IPv6

### IPv6 Protocol
- **Purpose**: Next generation Internet Protocol with 128-bit addressing
- **Address Space**: 2^128 addresses (340 undecillion addresses)
- **Header Size**: Fixed 40 bytes (vs IPv4's variable 20-60 bytes)
- **Features**: Built-in security, auto-configuration, improved QoS, no fragmentation by routers

```
IPv6 Header Structure (40 bytes fixed):
┌─────────────────────────────────────────────────────────────┐
│ Version │Traffic Class│        Flow Label                   │
│ (4 bits)│  (8 bits)   │        (20 bits)                    │
├─────────────────────────────────────────────────────────────┤
│        Payload Length         │  Next Header  │ Hop Limit   │
│         (16 bits)             │   (8 bits)    │  (8 bits)   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                Source Address (128 bits)                    │
│                                                             │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│              Destination Address (128 bits)                 │
│                                                             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

- **IPv6 Address Types:**
    - **Unicast**: One-to-one communication
        - Global Unicast: 2000::/3 (Internet routable)
        - Link-Local: FE80::/10 (Local network only)
        - Unique Local: FC00::/7 (Private addressing)
    - **Multicast**: One-to-many communication (FF00::/8)
    - **Anycast**: One-to-nearest communication

- **IPv6 Address Format:**
    - **Full**: 2001:0DB8:0000:0000:0000:0000:0000:0001
    - **Compressed**: 2001:DB8::1 (leading zeros and consecutive zeros omitted)
    - **Mixed**: 2001:DB8::192.168.1.1 (IPv4-mapped)

- **IPv6 vs IPv4 Comparison:**

    |Feature|IPv4|IPv6|
    |---|---|---|
    |**Address Length**|32 bits|128 bits|
    |**Header Size**|20-60 bytes|40 bytes (fixed)|
    |**Fragmentation**|Routers & hosts|Hosts only|
    |**Checksum**|Header checksum|No checksum|
    |**Auto-config**|DHCP required|SLAAC built-in|
    |**Security**|Optional (IPsec)|Built-in (IPsec)|
    |**QoS**|ToS field|Traffic Class + Flow Label|
    |**Broadcast**|Yes|No (multicast only)|

### ARP Protocol
- **Purpose**: Maps IP addresses to MAC addresses in IPv4 networks
- **Operation**: Broadcast ARP request, unicast ARP reply
- **Cache**: Stores IP-to-MAC mappings to reduce network traffic
- **Types**: ARP Request, ARP Reply, Gratuitous ARP, Proxy ARP

```
ARP Process Example:
┌─────────────┐                                    ┌─────────────┐
│   Host A    │                                    │   Host B    │
│192.168.1.10 │                                    │192.168.1.20 │
│AA:BB:CC:DD  │                                    │11:22:33:44  │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. ARP Request (Broadcast)                       │
       │ Who has 192.168.1.20? Tell 192.168.1.10          │
       │ Src MAC: AA:BB:CC:DD  Dst MAC: FF:FF:FF:FF:FF:FF │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ 2. ARP Reply (Unicast)                           │
       │ 192.168.1.20 is at 11:22:33:44                   │
       │ Src MAC: 11:22:33:44  Dst MAC: AA:BB:CC:DD       │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
   ┌───▼─────┐                                       ┌────▼────┐
   │ARP Cache│                                       │ARP Cache│
   │192.168.1│                                       │192.168.1│
   │.20 →    │                                       │.10 →    │
   │11:22:33:│                                       │AA:BB:CC:│
   │44       │                                       │DD       │
   └─────────┘                                       └─────────┘

ARP Message Types:
• ARP Request: Broadcast to find MAC address
• ARP Reply: Unicast response with MAC address
• Gratuitous ARP: Announces own IP/MAC mapping
• Proxy ARP: Router responds on behalf of another device
```

### ARP Flavours and Variants

#### 1. Standard ARP (Address Resolution Protocol)
- **RFC 826**: Original ARP specification
- **Operation**: Broadcast request, unicast reply
- **Scope**: Local network segment only

#### 2. Gratuitous ARP (GARP)
- **Purpose**: Announce IP/MAC mapping without being asked
- **Uses**: 
    - Detect IP conflicts
    - Update ARP caches after IP change
    - High availability failover
    - Network troubleshooting

```
Gratuitous ARP Example:
┌─────────────┐                                    ┌─────────────┐
│   Host A    │                                    │   Host B    │
│192.168.1.10 │                                    │192.168.1.20 │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ Gratuitous ARP (Broadcast)                       │
       │ Who has 192.168.1.10? Tell 192.168.1.10          │
       │ (Announcing own IP/MAC mapping)                  │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ Updates ARP cache with Host A's mapping          │
       │ ◄──────────────────────────────────────────────  │
```

#### 3. Proxy ARP
- **Purpose**: Router responds to ARP requests on behalf of other devices
- **Use Cases**: 
    - Subnet extension
    - Mobile IP
    - Network address translation
    - Connecting different network segments

```
Proxy ARP Example:
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Host A    │    │   Router    │    │   Host B    │
│192.168.1.10 │    │192.168.1.1  │    │192.168.2.20 │
│             │    │192.168.2.1  │    │             │
└──────┬──────┘    └──────┬──────┘    └──────┬──────┘
       │                  │                  │
       │ ARP: Who has     │                  │
       │ 192.168.2.20?    │                  │
       │ ────────────────►│                  │
       │                  │ Router responds  │
       │ ARP Reply:       │ with its own MAC │
       │ 192.168.2.20 is  │ (proxy response) │
       │ at Router-MAC    │                  │
       │ ◄────────────────│                  │
```

#### 4. Reverse ARP (RARP)
- **RFC 903**: Obsolete protocol
- **Purpose**: Map MAC address to IP address
- **Replaced by**: DHCP and BOOTP
- **Use Case**: Diskless workstations needing IP addresses

#### 5. Inverse ARP (InARP)
- **RFC 2390**: Used in Frame Relay networks
- **Purpose**: Discover IP address of remote end of virtual circuit
- **Operation**: Uses known DLCI to find remote IP

#### 6. IPv6 Neighbor Discovery (ND)
- **RFC 4861**: IPv6 replacement for ARP
- **Messages**: 
    - Neighbor Solicitation (NS) - like ARP request
    - Neighbor Advertisement (NA) - like ARP reply
    - Router Solicitation (RS)
    - Router Advertisement (RA)
    - Redirect

```
IPv6 Neighbor Discovery:
┌─────────────┐                                    ┌─────────────┐
│   Host A    │                                    │   Host B    │
│2001:db8::10 │                                    │2001:db8::20 │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ Neighbor Solicitation (Multicast)                │
       │ Target: 2001:db8::20                             │
       │ To: ff02::1:ff00:20 (solicited-node multicast)  │
       │ ──────────────────────────────────────────────► │
       │                                                  │
       │ Neighbor Advertisement (Unicast)                 │
       │ Target: 2001:db8::20, MAC: 11:22:33:44:55:66    │
       │ ◄────────────────────────────────────────────── │
```

#### 7. ARP Security Issues and Mitigations

**Common Attacks:**
- **ARP Spoofing/Poisoning**: Attacker sends fake ARP replies
- **ARP Cache Poisoning**: Corrupting ARP tables
- **Man-in-the-Middle**: Intercepting traffic via ARP spoofing
- **ARP Flooding**: Overwhelming switch MAC table

**Mitigation Techniques:**
```
1. Static ARP Entries:
   arp -s 192.168.1.20 11:22:33:44:55:66

2. Dynamic ARP Inspection (DAI):
   Switch(config)# ip arp inspection vlan 10
   Switch(config)# ip arp inspection validate src-mac dst-mac ip

3. Port Security:
   Switch(config-if)# switchport port-security
   Switch(config-if)# switchport port-security mac-address sticky

4. ARP Monitoring Tools:
   - arpwatch: Monitor ARP activity
   - arping: Send ARP requests
   - arp-scan: Discover hosts on network
```

**ARP Table Management:**
```
Windows:
arp -a                    # View ARP table
arp -d *                  # Clear ARP table
arp -s IP MAC             # Add static entry

Linux:
arp -a                    # View ARP table
ip neigh show             # View neighbor table
ip neigh flush all        # Clear neighbor table
ip neigh add IP lladdr MAC dev eth0  # Add static entry

Cisco:
show arp                  # View ARP table
clear arp                 # Clear ARP table
arp IP MAC arpa           # Add static entry
```

### Routing Protocols

#### RIP (Routing Information Protocol)
- **Type**: Distance Vector routing protocol
- **Metric**: Hop count (maximum 15 hops, 16 = unreachable)
- **Updates**: Periodic (every 30 seconds) and triggered
- **Versions**: RIPv1 (classful), RIPv2 (classless), RIPng (IPv6)
- **Algorithm**: Bellman-Ford algorithm

```
RIP Operation Example:
┌────────────-─┐   ┌────────────-─┐   ┌─────────────-┐
│   Router A   │   │   Router B   │   │   Router C   │
│192.168.1.0/24│   │192.168.2.0/24│   │192.168.3.0/24│
└──────┬──────-┘   └──────┬──────-┘   └──────┬──────-┘
       │                  │                  │
       └──────────────────┼──────────────────┘
                          │
                  ┌───────▼──----┐
                  │    Network   │
                  │192.168.4.0/24│
                  └───────────---┘

RIP Routing Table:

Router A's Routing Table:
┌─────────────────┬──────────┬─────────┬─────────┐
│   Destination   │   Mask   │Next Hop │Hop Count│
├─────────────────┼──────────┼─────────┼─────────┤
│ 192.168.1.0     │ /24      │ Direct  │    0    │
│ 192.168.2.0     │ /24      │Router B │    1    │
│ 192.168.3.0     │ /24      │Router B │    2    │
│ 192.168.4.0     │ /24      │Router B │    1    │
└─────────────────┴──────────┴─────────┴─────────┘
```

#### EIGRP (Enhanced Interior Gateway Routing Protocol)
- **Type**: Advanced Distance Vector (Hybrid) protocol
- **Vendor**: Cisco proprietary (now open standard)
- **Metric**: Composite metric (bandwidth, delay, reliability, load, MTU)
- **Algorithm**: DUAL (Diffusing Update Algorithm)
- **Features**: Fast convergence, loop-free, VLSM support, load balancing

```
EIGRP Metric Calculation:
Metric = [K1×Bandwidth + (K2×Bandwidth)/(256-Load) + K3×Delay] × [K5/(Reliability+K4)]

Default K values: K1=1, K2=0, K3=1, K4=0, K5=0
Simplified: Metric = Bandwidth + Delay

EIGRP Neighbor States:
┌─────────────┐    ┌─────────────┐
│   Router A  │    │   Router B  │
└──────┬──────┘    └──────┬──────┘
       │                  │
       │ 1. Hello Packets │
       │ ◄──────────────► │
       │                  │
       │ 2. Update Packets│
       │ ◄──────────────► │
       │                  │
       │ 3. ACK Packets   │
       │ ◄──────────────► │

Neighbor States: Down → Pending → Up
```

#### OSPF (Open Shortest Path First)
- **Type**: Link State routing protocol
- **Standard**: RFC 2328 (OSPFv2), RFC 5340 (OSPFv3)
- **Metric**: Cost based on bandwidth (10^8/bandwidth)
- **Algorithm**: Dijkstra's Shortest Path First
- **Areas**: Hierarchical design with Area 0 (backbone)

```
OSPF Area Design:
                    ┌─────────────┐
                    │   Area 0    │
                    │ (Backbone)  │
                    │             │
                    └──────┬──────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   ┌────▼────┐        ┌────▼────┐        ┌────▼────┐
   │ Area 1  │        │ Area 2  │        │ Area 3  │
   │(Standard│        │(Standard│        │ (Stub)  │
   │  Area)  │        │  Area)  │        │  Area)  │
   └─────────┘        └─────────┘        └─────────┘

```
OSPF Configuration (Single Area):
Router(config)# router ospf 1
Router(config-router)# router-id 1.1.1.1
! Network statement: Network Address + Wildcard Mask + Area
Router(config-router)# network 192.168.10.0 0.0.0.255 area 0
Router(config-router)# network 10.0.0.0 0.0.0.3 area 0
Router(config-router)# passive-interface GigabitEthernet0/1

! Interface Config (Newer method)
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip ospf 1 area 0
```

OSPF LSA Types:
• Type 1: Router LSA (within area)
• Type 2: Network LSA (DR generated)
• Type 3: Summary LSA (inter-area routes)
• Type 4: ASBR Summary LSA
• Type 5: External LSA (external routes)
```

#### BGP (Border Gateway Protocol)
- **Type**: Path Vector routing protocol
- **Purpose**: Inter-domain routing (between Autonomous Systems)
- **Version**: BGP-4 (RFC 4271)
- **Port**: TCP 179
- **Characteristics**: Policy-based, scalable, loop-free

**BGP Session Types:**
- **eBGP (External BGP)**: Between different ASes (TTL=1, AD=20)
- **iBGP (Internal BGP)**: Within same AS (TTL=255, AD=200)

```
BGP Configuration (eBGP & iBGP):
Router(config)# router bgp 65001
Router(config-router)# bgp router-id 1.1.1.1

! iBGP Neighbor (Same AS)
Router(config-router)# neighbor 10.0.0.2 remote-as 65001
Router(config-router)# neighbor 10.0.0.2 update-source Loopback0

! eBGP Neighbor (Different AS)
Router(config-router)# neighbor 172.16.1.1 remote-as 65002

! Advertise Networks
Router(config-router)# network 192.168.1.0 mask 255.255.255.0
```

**BGP Message Types:**
1. **OPEN**: Establish BGP session
2. **UPDATE**: Advertise/withdraw routes
3. **NOTIFICATION**: Error conditions
4. **KEEPALIVE**: Maintain session

```
BGP Session Establishment:
┌─────────────┐                                    ┌─────────────┐
│   Router A  │                                    │   Router B  │
│   AS 100    │                                    │   AS 200    │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. TCP Connection (Port 179)                     │
       │ ──────────────────────────────────────────────► │
       │                                                  │
       │ 2. OPEN Message                                  │
       │ (AS Number, BGP Version, Hold Time)              │
       │ ──────────────────────────────────────────────► │
       │                                                  │
       │ 3. OPEN Message                                  │
       │ ◄────────────────────────────────────────────── │
       │                                                  │
       │ 4. KEEPALIVE                                     │
       │ ◄──────────────────────────────────────────────► │
       │                                                  │
       │ 5. UPDATE Messages (Route Exchange)              │
       │ ◄══════════════════════════════════════════════► │

BGP States:
Idle → Connect → Active → OpenSent → OpenConfirm → Established
```

**BGP Attributes (Path Selection):**

```
┌─────────────────────┬─────────────┬─────────────────────────────────┐
│     Attribute       │    Type     │           Description           │
├─────────────────────┼─────────────┼─────────────────────────────────┤
│ AS_PATH             │Well-known   │ List of ASes route traversed    │
│ NEXT_HOP            │Well-known   │ Next hop IP address             │
│ ORIGIN              │Well-known   │ How route originated (IGP/EGP)  │
│ LOCAL_PREF          │Well-known   │ Local preference (iBGP only)    │
│ ATOMIC_AGGREGATE    │Well-known   │ Route aggregation indicator     │
│ AGGREGATOR          │Optional     │ AS and Router ID of aggregator  │
│ MED                 │Optional     │ Multi-Exit Discriminator        │
│ COMMUNITY           │Optional     │ Route tagging/policy            │
│ ORIGINATOR_ID       │Optional     │ Route reflector originator      │
│ CLUSTER_LIST        │Optional     │ Route reflector cluster list    │
└─────────────────────┴─────────────┴─────────────────────────────────┘
```

**BGP Path Selection Algorithm (Detailed):**
1. **Weight** (Cisco proprietary, 0-65535, higher better)
2. **Local Preference** (0-4294967295, higher better, iBGP only)
3. **Locally Originated** (network/redistribute > aggregate > received)
4. **AS_PATH Length** (shorter better)
5. **Origin Code** (IGP < EGP < Incomplete)
6. **MED** (Multi-Exit Discriminator, lower better, same AS only)
7. **Path Type** (eBGP > iBGP)
8. **IGP Metric** to next hop (lower better)
9. **Age** (oldest route preferred)
10. **Router ID** (lower better)
11. **Cluster Length** (shorter better)
12. **Neighbor Address** (lower better)

**BGP Communities:**
- **Standard Communities**: 32-bit values (AS:Value format)
    - **Well-known**: 0:0 (no-export), 0:1 (no-advertise), 0:2 (no-export-subconfed)
- **Extended Communities**: 64-bit values
- **Large Communities**: 96-bit values (RFC 8092)

```
BGP Community Examples:
router bgp 100
 neighbor 10.1.1.2 send-community
 network 192.168.1.0 mask 255.255.255.0
 
route-map SET_COMMUNITY permit 10
 set community 100:200
 set local-preference 150
```

**BGP Route Reflectors:**
- **Problem**: iBGP full mesh requirement (n*(n-1)/2 sessions)
- **Solution**: Route Reflector eliminates full mesh
- **Components**: Route Reflector (RR), Clients, Non-clients

```
Route Reflector Topology:
                    ┌─────────────┐
                    │     RR      │
                    │ (Reflector) │
                    └──────┬──────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   ┌────▼────┐        ┌────▼────┐        ┌────▼────┐
   │Client 1 │        │Client 2 │        │Client 3 │
   └─────────┘        └─────────┘        └─────────┘

RR Rules:
• Routes from clients → advertise to all peers
• Routes from non-clients → advertise to clients only
• Routes from eBGP → advertise to all peers
```

**BGP Confederation:**
- **Alternative** to Route Reflectors
- **Concept**: Divide large AS into smaller sub-ASes
- **Benefits**: Reduces iBGP sessions, maintains path information

**BGP Security:**
- **Route Hijacking**: Unauthorized route advertisements
- **Path Manipulation**: AS_PATH manipulation
- **Mitigation**: 
    - Route filtering
    - RPKI (Resource Public Key Infrastructure)
    - BGPsec (Path validation)
    - Route monitoring systems

#### IS-IS (Intermediate System to Intermediate System)
- **Type**: Link State routing protocol
- **Standard**: ISO 10589 (OSI), RFC 1142 (IP)
- **Levels**: Level 1 (intra-area), Level 2 (inter-area), Level 1-2 (both)
- **Addressing**: Uses NSAP (Network Service Access Point) addresses
- **Features**: Fast convergence, scalable, supports IPv4 and IPv6 natively

**IS-IS vs OSPF Comparison:**

```
┌─────────────────────┬─────────────────┬─────────────────┐
│      Feature        │      IS-IS      │      OSPF       │
├─────────────────────┼─────────────────┼─────────────────┤
│ Protocol Base       │ OSI (Layer 2)   │ IP (Layer 3)    │
│ Addressing          │ NSAP/NET        │ IP addresses    │
│ Area Design         │ 2-level         │ Multi-level     │
│ Backbone            │ Level 2         │ Area 0          │
│ IPv6 Support        │ Native          │ OSPFv3 needed   │
│ Metric              │ Narrow/Wide     │ Cost based      │
│ LSP/LSA Size        │ Up to 1492 bytes│ Limited         │
│ Convergence         │ Fast            │ Fast            │
│ Vendor Support      │ Multi-vendor    │ Multi-vendor    │
└─────────────────────┴─────────────────┴─────────────────┘
```

**IS-IS Addressing:**
- **NSAP Address**: 20 bytes total
    - **Area ID**: Variable length (1-13 bytes)
    - **System ID**: 6 bytes (like MAC address)
    - **NSEL**: 1 byte (always 00 for routers)

```
NSAP Address Format:
┌─────────────────────┬─────────────────────┬─────────────┐
│      Area ID        │     System ID       │    NSEL     │
│   (1-13 bytes)      │     (6 bytes)       │  (1 byte)   │
│                     │                     │     00      │
└─────────────────────┴─────────────────────┴─────────────┘

Example: 49.0001.1921.6800.1001.00
• 49: Private area (like RFC 1918)
• 0001: Area ID
• 1921.6800.1001: System ID (192.168.0.16.01)
• 00: NSEL (Network Service Access Point)
```

**IS-IS Levels:**
- **Level 1 (L1)**: Intra-area routing
    - Maintains detailed topology of local area
    - Default route to nearest Level 1-2 router
- **Level 2 (L2)**: Inter-area routing
    - Maintains area-level topology
    - Routes between areas
- **Level 1-2 (L1L2)**: Both levels
    - Participates in both L1 and L2 routing
    - Acts as area border router

```
IS-IS Area Design:
                    ┌─────────────┐
                    │   Area 2    │
                    │             │
                    │  ┌───────┐  │
                    │  │  L2   │  │
                    │  │Router │  │
                    │  └───┬───┘  │
                    └──────┼──────┘
                           │ L2 Adjacency
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   ┌────▼────┐        ┌────▼────┐        ┌────▼────┐
   │ Area 1  │        │ Area 0  │        │ Area 3  │
   │         │        │(Backbone│        │         │
   │ ┌─────┐ │        │ Area)   │        │ ┌─────┐ │
   │ │ L1  │ │        │ ┌─────┐ │        │ │ L1  │ │
   │ │Rtr  │ │        │ │L1L2 │ │        │ │Rtr  │ │
   │ └─────┘ │        │ │Rtr  │ │        │ └─────┘ │
   └─────────┘        │ └─────┘ │        └─────────┘
                      └─────────┘

L1 Routers: Intra-area only
L2 Routers: Inter-area backbone
L1L2 Routers: Area border routers
```

**IS-IS PDU Types:**
1. **Hello PDUs**: Neighbor discovery and adjacency
    - **L1 LAN Hello**: Level 1 LAN adjacency
    - **L2 LAN Hello**: Level 2 LAN adjacency
    - **Point-to-Point Hello**: P2P links
2. **LSP (Link State PDU)**: Topology information
    - **L1 LSP**: Level 1 topology
    - **L2 LSP**: Level 2 topology
3. **SNP (Sequence Number PDU)**: Database synchronization
    - **CSNP**: Complete SNP (periodic)
    - **PSNP**: Partial SNP (acknowledgment)

**IS-IS Metrics:**
- **Narrow Metrics**: 6-bit (0-63), total path max 1023
- **Wide Metrics**: 24-bit (0-16777215), supports TE extensions
- **Default Interface Cost**: 10 (regardless of bandwidth)

```
IS-IS Configuration Example:
router isis
 net 49.0001.1921.6800.1001.00
 is-type level-2-only
 metric-style wide
 
interface GigabitEthernet0/0
 ip router isis
 isis circuit-type level-2-only
 isis metric 100
```

**IS-IS Advantages:**
- **Protocol Independence**: Runs directly over Layer 2
- **IPv6 Ready**: Native support without protocol changes
- **Scalability**: Large LSPs, efficient flooding
- **Flexibility**: Easy to extend with new TLVs
- **Stability**: Mature protocol, widely deployed in ISPs

#### GRP (Generic Routing Protocol)
- **Purpose**: Framework for implementing routing protocols
- **Type**: Not a specific protocol, but a generic framework/API
- **Usage**: Used in network simulation and research environments
- **Implementation**: Provides common routing protocol functions

**GRP Components:**
- **Route Table Management**: Add, delete, modify routes
- **Neighbor Discovery**: Find and maintain neighbor relationships
- **Message Handling**: Send and receive routing updates
- **Timer Management**: Handle periodic updates and timeouts
- **Policy Framework**: Apply routing policies and filters

```
GRP Framework Architecture:
┌─────────────────────────────────────────────────────────────┐
│                    GRP Framework                            │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Policy    │  │   Timer     │  │  Message    │         │
│  │  Manager    │  │  Manager    │  │  Handler    │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Route     │  │  Neighbor   │  │  Interface  │         │
│  │   Table     │  │  Manager    │  │  Manager    │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
├─────────────────────────────────────────────────────────────┤
│                 Network Interface                           │
└─────────────────────────────────────────────────────────────┘
```
GRP vs Specific Protocols:
┌─────────────────┬─────────────────┬─────────────────┐
│    Feature      │      GRP        │ Specific (OSPF) │
├─────────────────┼─────────────────┼─────────────────┤
│ Implementation  │ Framework/API   │ Full Protocol   │
│ Standardization │ Research/Sim    │ RFC Standard    │
│ Algorithm       │ Pluggable       │ Fixed (SPF)     │
│ Message Format  │ Generic         │ Protocol-specific│
│ Deployment      │ Lab/Research    │ Production      │
└─────────────────┴─────────────────┴─────────────────┘
```

**GRP Use Cases:**
- **Protocol Development**: Rapid prototyping of new routing protocols
- **Network Simulation**: Testing routing behaviors in simulators
- **Research**: Academic research on routing algorithms
- **Education**: Teaching routing protocol concepts
- **Hybrid Protocols**: Combining features from multiple protocols

### High Availability Protocols

#### HSRP (Hot Standby Router Protocol)
- **Purpose**: First Hop Redundancy Protocol (FHRP)
- **Vendor**: Cisco proprietary
- **Virtual IP**: Shared IP address among routers
- **Priority**: 0-255 (default 100, highest wins)
- **Preemption**: Higher priority router can take over

```
HSRP Operation:
┌─────────────┐              ┌─────────────┐
│   Router A  │              │   Router B  │
│Priority: 110│              │Priority: 100│
│  (Active)   │              │ (Standby)   │
└──────┬──────┘              └──────┬──────┘
       │                            │
       └────────────┬───────────────┘
                    │
              ┌─────▼─────┐
              │   LAN     │
              │192.168.1.0│
              │    /24    │
              └─────┬─────┘
                    │
              ┌─────▼─────┐
              │   Host    │
              │ Gateway:  │
              │192.168.1.1│ ← Virtual IP
              │ (HSRP VIP)│
              └───────────┘

HSRP States:
• Initial: Starting state
• Learn: Learning configuration
• Listen: Listening for hellos
• Speak: Participating in election
• Standby: Backup router
• Active: Forwarding traffic
```

#### VRRP (Virtual Router Redundancy Protocol)
- **Purpose**: Standards-based First Hop Redundancy Protocol
- **Standard**: RFC 3768 (VRRPv2), RFC 5798 (VRRPv3)
- **Roles**: Master (active), Backup (standby)
- **Priority**: 1-254 (default 100, highest wins, 255 = IP owner)
- **Advertisement**: Master sends advertisements every 1 second
- **Multicast**: 224.0.0.18 (VRRPv2), FF02::12 (VRRPv3)

```
VRRP Operation:
┌─────────────┐              ┌─────────────┐
│   Router A  │              │   Router B  │
│Priority: 200│              │Priority: 100│
│  (Master)   │              │  (Backup)   │
│VRID: 1      │              │VRID: 1      │
└──────┬──────┘              └──────┬──────┘
       │                            │
       │ VRRP Advertisements        │
       │ Every 1 second             │
       │ ──────────────────────────► │
       │                            │
       └────────────┬───────────────┘
                    │
              ┌─────▼─────┐
              │   LAN     │
              │192.168.1.0│
              │    /24    │
              └─────┬─────┘
                    │
              ┌─────▼─────┐
              │   Host    │
              │ Gateway:  │
              │192.168.1.1│ ← Virtual IP (VIP)
              │ (VRRP VIP)│
              └───────────┘

VRRP States:
• Initialize: Starting state
• Backup: Listening for advertisements
• Master: Forwarding traffic, sending advertisements

VRRP Failover Process:
1. Master stops sending advertisements
2. Backup waits for Master_Down_Interval
3. Backup transitions to Master state
4. New Master sends gratuitous ARP
5. New Master starts sending advertisements
```

**VRRP vs HSRP Comparison:**

```
┌─────────────────────┬─────────────────┬─────────────────┐
│      Feature        │      VRRP       │      HSRP       │
├─────────────────────┼─────────────────┼─────────────────┤
│ Standard            │ RFC 3768/5798   │ Cisco Proprietary│
│ Multicast Address   │ 224.0.0.18      │ 224.0.0.2       │
│ Virtual MAC         │ 00:00:5E:00:01:XX│ 00:00:0C:07:AC:XX│
│ Priority Range      │ 1-254           │ 0-255            │
│ Default Priority    │ 100             │ 100              │
│ Advertisement Timer │ 1 second        │ 3 seconds        │
│ Preemption          │ Enabled default │ Disabled default │
│ Authentication      │ Simple/MD5      │ Simple/MD5       │
│ Load Balancing      │ No              │ No               │
└─────────────────────┴─────────────────┴─────────────────┘
```

**VRRP Configuration Example:**
```
Router A (Master):
interface GigabitEthernet0/0
 ip address 192.168.1.2 255.255.255.0
 vrrp 1 ip 192.168.1.1
 vrrp 1 priority 200
 vrrp 1 preempt
 vrrp 1 authentication md5 key-string MyKey

Router B (Backup):
interface GigabitEthernet0/0
 ip address 192.168.1.3 255.255.255.0
 vrrp 1 ip 192.168.1.1
 vrrp 1 priority 100
```

#### GLBP (Gateway Load Balancing Protocol)
- **Purpose**: Load balancing First Hop Redundancy Protocol
- **Vendor**: Cisco proprietary
- **Roles**: AVG (Active Virtual Gateway), AVF (Active Virtual Forwarder)
- **Load Balancing**: Round-robin, weighted, host-dependent
- **Virtual MAC**: Up to 4 virtual MAC addresses per group

```
GLBP Operation:
┌─────────────┐              ┌─────────────┐
│   Router A  │              │   Router B  │
│Priority: 200│              │Priority: 100│
│   (AVG)     │              │   (AVF)     │
│Weight: 100  │              │Weight: 50   │
└──────┬──────┘              └──────┬──────┘
       │                            │
       │ GLBP Hello Messages        │
       │ ◄────────────────────────► │
       │                            │
       └────────────┬───────────────┘
                    │
              ┌─────▼─────┐
              │   LAN     │
              │192.168.1.0│
              │    /24    │
              └─────┬─────┘
                    │
         ┌──────────┼──────────┐
         │          │          │
    ┌────▼────┐┌────▼────┐┌────▼────┐
    │ Host 1  ││ Host 2  ││ Host 3  │
    │Gateway: ││Gateway: ││Gateway: │
    │.1 (MAC1)││.1 (MAC2)││.1 (MAC1)│
    └─────────┘└─────────┘└─────────┘

GLBP Load Balancing Methods:
• Round-robin: Distribute equally among forwarders
• Weighted: Based on configured weights
• Host-dependent: Same host always uses same forwarder

GLBP States:
• Disabled: Interface down
• Initial: Starting state
• Listen: Listening for hellos
• Speak: Participating in election
• Standby: Backup AVG
• Active: Active AVG or AVF
```

**GLBP Configuration Example:**
```
Router A:
interface GigabitEthernet0/0
 ip address 192.168.1.2 255.255.255.0
 glbp 1 ip 192.168.1.1
 glbp 1 priority 200
 glbp 1 preempt
 glbp 1 load-balancing weighted
 glbp 1 weighting 100

Router B:
interface GigabitEthernet0/0
 ip address 192.168.1.3 255.255.255.0
 glbp 1 ip 192.168.1.1
 glbp 1 priority 100
 glbp 1 weighting 50
```

**FHRP Comparison Summary:**

```
┌─────────────────────┬─────────────┬─────────────┬─────────────┐
│      Feature        │    HSRP     │    VRRP     │    GLBP     │
├─────────────────────┼─────────────┼─────────────┼─────────────┤
│ Vendor              │ Cisco       │ Standard    │ Cisco       │
│ Load Balancing      │ No          │ No          │ Yes         │
│ Active Routers      │ 1           │ 1           │ Up to 4     │
│ Virtual MAC         │ 1           │ 1           │ Up to 4     │
│ Preemption Default  │ Disabled    │ Enabled     │ Enabled     │
│ Hello Timer         │ 3 seconds   │ 1 second    │ 3 seconds   │
│ Multicast Address   │ 224.0.0.2   │ 224.0.0.18  │ 224.0.0.102 │
└─────────────────────┴─────────────┴─────────────┴─────────────┘
```

### Network Address Translation (NAT)
- **Purpose**: Translates private IP addresses to public IP addresses
- **Types**: Static NAT, Dynamic NAT, PAT (Port Address Translation)
- **Benefits**: IP address conservation, security, flexibility

```
NAT Translation Example:
Private Network                    Public Network
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Host A    │    │ NAT Router  │    │   Internet  │
│192.168.1.10 │    │             │    │             │
│             │    │Inside: .1.1 │    │             │
└──────┬──────┘    │Outside:.2.1 │    └─────────────┘
       │           └──────┬──────┘
       │                  │
       │ Src: 192.168.1.10│ Src: 203.0.113.1
       │ Dst: 8.8.8.8     │ Dst: 8.8.8.8
       │ ────────────────►│ ────────────────►
       │                  │
       │ Src: 8.8.8.8     │ Src: 8.8.8.8
       │ Dst: 192.168.1.10│ Dst: 203.0.113.1
       │ ◄────────────────│ ◄────────────────

NAT Translation Table:
┌─────────────────┬─────────────────┬──────────┐
│  Inside Local   │ Inside Global   │   Port   │
├─────────────────┼─────────────────┼──────────┤
│ 192.168.1.10:80 │ 203.0.113.1:1024│   TCP    │
│ 192.168.1.11:80 │ 203.0.113.1:1025│   TCP    │
└─────────────────┴─────────────────┴──────────┘
```
```

NAT Configuration (Static, Dynamic, PAT):
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip nat inside
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip nat outside

! Static NAT (One-to-One)
Router(config)# ip nat inside source static 192.168.1.10 203.0.113.1

! Dynamic NAT (Many-to-Many)
Router(config)# access-list 1 permit 192.168.1.0 0.0.0.255
Router(config)# ip nat pool MY_POOL 203.0.113.10 203.0.113.20 netmask 255.255.255.0
Router(config)# ip nat inside source list 1 pool MY_POOL

! PAT (Overload - Many-to-One)
Router(config)# ip nat inside source list 1 interface GigabitEthernet0/1 overload
```

### Policy Based Routing (PBR)
- **Purpose**: Route packets based on policies rather than destination
- **Criteria**: Source IP, destination IP, protocol, port, packet size
- **Actions**: Set next-hop, set interface, set IP precedence, drop
- **Use Cases**: Traffic engineering, load balancing, security

### Quality of Service (QoS)
- **Purpose**: Prioritize network traffic based on application requirements
- **Models**: Best Effort, Integrated Services (IntServ), Differentiated Services (DiffServ)
- **Mechanisms**: Classification, marking, queuing, shaping, policing, congestion management

#### QoS Components and Flow

```
QoS Implementation Flow:
┌─────────────┐   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐
│Classification│──►│   Marking   │──►│   Queuing   │──►│ Scheduling  │──►│   Shaping/  │
│             │   │             │   │             │   │             │   │   Policing  │
└─────────────┘   └─────────────┘   └─────────────┘   └─────────────┘   └─────────────┘
      │                   │                   │                   │                   │
      ▼                   ▼                   ▼                   ▼                   ▼
 Identify traffic    Set DSCP/CoS     Place in queues   Service queues    Rate limiting
```

#### 1. Traffic Classification
**Methods:**
- **Access Control Lists (ACLs)**: Match based on L3/L4 headers
- **NBAR (Network-Based Application Recognition)**: Deep packet inspection
- **Trust Boundaries**: Trust existing markings

```
Classification Example:
class-map match-all VOICE
 match protocol rtp audio
 match ip dscp ef

class-map match-all VIDEO
 match protocol http url "*video*"
 match ip dscp af41

class-map match-any CRITICAL_DATA
 match access-group 101
 match protocol tcp port 443
```

#### 2. Traffic Marking
**Layer 2 Marking (CoS - Class of Service):**
- **802.1p**: 3-bit field in 802.1Q header
- **Values**: 0-7 (7 = highest priority)

**Layer 3 Marking (DSCP - Differentiated Services Code Point):**
- **ToS Byte**: 8-bit field in IP header
- **DSCP**: 6 bits (64 possible values)
- **ECN**: 2 bits (Explicit Congestion Notification)

```
DSCP Marking Values:
┌─────────────────┬─────────┬─────────┬─────────────────────────┐
│   Traffic Type  │  DSCP   │ Binary  │       Description       │
├─────────────────┼─────────┼─────────┼─────────────────────────┤
│ Voice           │   EF    │ 101110  │ Expedited Forwarding    │
│ Video           │  AF41   │ 100010  │ Assured Forwarding 4,1  │
│ Critical Data   │  AF31   │ 011010  │ Assured Forwarding 3,1  │
│ Best Effort     │   BE    │ 000000  │ Default/Best Effort     │
│ Scavenger       │   CS1   │ 001000  │ Class Selector 1        │
└─────────────────┴─────────┴─────────┴─────────────────────────┘

Assured Forwarding (AF) Classes:

┌─────────┬─────────┬─────────┬─────────┐
│  Class  │  Low    │ Medium  │  High   │
│         │ Drop    │  Drop   │  Drop   │
|---|---|---|---|
│ AF1x    │  AF11   │  AF12   │  AF13   │
│ AF2x    │  AF21   │  AF22   │  AF23   │
│ AF3x    │  AF31   │  AF32   │  AF33   │
│ AF4x    │  AF41   │  AF42   │  AF43   │
└─────────┴─────────┴─────────┴─────────┘

#### 3. Congestion Management (Queuing)
**Queuing Algorithms:**

**FIFO (First In, First Out):**
- Simple, no prioritization
- Single queue, packets processed in order

**Priority Queuing (PQ):**
- Multiple queues with strict priority
- Higher priority queues always served first
- Risk of starvation for lower priority traffic

**Weighted Fair Queuing (WFQ):**
- Allocates bandwidth based on flow weights
- Prevents single flow from monopolizing bandwidth

**Class-Based Weighted Fair Queuing (CBWFQ):**
- Combines classification with WFQ
- Guarantees minimum bandwidth per class

CBWFQ Configuration:

```
policy-map WAN_POLICY
 class VOICE
  priority percent 20
 class VIDEO
  bandwidth percent 30
 class CRITICAL_DATA
  bandwidth percent 25
 class class-default
  bandwidth percent 25
  fair-queue
```

**Low Latency Queuing (LLQ):**
- Combines CBWFQ with strict priority queue
- Priority queue for delay-sensitive traffic
- Remaining bandwidth shared among other classes

#### 4. Traffic Shaping
**Purpose**: Smooth traffic flow to match available bandwidth
**Method**: Buffer excess traffic and release at configured rate
**Benefits**: Reduces packet loss, smooths bursty traffic


Traffic Shaping Concepts:
```
┌─────────────────────────────────────────────────────────────┐
│                    Token Bucket Algorithm                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│    ┌─────────────┐     Tokens added at CIR rate             │
│    │   Bucket    │ ◄─────────────────────────────           │
│    │  (Bc size)  │                                          │
│    └──────┬──────┘                                          │
│           │                                                 │
│           ▼                                                 │
│    ┌─────────────┐     Packets consume tokens               │
│    │   Packets   │ ────────────────────────►                │
│    │             │                                          │
│    └─────────────┘                                          │
│                                                             │
│ CIR: Committed Information Rate                             │
│ Bc:  Committed Burst Size                                   │
│ Be:  Excess Burst Size                                      │
└─────────────────────────────────────────────────────────────┘
```

Shaping Configuration:
```
policy-map SHAPE_POLICY
 class class-default
  shape average 1000000  ! 1 Mbps
  service-policy WAN_POLICY
```

#### 5. Traffic Policing
**Purpose**: Enforce traffic rate limits by dropping or remarking excess traffic
**Method**: Monitor traffic rate and take action on violations
**Actions**: Drop, remark DSCP, transmit

```
Policing vs Shaping:
┌─────────────────┬─────────────────┬─────────────────┐
│    Feature      │    Policing     │     Shaping     │
├─────────────────┼─────────────────┼─────────────────┤
│ Excess Traffic  │ Drop/Remark     │ Buffer/Delay    │
│ Buffer Usage    │ No buffering    │ Uses buffers    │
│ Latency         │ No added delay  │ Adds delay      │
│ Implementation  │ Any interface   │ Outbound only   │
│ TCP Behavior    │ May cause drops │ TCP-friendly    │
└─────────────────┴─────────────────┴─────────────────┘
```

Policing Configuration:
```
policy-map POLICE_POLICY
 class BULK_DATA
  police cir 500000 bc 10000 be 10000
   conform-action transmit
   exceed-action set-dscp-transmit af11
   violate-action drop
```

#### 6. Congestion Avoidance
**Random Early Detection (RED):**
- Proactively drops packets before queue fills
- Prevents global TCP synchronization
- Uses queue depth to determine drop probability

**Weighted RED (WRED):**
- Applies different drop profiles per traffic class
- Higher priority traffic has higher drop thresholds

```
WRED Operation:
┌─────────────────────────────────────────────────────────────┐
│                    WRED Drop Profile                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ Drop    ▲                                                   │
│ Prob.   │     ┌─────────────────────                        │
│ 100%    │     │                                             │
│         │    /                                              │
│         │   /                                               │
│  50%    │  /                                                │
│         │ /                                                 │
│   0%    └─────────────────────────────────────────────►     │
│         0   Min    Max                            Queue     │
│             Threshold Threshold                   Depth     │
│                                                             │
│ • Below Min: No drops                                       │
│ • Min-Max: Linear increase in drop probability              │
│ • Above Max: Drop all packets                               │
└─────────────────────────────────────────────────────────────┘
```
```
WRED Configuration:
policy-map WRED_POLICY
 class BULK_DATA
  bandwidth percent 50
  random-detect dscp-based
  random-detect dscp af11 20 40 10
  random-detect dscp af12 15 30 10
```

#### 7. QoS Models Comparison
┌─────────────────┬─────────────────┬─────────────────┬─────────────────┐
│     Model       │  Best Effort    │    IntServ      │    DiffServ     │
├─────────────────┼─────────────────┼─────────────────┼─────────────────┤
│ Complexity      │ Simple          │ Complex         │ Moderate        │
│ Scalability     │ High            │ Low             │ High            │
│ State Info      │ None            │ Per-flow        │ Per-class       │
│ Signaling       │ None            │ RSVP            │ None            │
│ Granularity     │ None            │ Per-flow        │ Per-class       │
│ Deployment      │ Universal       │ Limited         │ Widespread      │
└─────────────────┴─────────────────┴─────────────────┴─────────────────┘

#### 8. QoS Best Practices
- **Trust Boundaries**: Set at network edge, verify markings
- **Classification**: Use NBAR for application recognition
- **Voice Traffic**: Use strict priority queue, limit to 33% of bandwidth
- **Video Traffic**: Use guaranteed bandwidth, allow bursting
- **Scavenger Class**: For unwanted traffic (P2P, gaming)
- **Monitoring**: Use QoS statistics to verify policy effectiveness

### SD-WAN (Software-Defined Wide Area Network)
- **Purpose**: Centralized control and management of WAN connections
- **Benefits**: Cost reduction, improved performance, simplified management
- **Components**: SD-WAN edge devices, controllers, orchestrators
- **Features**: Dynamic path selection, application-aware routing, centralized policies

<br>&nbsp;
## Layer 4

### TCP Protocol

*1. Header Structure:*

TCP Header (20-60 bytes):
```
┌─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┐
│                Source Port              │              Destination Port           │
│                (16 bits)                │                (16 bits)                │
├───────────────────────────────────────────────────────────────────────────────────┤
│                                   Sequence Number                                 │
│                                     (32 bits)                                     │
├───────────────────────────────────────────────────────────────────────────────────┤
│                                 Acknowledgment Number                             │
│                                     (32 bits)                                     │
├─────────────┬─────────────┬─────────────┬─────────────┬─────────────┬─────────────┤
│ Data Offset │  Reserved   │   Flags     │                Window Size              │
│  (4 bits)   │  (4 bits)   │  (8 bits)   │                (16 bits)                │
├─────────────┼─────────────┼─────────────┴─────────────┴─────────────┴─────────────┤
│                Checksum                 │              Urgent Pointer             │
│               (16 bits)                 │               (16 bits)                 │
├───────────────────────────────────────────────────────────────────────────────────┤
│                    Options (0-320 bits, if Data Offset > 5)                       │
│                         + Padding to 32-bit boundary                              │
└───────────────────────────────────────────────────────────────────────────────────┘
```
TCP Flags (8 bits):
```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ CWR │ ECE │ URG │ ACK │ PSH │ RST │ SYN │ FIN │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘

Flag Meanings:
• CWR: Congestion Window Reduced
• ECE: ECN-Echo (Explicit Congestion Notification)
• URG: Urgent pointer field is significant
• ACK: Acknowledgment field is significant
• PSH: Push function (deliver data immediately)
• RST: Reset the connection
• SYN: Synchronize sequence numbers
• FIN: No more data from sender
```

![](https://github.com/ravikumark815/notes/blob/main/images/tcp-header.png)
- `Source Port` (16 bits)
- `Destination Port` (16 bits)
- `Sequence No` (32 bits): Is SYN is set, this is the initial sequence no. Else, it is the accumulated sequence number. 
- `Acknowledgement No` (32 bits): If ACK is set, then it is the next sequence no that sender expects. It also shows no of bytes received. 
- `Data Offset` (4 bits): Specifies the size of TCP header so that we can know where actual data starts. 
- `Reserved` (4 bits)
- `Flags:` 
    - `CWR` [Congestion Window Reduced]: indicates that a TCP segement with ECE flag set is received
    - `ECE` [ECN-Echo]: 
        - If SYN is set: indicates peer is ECN capable
        - Else indicates network congestion
    - `URG` [Urgent]
    - `ACK` [Acknowledgement]
    - `PSH` [Push]: Push the buffered data to receiving application
    - `RST` [Reset]
    - `SYN` [Synchronize] sequence numbers. Only first packet should have it set
    - `FIN` [Final] Last packet from sender
- `Window` (16 bits): The size of the receive window
- `Checksum` (16 bits): Used for error-checking of TCP header. 
- `Urgent Pointer` (16 bits): If URG is set, then it is an offset from the dequence no indicating the last urgent data byte
- `Options` (0-320 bits, in units of 32 bits): 

*2. TCP Connection Establishment [3-Way Handshake]*

![](https://github.com/ravikumark815/notes/blob/main/images/3-way.png)

```
┌─────────────┐                                    ┌─────────────┐
│   Client    │                                    │   Server    │
│             │                                    │             │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. SYN                                           │
       │ SYN=1, Seq=A (Random: 1000)                      │
       │ ──────────────────────────────────────────────►  │
       │                                                  │ LISTEN → SYN_RCVD
       │ 2. SYN-ACK                                       │
       │ SYN=1, ACK=1, Seq=B (Random: 2000), Ack=A+1      │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
SYN_SENT → ESTABLISHED                                    │
       │ 3. ACK                                           │
       │ ACK=1, Seq=A+1 (1001), Ack=B+1 (2001)            │
       │ ──────────────────────────────────────────────►  │
       │                                                  │ SYN_RCVD → ESTABLISHED
       │ 4. Data Transfer                                 │
       │ ◄──────────────────────────────────────────────  │
       │ ──────────────────────────────────────────────►  │
       │                                                  │

TCP States:
Client: CLOSED → SYN_SENT → ESTABLISHED
Server: CLOSED → LISTEN → SYN_RCVD → ESTABLISHED
```

- `SYN`: Client sends a TCP segment with SYN=1 Sequence_No=A (Random)
- `SYN-ACK`: Server responds: SYN=1 ACK=1 Sequence_Mo=B (Random) Ack_No=A+1
- `ACK`: Client sends: ACK=1 Sequence_No=A+1 Ack No=B+1

*3. TCP Connection Termination [4-Way Handshake]*

![](https://github.com/ravikumark815/notes/blob/main/images/4-way.png)

```
┌─────────────┐                                    ┌─────────────┐
│   Client    │                                    │   Server    │
│ (Initiator) │                                    │ (Responder) │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. FIN                                           │
       │ FIN=1, Seq=X                                     │
       │ ──────────────────────────────────────────────►  │
       │                                                  │ ESTABLISHED → CLOSE_WAIT
ESTABLISHED → FIN_WAIT_1                                  │
       │ 2. ACK                                           │
       │ ACK=1, Ack=X+1                                   │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
FIN_WAIT_1 → FIN_WAIT_2                                   │
       │                                                  │ (Server can still send data)
       │ 3. FIN                                           │
       │ FIN=1, Seq=Y                                     │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │ CLOSE_WAIT → LAST_ACK
FIN_WAIT_2 → TIME_WAIT                                    │
       │ 4. ACK                                           │
       │ ACK=1, Ack=Y+1                                   │
       │ ──────────────────────────────────────────────►  │
       │                                                  │ LAST_ACK → CLOSED
       │ (2MSL Timer: 2 × Maximum Segment Lifetime)       │
TIME_WAIT → CLOSED                                        │

TCP States During Termination:
Initiator: ESTABLISHED → FIN_WAIT_1 → FIN_WAIT_2 → TIME_WAIT → CLOSED
Responder: ESTABLISHED → CLOSE_WAIT → LAST_ACK → CLOSED

Why 4-Way? TCP is full-duplex, each direction must be closed separately.
```

- `FIN`: Initiator sends a TCP segment with FIN=1 FIN_WAIT_1 timer started
- `ACK`: Responder to Initiator: ACK=1 CLOSE_WAIT timer started
- `FIN`: Responder to Initiator: FIN=1
- `ACK`: Initiator to Responder: Timer closed and connection terminated

*4. Features/Functions:*
-  Segment Numbering System:
<br>&nbsp; • Byte numbers assigned to data bytes.
<br>&nbsp; • Sequence numbers assigned to Segments.
<br>&nbsp; • Acknowledgement numbers assigned to received segments.
-  Connection Oriented: Order of data is maintained.
-  Full Duplex
-  Flow Control:
<br>&nbsp; • Limits the rate at which data transfers.
<br>&nbsp; • Sliding Window: How much data can be transferred in next segment?
-  Error Control: Detects
<br>&nbsp; • Corrupted segments
<br>&nbsp; • Lost Segments
<br>&nbsp; • Out of Order segments
<br>&nbsp; • Duplicate Segments
-  Congestion Control:
<br>&nbsp; • Amount of data sent by sender is variating.
-  Past Recovery: When there is packet loss:
<br>&nbsp; • Reduce Control Window Size by 50%
<br>&nbsp; • Reduce Sesson threshold by 50% of control window.
<br>&nbsp; • Retransmit lost packet.
<br>&nbsp; • Half window of silence
<br>&nbsp; • Maintain inflight = cwnd until new ACK arrives at sender
-  Improvisation Techniques: Due to half window of silence there’s underutilization of network resources.
<br>&nbsp; • Improve inflight data by using SACK (Selective Acknowledgement <br>&nbsp; • Knowledge of gaps in receive buffer). 
<br>&nbsp; • Rate halving technique.
<br>&nbsp; • Proportional rate reduction.

*5. TCP Timers:*
- **Round Trip Time (RTT):** Time required for segment to reach destination and be acknowledged. 
- **Retransmission Time Out (RTO):** Starts when segment is sent and stops when ACK is received. If it crosses RTT, segment retransmitted.
- **Persistent Timer:** To deal with zero-window-size deadlock situation, this timer is set to probe a segment with only 1 byte of data and sent to cause resend from server. 
- **Keep Alive Timer:** To prevent long idle connection between two TCP nodes. Usually, its 2 hrs and then, 10 probes of 75 sec intervals are sent. 
- **Time Wait Timer:** Used during connection termination. Refer 4-way handshake.

```
Maximum Segment Size: 1460B
Maximum Datagram Size: 1480B
Maximum Transaction Unit: 1500B
```

### UDP Protocol

*1. Header Structure:*

```
UDP Header (8 bytes - Fixed Size):
┌─────────────────────────────────────┬─────────────────────────────────────┐
│            Source Port              │         Destination Port            │
│            (16 bits)                │            (16 bits)                │
├─────────────────────────────────────┼─────────────────────────────────────┤
│             Length                  │            Checksum                 │
│            (16 bits)                │            (16 bits)                │
└─────────────────────────────────────┴─────────────────────────────────────┘
│◄─────────────────── 8 bytes total ──────────────────────►│

Field Details:
• Source Port: Sending application port (0-65535)
• Destination Port: Receiving application port (0-65535)
• Length: UDP header + data length (minimum 8 bytes)
• Checksum: Error detection (optional in IPv4, mandatory in IPv6)
```

![](https://github.com/ravikumark815/notes/blob/main/images/udp-header.png)

*2. UDP Characteristics:*
- **Connectionless**: No connection establishment required
- **Unreliable**: No guarantee of delivery, ordering, or duplicate protection
- **Fast**: Minimal overhead compared to TCP
- **Stateless**: Each datagram is independent
- **No Flow Control**: No mechanism to control data flow rate
- **No Congestion Control**: No network congestion management

*3. UDP vs TCP Comparison:*

```
┌─────────────────────┬─────────────────┬─────────────────┐
│      Feature        │       TCP       │       UDP       │
├─────────────────────┼─────────────────┼─────────────────┤
│ Connection          │ Connection-based│ Connectionless  │
│ Reliability         │ Reliable        │ Unreliable      │
│ Ordering            │ Ordered         │ No ordering     │
│ Error Detection     │ Yes + Recovery  │ Detection only  │
│ Flow Control        │ Yes             │ No              │
│ Congestion Control  │ Yes             │ No              │
│ Header Size         │ 20-60 bytes     │ 8 bytes (fixed) │
│ Speed               │ Slower          │ Faster          │
│ Use Cases           │ Web, Email, FTP │ DNS, DHCP, VoIP │
└─────────────────────┴─────────────────┴─────────────────┘
```

*4. Common UDP Applications:*
- **DNS (Port 53)**: Domain name resolution
- **DHCP (Port 67/68)**: IP address assignment
- **SNMP (Port 161/162)**: Network management
- **TFTP (Port 69)**: Trivial file transfer
- **NTP (Port 123)**: Time synchronization
- **VoIP/RTP**: Real-time audio/video
- **Online Gaming**: Low-latency gaming protocols
- **Streaming Media**: Live video/audio streaming

*5. UDP Pseudo Header (for Checksum Calculation):*

```
IPv4 Pseudo Header:
┌─────────────────────────────────────────────────────────────┐
│                    Source IP Address                        │
│                      (32 bits)                              │
├─────────────────────────────────────────────────────────────┤
│                 Destination IP Address                      │
│                      (32 bits)                              │
├─────────────────────┬───────────────────┬───────────────────┤
│      Reserved       │     Protocol      │    UDP Length     │
│      (8 bits)       │     (8 bits)      │    (16 bits)      │
│        0x00         │       0x11        │                   │
└─────────────────────┴───────────────────┴───────────────────┘
```

## Layer 7

### Dynamic Host Configuration Protocol [DHCP]
- Used to manage IP allocation in a network
- **DHCP DORA Process:**
    ![](https://github.com/ravikumark815/notes/blob/main/images/dhcp-dora.png)

```
DHCP DORA Process (Discover, Offer, Request, Acknowledge):

┌─────────────┐                                    ┌─────────────┐
│   Client    │                                    │ DHCP Server │
│ (No IP yet) │                                    │192.168.1.1  │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. DHCP DISCOVER (Broadcast)                     │
       │ Src: 0.0.0.0:68  Dst: 255.255.255.255:67         │
       │ MAC: Client MAC, Transaction ID: 0x12345678      │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ 2. DHCP OFFER (Broadcast)                        │
       │ Src: 192.168.1.1:67  Dst: 255.255.255.255:68     │
       │ Offered IP: 192.168.1.100                        │
       │ Subnet: 255.255.255.0, Gateway: 192.168.1.1      │
       │ DNS: 8.8.8.8, Lease: 24 hours                    │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
       │ 3. DHCP REQUEST (Broadcast)                      │
       │ Src: 0.0.0.0:68  Dst: 255.255.255.255:67         │
       │ Requested IP: 192.168.1.100                      │
       │ Server ID: 192.168.1.1                           │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ 4. DHCP ACK (Unicast)                            │
       │ Src: 192.168.1.1:67  Dst: 192.168.1.100:68       │
       │ Confirmed IP: 192.168.1.100                      │
       │ Lease confirmed for 24 hours                     │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
   ┌───▼────┐
   │ Client │ Now has IP: 192.168.1.100
   │ Config │ Subnet: 255.255.255.0
   │        │ Gateway: 192.168.1.1
   │        │ DNS: 8.8.8.8
   └────────┘

Message Types:
• DISCOVER: Client broadcasts to find DHCP servers
• OFFER: Server offers IP configuration to client  
• REQUEST: Client requests specific IP from chosen server
• ACK: Server confirms IP lease to client
• NACK: Server denies IP request
• RELEASE: Client releases IP back to server
• RENEW: Client renews existing lease
```
    
    - `DISCOVER` [Broadcast]: The client sends a DISCOVER in broadcast to all servers in the subnet.
    - `OFFER` [Broadcast]: Every server in the subnet sends an OFFER with the offered configuration to the client. 
    - `REQUEST` [Broadcast]: The client selects one of the offered configurations and then sends a REQUEST. Broadcast is sent so that all servers receive the message, even to those that do not offer the accepted configuration. This allows servers to flush this offer from memory.
    - `ACK` [Unicast]: The server that receives the REQUEST checks if that configuration belongs to it. And if it is so, send an ACK message to confirm the lease.

- Packet Flow with Relay agent:
    - `DISCOVER`: The client sends a DISCOVER in broadcast. The relay agent receives the message and forwards it to the server, which is in a different subnet, in unicast. 
    - `OFFER`: The server sends an OFFER in unicast to the address. The relay agent receives the message and forwards it to the client in broadcast.
    - `REQUEST`: The client selects one of the offered configurations and then sends a REQUEST in broadcast. The relay agent receives the message and forwards it to the server, which is in a different subnet, in unicast.
    - `ACK`: The server that receives the REQUEST checks if that configuration belongs to it. And if it is so, send an ACK in unicast to the address. The relay agent receives the message and forwards it to the client in broadcast.

- Other DHCP Messages:
    - `DHCP NACK`: Negative Acknowledgement. Whenever a DHCP server receives a request for an IP address that is invalid according to the scopes that are configured, it sends a DHCP NACK message to the client. 
    - `DHCP Decline`: If the DHCP client determines the offered configuration parameters are different or invalid, it sends a DHCP decline message to the server. When there is a reply to the gratuitous ARP by any host to the client, the client sends a DHCP decline message to the server showing the offered IP address is already in use.
    - `DHCP Release`: A DHCP client sends a DHCP release packet to the server to release the IP address and cancel any remaining lease time.

- Common DHCP Options:
    - `DHCP option 1`: subnet mask to be applied on the interface asking for an IP address.
    - `DHCP option 3`: default router or last resort gateway for this interface
    - `DHCP option 6`: which DNS to include in the IP configuration for name resolution.
    - `DHCP option 51`: lease time for this IP address
    - `DHCP option 2`: time offset in seconds from UTC to be applied on the current time.
    - `DHCP option 4`: list of time server
    - `DHCP option 12`: host name of the client, very useful for IoT and any device without user
    - `DHCP option 121`: classless static route table composed of multiple network and subnet mask.

```
DHCP Server Configuration:
Router(config)# ip dhcp pool LAN_POOL
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# lease 7

! DHCP Excluded Addresses (Reserve IPs)
Router(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10

! DHCP Relay Agent (on interface facing client)
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip helper-address 10.0.0.1
```

### Domain Name Server [DNS]:
- DNS is a hierarchical distributed naming system that translates human-readable domain names to IP addresses
- Port: `53 UDP` (primary), `53 TCP` (zone transfers, large responses)
- **DNS Hierarchy**: Root (.) → TLD (.com, .org) → Second-level (google.com) → Subdomain (www.google.com)

- **DNS Components:**
    - **DNS Resolver**: Client-side component that initiates queries
    - **Recursive Resolver**: ISP/organization DNS server that performs full resolution
    - **Root Name Servers**: 13 logical servers (A-M) that know TLD servers
    - **TLD Servers**: Manage top-level domains (.com, .org, .net, country codes)
    - **Authoritative Servers**: Hold actual DNS records for domains
- DNS Lookup:
    - Local DNS Resolver/Cache
    - Root DNS server
    - Top-Level Domain Server (TLD)
    - Authoritative DNS Server/Recursive DNS Server
    - Web Server
- DNS Record: Instructions that live in authoritative DNS servers and provide info about domain including IP address, how to handle requests to that domain. Common Types:
    |   |   |   |
    |---|---|---|
    A	    | 1	|   IPv4Address record
    AAAA	|28|	IPv6 address record
    CAA	    |257|	Certification Authority Authorization
    CERT	|37|	Certificate record
    CNAME	|5|	    Canonical name record
    HTTPS	|65|	HTTPS Binding
    IPSECKEY|45|	IPsec Key
    MX	    |15|	Mail exchange record
    NS	    |2|	    Name server record
    PTR	    |12|	PTR Resource Record
    SOA	    |6|	    Start of [a zone of] authority record
    TXT	    |16|	Text record
    URI	    |256|	Uniform Resource Identifier
    
- Types of Queries:
    - `Recursive Query`: In this query, if the resolver is unable to find the record, in that case, DNS client wants the DNS Server will respond to the client in any way like with the requested source record or an error message.
    - `Iterative Query`: Iterative Query is the query in which DNS Client wants the best answer possible from the DNS Server.
    - `Non-Recursive Query`: Non-Recursive Query is the query that occurs when a DNS Resolver queries a DNS Server for some record that has access to it because of the record that exists in its cache.

![](https://github.com/ravikumark815/notes/blob/main/images/dns-query.png)

### Access Control Lists (ACLs)
- **Purpose**: Filter network traffic based on rules
- **Types**: Standard (1-99) and Extended (100-199)
- **Implicit Deny**: All ACLs have an invisible "deny all" at the end

```
ACL Configuration (Standard & Extended):
! Standard ACL (Source IP only)
Router(config)# access-list 10 permit 192.168.1.0 0.0.0.255
Router(config)# access-list 10 deny any

! Apply Standard ACL
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip access-group 10 out

! Extended ACL (Source, Dest, Protocol, Port)
Router(config)# access-list 100 permit tcp 192.168.1.0 0.0.0.255 host 10.0.0.1 eq 80
Router(config)# access-list 100 deny ip any any

! Apply Extended ACL
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip access-group 100 in
```

### Internet Protocol Security [IPsec]
- Security:
    - Confidentiality: by encrypting our data, nobody except the sender and receiver will be able to read our data.
    - Integrity: we want to make sure that nobody changes the data in our packets. By calculating a hash value, the sender and receiver will be able to check if changes have been made to the packet.
    - Authentication: the sender and receiver will authenticate each other to make sure that we are really talking with the device we intend to.
    - Anti-replay: even if a packet is encrypted and authenticated, an attacker could try to capture these packets and send them again. By using sequence numbers, IPsec will not transmit any duplicate packets.

- Internet Key Exchange [IKE] is used to establish an IPsec tunnel in two phases
    - IKE Phase 1:
        1. Negotiation:
            - Hashing: MD5/SHA
            - Authentication: Shared Key/Digital Certificates
            - DH group: To determine strength of the key being used. 
            - Lifetime: Duration of the tunnel
            - Encryption: DES, 3DES, AES
        2. DH Key Exchange: Once Negotiation succeeds, peers use DH Group to exchange keying material. End result: Both peers will have a shared key
        3. Authentiation: Peers will authenticate using the method negotiated earlier. Finally we have a ISAKMP (Internet Security Association and Key Management Protocol) session established. 
    - IKE Phase 2

- IKE Phase 1 can be completed in 2 modes:
    - Main Mode:
    - Aggressive Mode:

![](https://github.com/ravikumark815/notes/blob/main/images/IKE-phase1-main.png)

![](https://github.com/ravikumark815/notes/blob/main/images/IKE-phase2-quick.png)

### Secure Sockets Layer [SSL] / Transport Level Security [TLS]:
1. Client Hello
    - The client initiates communication with a CLIENT HELLO message, providing:
        - SSL/TLS Protocol Version
        - Session ID
        - List of Cipher Suites
        - List of CLIENT HELLO Extensions
2. Server Hello
    - The server checks the provided protocol version and cipher suites for compatibility.
    - It responds with a SERVER HELLO message, containing:
        - Chosen SSL/TLS Protocol Version
        - Selected Cipher Suite
        - Server Certificate (without private key)
        - List of SERVER HELLO Extensions
3. Server Authentication (Client Validates Server Certificate)
    - The client verifies the server’s certificate by checking:
        - Validity period
        - Trusted Certificate Authority (CA)
        - Issuer’s digital signature validation
        - Domain name match
4. Key Exchange & Session Establishment
    - The client:
        - Generates a pre-master secret
        - Encrypts it using the server’s public key
        - Sends it to the server
    - The server:
        - Decrypts the pre-master secret using its private key
        - Uses it to derive the master secret
    - Both client and server generate session keys from the master secret
5. Secure Communication Begins
    - Both parties exchange a final handshake message to indicate that:
        - Future communication will be encrypted
        - Handshake is complete
    - The SSL session starts with encrypted communication using session keys.

![](https://github.com/ravikumark815/notes/blob/main/images/SSL-handshake.png)

### HyperText Transfer Protocol [HTTP]
- Application layer protocol for distributed, collaborative, hypermedia information systems
- Port: `80 TCP`
- Stateless protocol: Each request is independent, no session state maintained
- Request-Response model: Client sends request, server sends response

- **HTTP Methods:**
    |Method|Purpose|Idempotent|Safe|
    |---|---|---|---|
    |GET|Retrieve data|Yes|Yes|
    |POST|Submit data|No|No|
    |PUT|Update/Create resource|Yes|No|
    |DELETE|Remove resource|Yes|No|
    |HEAD|Get headers only|Yes|Yes|
    |OPTIONS|Get allowed methods|Yes|Yes|
    |PATCH|Partial update|No|No|

- **HTTP Status Codes:**
    |Code Range|Category|Common Examples|
    |---|---|---|
    |1xx|Informational|100 Continue, 101 Switching Protocols|
    |2xx|Success|200 OK, 201 Created, 204 No Content|
    |3xx|Redirection|301 Moved Permanently, 302 Found, 304 Not Modified|
    |4xx|Client Error|400 Bad Request, 401 Unauthorized, 404 Not Found|
    |5xx|Server Error|500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable|

- **HTTP Headers:**
    - `Content-Type`: MIME type of request/response body
    - `Content-Length`: Size of request/response body in bytes
    - `User-Agent`: Client application information
    - `Accept`: Media types client can process
    - `Authorization`: Authentication credentials
    - `Cache-Control`: Caching directives
    - `Cookie`: Client-stored data sent to server
    - `Set-Cookie`: Server instruction to store data on client

- **HTTP Versions:**
    - `HTTP/1.0`: Basic functionality, connection per request
    - `HTTP/1.1`: Persistent connections, chunked encoding, host header
    - `HTTP/2`: Multiplexing, server push, header compression
    - `HTTP/3`: QUIC transport, improved performance over UDP

- **HTTP Request/Response Flow:**
```
┌─────────────┐                                    ┌─────────────┐
│   Client    │                                    │   Server    │
│ (Browser)   │                                    │ (Web Server)│
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. HTTP Request                                  │
       │ GET /index.html HTTP/1.1                         │
       │ Host: www.example.com                            │
       │ User-Agent: Mozilla/5.0                          │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ 2. HTTP Response                                 │
       │ HTTP/1.1 200 OK                                  │
       │ Content-Type: text/html                          │
       │ Content-Length: 1234                             │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
       │ 3. HTML Content                                  │
       │ <html><body>...</body></html>                    │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
```

### HyperText Transfer Protocol Secure [HTTPS]
- HTTP over TLS/SSL encryption
- Port: `443 TCP`
- Provides: Confidentiality, Integrity, Authentication

- **HTTPS Handshake Process:**
    1. **TCP Handshake**: Establish TCP connection on port 443
    2. **TLS Handshake**: 
        - Client Hello (supported cipher suites, TLS version)
        - Server Hello (chosen cipher suite, certificate)
        - Certificate verification by client
        - Key exchange (pre-master secret)
        - Session key derivation
        - Finished messages
    3. **Encrypted HTTP Communication**: All HTTP traffic encrypted with session keys

- **Certificate Validation:**
    - Certificate Authority (CA) signature verification
    - Certificate validity period check
    - Domain name matching
    - Certificate chain validation
    - Certificate Revocation List (CRL) or OCSP check

- **Security Benefits:**
    - **Confidentiality**: Data encrypted in transit
    - **Integrity**: Data tampering detection
    - **Authentication**: Server identity verification
    - **Non-repudiation**: Digital signatures prevent denial

- **HTTPS Connection Flow:**
```
┌─────────────┐                                    ┌─────────────┐
│   Client    │                                    │   Server    │
│ (Browser)   │                                    │ (Web Server)│
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. TCP Handshake (Port 443)                      │
       │ ──────────────────────────────────────────────►  │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
       │ 2. TLS Handshake                                 │
       │ Client Hello (cipher suites, TLS version)        │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ Server Hello + Certificate                       │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
       │ 3. Certificate Verification                      │
       │ (Check CA, validity, domain)                     │
       │                                                  │
       │ 4. Key Exchange                                  │
       │ Pre-master secret (encrypted with server pubkey) │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ 5. Session Keys Derived                          │
       │ Both sides generate session keys                 │
       │                                                  │
       │ 6. Encrypted HTTP Communication                  │
       │ 🔒 GET /secure-page HTTP/1.1 🔒                 │
       │ ──────────────────────────────────────────────►  │
       │ 🔒 HTTP/1.1 200 OK + Encrypted Content 🔒       │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
```

### Simple Mail Transfer Protocol [SMTP]
- Protocol for sending email messages between servers
- Ports: `25 TCP` (plain), `587 TCP` (TLS), `465 TCP` (SSL)
- Store-and-forward mechanism
- Text-based protocol with command-response structure

- **SMTP Commands:**
    |Command|Purpose|Example|
    |---|---|---|
    |HELO/EHLO|Identify client to server|EHLO mail.example.com|
    |MAIL FROM|Specify sender|MAIL FROM:<sender@example.com>|
    |RCPT TO|Specify recipient|RCPT TO:<recipient@example.com>|
    |DATA|Begin message content|DATA|
    |QUIT|End session|QUIT|
    |RSET|Reset session|RSET|
    |VRFY|Verify email address|VRFY user@example.com|

- **SMTP Response Codes:**
    |Code|Category|Meaning|
    |---|---|---|
    |2xx|Success|Command completed successfully|
    |3xx|Intermediate|More information needed|
    |4xx|Transient Error|Temporary failure, retry later|
    |5xx|Permanent Error|Command failed, don't retry|

- **Email Flow:**
    1. **Mail User Agent (MUA)** → **Mail Transfer Agent (MTA)**
    2. **MTA** → **Mail Transfer Agent** (recipient's server)
    3. **MTA** → **Mail Delivery Agent (MDA)**
    4. **MDA** stores in mailbox
    5. **Mail User Agent** retrieves via POP3/IMAP

- **SMTP Email Delivery Process:**
```
┌─────────────┐    SMTP     ┌─────────────┐    SMTP     ┌─────────────┐
│   Sender    │   Port 25   │   Sender    │   Port 25   │ Recipient   │
│     MUA     │   587/465   │     MTA     │             │     MTA     │
│ (Outlook)   │ ──────────► │ (mail.com)  │ ──────────► │ (gmail.com) │
└─────────────┘             └─────────────┘             └──────┬──────┘
                                                               │
                            ┌─────────────┐                    │ Local
                            │ Recipient   │                    │ Delivery
                            │     MDA     │ ◄─────────────────-┘
                            │ (Mailbox)   │
                            └──────┬──────┘
                                   │
                            ┌──────▼──────┐
                            │ Recipient   │  POP3/IMAP
                            │     MUA     │  Port 110/993
                            │ (Gmail App) │
                            └─────────────┘

SMTP Commands Flow:
Client                          Server
  │                               │
  │ EHLO client.example.com       │
  │ ────────────────────────────► │
  │ 250 Hello client.example.com  │
  │ ◄──────────────────────────── │
  │                               │
  │ MAIL FROM:<sender@example.com>│
  │ ────────────────────────────► │
  │ 250 OK                        │
  │ ◄──────────────────────────── │
  │                               │
  │ RCPT TO:<recipient@gmail.com> │
  │ ────────────────────────────► │
  │ 250 OK                        │
  │ ◄──────────────────────────── │
  │                               │
  │ DATA                          │
  │ ────────────────────────────► │
  │ 354 Start mail input          │
  │ ◄──────────────────────────── │
  │                               │
  │ Subject: Hello World          │
  │ From: sender@example.com      │
  │ To: recipient@gmail.com       │
  │                               │
  │ Hello, this is a test email.  │
  │ .                             │
  │ ────────────────────────────► │
  │ 250 Message accepted          │
  │ ◄──────────────────────────── │
  │                               │
  │ QUIT                          │
  │ ────────────────────────────► │
  │ 221 Bye                       │
  │ ◄──────────────────────────── │
```

- **SMTP Authentication (SMTP-AUTH):**
    - LOGIN: Base64 encoded username/password
    - PLAIN: Base64 encoded null-separated credentials
    - CRAM-MD5: Challenge-response authentication
    - OAUTH2: Token-based authentication

### File Transfer Protocol [FTP]
- Protocol for transferring files between client and server
- Ports: `21 TCP` (control), `20 TCP` (data)
- Two separate connections: Control and Data
- Text-based command protocol

- **FTP Connection Modes:**
    - **Active Mode:**
        - Client connects to server port 21 (control)
        - Server connects back to client for data transfer
        - Firewall issues: Server initiates data connection
    - **Passive Mode:**
        - Client connects to server port 21 (control)
        - Client initiates data connection to server
        - Firewall-friendly: Client initiates both connections

- **FTP Active vs Passive Mode:**
```
ACTIVE MODE:
┌─────────────┐                                    ┌─────────────┐
│   Client    │                                    │ FTP Server  │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. Control Connection (Port 21)                  │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ 2. PORT command (client IP:port)                 │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ 3. Data Connection (Port 20 → Client Port)       │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
       │ 4. File Transfer                                 │
       │ ◄──────────────────────────────────────────────  │

PASSIVE MODE:
┌─────────────┐                                    ┌─────────────┐
│   Client    │                                    │ FTP Server  │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. Control Connection (Port 21)                  │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ 2. PASV command                                  │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ 3. Server responds with IP:port                  │
       │ ◄──────────────────────────────────────────────  │
       │                                                  │
       │ 4. Data Connection (Client → Server Port)        │
       │ ──────────────────────────────────────────────►  │
       │                                                  │
       │ 5. File Transfer                                 │
       │ ──────────────────────────────────────────────►  │

Firewall Considerations:
Active Mode:  ❌ Server initiates connection to client (blocked by firewall)
Passive Mode: ✅ Client initiates both connections (firewall-friendly)
```

- **FTP Commands:**
    |Command|Purpose|Example|
    |---|---|---|
    |USER|Specify username|USER anonymous|
    |PASS|Specify password|PASS guest@example.com|
    |PWD|Print working directory|PWD|
    |CWD|Change working directory|CWD /pub|
    |LIST|List directory contents|LIST|
    |RETR|Download file|RETR filename.txt|
    |STOR|Upload file|STOR filename.txt|
    |DELE|Delete file|DELE filename.txt|
    |MKD|Make directory|MKD newfolder|
    |RMD|Remove directory|RMD oldfolder|
    |QUIT|End session|QUIT|

- **FTP Response Codes:**
    |Code|Category|Examples|
    |---|---|---|
    |1xx|Positive Preliminary|150 File status okay|
    |2xx|Positive Completion|200 Command okay, 226 Transfer complete|
    |3xx|Positive Intermediate|331 User name okay, need password|
    |4xx|Transient Negative|425 Can't open data connection|
    |5xx|Permanent Negative|550 File not found|

- **Secure FTP Alternatives:**
    - **FTPS**: FTP over SSL/TLS (ports 990, 21)
    - **SFTP**: SSH File Transfer Protocol (port 22)
    - **SCP**: Secure Copy Protocol (port 22)

### Simple Network Management Protocol (SNMP)
- **Purpose**: Network monitoring, management, and configuration
- **Ports**: 161 UDP (agent), 162 UDP (manager/traps)
- **Architecture**: Manager-Agent model
- **Versions**: SNMPv1, SNMPv2c, SNMPv3
- **Transport**: UDP (primarily), TCP (for large data transfers)

#### SNMP Components:
- **SNMP Manager (NMS)**: Network Management System that queries agents
- **SNMP Agent**: Software running on managed devices
- **Management Information Base (MIB)**: Hierarchical database of manageable objects
- **Object Identifier (OID)**: Unique dotted decimal identifier for each object

#### SNMP Versions Comparison:

```
┌─────────────────┬─────────────┬─────────────┬─────────────┐
│    Feature      │   SNMPv1    │   SNMPv2c   │   SNMPv3    │
├─────────────────┼─────────────┼─────────────┼─────────────┤
│ Security        │ Community   │ Community   │ User-based  │
│ Authentication  │ Plain text  │ Plain text  │ MD5/SHA     │
│ Encryption      │ None        │ None        │ DES/AES     │
│ Error Handling  │ Basic       │ Enhanced    │ Enhanced    │
│ Bulk Operations │ No          │ GetBulk     │ GetBulk     │
│ 64-bit Counters │ No          │ Yes         │ Yes         │
│ Inform Messages │ No          │ Yes         │ Yes         │
└─────────────────┴─────────────┴─────────────┴─────────────┘
```

#### SNMP Operations:
1. **GET**: Retrieve single OID value
2. **GET-NEXT**: Retrieve next OID in MIB tree
3. **GET-BULK**: Retrieve multiple OIDs (v2c/v3 only)
4. **SET**: Modify OID value
5. **TRAP**: Unsolicited notification from agent
6. **INFORM**: Acknowledged notification (v2c/v3 only)

#### MIB Structure:
```
MIB Tree Hierarchy:
                    root
                     │
            ┌────────┼────────┐
            │        │        │
          iso(1)   itu-t(0)  joint(2)
            │
         org(3)
            │
         dod(6)
            │
       internet(1)
            │
    ┌───────┼───────┐
    │       │       │
 mgmt(2) private(4) experimental(3)
    │       │
  mib-2(1) enterprise(1)
    │       │
┌───┼───┐   └─ cisco(9)
│   │   │      │
│   │   │   ┌──┼──┐
│   │   │   │  │  │
│   │   │ local(2) temporary(3)
│   │   │
│   │ interfaces(2)
│   │   │
│   │ ifTable(2)
│   │   │
│   │ ifEntry(1)
│   │   │
│   │ ifDescr(2)
│   │
│ system(1)
│   │
│ sysDescr(1) → OID: 1.3.6.1.2.1.1.1.0
│ sysObjectID(2)
│ sysUpTime(3)
│ sysContact(4)
│ sysName(5)
│ sysLocation(6)
```

#### Common MIB Objects:

```
┌─────────────────────┬─────────────────────────┬─────────────────────────┐
│        OID          │       Object Name       │      Description        │
├─────────────────────┼─────────────────────────┼─────────────────────────┤
│ 1.3.6.1.2.1.1.1.0   │ sysDescr               │ System description      │
│ 1.3.6.1.2.1.1.3.0   │ sysUpTime              │ System uptime           │
│ 1.3.6.1.2.1.1.5.0   │ sysName                │ System name             │
│ 1.3.6.1.2.1.2.1.0   │ ifNumber               │ Number of interfaces    │
│ 1.3.6.1.2.1.2.2.1.2 │ ifDescr                │ Interface description   │
│ 1.3.6.1.2.1.2.2.1.8 │ ifOperStatus           │ Interface status        │
│ 1.3.6.1.2.1.2.2.1.10│ ifInOctets             │ Input bytes counter     │
│ 1.3.6.1.2.1.2.2.1.16│ ifOutOctets            │ Output bytes counter    │
│ 1.3.6.1.2.1.4.1.0   │ ipForwarding           │ IP forwarding enabled   │
│ 1.3.6.1.2.1.6.9.0   │ tcpCurrEstab           │ Current TCP connections │
└─────────────────────┴─────────────────────────┴─────────────────────────┘
```

#### SNMP Security (SNMPv3):
- **User-based Security Model (USM)**
- **View-based Access Control Model (VACM)**

```
SNMPv3 Security Levels:
┌─────────────────┬─────────────────┬─────────────────┐
│ Security Level  │ Authentication  │   Encryption    │
├─────────────────┼─────────────────┼─────────────────┤
│ noAuthNoPriv    │ None            │ None            │
│ authNoPriv      │ MD5 or SHA      │ None            │
│ authPriv        │ MD5 or SHA      │ DES or AES      │
└─────────────────┴─────────────────┴─────────────────┘

SNMPv3 Configuration Example:
snmp-server group ADMIN v3 priv
snmp-server user admin ADMIN v3 auth sha MyAuthKey priv aes 128 MyPrivKey
snmp-server host 192.168.1.100 version 3 priv admin
```

#### SNMP Traps:
- **Purpose**: Asynchronous notifications from agents to managers
- **Types**: Generic traps (standard) and Enterprise-specific traps
- **Delivery**: Best-effort (UDP), no acknowledgment in v1/v2c

```
Common SNMP Traps:
┌─────────────────┬─────────────────────────────────────────┐
│   Trap Type     │              Description                │
├─────────────────┼─────────────────────────────────────────┤
│ coldStart       │ Agent restarted                         │
│ warmStart       │ Agent reinitialized                     │
│ linkDown        │ Interface went down                     │
│ linkUp          │ Interface came up                       │
│ authFailure     │ Authentication failure                  │
│ egpNeighborLoss │ EGP neighbor unreachable               │
│ enterpriseSpec  │ Vendor-specific trap                    │
└─────────────────┴─────────────────────────────────────────┘
```

#### SNMP Monitoring Tools:
- **Commercial**: SolarWinds, PRTG, ManageEngine OpManager
- **Open Source**: Nagios, Zabbix, LibreNMS, Cacti
- **Command Line**: snmpwalk, snmpget, snmpset, snmptrap

```
SNMP Command Examples:
# Get system description
snmpget -v2c -c public 192.168.1.1 1.3.6.1.2.1.1.1.0

# Walk interface table
snmpwalk -v2c -c public 192.168.1.1 1.3.6.1.2.1.2.2.1.2

# Set system contact
snmpset -v2c -c private 192.168.1.1 1.3.6.1.2.1.1.4.0 s "admin@company.com"

# SNMPv3 with authentication and encryption
snmpget -v3 -u admin -l authPriv -a SHA -A MyAuthKey -x AES -X MyPrivKey 192.168.1.1 1.3.6.1.2.1.1.1.0
```

- **SNMP Architecture:**
```
┌─────────────────────────────────────────────────────┐
│                    SNMP Manager                     │
│                 (Network Monitoring)                │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │
│  │   Nagios    │  │    PRTG     │  │ SolarWinds  │  │
│  └─────────────┘  └─────────────┘  └─────────────┘  │
└─────────────────────┬───────────────────────────────┘
                      │ Port 162 (Traps)
                      │ Port 161 (Queries)
        ┌─────────────┼─────────────┐
        │             │             │
        ▼             ▼             ▼
┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│SNMP Agent   │ │SNMP Agent   │ │SNMP Agent   │
│   Router    │ │   Switch    │ │   Server    │
│             │ │             │ │             │
│ ┌─────────┐ │ │ ┌─────────┐ │ │ ┌─────────┐ │
│ │   MIB   │ │ │ │   MIB   │ │ │ │   MIB   │ │
│ │Database │ │ │ │Database │ │ │ │Database │ │
│ └─────────┘ │ │ └─────────┘ │ │ └─────────┘ │
└─────────────┘ └─────────────┘ └─────────────┘

SNMP Operations Flow:
Manager                                Agent
   │                                     │
   │ GET Request (OID: 1.3.6.1.2.1.1.1.0)|
   │ ──────────────────────────────────► │
   │                                     │ Query MIB
   │                                     │ for sysDescr
   │ GET Response (Cisco IOS Router)     │
   │ ◄────────────────────────────────── │
   │                                     │
   │ SET Request (OID + New Value)       │
   │ ──────────────────────────────────► │
   │                                     │ Update MIB
   │ SET Response (Success/Error)        │ Object
   │ ◄────────────────────────────────── │
   │                                     │
   │                                     │ Event Occurs
   │ TRAP Notification (Unsolicited)     │ (Link Down)
   │ ◄────────────────────────────────── │
   │                                     │
```

- **SNMP Operations:**
    |Operation|Direction|Purpose|
    |---|---|---|
    |GET|Manager → Agent|Retrieve single value|
    |GET-NEXT|Manager → Agent|Retrieve next value in MIB tree|
    |GET-BULK|Manager → Agent|Retrieve multiple values (v2c/v3)|
    |SET|Manager → Agent|Modify agent configuration|
    |TRAP|Agent → Manager|Unsolicited notification|
    |INFORM|Agent → Manager|Acknowledged notification (v2c/v3)|

- **SNMP Versions:**
    - **SNMPv1**: 
        - Basic functionality
        - Community strings for authentication
        - No encryption
        - Security: Community string in plain text
    - **SNMPv2c**: 
        - Improved error handling
        - Bulk operations (GET-BULK)
        - Community strings for authentication
        - No encryption
    - **SNMPv3**: 
        - User-based security model
        - Authentication (MD5, SHA)
        - Encryption (DES, AES)
        - Access control

- **Common MIB Objects:**
    |OID|Object|Description|
    |---|---|---|
    |1.3.6.1.2.1.1.1.0|sysDescr|System description|
    |1.3.6.1.2.1.1.3.0|sysUpTime|System uptime|
    |1.3.6.1.2.1.2.2.1.10|ifInOctets|Interface input bytes|
    |1.3.6.1.2.1.2.2.1.16|ifOutOctets|Interface output bytes|
    |1.3.6.1.2.1.25.1.1.0|hrSystemUptime|Host resources uptime|

### Network Flow Monitoring [NetFlow]
- Cisco proprietary protocol for network traffic analysis (now industry standard)
- Ports: `2055 UDP` (v5), `9995 UDP` (v9), `4739 UDP` (IPFIX)
- Flow-based monitoring: Groups packets with common characteristics into flows
- Used for bandwidth monitoring, security analysis, capacity planning, billing

- **Flow Definition:**
    - **Traditional 5-tuple:**
        - Source IP Address
        - Destination IP Address  
        - Source Port
        - Destination Port
        - Protocol (TCP/UDP/ICMP)
    - **Extended 7-tuple (NetFlow v5+):**
        - Type of Service (ToS) byte
        - Input Interface index
    - **Advanced Flow Keys (v9/IPFIX):**
        - VLAN ID, MPLS labels, BGP AS numbers
        - Application ID, User ID, URL categories

- **NetFlow Versions Comparison:**

    |Feature|NetFlow v5|NetFlow v9|IPFIX|sFlow|
    |---|---|---|---|---|
    |**Format**|Fixed|Template-based|Template-based|Sampling-based|
    |**IPv6 Support**|❌|✅|✅|✅|
    |**Flexible Fields**|❌|✅|✅|✅|
    |**Vendor**|Cisco|Cisco|IETF Standard|InMon|
    |**Port**|2055|9995|4739|6343|
    |**Security**|Basic|Enhanced|Advanced|Basic|
    |**Scalability**|Medium|High|Very High|Very High|

- **NetFlow v5 Record Structure:**
    - **Header**: Version, count, uptime, timestamp, sequence
    - **Flow Records**: Up to 30 flows per packet
    - **Fixed Fields**: 48 bytes per flow record
    - **Limitations**: IPv4 only, no VLAN support, fixed format

- **NetFlow v9 Template System:**
    - **Template Flowset**: Defines record format (Template ID + Field definitions)
    - **Data Flowset**: Contains actual flow data matching template
    - **Options Template**: Metadata about exporter (sampling rate, interface names)
    - **Flexible Export**: Custom fields, variable record length

- **IPFIX Enhancements:**
    - **Information Elements**: Standardized field definitions (IANA registry)
    - **Enterprise Elements**: Vendor-specific extensions
    - **Transport Protocols**: UDP, TCP, SCTP support
    - **Security**: TLS/DTLS encryption, authentication
    - **Reliability**: Message sequence numbers, template withdrawal

- **NetFlow Components:**
    - **Flow Exporter**: Router/switch generating flow records
    - **Flow Collector**: Server receiving and storing flow data
    - **Flow Analyzer**: Application analyzing collected data

- **NetFlow Architecture:**
```
┌─────────────────────────────────────────────────────────────┐
│                    Network Traffic                          │
└─────────────────────┬───────────────────────────────────────┘
                      │
┌─────────────────────▼──────────────────────────────────────┐
│                Flow Exporters                              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Router    │  │   Switch    │  │  Firewall   │         │
│  │             │  │             │  │             │         │
│  │ NetFlow     │  │ NetFlow     │  │ NetFlow     │         │
│  │ Enabled     │  │ Enabled     │  │ Enabled     │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────┬──────────────────────────────────────┘
                      │ UDP 2055/9995
                      │ Flow Records
┌─────────────────────▼───────────────────────────────────────┐
│                Flow Collector                               │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              Flow Database                          │    │
│  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐    │    │
│  │  │ Flow 1  │ │ Flow 2  │ │ Flow 3  │ │ Flow N  │    │    │
│  │  └─────────┘ └─────────┘ └─────────┘ └─────────┘    │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────┬───────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────┐
│                Flow Analyzers                               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐          │
│  │  Bandwidth  │  │  Security   │  │  Capacity   │          │
│  │ Monitoring  │  │  Analysis   │  │  Planning   │          │
│  └─────────────┘  └─────────────┘  └─────────────┘          │
└─────────────────────────────────────────────────────────────┘

Flow Record Structure:
┌─────────────────────────────────────────────────────────────┐
│                    Flow Record                              │
├─────────────────────────────────────────────────────────────┤
│ Source IP: 192.168.1.100    │ Dest IP: 10.0.0.50            │
│ Source Port: 443            │ Dest Port: 52341              │
│ Protocol: TCP (6)           │ ToS: 0x00                     │
│ Input Interface: Gi0/1      │ Output Interface: Gi0/2       │
│ Packet Count: 1,250         │ Byte Count: 1,875,000         │
│ Start Time: 14:30:15        │ End Time: 14:35:22            │
│ Flow Duration: 5 min 7 sec  │ TCP Flags: 0x18 (PSH,ACK)    │
└─────────────────────────────────────────────────────────────┘
```

- **NetFlow Configuration Example:**
```
Cisco Router Configuration:
ip flow-export version 9
ip flow-export destination 192.168.1.100 9995
ip flow-export source GigabitEthernet0/0
ip flow-export template timeout-rate 1
ip flow-export template refresh-rate 20

interface GigabitEthernet0/1
 ip route-cache flow
 ip flow ingress
 ip flow egress
```

- **sFlow vs NetFlow:**
    - **sFlow**: Sampling-based, lower CPU impact, real-time
    - **NetFlow**: Flow-based, more detailed, higher accuracy
    - **Use Cases**: sFlow for high-speed links, NetFlow for detailed analysis

---

## VoIP Protocols

### SIP (Session Initiation Protocol)
- **Purpose**: Signaling protocol for VoIP calls, video conferencing, instant messaging
- **Standard**: RFC 3261
- **Port**: 5060 (UDP/TCP), 5061 (TLS)
- **Architecture**: User Agent Client (UAC), User Agent Server (UAS), Proxy Server
- **Methods**: INVITE, ACK, BYE, CANCEL, REGISTER, OPTIONS

```
SIP Call Flow (Basic Call Setup):
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Alice     │    │ SIP Proxy   │    │ SIP Proxy   │    │     Bob     │
│ (Caller)    │    │  Server A   │    │  Server B   │    │  (Callee)   │
└──────┬──────┘    └──────┬──────┘    └──────┬──────┘    └──────┬──────┘
       │                  │                  │                  │
       │ 1. INVITE        │                  │                  │
       │ ────────────────►│                  │                  │
       │                  │ 2. INVITE        │                  │
       │                  │ ────────────────►│                  │
       │                  │                  │ 3. INVITE        │
       │                  │                  │ ────────────────►│
       │                  │                  │                  │
       │                  │                  │ 4. 180 Ringing   │
       │                  │                  │ ◄────────────────│
       │                  │ 5. 180 Ringing   │                  │
       │                  │ ◄────────────────│                  │
       │ 6. 180 Ringing   │                  │                  │
       │ ◄────────────────│                  │                  │
       │                  │                  │                  │
       │                  │                  │ 7. 200 OK        │
       │                  │                  │ ◄────────────────│
       │                  │ 8. 200 OK        │                  │
       │                  │ ◄────────────────│                  │
       │ 9. 200 OK        │                  │                  │
       │ ◄────────────────│                  │                  │
       │                  │                  │                  │
       │ 10. ACK          │                  │                  │
       │ ────────────────►│                  │                  │
       │                  │ 11. ACK          │                  │
       │                  │ ────────────────►│                  │
       │                  │                  │ 12. ACK          │
       │                  │                  │ ────────────────►│
       │                  │                  │                  │
       │◄═══════════════════ RTP Media Stream ═══════════════════►│
       │                  │                  │                  │
       │ 13. BYE          │                  │                  │
       │ ────────────────►│                  │                  │
       │                  │ 14. BYE          │                  │
       │                  │ ────────────────►│                  │
       │                  │                  │ 15. BYE          │
       │                  │                  │ ────────────────►│
       │                  │                  │                  │
       │                  │                  │ 16. 200 OK       │
       │                  │                  │ ◄────────────────│
       │                  │ 17. 200 OK       │                  │
       │                  │ ◄────────────────│                  │
       │ 18. 200 OK       │                  │                  │
       │ ◄────────────────│                  │                  │

SIP Message Structure:
INVITE sip:bob@example.com SIP/2.0
Via: SIP/2.0/UDP alice.example.com:5060
From: Alice <sip:alice@example.com>;tag=1928301774
To: Bob <sip:bob@example.com>
Call-ID: a84b4c76e66710@alice.example.com
CSeq: 314159 INVITE
Contact: <sip:alice@alice.example.com>
Content-Type: application/sdp
Content-Length: 142

v=0
o=alice 53655765 2353687637 IN IP4 alice.example.com
s=-
c=IN IP4 alice.example.com
t=0 0
m=audio 49170 RTP/AVP 0
a=rtpmap:0 PCMU/8000
```

### H.323 Protocol
- **Purpose**: ITU-T standard for multimedia communications over packet networks
- **Components**: Terminals, Gateways, Gatekeepers, MCUs (Multipoint Control Units)
- **Protocols**: H.225 (call signaling), H.245 (media control), RAS (registration)
- **Ports**: 1720 (H.225), Dynamic (H.245), 1719 (RAS)

```
H.323 Call Flow:
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  Terminal A │    │ Gatekeeper  │    │ Gatekeeper  │    │  Terminal B │
│  (Caller)   │    │      A      │    │      B      │    │  (Callee)   │
└──────┬──────┘    └──────┬──────┘    └──────┬──────┘    └──────┬──────┘
       │                  │                  │                  │
       │ 1. ARQ           │                  │                  │
       │ (Admission Req)  │                  │                  │
       │ ────────────────►│                  │                  │
       │                  │                  │                  │
       │ 2. ACF           │                  │                  │
       │ (Admission Conf) │                  │                  │
       │ ◄────────────────│                  │                  │
       │                  │                  │                  │
       │ 3. H.225 Setup   │                  │                  │
       │ ────────────────────────────────────────────────────►│
       │                  │                  │                  │
       │                  │                  │ 4. ARQ           │
       │                  │                  │ ◄────────────────│
       │                  │                  │                  │
       │                  │                  │ 5. ACF           │
       │                  │                  │ ────────────────►│
       │                  │                  │                  │
       │ 6. H.225 Call Proceeding            │                  │
       │ ◄────────────────────────────────────────────────────│
       │                  │                  │                  │
       │ 7. H.225 Alerting│                  │                  │
       │ ◄────────────────────────────────────────────────────│
       │                  │                  │                  │
       │ 8. H.225 Connect │                  │                  │
       │ ◄────────────────────────────────────────────────────│
       │                  │                  │                  │
       │ 9. H.245 Terminal Capability Set    │                  │
       │ ◄──────────────────────────────────────────────────►│
       │                  │                  │                  │
       │ 10. H.245 Master/Slave Determination│                  │
       │ ◄──────────────────────────────────────────────────►│
       │                  │                  │                  │
       │ 11. H.245 Open Logical Channel      │                  │
       │ ◄──────────────────────────────────────────────────►│
       │                  │                  │                  │
       │◄═══════════════════ RTP Media Stream ═══════════════════►│
       │                  │                  │                  │
       │ 12. H.245 Close Logical Channel     │                  │
       │ ◄──────────────────────────────────────────────────►│
       │                  │                  │                  │
       │ 13. H.225 Release Complete          │                  │
       │ ◄──────────────────────────────────────────────────►│
       │                  │                  │                  │
       │ 14. DRQ          │                  │                  │
       │ (Disengage Req)  │                  │                  │
       │ ────────────────►│                  │                  │
       │                  │                  │                  │
       │ 15. DCF          │                  │                  │
       │ (Disengage Conf) │                  │                  │
       │ ◄────────────────│                  │                  │

H.323 Protocol Stack:
┌─────────────────────────────────────────────────────────────┐
│                   Applications                              │
├─────────────────────────────────────────────────────────────┤
│ H.225 Call Signaling │ H.245 Control │ RAS │ Audio/Video   │
├─────────────────────────────────────────────────────────────┤
│                    RTP/RTCP                                 │
├─────────────────────────────────────────────────────────────┤
│                      UDP                                    │
├─────────────────────────────────────────────────────────────┤
│                      IP                                     │
├─────────────────────────────────────────────────────────────┤
│                   Data Link                                 │
├─────────────────────────────────────────────────────────────┤
│                   Physical                                  │
└─────────────────────────────────────────────────────────────┘
```

### RTP (Real-time Transport Protocol)
- **Purpose**: Transport protocol for real-time applications (audio, video)
- **Standard**: RFC 3550
- **Port Range**: 16384-32767 (even ports for RTP, odd for RTCP)
- **Features**: Sequence numbering, timestamping, payload identification
- **Companion**: RTCP (Real-time Transport Control Protocol)

```
RTP Header Structure:
┌─────────────┬─────────────┬─────────────┬─────────────┐
│  V  │  P    │  X  │  CC   │  M  │   PT  │
│(2b) │ (1b)  │(1b) │ (4b)  │(1b) │ (7b)  │
├─────────────┴─────────────┼─────────────┴─────────────┤
│        Sequence Number    │                           │
│         (16 bits)         │                           │
├───────────────────────────┴───────────────────────────┤
│                 Timestamp                             │
│                 (32 bits)                             │
├───────────────────────────────────────────────────────┤
│            Synchronization Source (SSRC)              │
│                 (32 bits)                             │
├───────────────────────────────────────────────────────┤
│         Contributing Source (CSRC) List               │
│              (0-15 items, 32 bits each)               │
└───────────────────────────────────────────────────────┘

Field Descriptions:
• V (Version): RTP version (2)
• P (Padding): Padding flag
• X (Extension): Header extension flag
• CC (CSRC Count): Number of CSRC identifiers
• M (Marker): Application-specific marker bit
• PT (Payload Type): Format of RTP payload
• Sequence Number: Increments by 1 for each packet
• Timestamp: Sampling instant of first octet
• SSRC: Synchronization source identifier
• CSRC: Contributing source identifiers

RTP Media Flow:
┌─────────────┐                                    ┌─────────────┐
│   Sender    │                                    │  Receiver   │
│             │                                    │             │
│ ┌─────────┐ │                                    │ ┌─────────┐ │
│ │ Audio   │ │                                    │ │ Audio   │ │
│ │ Codec   │ │                                    │ │ Decoder │ │
│ └────┬────┘ │                                    │ └────▲────┘ │
│      │      │                                    │      │      │
│ ┌────▼────┐ │    RTP Packets (Even Port)         │ ┌────┴────┐ │
│ │   RTP   │ │ ──────────────────────────────────►│ │   RTP   │ │
│ │ Encoder │ │                                    │ │ Decoder │ │
│ └────┬────┘ │                                    │ └────▲────┘ │
│      │      │                                    │      │      │
│ ┌────▼────┐ │   RTCP Packets (Odd Port)          │ ┌────┴────┐ │
│ │  RTCP   │ │ ◄────────────────────────────────► │ │  RTCP   │ │
│ │         │ │                                    │ │         │ │
│ └─────────┘ │                                    │ └─────────┘ │
└─────────────┘                                    └─────────────┘

RTCP Packet Types:
• SR (Sender Report): Transmission and reception statistics
• RR (Receiver Report): Reception statistics
• SDES (Source Description): Source identification
• BYE: Indicates end of participation
• APP: Application-specific functions

RTP Payload Types (Common):
┌─────────┬─────────────────┬─────────────────────────┐
│   PT    │   Encoding      │       Description       │
├─────────┼─────────────────┼─────────────────────────┤
│    0    │ PCMU            │ G.711 μ-law             │
│    8    │ PCMA            │ G.711 A-law             │
│   18    │ G729            │ G.729 Audio             │
│   96-127│ Dynamic         │ Negotiated via SDP      │
└─────────┴─────────────────┴─────────────────────────┘
```

---

## Life of a Packet (What Happens When...)
*Detailed breakdown of "System vs Network" interaction when typing a URL.*

### 1. Physical Keyboard & Interrupts
*   **Key Press:** Key bottoms out, closing electrical circuit; allowed current flows.
*   **Scanning:** Keyboard controller scans matrix, debounces electrical noise, converts to keycode.
*   **Transmission:** Keycode sent via USB (polling endpoint ~10ms) or Bluetooth.
*   **Interrupt (Hardware):** USB Controller fires interrupt; CPU pauses to run Interrupt Handler (IDT).
*   **Interrupt (Software):** Kernel driver (`KBDHID.sys` / `I/O Kit`) processes scancode.

### 2. OS Processing (Windows/Linux/Mac)
*   **Windows:** `Win32K.sys` determines valid window; posts `WM_KEYDOWN` message to queue.
*   **Mac:** `WindowServer` dispatches `KeyDown` event to application's Mach port.
*   **App Logic:** Browser's main thread picks up message, triggers `kvirtualeydown` event.

### 3. Parsing & Auto-Complete
*   **Search vs URL:** Browser checks if text is valid URL or search term.
*   **HSTS Check:** Browser checks HSTS list; upgrades HTTP to HTTPS if found.
*   **Non-ASCII:** Hostname converted to Punycode if non-ASCII characters present.

### 4. DNS Lookup (The Resolution)
*   **Browser Cache:** Checked first (`chrome://net-internals/#dns`).
*   **OS Cache:** `gethostbyname` checks local cache and `hosts` file.
*   **Resolver:** Request sent to configured DNS Server (Iterative/Recursive).
*   **Packet:** `SIP=LocalIP`, `DIP=DNS_Server_IP`, `SPort=Random`, `DPort=53 (UDP)`.
*   **ARP Check:** If DNS server on local subnet, ARP for MAC.

### 5. ARP Process (Link Layer)
*   **Cache Check:** OS checks local ARP cache (`arp -a`) for Target IP.
*   **Routing Table:** If Target IP remote, lookup Default Gateway IP.
*   **Broadcast:** If MAC unknown, send ARP Request (`Who has IP?`).
*   **Packet:** `SMAC=LocalMAC`, `DMAC=FF:FF:FF:FF:FF:FF`, `SIP=LocalIP`, `DIP=TargetIP`.
*   **Switch Logic:** Switch floods (if no CAM); Router replies with Interface MAC.
*   **Reply:** `SMAC=TargetMAC`, `DMAC=LocalMAC` (Unicast).

### 6. Opening a Socket (Transport Layer)
*   **Syscall:** Browser calls `socket(AF_INET, SOCK_STREAM)` calling kernel.
*   **Three-Way Handshake (TCP):**
    1.  **SYN:** `Flags=SYN`, `Seq=Risk`, `SPort=Random`, `DPort=443`.
    2.  **SYN-ACK:** `Flags=SYN,ACK`, `Ack=Risk+1`, `Seq=ServerISN`, `SIP=ServerIP`.
    3.  **ACK:** `Flags=ACK`, `Ack=ServerISN+1`, `SIP=LocalIP`.

### 7. TLS Handshake (Security)
*   **Client Hello:** Sends TLS version, cipher suites, randomness.
*   **Server Hello:** Selects cipher, sends Certificate (Public Key) + Randomness.
*   **Verification:** Client verifies Cert Authority (CA) signature chain.
*   **Key Exchange:** Client sends Pre-Master Secret encrypted with Server's Public Key.
*   **Session Keys:** Both derive symmetric Session Keys; exchange `Finished` hashes.

### 8. HTTP Protocol (Application Layer)
*   **Request:** `GET / HTTP/1.1`. Headers: `Host: google.com`, `Connection: keep-alive`.
*   **Processing:** HTTPD (Apache/Nginx) matches Virtual Host, checks rewrites/permissions.
*   **Response:** Server returns `200 OK` (or `304 Not Modified`) + HTML Payload.
*   **Persistence:** Connection stays open if `Keep-Alive` requested.

### 9. Browser Rendering (The Engine)
*   **Parsing:** HTML parsed into DOM Tree; fixes invalid syntax automatically.
*   **Resources:** Background fetch for CSS, JS, Images (`GET` requests).
*   **CSSOM:** CSS parsed into CSS Object Model (Style Rules).
*   **Render Tree:** DOM + CSSOM combined; invisible elements (head, display:none) excluded.
*   **Layout:** Calculates geometry (width, height, position) of each node (Reflow).
*   **Paint:** Rasterizes elements (color, shadow) onto layers (CPU/GPU).
*   **Composite:** GPU combines layers; displays final frame on screen.

---

## Wireless Technologies

### WLAN Protocols and Standards

#### IEEE 802.11 Evolution

```
Wi-Fi Standards Evolution:
┌─────────────┬─────────────┬─────────────┬─────────────┬─────────────┐
│  Standard   │    Year     │  Max Speed  │  Frequency  │   Range     │
├─────────────┼─────────────┼─────────────┼─────────────┼─────────────┤
│ 802.11      │    1997     │   2 Mbps    │   2.4 GHz   │   20 meters │
│ 802.11a     │    1999     │  54 Mbps    │   5 GHz     │   35 meters │
│ 802.11b     │    1999     │  11 Mbps    │   2.4 GHz   │   35 meters │
│ 802.11g     │    2003     │  54 Mbps    │   2.4 GHz   │   38 meters │
│ 802.11n     │    2009     │ 600 Mbps    │ 2.4/5 GHz   │   70 meters │
│ 802.11ac    │    2013     │ 6.93 Gbps   │   5 GHz     │   35 meters │
│ 802.11ax    │    2019     │ 9.6 Gbps    │ 2.4/5 GHz   │   30 meters │
│ (Wi-Fi 6)   │             │             │             │             │
│ 802.11ax-6E │    2020     │ 9.6 Gbps    │2.4/5/6 GHz  │   30 meters │
│ (Wi-Fi 6E)  │             │             │             │             │
│ 802.11be    │    2024     │ 46 Gbps     │2.4/5/6 GHz  │   30 meters │
│ (Wi-Fi 7)   │             │             │             │             │
└─────────────┴─────────────┴─────────────┴─────────────┴─────────────┘
```

#### Wi-Fi 6 (802.11ax) Features
- **OFDMA**: Orthogonal Frequency Division Multiple Access
- **MU-MIMO**: Multi-User Multiple Input Multiple Output (8x8)
- **BSS Coloring**: Reduces interference in dense environments
- **Target Wake Time (TWT)**: Power saving for IoT devices
- **1024-QAM**: Higher modulation for increased throughput

### Wireless Client Connection Process

#### 1. RF (Radio Frequency) Fundamentals
- **Frequency Bands**: 2.4 GHz (ISM), 5 GHz (UNII), 6 GHz (UNII-5-8)
- **Channels**: Non-overlapping channels for interference avoidance
- **Power**: Measured in dBm, mW, or EIRP
- **Antenna Types**: Omnidirectional, directional, MIMO

```
2.4 GHz Channel Layout (20 MHz channels):
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │  6  │  7  │  8  │  9  │ 10  │ 11  │ 12  │ 13  │ 14  │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
2412  2417  2422  2427  2432  2437  2442  2447  2452  2457  2462  2467  2472  2484 MHz

Non-overlapping channels: 1, 6, 11 (in most countries)

5 GHz Channel Layout (Sample):
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ 36  │ 40  │ 44  │ 48  │ 52  │ 56  │ 60  │ 64  │ 100 │ 104 │ ... │ 165 │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
5180  5200  5220  5240  5260  5280  5300  5320  5500  5520       5825 MHz

More channels available, less interference
```

#### 2. SSID (Service Set Identifier)
- **Purpose**: Network name identifier for wireless networks
- **Length**: 0-32 bytes (characters)
- **Types**: 
    - **Basic Service Set (BSS)**: Single AP
    - **Extended Service Set (ESS)**: Multiple APs with same SSID
    - **Independent BSS (IBSS)**: Ad-hoc network

```
SSID Broadcast Types:
┌─────────────────────────────────────────────────────────────┐
│                    SSID Broadcasting                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ ┌─────────────┐    Beacon Frames     ┌─────────────┐        │
│ │     AP      │ ──────────────────► │   Client    │        │
│ │             │    (SSID: "WiFi")    │             │        │
│ │ Broadcast   │                      │ Sees "WiFi" │        │
│ │ Enabled     │                      │ in list     │        │
│ └─────────────┘                      └─────────────┘        │
│                                                             │
│ ┌─────────────┐    Beacon Frames     ┌─────────────┐        │
│ │     AP      │ ──────────────────► │   Client    │        │
│ │             │   (SSID: Hidden)     │             │        │
│ │ Broadcast   │                      │ Sees hidden │        │
│ │ Disabled    │                      │ network     │        │
│ └─────────────┘                      └─────────────┘        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### 3. Wireless Client Association Process

```
802.11 Association Process:
┌─────────────┐                                    ┌─────────────┐
│   Client    │                                    │     AP      │
│             │                                    │             │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. Passive Scanning                              │
       │    (Listen for Beacon frames)                    │
       │ ◄────────────────────────────────────────────── │
       │    Beacon (SSID, Capabilities, Rates)           │
       │                                                  │
       │ 2. Active Scanning (Optional)                    │
       │    Probe Request (SSID or Broadcast)             │
       │ ──────────────────────────────────────────────► │
       │                                                  │
       │ 3. Probe Response                                │
       │    (SSID, Capabilities, Rates)                   │
       │ ◄────────────────────────────────────────────── │
       │                                                  │
       │ 4. Authentication Request                        │
       │    (Open System or Shared Key)                   │
       │ ──────────────────────────────────────────────► │
       │                                                  │
       │ 5. Authentication Response                       │
       │    (Success/Failure)                             │
       │ ◄────────────────────────────────────────────── │
       │                                                  │
       │ 6. Association Request                           │
       │    (SSID, Capabilities, Rates)                   │
       │ ──────────────────────────────────────────────► │
       │                                                  │
       │ 7. Association Response                          │
       │    (Success + AID/Failure)                       │
       │ ◄────────────────────────────────────────────── │
       │                                                  │
       │ 8. 4-Way Handshake (WPA/WPA2/WPA3)              │
       │ ◄──────────────────────────────────────────────► │
       │                                                  │
       │ 9. Data Communication                            │
       │ ◄══════════════════════════════════════════════► │

State Transitions:
Unauthenticated/Unassociated → Authenticated/Unassociated → Authenticated/Associated
```

#### 4. Wireless LAN Controller (WLC) Architecture

```
WLC Deployment Models:
┌─────────────────────────────────────────────────────────────┐
│                 Centralized WLC Model                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                    ┌─────────────┐                         │
│                    │     WLC     │                         │
│                    │ Controller  │                         │
│                    └──────┬──────┘                         │
│                           │                                 │
│                    CAPWAP Tunnels                          │
│        ┌──────────────────┼──────────────────┐             │
│        │                  │                  │             │
│   ┌────▼────┐        ┌────▼────┐        ┌────▼────┐        │
│   │Lightweight│      │Lightweight│      │Lightweight│      │
│   │    AP     │      │    AP     │      │    AP     │      │
│   │  (LAP)    │      │  (LAP)    │      │  (LAP)    │      │
│   └───────────┘      └───────────┘      └───────────┘      │
│                                                             │
└─────────────────────────────────────────────────────────────┘

CAPWAP (Control and Provisioning of Wireless Access Points):
┌─────────────────────────────────────────────────────────────┐
│                    CAPWAP Protocol                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ Control Messages (UDP 5246):                               │
│ • Discovery Request/Response                                │
│ • Join Request/Response                                     │
│ • Configuration Status Request/Response                     │
│ • Change State Event Request/Response                       │
│                                                             │
│ Data Messages (UDP 5247):                                  │
│ • 802.11 Data frames                                        │
│ • Keep Alive                                                │
│                                                             │
│ CAPWAP Tunnel Modes:                                        │
│ • Split MAC: AP handles real-time functions                │
│ • Local MAC: AP handles all 802.11 functions               │
│                                                             │
└─────────────────────────────────────────────────────────────┘

WLC Functions:
• Centralized Configuration Management
• RF Management (Power, Channel Assignment)
• Client Load Balancing
• Rogue AP Detection
• Mobility Management (Roaming)
• Security Policy Enforcement
• Quality of Service (QoS)
• Guest Access Management
```

#### 5. Wireless Security Evolution

```
Wireless Security Timeline:
┌─────────────┬─────────────┬─────────────┬─────────────┬─────────────┐
│  Security   │    Year     │ Encryption  │    Auth     │   Status    │
├─────────────┼─────────────┼─────────────┼─────────────┼─────────────┤
│    WEP      │    1997     │   RC4       │ Shared Key  │ Deprecated  │
│             │             │  40/104-bit │             │ (Broken)    │
├─────────────┼─────────────┼─────────────┼─────────────┼─────────────┤
│   WPA       │    2003     │   TKIP      │   802.1X    │ Deprecated  │
│             │             │   RC4       │   PSK       │             │
├─────────────┼─────────────┼─────────────┼─────────────┼─────────────┤
│   WPA2      │    2004     │    AES      │   802.1X    │   Current   │
│             │             │   CCMP      │   PSK       │             │
├─────────────┼─────────────┼─────────────┼─────────────┼─────────────┤
│   WPA3      │    2018     │    AES      │    SAE      │   Latest    │
│             │             │   GCMP      │   802.1X    │             │
└─────────────┴─────────────┴─────────────┴─────────────┴─────────────┘

WPA2/WPA3 4-Way Handshake:
┌─────────────┐                                    ┌─────────────┐
│   Client    │                                    │     AP      │
│             │                                    │             │
└──────┬──────┘                                    └──────┬──────┘
       │                                                  │
       │ 1. Message 1 (ANonce)                            │
       │ ◄────────────────────────────────────────────── │
       │                                                  │
       │ 2. Message 2 (SNonce + MIC)                      │
       │ ──────────────────────────────────────────────► │
       │                                                  │
       │ 3. Message 3 (GTK + MIC)                         │
       │ ◄────────────────────────────────────────────── │
       │                                                  │
       │ 4. Message 4 (ACK + MIC)                         │
       │ ──────────────────────────────────────────────► │
       │                                                  │
       │ Encrypted Data Communication                     │
       │ ◄══════════════════════════════════════════════► │

Key Derivation:
PMK (Pairwise Master Key) ← PSK or 802.1X
PTK (Pairwise Transient Key) ← PMK + ANonce + SNonce + MAC addresses
GTK (Group Temporal Key) ← Generated by AP for multicast/broadcast
```

#### 6. Wireless Roaming
- **Layer 2 Roaming**: Same subnet, fast handoff
- **Layer 3 Roaming**: Different subnet, requires tunneling
- **802.11r (Fast BSS Transition)**: Reduces roaming time
- **802.11k (Radio Resource Management)**: Neighbor reports
- **802.11v (Wireless Network Management)**: BSS transition management

```
Roaming Process:
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│     AP1     │    │   Client    │    │     AP2     │
│             │    │             │    │             │
└──────┬──────┘    └──────┬──────┘    └──────┬──────┘
       │                  │                  │
       │ Data Transfer    │                  │
       │ ◄──────────────► │                  │
       │                  │                  │
       │ Signal Weakens   │ Scanning for     │
       │                  │ better signal    │
       │                  │ ────────────────►│
       │                  │                  │
       │                  │ Probe Response   │
       │                  │ ◄────────────────│
       │                  │                  │
       │                  │ Reassociation    │
       │                  │ Request          │
       │                  │ ────────────────►│
       │                  │                  │
       │                  │ Reassociation    │
       │                  │ Response         │
       │                  │ ◄────────────────│
       │                  │                  │
       │                  │ Data Transfer    │
       │                  │ ◄──────────────► │
```

#### 7. Wireless Troubleshooting
- **Signal Strength**: RSSI (Received Signal Strength Indicator)
- **Signal Quality**: SNR (Signal-to-Noise Ratio)
- **Interference**: Co-channel and adjacent channel interference
- **Coverage**: Dead zones and coverage holes
- **Capacity**: Client density and bandwidth requirements

```
Common Wireless Issues:
┌─────────────────────┬─────────────────────────────────────┐
│       Issue         │            Solution                 │
├─────────────────────┼─────────────────────────────────────┤
│ Poor Signal         │ Adjust AP placement/power          │
│ Interference        │ Change channels, reduce power       │
│ Slow Performance    │ Check for congestion, upgrade APs   │
│ Connection Drops    │ Check roaming settings, RF issues   │
│ Authentication Fail │ Verify credentials, certificates    │
│ IP Assignment       │ Check DHCP, VLAN configuration     │
└─────────────────────┴─────────────────────────────────────┘
```

---

## Mobile Networks (LTE/5G)

### LTE (Long Term Evolution) - 4G

#### LTE Network Architecture

```
LTE Network Components:
┌─────────────────────────────────────────────────────────────┐
│                    LTE Architecture                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ ┌─────────────┐    ┌─────────────┐    ┌─────────────┐       │
│ │     UE      │    │    eNB      │    │     EPC     │       │
│ │ (User       │    │ (Enhanced   │    │ (Evolved    │       │
│ │ Equipment)  │    │ Node B)     │    │ Packet Core)│       │
│ └──────┬──────┘    └──────┬──────┘    └──────┬──────┘       │
│        │                  │                  │              │
│        │ LTE-Uu Interface │ S1 Interface     │              │
│        │ ◄──────────────► │ ◄──────────────► │              │
│        │                  │                  │              │
│        │                  │                  │              │
│ ┌──────▼──────┐    ┌──────▼──────┐    ┌──────▼──────┐       │
│ │   Radio     │    │   Radio     │    │   Core      │       │
│ │ Interface   │    │ Access      │    │  Network    │       │
│ │             │    │ Network     │    │             │       │
│ └─────────────┘    └─────────────┘    └─────────────┘       │
│                                                             │
└─────────────────────────────────────────────────────────────┘

EPC Components:
┌─────────────────────────────────────────────────────────────┐
│                 Evolved Packet Core (EPC)                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │
│ │     MME     │  │     SGW     │  │     PGW     │           │
│ │ (Mobility   │  │ (Serving    │  │ (Packet     │           │
│ │ Management  │  │ Gateway)    │  │ Data        │           │
│ │ Entity)     │  │             │  │ Network     │           │
│ │             │  │             │  │ Gateway)    │           │
│ └──────┬──────┘  └──────┬──────┘  └──────┬──────┘           │
│        │                │                │                  │
│        │ S1-MME         │ S1-U           │ SGi              │
│        │ ◄─────────────►│ ◄─────────────►│ ◄──────────────► │
│        │                │                │                  │
│ ┌──────▼──────┐  ┌──────▼──────┐  ┌──────▼──────┐           │
│ │     HSS     │  │    PCRF     │  │  Internet   │           │
│ │ (Home       │  │ (Policy &   │  │             │           │
│ │ Subscriber  │  │ Charging    │  │             │           │
│ │ Server)     │  │ Rules       │  │             │           │
│ │             │  │ Function)   │  │             │           │
│ └─────────────┘  └─────────────┘  └─────────────┘           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### LTE Protocol Stack

```
LTE Protocol Stack (User Plane):
┌─────────────────────────────────────────────────────────────┐
│                    User Equipment (UE)                     │
├─────────────────────────────────────────────────────────────┤
│                   Application                               │
├─────────────────────────────────────────────────────────────┤
│                      IP                                     │
├─────────────────────────────────────────────────────────────┤
│                     PDCP                                    │
│            (Packet Data Convergence Protocol)              │
├─────────────────────────────────────────────────────────────┤
│                      RLC                                    │
│              (Radio Link Control)                          │
├─────────────────────────────────────────────────────────────┤
│                      MAC                                    │
│             (Medium Access Control)                        │
├─────────────────────────────────────────────────────────────┤
│                      PHY                                    │
│                 (Physical Layer)                           │
└─────────────────────────────────────────────────────────────┘

LTE Protocol Stack (Control Plane):
┌─────────────────────────────────────────────────────────────┐
│                    User Equipment (UE)                     │
├─────────────────────────────────────────────────────────────┤
│                      NAS                                    │
│             (Non-Access Stratum)                           │
├─────────────────────────────────────────────────────────────┤
│                      RRC                                    │
│            (Radio Resource Control)                        │
├─────────────────────────────────────────────────────────────┤
│                     PDCP                                    │
├─────────────────────────────────────────────────────────────┤
│                      RLC                                    │
├─────────────────────────────────────────────────────────────┤
│                      MAC                                    │
├─────────────────────────────────────────────────────────────┤
│                      PHY                                    │
└─────────────────────────────────────────────────────────────┘
```

#### LTE Key Technologies
- **OFDMA**: Orthogonal Frequency Division Multiple Access (Downlink)
- **SC-FDMA**: Single Carrier FDMA (Uplink)
- **MIMO**: Multiple Input Multiple Output antennas
- **Carrier Aggregation**: Combining multiple frequency bands
- **QoS**: Quality of Service with bearer management

```
LTE Attach Procedure:
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│     UE      │    │    eNB      │    │     MME     │    │     HSS     │
│             │    │             │    │             │    │             │
└──────┬──────┘    └──────┬──────┘    └──────┬──────┘    └──────┬──────┘
       │                  │                  │                  │
       │ 1. RRC Connection Request           │                  │
       │ ──────────────► │                  │                  │
       │                  │                  │                  │
       │ 2. RRC Connection Setup             │                  │
       │ ◄────────────── │                  │                  │
       │                  │                  │                  │
       │ 3. RRC Connection Setup Complete    │                  │
       │ ──────────────► │                  │                  │
       │                  │                  │                  │
       │ 4. Attach Request│                  │                  │
       │ ──────────────► │ 5. Initial UE Message              │
       │                  │ ──────────────► │                  │
       │                  │                  │                  │
       │                  │                  │ 6. Authentication│
       │                  │                  │ & Security       │
       │                  │                  │ ◄──────────────► │
       │                  │                  │                  │
       │                  │ 7. Security Mode Command           │
       │                  │ ◄────────────── │                  │
       │ 8. Security Mode Command            │                  │
       │ ◄────────────── │                  │                  │
       │                  │                  │                  │
       │ 9. Security Mode Complete           │                  │
       │ ──────────────► │ ──────────────► │                  │
       │                  │                  │                  │
       │                  │                  │ 10. Update Location
       │                  │                  │ ──────────────► │
       │                  │                  │                  │
       │                  │                  │ 11. Update Location Ack
       │                  │                  │ ◄────────────── │
       │                  │                  │                  │
       │                  │ 12. Initial Context Setup Request │
       │                  │ ◄────────────── │                  │
       │                  │                  │                  │
       │ 13. RRC Reconfiguration             │                  │
       │ ◄────────────── │                  │                  │
       │                  │                  │                  │
       │ 14. RRC Reconfiguration Complete    │                  │
       │ ──────────────► │ 15. Initial Context Setup Response │
       │                  │ ──────────────► │                  │
       │                  │                  │                  │
       │ 16. Attach Accept│                  │                  │
       │ ◄────────────── │ ◄────────────── │                  │
       │                  │                  │                  │
       │ 17. Attach Complete                 │                  │
       │ ──────────────► │ ──────────────► │                  │
```

### 5G New Radio (NR)

#### 5G Network Architecture

```
5G Network Architecture:
┌─────────────────────────────────────────────────────────────┐
│                    5G System (5GS)                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ ┌─────────────┐    ┌─────────────┐    ┌─────────────┐       │
│ │     UE      │    │    gNB      │    │    5GC      │       │
│ │ (User       │    │ (Next       │    │ (5G Core    │       │
│ │ Equipment)  │    │ Generation  │    │ Network)    │       │
│ │             │    │ Node B)     │    │             │       │
│ └──────┬──────┘    └──────┬──────┘    └──────┬──────┘       │
│        │                  │                  │              │
│        │ Uu Interface     │ NG Interface     │              │
│        │ ◄──────────────► │ ◄──────────────► │              │
│        │                  │                  │              │
│        │                  │                  │              │
│ ┌──────▼──────┐    ┌──────▼──────┐    ┌──────▼──────┐       │
│ │   Radio     │    │   Radio     │    │   Core      │       │
│ │ Interface   │    │ Access      │    │  Network    │       │
│ │             │    │ Network     │    │             │       │
│ └─────────────┘    └─────────────┘    └─────────────┘       │
│                                                             │
└─────────────────────────────────────────────────────────────┘

5G Core Network Functions:
┌─────────────────────────────────────────────────────────────┐
│                    5G Core (5GC)                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │
│ │     AMF     │  │     SMF     │  │     UPF     │           │
│ │ (Access &   │  │ (Session    │  │ (User Plane │           │
│ │ Mobility    │  │ Management  │  │ Function)   │           │
│ │ Management  │  │ Function)   │  │             │           │
│ │ Function)   │  │             │  │             │           │
│ └──────┬──────┘  └──────┬──────┘  └──────┬──────┘           │
│        │                │                │                  │
│        │                │                │                  │
│ ┌──────▼──────┐  ┌──────▼──────┐  ┌──────▼──────┐           │
│ │     UDM     │  │     PCF     │  │     NRF     │           │
│ │ (Unified    │  │ (Policy     │  │ (Network    │           │
│ │ Data        │  │ Control     │  │ Repository  │           │
│ │ Management) │  │ Function)   │  │ Function)   │           │
│ └─────────────┘  └─────────────┘  └─────────────┘           │
│                                                             │
│ ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │
│ │     AUSF    │  │     NSSF    │  │     NEF     │           │
│ │ (Authentication│ (Network    │  │ (Network    │           │
│ │ Server      │  │ Slice       │  │ Exposure    │           │
│ │ Function)   │  │ Selection   │  │ Function)   │           │
│ │             │  │ Function)   │  │             │           │
│ └─────────────┘  └─────────────┘  └─────────────┘           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### 5G Key Technologies

```
5G Technology Comparison:
┌─────────────────┬─────────────────┬─────────────────┬─────────────────┐
│    Feature      │      4G LTE     │      5G NSA     │      5G SA      │
├─────────────────┼─────────────────┼─────────────────┼─────────────────┤
│ Peak Speed      │ 1 Gbps          │ 2-3 Gbps        │ 10+ Gbps        │
│ Latency         │ 10-20 ms        │ 8-12 ms         │ 1-5 ms          │
│ Core Network    │ EPC             │ EPC             │ 5GC             │
│ Control Plane   │ 4G              │ 4G              │ 5G              │
│ User Plane      │ 4G              │ 4G/5G           │ 5G              │
│ Network Slicing │ No              │ Limited         │ Full            │
│ Edge Computing  │ Limited         │ Limited         │ Native          │
└─────────────────┴─────────────────┴─────────────────┴─────────────────┘

5G Frequency Bands:
┌─────────────────┬─────────────────┬─────────────────┬─────────────────┐
│      Band       │   Frequency     │   Bandwidth     │    Use Case     │
├─────────────────┼─────────────────┼─────────────────┼─────────────────┤
│ Low Band        │ < 1 GHz         │ 5-20 MHz        │ Wide Coverage   │
│ (Sub-6)         │ 600-900 MHz     │                 │ Rural Areas     │
├─────────────────┼─────────────────┼─────────────────┼─────────────────┤
│ Mid Band        │ 1-6 GHz         │ 20-100 MHz      │ Urban Coverage  │
│ (Sub-6)         │ 2.5, 3.5 GHz    │                 │ Capacity        │
├─────────────────┼─────────────────┼─────────────────┼─────────────────┤
│ High Band       │ 24-100 GHz      │ 100-800 MHz     │ Ultra-high      │
│ (mmWave)        │ 28, 39 GHz      │                 │ Speed/Capacity  │
└─────────────────┴─────────────────┴─────────────────┴─────────────────┘
```

#### 5G Use Cases and Network Slicing

```
5G Use Cases:
┌─────────────────────────────────────────────────────────────┐
│                    5G Use Cases                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │
│ │   eMBB      │  │    URLLC    │  │    mMTC     │           │
│ │ (Enhanced   │  │ (Ultra      │  │ (Massive    │           │
│ │ Mobile      │  │ Reliable    │  │ Machine     │           │
│ │ Broadband)  │  │ Low Latency │  │ Type        │           │
│ │             │  │ Comms)      │  │ Comms)      │           │
│ └──────┬──────┘  └──────┬──────┘  └──────┬──────┘           │
│        │                │                │                  │
│        ▼                ▼                ▼                  │
│ • 4K/8K Video    • Autonomous     • IoT Sensors            │
│ • AR/VR          • Industrial      • Smart Cities          │
│ • Gaming         • Remote Surgery  • Agriculture           │
│ • Streaming      • Robotics        • Asset Tracking        │
│                                                             │
└─────────────────────────────────────────────────────────────┘

Network Slicing:
┌─────────────────────────────────────────────────────────────┐
│                   Network Slicing                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                    Physical Infrastructure                  │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │              5G Network Resources                       │ │
│ └─────────────────────────────────────────────────────────┘ │
│                           │                                 │
│        ┌──────────────────┼──────────────────┐              │
│        │                  │                  │              │
│ ┌──────▼──────┐    ┌──────▼──────┐    ┌──────▼──────┐       │
│ │   Slice 1   │    │   Slice 2   │    │   Slice 3   │       │
│ │    eMBB     │    │   URLLC     │    │    mMTC     │       │
│ │             │    │             │    │             │       │
│ │ • High BW   │    │ • Low Lat   │    │ • High Conn │       │
│ │ • Mobility  │    │ • Reliable  │    │ • Low Power │       │
│ │ • Consumer  │    │ • Critical  │    │ • Sensors   │       │
│ └─────────────┘    └─────────────┘    └─────────────┘       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### 5G Protocol Stack

```
5G NR Protocol Stack (User Plane):
┌─────────────────────────────────────────────────────────────┐
│                    User Equipment (UE)                     │
├─────────────────────────────────────────────────────────────┤
│                   Application                               │
├─────────────────────────────────────────────────────────────┤
│                      IP                                     │
├─────────────────────────────────────────────────────────────┤
│                     SDAP                                    │
│         (Service Data Adaptation Protocol)                 │
├─────────────────────────────────────────────────────────────┤
│                     PDCP                                    │
│            (Packet Data Convergence Protocol)              │
├─────────────────────────────────────────────────────────────┤
│                      RLC                                    │
│              (Radio Link Control)                          │
├─────────────────────────────────────────────────────────────┤
│                      MAC                                    │
│             (Medium Access Control)                        │
├─────────────────────────────────────────────────────────────┤
│                      PHY                                    │
│                 (Physical Layer)                           │
└─────────────────────────────────────────────────────────────┘

5G NR Protocol Stack (Control Plane):
┌─────────────────────────────────────────────────────────────┐
│                    User Equipment (UE)                     │
├─────────────────────────────────────────────────────────────┤
│                      NAS                                    │
│             (Non-Access Stratum)                           │
├─────────────────────────────────────────────────────────────┤
│                      RRC                                    │
│            (Radio Resource Control)                        │
├─────────────────────────────────────────────────────────────┤
│                     PDCP                                    │
├─────────────────────────────────────────────────────────────┤
│                      RLC                                    │
├─────────────────────────────────────────────────────────────┤
│                      MAC                                    │
├─────────────────────────────────────────────────────────────┤
│                      PHY                                    │
└─────────────────────────────────────────────────────────────┘
```

#### Interview-Worthy 5G Concepts

**Key 5G Technologies:**
- **Massive MIMO**: 64-256 antenna elements for beamforming
- **Beamforming**: Directional signal transmission
- **Carrier Aggregation**: Up to 32 component carriers
- **Dual Connectivity**: Simultaneous 4G and 5G connections
- **Network Function Virtualization (NFV)**: Software-based network functions
- **Software Defined Networking (SDN)**: Centralized network control

**5G Security Enhancements:**
- **Enhanced Authentication**: 5G-AKA protocol
- **Network Slicing Security**: Isolation between slices
- **Edge Computing Security**: Distributed security functions
- **Privacy Protection**: SUPI (Subscription Permanent Identifier) encryption

**5G Performance Targets:**
- **Peak Data Rate**: 20 Gbps downlink, 10 Gbps uplink
- **User Experience**: 100 Mbps downlink, 50 Mbps uplink
- **Latency**: 1ms for URLLC, 4ms for eMBB
- **Connection Density**: 1 million devices per km²
- **Mobility**: Up to 500 km/h
- **Energy Efficiency**: 100x improvement over 4G
- **Spectrum Efficiency**: 3x improvement over 4G

---
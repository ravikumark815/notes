# Networking Notes
### Terminology:
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

### Types of Networks based on Area:
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

### Types of Networks based on Topology:
- Mesh Topology
- Ring Topology
- Bus Topology
- Star Topology
- Hybrid Topology
- Point to Point Topology

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/topologies.png)

### Signaling:
- **Baseband Signaling:** Can only transmit a single signal at any given time. 
- **Broadband Signaling:** Can transmit multiple signals at any given time. 
 
### Cable Types:
- **Coaxial Cabling:** Coaxial cable has an inner conductor that runs down the middle of the cable. This type of cabling comes in two types, thinnet and thicknet. Max Transmission Speed of 10 Mbps
- **Twisted-pair Cabling:** Has four pair of wires.  It comes in two versions, UTP (Unshielded Twisted-Pair) and STP (Shielded Twisted-Pair). Uses 8P8C/RJ45 Connector
- **Fiber-optic Cabling:** Uses optical fibers to transmit data in the form of light signals. There are two types of fiber-optic cables - Single-mode fiber (SMF) and Multi-mode fiber (MMF). Uses ST/SC Connectors

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/cables.png)

### Ethernet Standards:
- **10Base-T (IEEE 802.3):** 10 Mbps with category 3 unshielded twisted pair (UTP) wiring, up to 100 meters long.
- **100Base-TX (IEEE 802.3u):** known as Fast Ethernet, uses category 5, 5E, or 6 UTP wiring, up to 100 meters long.
- **100Base-FX (IEEE 802.3u):** a version of Fast Ethernet that uses multi-mode optical fiber. Up to 412 meters long.
- **1000Base-CX (IEEE 802.3z):** uses copper twisted-pair cabling. Up to 25 meters long.
- **1000Base-T (IEEE 802.3ab):** Gigabit Ethernet that uses Category 5 UTP wiring. Up to 100 meters long.
- **1000Base-SX (IEEE 802.3z):** 1 Gigabit Ethernet running over multimode fiber-optic cable.
- **1000Base-LX (IEEE 802.3z):** 1 Gigabit Ethernet running over single-mode fiber.
- **10GBase-T (802.3.an):** 10 Gbps connections over category 5e, 6, and 7 UTP cables.

### Cable Categories:
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

### Other Cables:
Direct Attachment Cable (DAC) Copper Twinax:
- Comes in various lengths with SFPs at each end.
- SFP: Hot pluggable transceiver. 
- SFPs supports various connectors and data rates up to 10Gbps. 
- Roll over cable: Special cable used in Cisco environment to connect a com port to console port.

### Ethernet Cable Forms:
- **Straight-through Cable:** On a straight through cable, the wired pins match. Straight through cable use one wiring standard: both ends use T568A wiring standard or both ends use T568B wiring standard. 
- **Crossover Cable:** Crossover cable uses two different wiring standards: one end uses the T568A wiring standard, and the other end uses the T568B wiring standard. Pin1->Pin3 and Pin2->Pin6

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/straight-through.png)
![](https://github.com/ravikumark815/networking/blob/main/Notes-images/crossover.png)

> **Medium Dependent Interface (MDI):** It is a type of ethernet port connection that uses twisted-pair cabling to link two network devices. MDIX (MDI Crossover) is a version of MDI that enables connection between like devices.

### Data flow Types:
- **Simplex Mode:** Communication is unidirectional.
- **Half-Duplex Mode:** Each station can both transmit and receive, but not at the same time.
- **Full-Duplex Mode:** Both stations can transmit and receive simultaneously.
 
![](https://github.com/ravikumark815/networking/blob/main/Notes-images/data-flow.png)

### Communication Types:
- **Unicast:** Communication from one point to another point
- **Broadcast:** Communication from one point to all other points
- **Multicast:** Communication from one/more points to a set of other points
- **Anycast:** It is a network addressing and routing methodology in which a single destination IP address is shared by nodes in multiple locations.
![](https://github.com/ravikumark815/networking/blob/main/Notes-images/communication-types.png)

### Network Domain:
- **Broadcast Domain:** A broadcast domain is a logical division of a computer network, in which all nodes can reach each other by broadcast at the data link layer.
- **Collision Domain:** A collision domain is a network segment connected by a shared medium where simultaneous data transmissions collide with one another. 

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/network-domains.png)

> **54321 Rule:**
- 5 - the number of network segments
- 4 - the number of repeaters needed to join the segments into one collision domain
- 3 - the number of network segments that have active (transmitting) devices attached
- 2 - the number of segments that do not have active devices attached
- 1 - the number of collision domains

### Layered Models: 
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

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/cisco-3-layer.png)

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
![](https://github.com/ravikumark815/networking/blob/main/Notes-images/mac.png)

### Carrier Sense Multiple Access/Collision Detection (CSMA/CD):
-  Used to find if any other device sending traffic in a bus topology to avoid collisions in a CD. 
-  Before sending traffic, a device broadcasts if another device is communicating. If there is no response, it goes ahead and sends traffic. 
-  If a collision takes place, a backoff/jam signal is sent. 

### Data Flow in Hub, Bridge, Switch, Router:

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/data-flow-topo.png)

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

## Layer 2
**Ethernet:**

*1. Header:*
<br>![](https://github.com/ravikumark815/networking/blob/main/Notes-images/ethernet-header.png)

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

**VLAN Trunking Protocol (VTP):**
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

## Layer 3
**Internet Protocol [IP]:**

*1. Header:*
![](https://github.com/ravikumark815/networking/blob/main/Notes-images/ip-header.png)
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
![](https://github.com/ravikumark815/networking/blob/main/Notes-images/icmp-header.png)

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

## Layer 4

**Transmission Control Protocol [TCP]:**

*1. Header:*

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/tcp-header.png)
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

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/3-way.png)

- `SYN`: Client sends a TCP segment with SYN=1 Sequence_No=A (Random)
- `SYN-ACK`: Server responds: SYN=1 ACK=1 Sequence_Mo=B (Random) Ack_No=A+1
- `ACK`: Client sends: ACK=1 Sequence_No=A+1 Ack No=B+1

*3. TCP Connection Termination [4-Way Handshake]*

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/4-way.png)

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

**User Datagram Protocol [UDP]**

*1.Header*

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/udp-header.png)

## Layer 7

### Dynamic Host Configuration Protocol [DHCP]
- Used to manage IP allocation in a network
- Packet Flow:
    ![](https://github.com/ravikumark815/networking/blob/main/Notes-images/dhcp-dora.png)
    
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

### Domain Name Server [DNS]:
- DNS is a protocol that is used to convert easily readable names for communicating over the network, instead of remembering IP Address.
- Port: `53 UDP`
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

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/dns-query.png)

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

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/IKE-phase1-main.png)

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/IKE-phase2-quick.png)

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

![](https://github.com/ravikumark815/networking/blob/main/Notes-images/SSL-handshake.png)
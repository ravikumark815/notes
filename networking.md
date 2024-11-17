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
1.	Physical Layer (Bits)
2.	Datalink Layer (Frame)
3.	Network Layer (Packet)
4.	Transport Layer (Segment)
5.	Session Layer (Data)
6.	Presentation Layer (Data)
7.	Application Layer (Data)

**TCP/IP Model (4):**
1.	Physical Layer (Frame): Physical Addresses (MAC)
2.	Network Layer (Packet): IP Addresses (IP)
3.	Transport Layer (Segment): Port Addresses (Ports)
4.	Application Layer (Data): Specific Addresses (Data)

**TCP/IP Model (5 – In use by CCNA):**
1.	Physical Layer (Bits)
2.	Datalink Layer (Frame): Physical Address (MAC)
3.	Network Layer (Packet): IP Addresses (IP)
4.	Transport Layer (Segment): Port Addresses (Ports)
5.	Application Layer (Data): Specific Addresses (Data)

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

- Exceptions, Reservations and Special addresses:
<br>&nbsp; • 0.0.0.0/8 - Default network
<br>&nbsp; • 127.0.0.0/8 – Local Loopback address. 
<br>&nbsp; • 224.0.0.X – Link local multicasts, generally used by routing tables.
<br>&nbsp; • 224.0.0.5-224.0.0.6 - OSPF
<br>&nbsp; • Directed Broadcast address: Fill 1s in the entire host portion of the address.
<br>&nbsp; • Local Broadcast address: Fill 1s in all 32 bits. Generally used for DHCP address
<br>&nbsp; • 10.0.0.0/8 – Private IP address range (not routable on internet)
<br>&nbsp; • 172.16.0.0/12 – Private IP address range (not routable on internet)
<br>&nbsp; • 192.168.0.0/16 – Private IP address range (not routable on internet)
<br>&nbsp; • 169.254.0.0/16 – Non-routable Link Local Addresses (Automatic Private IP Addressing)

- Subnet Masks:
<br>&nbsp; • Used to determine network and host portion of a given IP address through AND operation.
<br>&nbsp; • Is the device remote (route through default gateway) or local (ARP)?
<br>&nbsp; • Class A: 255.0.0.0
<br>&nbsp; • Class B: 255.255.0.0
<br>&nbsp; • Class C: 255.255.255.0
<br>&nbsp; • Discontinuous subnet masks not supported:
`11110000.11111111.00000110.11000000 (240.244.3.191)`
<br>&nbsp; • Only contiguous subnet masks are supported.
`11111111.11110000.00000000.00000000 (255.240.0.0)`

- Classless Inter Domain Routing (CIDR):
<br>&nbsp; • Replaces classful IP addressing with variable length subnet mask (VLSM)
<br>&nbsp; • CIDR notation /X where X denotes number of 1’s present in binary form of a subnet mask.
<br>&nbsp; • Reduces wastage of big number of addresses.
<br>&nbsp; • Ex: /11 = 255.224.0.0

- **Subnetting:**
<br>&nbsp; • Work the following for a given IP address: Network address, First IP address, Last IP address, Broadcast address. 
<br>&nbsp; • Binary method to work an IP address:
<br>&nbsp; &nbsp; • Subnet address: Fill the host portion with binary 0s.
<br>&nbsp; &nbsp; • Broadcast address: Fill the host portion with binary 1s.
<br>&nbsp; &nbsp; • First host: Fill the host portion with binary 0s and set the last bit to 1.
<br>&nbsp; &nbsp; • Last host: Fill the host portion with binary 1s and set the last bit to 0.
<br>&nbsp; &nbsp; • Ex: 172.16.35.123/20:
<br>&nbsp; &nbsp; Subnet: 172.16.0010 0000.0000 0000 = 172.16.32.0
<br>&nbsp; &nbsp; 1st Host: 172.16.0010 0000.0000 0001 = 172.16.32.1
<br>&nbsp; &nbsp; Last Host: 172.16.0010 1111.1111 1110 = 172.16.47.254
<br>&nbsp; &nbsp; Broadcast: 172.16.0010 1111.1111 1111 = 172.16.47.255
<br>&nbsp; • Number of hosts in a network: 2h – 2 (h = number of bits in host portion)
<br>&nbsp; • Number of networks: 2n (n = number of bits in network portion)
<br>&nbsp; • Number of subnets: 2n (n = number of bits in variating network octet)

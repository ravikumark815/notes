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
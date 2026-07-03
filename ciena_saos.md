## New SAOS 10 updated from monolithic to microservice based architecture
	- Disaggregated from the fixed hardware
	- Microservice based modular operating system
	- Utilized x86 based architecture
	- Provides NETCONF/YANG support
	- Service support for carrier ethernet, IP, MPLS, L2 VPNs and L3 VPNs


## Disaggregation:
	- Allows incremental partial upgrades without affecting entire codebase
	- Containers are independent and version controlled

## Programmability:
	- CLI (Uses NETCONF in the backend)
	- SNMP
	- NETCONF
	- YANG
    - Automation (blueplanet, ciena navigator, cnm)

## Architecture:
### Hardware:
	- CPU
	- Memory
	- Disk
	- Platform Hardware: Switching Silicon, SFPs, Fans, Sensors
### Software:
	- Installed through Ciena's Zero Touch Provisioning (ZTP)
	- ZTP enabled automatic configuration
	- Installation of SAOS 10 is done through ONIE (Open Network Install Environment) :: Open source install environment that acts as an enhanced bootloader utilizing facilities in a linux busy box environment

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                    YANG Model Management Plane and Front-end Database               │   
├────────────────────────────────┐────────────────────────────┐───────────────────────┤   ┌────────────┐
│     Ethernet Control Plane     |     MPLS Control Plane     │    IP Control Plane   |   │            |
├────────────────────────────────┘────────────────────────────┘───────────────────────┤   │Distributed |
│                                          Dataplane                                  │   │Infra       |
├─────────────────────────────────────────────────────────────────────────────────────┤   │Structure   |
│                                Hardware Abstraction Layer                           │   │Backend     |
├─────────────────────────────────────────────┐───────────────────────────────────────┤   │DB          |
│                   Ciena vSwitch             |        Switch Abstraction Layer       │   │            |
├─────────────────────────────────────────────┘───────────────────────────────────────┤   └────────────┘
│                                        Containers                                   │   
├─────────────────────────────────────────────────────────────────────────────────────┤   
│                                Linux Kernel and Utilities                           │
└─────────────────────────────────────────────────────────────────────────────────────┘
```


### Supports:
- Northbound interfaces including CLI
- SNMP support for traps and informs
- NBI, telemetry monitoring, statstics using gNMI

#### gNMI:
- A unified management protocol for streaming telemetry data
- Uses gRPC, which defines remote procedure call framework


## Terminology
### Logical Port:
- A port that is directly mapped to a physical port or LAG port that is mapped to a number of physical ports
- They can provide the attachment point for service creation

### Forwarding Domain:
- Its a vSwitch that can coexist with many other FDs within the system
- They allow the system to provide a variety of methods for classification, seggregation and flexibility in frame processing. 
- They basically segment the system by creating a mac-flood environment (broadcast domain)

### Flow Points:
- Virtual connection points to a Forwarding Domain
- Flow Points attach to a forwarding domain.
- They can attached to a logical port at the same time.
- A single flow point may be assiciated only with a single forwarding domain

### Classifier:
- Determine which traffic belongs to a particular flow point
- Each flow point is configured with one or more classifiers
- Classfiers can be used with one or more Flow Points
- Essentially they define what traffic can flow through an FD as shown in the diagram below
- With classifiers - we can include multiple VLANs, untagged frames, control frame traffic etc. 

### ETTP:
- A logical port maps to one or more Ethernet Trail Termination Point (ETTPs). The physical port on a system is an ETTP. 
- They are created automatically and they couple a transciever XCVR to a port

### L3 interfaces:
- They facilitate the operation of IP and MPLS protocols to drive the control-plane functionality
- They associate to the lower-layer objects, FD, FPs. 

![](https://github.com/ravikumark815/notes/blob/main/images/ciena_saos-l2l3.png)

## SAOS 10 Security
- Defines how to manage and protect resources from unauthorized and detrimental access
- Supports a bunch of security parameters: 
    - MacSec
    - User Access Security
    - SSH Public Key Auth
    - X.509 Certificates
    - 802.1x
    - TLS
    - Secure Boot

## SAOS 10 OAM: Telemetry Data
- Provides a full operation, administration and maintenance suite for alarms, statistics and data monitoring which is collected through the NETCONF/YANG interface. 
- A microservice named telemetry is running all the time using which information is collected
- Also supports gRPC/gNMI push based interfaces.  There is a built in gNMI client for this purpose. 
- Secure communication of this telemetry data using TLS. SNMPv1 and v2 are supported as well. 
- Ex: Statistics, CPU, memory usage, FP stats, transciever events etc. 
- 802.1ag CFM is supported: 
    - Connectivity Fault Management. 
    - CFM uses Continuity Check  messages (CCM) at an interval to Maintenance End Points (MEPs) using Maintenance Association (MA). 
    - The trace links and loopback messages to locate a fault more specifically. 
    - Hierarchical Fault management
- Supports Y.1731 Performance Monitoring standard (Frame delay measurement) that use Delay Measurement messages (DMM) and Delay Measurement Reply (DMR) with timers to measure performance. 
- Supports 802.3ah EOAM standard: Ethernet in first mile routers. Uses EOAM PDUs for link failure discovery.
- Supports RFC 2544 Service Assurance Testing. Focused on network performance - benchmarking mostly. Throughput, burstability, frame-loss test, latency test, rtt, interface testing etc.
- Zero Touch Provisioning (ZTP), Secure Zero Tech Provisioning (SZTP over TLS), RFC based SZTP. 

## SAOS 10 QoS Support:
- Scheduled Services based on priorities of interfaces. 
- By default egress shaping is disabled for all logical ports. 
- Hierarchal Egress QoS consists of:
    - Scheduling at more than one level relative to a logical-port
    - Multiple Queue Group instances per logical-port. Each queue-group instance is being scheduled independently. 

![](https://github.com/ravikumark815/notes/blob/main/images/ciena_saos-qos_egress.png)

## SAOS 10 Supported Platforms
### 39xx Family:
- Cost-effective, compact, upto 10Gigabit ethernet
- Support PONs, MPLS, IP etc.
- 3922, 3924, 3926, 3928, 3948, 3984, 3985

### 51xx Family:
- Effecient aggregation of higher capacity links, PON, IP, Segment Routing etc.
- OAM, QoS
- 5130, 5131, 5132, 5144, 5162, 5164, 5166, 5168, 5170, 5171

### 81xx Family:
- Coherent aggregation routers and switches
- 1GbE - 100GbE
- WaveLogicAi module support, pluggables etc.
- 8110, 8112, 8114, 8180, 8190

## Licensing:
- License service starts with software initialization
- Entitlements: perpetual, trial, subscription
- Application: 39xx, 51xx, 81xx can be chosen during setup
- Built in trial license: 90 days, no license portal needed

### Licenses can be processed in 2 ways:
- Local Licensing: Registration request file is generated from the node, uploaded to ciena portal, a license file is downloaded from the portal and uploaded to the node 
- License Server: Nodes can be configured with license server, and the rest is same as above 


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


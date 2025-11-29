# DPDK (Data Plane Development Kit)

## Preset
- **Created by**: Intel, now a Linux Foundation project.
- **Purpose**: A set of libraries and drivers for fast packet processing in user space.
- **Key Principle**: Bypass the kernel's network stack to achieve high throughput and low latency.
- **Official Docs**: [doc.dpdk.org](https://doc.dpdk.org)

## Table of Contents

- [Core Concepts](#core-concepts)
- [DPDK vs. Kernel Networking](#dpdk-vs-kernel-networking)
- [The Kernel Networking Path](#the-kernel-networking-path)
- [Architecture](#architecture)
- [UIO vs VFIO](#uio-vs-vfio)
- [Key Libraries & Components](#key-libraries--components)
  - [EAL (Environment Abstraction Layer)](#eal-environment-abstraction-layer)
  - [Mbuf (`rte_mbuf`)](#mbuf-rte_mbuf)
  - [Mempool (`rte_mempool`)](#mempool)
  - [Ring (`rte_ring`)](#ring)
  - [Ethdev (`rte_ethdev`)](#ethdev)
  - [Poll Mode Driver (PMD)](#poll-mode-driver)
- [Packet Processing Flow](#packet-processing-flow)
- [Setup & Compilation](#setup-&-compilation)
- [Running a DPDK Application](#running-a-dpdk-application)
- [Performance Tuning](#performance-tuning)
- [Vhost-user & Virtio](#vhost-user-&-virtio)
- [Cryptodev](#cryptodev)
- [Eventdev](#eventdev)
- [Flow API (`rte_flow`)](#flow-api)
- [Troubleshooting & Debugging](#troubleshooting-&-debugging)
---

## Core Concepts

DPDK achieves high performance by moving packet processing from the kernel to user space and employing several key techniques.

```
  Kernel Space Networking (Slow Path)        |      DPDK Kernel Bypass (Fast Path)
---------------------------------------------|--------------------------------------------
| +------------------+                        |   +------------------+
| |   Application    |                        |   | DPDK Application |
| +------------------+                        |   +------------------+
|        |  (syscall)                         |        | (direct access)
|        v                                    |        v
| +------------------+                        | +------------------+
| | Kernel TCP/IP    |                        | | Poll Mode Driver |
| |      Stack       |                        | |      (PMD)       |
| +------------------+                        | +------------------+
|        |  (interrupt)                       |        | (polling)
|        v                                    |        v
| +------------------+                        | +------------------+
| |   NIC Driver     |                        | |       NIC        |
| +------------------+                        | +------------------+
|        |                                    |
|        v                                    |
| +------------------+                        |
| |       NIC        |                        |
| +------------------+                        |
---------------------------------------------+--------------------------------------------
```

| Concept | Description | Benefit |
| :--- | :--- | :--- |
| **Kernel Bypass** | DPDK applications directly access NIC hardware, avoiding the overhead of the kernel's network stack (system calls, context switches). | Drastically reduced latency and higher throughput. |
| **Poll Mode Drivers (PMDs)** | Instead of using interrupts to signal packet arrival, DPDK continuously polls the NIC's receive queues. | Eliminates interrupt handling overhead, providing deterministic, low-latency packet reception. |
| **CPU Affinity / Core Pinning** | Dedicating specific CPU cores to DPDK tasks (polling, processing) to avoid context switching and improve cache efficiency. | Predictable performance, avoids scheduler overhead. |
| **Hugepages** | Using large memory pages (e.g., 2MB or 1GB instead of the standard 4KB) to reduce misses in the TLB (Translation Lookaside Buffer), a CPU cache for memory addresses. | Faster memory access for packet buffers and other data structures, as the CPU spends less time looking up physical memory locations. |
| **Zero-Copy Buffers** | Packet data is processed directly from the buffers where the NIC placed it via **DMA (Direct Memory Access)**, without being copied between kernel and user space. | Reduces memory bandwidth usage and CPU cycles that would be wasted on copying data. |

## DPDK vs. Kernel Networking

| Feature | Kernel Networking Stack | DPDK |
| :--- | :--- | :--- |
| **Processing Location** | Kernel space | User space |
| **Packet Reception** | Interrupt-driven | Polling (PMD) |
| **Memory Management** | Kernel `sk_buff`s, standard pages | User space `mbuf`s, hugepages |
| **CPU Scheduling** | Kernel scheduler (preemptive) | Run-to-completion on dedicated cores |
| **API** | POSIX Sockets API (`send`, `recv`) | DPDK APIs (`rte_eth_rx_burst`, `rte_eth_tx_burst`) |
| **Performance** | General purpose, lower throughput | High performance, low latency |
| **Use Case** | General networking, web servers | NFV, vSwitches, firewalls, high-speed routers |

---

## The Kernel Networking Path (The Slow Path)

To understand why DPDK is so fast, it's essential to first understand the traditional networking path through the operating system's kernel, which is optimized for general-purpose use, not high performance.

```
  +------------------+
  |   Application    |
  +------------------+
        ^      | 6. Data copied from kernel to user space
        |      v 5. Packet traverses kernel TCP/IP stack
  +------------------+
  |   Kernel Space   |
  +------------------+
        ^      | 4. Data copied from NIC buffer to kernel memory (sk_buff)
        |      v 3. CPU context switch to handle interrupt
  +------------------+
  |    NIC Driver    |
  +------------------+
        ^      | 2. NIC raises an interrupt
        |      v 1. Packet arrives at NIC via DMA
  +------------------+
  |       NIC        |
  +------------------+
```

1.  **Packet Arrival & DMA**: A packet arrives at the Network Interface Card (NIC). The NIC uses **Direct Memory Access (DMA)** to write the packet data into a pre-allocated buffer in kernel memory without involving the CPU.
2.  **Interrupt**: Once the packet is in memory, the NIC sends a hardware interrupt to the CPU to signal that a new packet has arrived.
3.  **Context Switch & Interrupt Handling**: The CPU stops what it's doing (a *context switch*), saves its state, and executes the NIC driver's interrupt handler. This is a significant source of overhead.
4.  **Data Copy to `sk_buff`**: The driver copies the packet data from the DMA buffer into the kernel's internal network buffer structure, known as a socket buffer (`sk_buff`). This memory copy consumes CPU cycles and memory bandwidth.
5.  **Kernel Stack Processing**: The packet travels up the kernel's network stack (e.g., TCP/IP stack), where it is processed at each layer (IP, TCP/UDP). This involves more CPU work for checksums, header parsing, and firewall rule checks.
6.  **Copy to User Space**: Finally, the data is copied from the kernel's `sk_buff` into the memory of the user-space application that is waiting for it (e.g., via a `recv()` system call).
7.  **Application Wake-up**: The kernel wakes up the application process, which can now use the data.

**Key Overheads Bypassed by DPDK:**
-   **Interrupts**: Polling is more efficient for high packet rates.
-   **Context Switches**: Dedicating cores to polling avoids this.
-   **Memory Copies**: Zero-copy approach avoids moving data between kernel and user space.
-   **System Calls**: Direct hardware access avoids the overhead of `send()` and `recv()`.


---

## Architecture

DPDK is structured as a set of libraries built on top of the Environment Abstraction Layer (EAL).

```
+-----------------------------------------------------------------+
|                     DPDK Application                            |
| (e.g., L3 Forwarding, OVS-DPDK, Firewall)                       |
+-----------------------------------------------------------------+
|         DPDK Libraries (APIs for application development)       |
|                                                                 |
|  librte_ethdev   librte_cryptodev   librte_eventdev  librte_flow  |
|  librte_ring     librte_mempool     librte_mbuf      librte_timer |
+-----------------------------------------------------------------+
|        EAL (Environment Abstraction Layer)                      |
|  - Core/Memory Management (Hugepages, CPU Affinity)             |
|  - Hardware Abstraction (PCI, Bus enumeration)                  |
|  - Generic device drivers                                       |
+-----------------------------------------------------------------+
|         Kernel Space (Linux/FreeBSD)                            |
|                                                                 |
|  UIO / VFIO Drivers   Hugepages Driver   Kernel Services        |
+-----------------------------------------------------------------+
|                       Hardware                                  |
|  - NICs (Intel, Mellanox, etc.)                                 |
|  - Crypto Accelerators                                          |
|  - CPU, Memory                                                  |
+-----------------------------------------------------------------+
```

### UIO vs VFIO

-   **UIO (Userspace I/O)**: An older kernel framework that allows a device's memory to be mapped into user space. It's simple but lacks security, as it doesn't provide memory isolation. A misbehaving driver could access any part of system memory.
-   **VFIO (Virtual Function I/O)**: The modern, secure framework for user-space drivers. It leverages the **IOMMU (Input-Output Memory Management Unit)**—a hardware component—to create isolated memory regions for each device. This means a DPDK application can only access its own device's memory, preventing it from interfering with the kernel or other processes. **VFIO is the recommended driver for DPDK.**

> **What is an IOMMU?** Think of it as an MMU (Memory Management Unit) for your I/O devices. Just as an MMU translates virtual addresses to physical addresses for the CPU, an IOMMU does the same for devices like NICs, ensuring they can only access the specific memory regions they've been granted permission to. This is critical for security and stability.

---

## Key Libraries & Components

### EAL (Environment Abstraction Layer)
The EAL is the core of DPDK, responsible for initializing the environment and providing a hardware-agnostic API to the upper layers.
- **Responsibilities**:
  - Loading drivers and probing devices.
  - Allocating hugepages and other memory resources.
  - Handling CPU affinity and core pinning.
  - Abstracting platform-specific details (PCI bus, memory layout).
- **Initialization**: Every DPDK application must start by calling `rte_eal_init()`.

### Mbuf (`rte_mbuf`)
The `mbuf` is the fundamental data structure for carrying network packets. It's a small metadata structure prepended to a larger buffer that holds the actual packet data.

```
  +--------------------------------+
  |         rte_mbuf (metadata)    |
  |--------------------------------|
  |         (headroom)             |
  |--------------------------------| <--- data_off
  |         Packet Data            |
  |         (e.g., Ethernet, IP)   |
  |                                |
  |--------------------------------|
  |         (tailroom)             |
  +--------------------------------+
```

```c
struct rte_mbuf {
    // ... cache-aligned fields ...
    void *buf_addr;          // Start of buffer.
    phys_addr_t buf_physaddr; // Physical address of buffer.
    uint16_t buf_len;        // Length of the buffer.

    // ... fields for packet manipulation ...
    uint16_t data_off;       // Start of data in buffer.
    uint16_t data_len;       // Length of data.
    uint16_t pkt_len;        // Total packet length (including segments).

    struct rte_mempool *pool; // Mempool it was allocated from.
    struct rte_mbuf *next;    // Next segment in a chained buffer.
    // ... and many more fields for offloads, VLAN tags, etc.
};
```

### Mempool (`rte_mempool`)
A `mempool` is a pre-allocated pool of fixed-size objects in memory, typically `mbufs`. It uses a lockless ring to provide extremely fast and efficient allocation/deallocation, avoiding costly system calls (`malloc`/`free`) in the fast path.

- **Per-Core Cache**: To further reduce contention on the shared ring, each core maintains a local cache of objects from the mempool. This makes allocations and frees even faster, as they often need to access the shared pool at all.

```
  +-------------------------------------------------+
  |                  rte_mempool                    |
  |-------------------------------------------------|
  |  +-----------------+                            |
  |  | rte_ring (free) | --> [mbuf_ptr] [mbuf_ptr] ... |
  |  +-----------------+                            |
  |                                                 |
  |  +-------------------------------------------+  |
  |  | Contiguous Memory Block for All Objects   |  |
  |  | [mbuf1] [mbuf2] [mbuf3] [mbuf4] ...       |  |
  |  +-------------------------------------------+  |
  +-------------------------------------------------+
```

```c
// Create a mempool for mbufs
struct rte_mempool *mbuf_pool = rte_pktmbuf_pool_create("MBUF_POOL",
                                                      NUM_MBUFS,
                                                      MBUF_CACHE_SIZE, 0,
                                                      RTE_MBUF_DEFAULT_BUF_SIZE,
                                                      rte_socket_id());
```

### Ring (`rte_ring`)
A `rte_ring` is a lockless, multi-producer, multi-consumer (MPMC) circular queue. It is used for passing messages or pointers (like `mbuf` pointers) between DPDK cores or threads with minimal overhead.

```
  Producer Core 1 --\                                /--> Consumer Core 1
                     \                              /
                      +--> [rte_ring] --> [ptr|ptr| | |ptr] --+
                     /                              \
  Producer Core 2 --/                                \--> Consumer Core 2
```

```c
// Create a ring
struct rte_ring *tx_ring = rte_ring_create("TX_RING", 1024, rte_socket_id(), 0);

// Enqueue and Dequeue
rte_ring_enqueue(tx_ring, (void *)mbuf);
rte_ring_dequeue(tx_ring, &obj);
```

### Ethdev (`rte_ethdev`)
The `rte_ethdev` library provides a generic API for managing Ethernet devices (NICs).
- **Functions**:
  - Device configuration (`rte_eth_dev_configure`).
  - Queue setup (`rte_eth_rx_queue_setup`, `rte_eth_tx_queue_setup`).
  - Starting/stopping the device (`rte_eth_dev_start`).
  - Receiving and transmitting packets (`rte_eth_rx_burst`, `rte_eth_tx_burst`).

### Poll Mode Driver (PMD)
A PMD is a user-space driver that directly interacts with the NIC hardware.
- **Polling**: It continuously polls the NIC's receive (Rx) descriptor ring for new packets.
- **No Interrupts**: This avoids the overhead of kernel interrupts, context switches, and data copies.
- **Device Specific**: Each supported NIC has its own PMD (e.g., `ixgbe` for Intel 10GbE, `mlx5` for Mellanox).

---

## Packet Processing Flow

A typical DPDK application follows this high-level flow:

```
                                    (Fast Path)
  +--------------------------------------------------------------------------------+
  |                                                                                |
  |   +-----------+   rte_eth_rx_burst()   +-------------+      +-----------+      |
  |   | NIC RxQ   | ---------------------> |   Core 1    | ---> | rte_ring  |      |
  |   +-----------+                        | (Processes) |      +-----------+      |
  |                                        +-------------+           |             |
  |                                                                  |             |
  |   +-----------+   rte_eth_tx_burst()   +-------------+           |             |
  |   | NIC TxQ   | <--------------------- |   Core 2    | <---------+             |
  |   +-----------+                        | (Forwards)  |                         |
  |                                        +-------------+                         |
  |                                                                                |
  +--------------------------------------------------------------------------------+
```

```
1. EAL Initialization:
   - rte_eal_init() parses command-line args, sets up hugepages, CPU affinity, and probes devices.

2. Resource Allocation:
   - Create mempools for mbufs: rte_pktmbuf_pool_create().
   - Create rings for inter-core communication (if needed): rte_ring_create().

3. Device Configuration:
   - Configure each Ethernet port: rte_eth_dev_configure().
   - Set up Rx and Tx queues for each port: rte_eth_rx_queue_setup(), rte_eth_tx_queue_setup().

4. Start Device:
   - Start the Ethernet port: rte_eth_dev_start().

5. Main Processing Loop (Fast Path):
   - Loop forever on each processing core:
     - Receive a burst of packets from an Rx queue:
       struct rte_mbuf *pkts[BURST_SIZE];
       uint16_t nb_rx = rte_eth_rx_burst(port_id, queue_id, pkts, BURST_SIZE);

     - Process each received packet:
       for (i = 0; i < nb_rx; i++) {
           // Read/modify packet data in pkts[i]
           // e.g., Parse headers, modify IP, etc.
       }

     - Transmit a burst of packets to a Tx queue:
       uint16_t nb_tx = rte_eth_tx_burst(port_id, queue_id, pkts, nb_rx);

     - Free any untransmitted packets back to the mempool:
       for (i = nb_tx; i < nb_rx; i++) {
           rte_pktmbuf_free(pkts[i]);
       }
```

---

## Setup & Compilation

### 1. System Prerequisites
- **Hugepages**: Reserve hugepages at boot time.
  ```bash
  # In /etc/default/grub, add to GRUB_CMDLINE_LINUX:
  default_hugepagesz=1G hugepagesz=1G hugepages=8
  sudo update-grub && sudo reboot
  ```
- **Kernel Drivers**: Unbind NIC from kernel driver and bind to a DPDK-compatible driver (`vfio-pci` is recommended).
  ```bash
  # Load VFIO driver
  sudo modprobe vfio-pci

  # Find NIC PCI address
  lspci | grep -i ethernet

  # Use dpdk-devbind.py script
  sudo ./usertools/dpdk-devbind.py --bind=vfio-pci 0000:03:00.0
  ```

### 2. Compiling DPDK
DPDK uses the Meson build system.
```bash
# Install dependencies (e.g., on Ubuntu)
sudo apt-get install meson python3-pyelftools ninja-build

# Configure and build
meson build
cd build
ninja
sudo ninja install
sudo ldconfig
```

### 3. Compiling a DPDK Application
Applications are compiled against the installed DPDK libraries.
```bash
# Set PKG_CONFIG_PATH
export PKG_CONFIG_PATH=/usr/local/lib/x86_64-linux-gnu/pkgconfig

# Compile using pkg-config
gcc my_app.c -o my_app $(pkg-config --cflags --libs libdpdk)
```

---

## Running a DPDK Application

DPDK applications are launched via the EAL, which takes a standard set of arguments.

```bash
sudo ./my_app -l 1-3 -n 4 -- -p 0x3 --config="(0,0,1),(1,0,2),(2,0,3)"
```

| EAL Argument | Description | Example |
| :--- | :--- | :--- |
| `-l <corelist>` | **Core List**: Specifies which CPU cores to run on. Core 0 is the main core. | `-l 1-3` (runs on cores 1, 2, 3) |
| `-n <channels>` | **Memory Channels**: Number of memory channels. | `-n 4` |
| `-a <pci>` | **Allowlist**: Whitelist a PCI device for use. | `-a 0000:03:00.0` |
| `--` | Separator between EAL arguments and application-specific arguments. | |

| App Argument | Description | Example |
| :--- | :--- | :--- |
| `-p <portmask>` | **Port Mask**: A bitmask of which Ethernet ports to use. | `-p 0x3` (uses ports 0 and 1) |
| `--config="..."` | Application-specific configuration string. | `"(0,0,1),(1,0,2)"` (port,queue,core mapping) |

---

## Performance Tuning

- **CPU Affinity & Isolation**: Pin polling threads to specific cores using `-l`. For best performance, isolate these cores from the general kernel scheduler using the `isolcpus` kernel parameter at boot time. This prevents other system tasks from interrupting your data plane threads.
- **NUMA Awareness**: On systems with **Non-Uniform Memory Access (NUMA)**, a CPU can access its local memory faster than memory connected to another CPU. For optimal performance, ensure that a DPDK thread, its memory allocations (mempools, rings), and the NIC it's polling are all on the same NUMA node. Use `-l` to assign cores and `--socket-mem` to allocate memory on a specific node.
  - Check NUMA layout: `lscpu` or `numactl -H`.
- **Vector Instructions**: Use AVX/SSE instructions for processing multiple packets at once. Many PMDs have vectorized versions that are enabled by default on supported hardware.
- **Compiler Flags**: Use performance-oriented flags like `-O3 -march=native`.
- **Tx Offloads**: Enable hardware offloads like checksum calculation (`DEV_TX_OFFLOAD_IPV4_CKSUM`) to free up CPU cycles.
- **Bursting**: Process packets in bursts (e.g., 32 at a time) rather than one by one. This amortizes function call overhead and improves cache performance.

---

## Vhost-user & Virtio
- **Purpose**: High-performance communication between a DPDK application (like OVS-DPDK) and a virtual machine (VM).
- **Vhost-user**: A DPDK-based backend that implements the virtio data path in user space.
- **Virtio**: A paravirtualized standard for I/O devices in VMs.
- **Mechanism**: The VM's virtio driver communicates with the DPDK vhost-user backend over a shared memory region, bypassing the hypervisor's kernel for data plane traffic.

## Cryptodev
- A DPDK library for offloading cryptographic operations (e.g., AES, SHA) to hardware accelerators or for software-based crypto processing.
- Provides a generic API for symmetric and asymmetric crypto.

## Eventdev
- An event-driven programming model for scheduling and dispatching packets/events to processing cores.
- **Components**:
  - **Event**: A message representing a packet or task.
  - **Event Queue**: Queues events for processing.
  - **Event Port**: Connects a core to the event device.
- **Benefit**: Decouples packet I/O from packet processing, enabling more flexible and scalable application designs.

## Flow API (`rte_flow`)
- A generic API to configure the flow processing pipeline of a NIC.
- Allows offloading complex packet classification, filtering, and steering rules directly to the hardware.
- **Example**: Create a rule to steer all TCP traffic on port 80 to a specific Rx queue.

---

## Troubleshooting & Debugging

- **Check Bindings**: Use `dpdk-devbind.py --status` to ensure NICs are bound to `vfio-pci` or `uio_pci_generic`.
- **Check Hugepages**: Use `cat /proc/meminfo | grep Huge` to verify hugepages are allocated and available.
- **Port Statistics**: Use `rte_eth_stats_get()` and `rte_eth_xstats_get()` to check for packet drops. `imissed` indicates the NIC hardware dropped packets (often due to full Rx queues), while `rx_nombuf` means the driver had no available mbufs to receive packets into. A high `rx_nombuf` count means your mempool is too small or your application is not freeing mbufs fast enough.


## Interview Questions

- **Q: What is the main goal of DPDK?**
  - A: To provide a framework for fast packet processing in user space by bypassing the kernel network stack, thus achieving high throughput and low latency.
  - A: A user-space driver that continuously polls the NIC for new packets instead of relying on interrupts. This eliminates interrupt overhead and is a key source of DPDK's performance.
  - A: To reduce TLB (Translation Lookaside Buffer) misses. Standard operating systems use 4KB memory pages. Accessing 1GB of memory would require 262,144 TLB entries. With 2MB hugepages, it only requires 512 entries, and with 1GB pages, just one. Fewer TLB entries mean fewer cache misses when translating virtual to physical addresses, significantly speeding up memory access.
  - A: It's a technique where a user-space application directly accesses hardware (like a NIC), avoiding the overhead of the kernel's processing stack, such as system calls, context switches, and data copies.
  - A: An `rte_mbuf` is the primary data structure in DPDK for carrying network packet data. It contains metadata (like packet length) and a pointer to the actual packet data stored in a buffer.

- **Q: Explain the difference between a `mbuf` and a `mempool`.**
  A: A `mbuf` (`rte_mbuf`) is a data structure that holds packet data and metadata. A `mempool` (`rte_mempool`) is a pre-allocated pool of fixed-size objects, from which `mbufs` are efficiently allocated and freed to avoid the overhead of `malloc`/`free`.
- **Q: What is a `rte_ring` and why is it lockless?**
  A: It's a circular buffer used for passing messages or pointers between CPU cores. It is "lockless" because it uses atomic hardware instructions (like Compare-And-Swap) to manage concurrent access from multiple producers and consumers, avoiding the overhead of traditional locks.
- **Q: What is the role of the EAL?**
  A: The Environment Abstraction Layer (EAL) is responsible for initializing the DPDK environment. It handles CPU affinity, memory management (hugepages), PCI bus enumeration, and loading drivers, providing a hardware-agnostic layer for applications.
- **Q: Describe the lifecycle of an `rte_mbuf`.**
  A: 1. It is pre-allocated as part of a `mempool`. 2. It is acquired from the mempool by a PMD when a packet arrives at the NIC. 3. The PMD writes the packet data into the mbuf's buffer. 4. `rte_eth_rx_burst` passes a pointer to the mbuf to the application. 5. The application processes it. 6. The application either sends it via `rte_eth_tx_burst` (where the hardware will use it) or frees it directly back to its original mempool using `rte_pktmbuf_free`.
- **Q: What is the difference between UIO and VFIO drivers for DPDK? Which is preferred?**
  A: UIO is an older, simpler driver framework. VFIO is a more modern, secure framework that uses the IOMMU to provide true memory isolation between the device and user space. VFIO is strongly preferred because it prevents a faulty or malicious user-space driver from compromising the entire system.

- **Q: How does NUMA affect DPDK performance, and how do you optimize for it?**
  A: Accessing memory on a remote NUMA node is slower than local access. For optimal performance, a DPDK application must ensure that a core's memory allocations (mempools, rings) and the NIC it's polling are all on the same NUMA node. This is configured via EAL arguments (`-l` for cores, `--socket-mem` for memory) and application logic.
- **Q: Describe the packet flow from the NIC to a DPDK application and back out.**
  A: 1) NIC DMA's the incoming packet into a `mbuf` in an Rx queue. 2) The PMD, running on a dedicated core, polls the Rx descriptor ring and sees the new packet. 3) `rte_eth_rx_burst()` provides the application with a pointer to the `mbuf`. 4) The application processes the packet. 5) The application calls `rte_eth_tx_burst()`, placing the `mbuf` pointer onto a Tx queue. 6) The NIC's Tx engine DMAs the packet data from the `mbuf` and sends it on the wire. 7) The `mbuf` is freed back to its mempool.
- **Q: What is `rte_flow` and why is it useful?**
  A: `rte_flow` is a generic API for offloading packet classification and steering rules to the NIC hardware. It is useful for creating complex filtering logic (e.g., based on 5-tuples, tunnels, etc.) that runs at line rate on the NIC, freeing up CPU cores from doing classification work and allowing them to focus on more complex processing. This is crucial for building high-performance virtual switches or firewalls.
- **Q: When would you choose DPDK over a kernel-based solution like XDP? What are the trade-offs?**
  A: **Choose DPDK for**: Maximum performance, lowest latency, and full control over the data plane, especially for building complex network functions (vSwitches, NFV). The trade-off is higher complexity, dedicated CPU cores, and losing kernel networking features. **Choose XDP for**: High performance within the kernel, where you can benefit from the existing kernel stack (TCP/IP, sockets) and tooling. It's great for DDoS mitigation, load balancing, and filtering at the earliest point in the kernel. The trade-off is less control than DPDK and the learning curve of eBPF.
- **Q: How would you design a simple L3 forwarding application using DPDK?**
  A: 1. Initialize EAL, mempools, and configure two or more NIC ports. 2. Create a forwarding table (e.g., `rte_lpm` for Longest Prefix Match). 3. Dedicate at least one core per Rx port for polling. 4. In the main loop, each core receives a burst of packets. 5. For each packet, parse the Ethernet and IP headers. 6. Perform a lookup in the LPM table using the destination IP to find the next hop and egress port. 7. Decrement the IP TTL and update the header checksum. 8. Update the source and destination MAC addresses. 9. Send the packet to the correct egress port's Tx queue.

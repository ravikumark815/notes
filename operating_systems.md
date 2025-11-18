# Operating Systems (OS) Notes

## Index
1. Introduction & Functions of OS  
2. System Architecture  
3. Processes & Threads  
4. CPU Scheduling  
5. Process Synchronization  
6. Deadlocks  
7. Memory Management  
8. File Systems  
9. I/O Systems  
10. Security & Protection  
11. Virtualization & Containers  
12. Advanced Topics  
13. Case Studies  

---

## 1. Introduction & Functions of OS
- **Definition:** Software that acts as an interface between user and hardware.
- **Functions:**
  - Process Management
  - Memory Management
  - File and I/O Management
  - Security and Protection
  - Networking and Communication
  - Virtualization and Resource Allocation
- **Goals:** Efficiency, convenience, fairness.

---

## 2. System Architecture

### 2.1 Kernel Types
- **Monolithic:** All OS services in one address space (e.g., Linux).
- **Microkernel:** Minimal services in kernel; rest in user space (e.g., Minix).
- **Hybrid:** Combination of both (e.g., Windows NT, macOS XNU).
- **Exokernel:** Exposes hardware to applications with minimal abstraction.
- **Nanokernel:** Even smaller than microkernel; delegates everything.

### 2.2 System Calls
- Interface for user programs to request OS services.
- Categories:
  - Process control (`fork`, `exec`, `exit`)
  - File manipulation (`open`, `read`, `write`)
  - Device management
  - Information maintenance
  - Communication (`pipe`, `socket`)

### 2.3 Boot Process
1. Power-On Self Test (POST)
2. Bootloader loads kernel into memory
3. Kernel initializes devices, memory, and system services
4. User-space init/systemd runs

---

## 3. Processes & Threads

### 3.1 Processes
- **Definition:** A program in execution.
- **Components:** Code, Data, Stack, Heap.
- **PCB (Process Control Block):** PID, Program Counter, Registers, I/O, Accounting.
- **Process States:**
```
NEW → READY → RUNNING → WAITING → READY → TERMINATED
```
- **Diagram:**
```
  +-------+        +-------+
  |  New  |------->| Ready |
  +-------+        +-------+
                      |
                      v
                  +--------+
                  | Running|
                  +--------+
                   /               +-------+       +-------+
          |Waiting|       |Terminat|
          +-------+       +-------+
```

### 3.2 Threads
- **User Threads:** Managed in user space.
- **Kernel Threads:** Managed by kernel.
- **Multithreading Models:**
  - Many-to-One
  - One-to-One
  - Many-to-Many

---

## 4. CPU Scheduling

### 4.1 Criteria
- CPU Utilization, Throughput, Turnaround Time, Waiting Time, Response Time.

### 4.2 Algorithms with Pseudocode
#### FCFS
- Non-preemptive; processes served in arrival order.
```plaintext
sort by arrival_time
for each process in order:
    wait_time = start_time - arrival_time
```

#### SJF
- Select process with smallest burst time.
```plaintext
while processes remain:
    pick process with shortest burst
    execute until completion
```

#### Round Robin
- Preemptive with fixed time quantum.
```plaintext
queue = all processes
while queue not empty:
    p = dequeue()
    execute p for quantum or until finish
    if not finished: enqueue(p)
```

#### Priority Scheduling
- Pick highest priority; preemptive or non-preemptive.

**Comparison Table:**
| Algorithm  | Preemptive? | Starvation? | Performance |
|------------|------------|-------------|------------|
| FCFS       | No         | No          | Simple     |
| SJF        | Both       | Yes         | Optimal avg wait |
| Priority   | Both       | Yes         | Flexible   |
| Round Robin| Yes        | No          | Fair       |

---

## 5. Process Synchronization

### 5.1 Critical Section Problem
- **Requirements:** Mutual Exclusion, Progress, Bounded Waiting.

### 5.2 Semaphores
```c
wait(S):
    while S <= 0;
    S--;

signal(S):
    S++;
```

### 5.3 Monitors
- Higher-level abstraction to enforce mutual exclusion.

### 5.4 Classical Problems
- **Dining Philosophers:** Prevent deadlock/starvation.
- **Readers-Writers:** Balance concurrency.
- **Producer-Consumer:** Use bounded buffer.

---

## 6. Deadlocks

### 6.1 Necessary Conditions
- Mutual Exclusion
- Hold and Wait
- No Preemption
- Circular Wait

### 6.2 Banker's Algorithm (Avoidance)
```plaintext
Work = Available
Finish[i] = false

while exists i s.t Finish[i]==false and Need[i] <= Work:
    Work = Work + Allocation[i]
    Finish[i] = true

if all Finish[i] == true:
    safe
else:
    unsafe
```

---

## 7. Memory Management

### 7.1 Techniques
- Contiguous Allocation
- Paging (fixed-size blocks)
- Segmentation (variable-sized segments)
- Virtual Memory (demand paging, swapping)

### 7.2 Page Replacement Algorithms
#### FIFO
- Replace oldest page.
```plaintext
use a queue; evict front
```

#### LRU
- Replace least recently used.
```plaintext
use stack or timestamp
```

#### Optimal
- Replace page not needed for longest time.

**Diagram for Paging:**
```
Logical Address
+-----------+-----------+
| Page No.  | Offset    |
+-----------+-----------+

Physical Address
+-----------+-----------+
| Frame No. | Offset    |
+-----------+-----------+
```

---

## 8. File Systems
- **Directory Structures:** Single-level, Tree, Graph.
- **Allocation Methods:** Contiguous, Linked, Indexed.
- **Free Space Management:** Bitmaps, Free lists.
- **Journaling:** Maintain logs for crash recovery.

---

## 9. I/O Systems
- Buffering, Caching, Spooling.
- Device Drivers: Abstract hardware.
- Disk Scheduling Algorithms:
  - FCFS
  - SSTF
  - SCAN, C-SCAN

---

## 10. Security & Protection
- **Authentication:** Passwords, Biometrics.
- **Authorization:** ACLs, Capabilities.
- **Encryption:** Symmetric, Asymmetric.
- **Protection Models:** Domains, Rings.

---

## 11. Virtualization & Containers
- **Hypervisors:**
  - Type-1: Bare-metal (e.g., Xen, ESXi)
  - Type-2: Hosted (e.g., VirtualBox)
- **Containers:** OS-level virtualization (Docker, LXC).
- **Paravirtualization:** Guest OS aware of virtualization.
- **Live Migration:** Moving VMs without downtime.

---

## 12. Advanced Topics

### NUMA (Non-Uniform Memory Access)
- Memory access time depends on memory location relative to CPU.
- Each CPU has local memory faster to access than remote memory.
- Improves scalability for multiprocessors.
- Diagram:
```
CPU0 ---- Local Memory 0 (fast)
  |
  +---- Remote Memory 1 (slower)
CPU1 ---- Local Memory 1 (fast)
```

### Microkernels vs Exokernels
- **Microkernel:** Minimal kernel; services like drivers run in user space for modularity.
- **Exokernel:** Gives maximum control to applications by exposing hardware directly.

### Distributed Systems Basics
- Transparency: location, replication, concurrency, fault tolerance.
- Distributed File Systems: NFS, HDFS.
- Consensus Algorithms: Paxos, Raft.

### Cloud OS Concepts
- VMs vs Containers: Isolation vs efficiency.
- Orchestration: Kubernetes manages container deployment.
- Serverless: Functions executed without managing servers.

---

## 13. Case Studies

### Linux
- Monolithic kernel with loadable modules.
- Completely Fair Scheduler (CFS).
- Ext4 File System.

### Windows
- Hybrid kernel architecture.
- NTFS File System.
- Win32 API.

### macOS
- XNU hybrid kernel (Mach + BSD).
- APFS File System.

### Android
- Linux kernel plus middleware and runtime.

---

## Appendix: Algorithms with Examples

### Scheduling Gantt Chart Example (Round Robin, Quantum=2)
| Time | 0-2 | 2-4 | 4-6 | 6-8 | 8-10 | 10-12 |
|-------|-----|-----|-----|-----|-------|-------|
| P1    | X   |     |     |     |       |       |
| P2    |     | X   |     |     |       |       |
| P3    |     |     | X   |     |       |       |
| P1    |     |     |     | X   |       |       |
| P2    |     |     |     |     | X     |       |
| P3    |     |     |     |     |       | X     |

---

### Page Replacement Step Example (FIFO)
Frames: 3, Reference string: 7, 0, 1, 2, 0, 3, 0, 4

| Step | Reference | Frames          | Page Fault? |
|-------|-----------|-----------------|-------------|
| 1     | 7         | 7               | Yes         |
| 2     | 0         | 7,0             | Yes         |
| 3     | 1         | 7,0,1           | Yes         |
| 4     | 2         | 0,1,2           | Yes         |
| 5     | 0         | 0,1,2           | No          |
| 6     | 3         | 1,2,3           | Yes         |
| 7     | 0         | 2,3,0           | Yes         |
| 8     | 4         | 3,0,4           | Yes         |

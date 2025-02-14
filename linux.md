## File and Directory Management
- `ls`:  List files and directories.
    - `ls -l`: Long list with detailed information including permissions, size, date etc.
    - `ls -a`: Show hidden files and dirs
    - `ls- lh`: Display filesize in human readable format
    - `ls -F`: Distinguish files and dirs by adding '/' at the end for dirs.
    - `ls -lr`: Sort in reverse order
    - `ls -lt`: Sort files by modification time
    - `ls -lS`: Sort files by file size
- `cp`:  Copy files and directories.
    - `cp -r`: Copy the source directory recursively
    - `cp -b`: Create backups for destination files
    - `cp -f`: Replace the file, if it already exists
    - `cp -n`: Do not overwrite the file, if it already exists
    - `cp -v`: Verbose mode
- `mv`:  Move or rename files and directories.
    - `mv -f source destination`: Overwrite if destination file already exists
    - `mv -v source destination`: Verbose mode
- `mkdir`:  Create new directories.
    - `mkdir -p /path/to/your/file.txt`: Create interim directories if they don't exist
- `cat`:  Concatenate and display file contents.
    - `cat -n test1.txt`: Show line numbers
    - `cat test1.txt test2.txt`: Display contents of multiple files sequentially
    - `cat test1.txt > test2.txt`: Replace contents of test2.txt with test1.txt
    - `cat test1.txt >> test2.txt`: Append contents of test1.txt to test2.txt
    - `tac test1.txt`: Display in reverse order
- `pwd`:  Print the current working directory.
    - `echo "$OLDPWD"`: Display previous working directory
- `cd`:  Change the directory.
    - `cd`: Home Directory
    - `cd -`: Switch to previous directory
- `rm`:  Remove files or directories.
    - `rm -f`: Force delete
    - `rm -r`: Delete recursively
- `ln`:  Create hard and symbolic links.
    - `ln file.txt link.txt`: Creates a hard link - link.txt that points to file.txt
    - `ln -s file.txt link.txt`: Creates a symbolic link - link.txt that points to file.
- `lsns`:  List namespace details.

## Viewing and Manipulating Files
- `less/more`:  View file content page by page.
    - `less -N /var/log/dmesg`: Show line numbers
    - `less -X /var/log/dmesg`: Keep content on screen after quitting.
    - `less -F /var/log/dmesg`: Monitor the file in real time
    - Press `v` while viewing file to transfer the file to text editor
- `tail/head`:  Display the last or first lines of a file.
    - `tail -n /var/log/dmesg`: Show line numbers
    - `tail -20 /var/log/dmesg`: Display last 20 lines
    - `tail -f /var/log/dmesg`: Monitor the file in real time
- `diff`:  Compare two files line by line.
    - `diff -c f1.txt f2.txt`: Display context format
    - `diff -u f1.txt f2.txt`: Display compact format
    - `diff -i f1.txt f2.txt`: Ignore case
- `cmp`:  Compare two files byte by byte.
    - `cmp -s f1.txt f2.txt`: Supress cmp command's output
- `grep/egrep/pgrep`:  Search for patterns in files or processes.
    - `grep -i "foo" ./*.txt`: Case insensitive
    - `grep -w "foo" ./*.log`: Check for full words, not sub-strings
    - `grep -e '^[a-zA-Z]' -e'foo$' test.txt`: Search using regular expressions
    - `grep -E '^[a-z]|AB CD' test.txt`: Search using extended regular expressions
    - `grep -A 5 "foo" ./*.c`: Display 5 lines after match
    - `grep -B 3 "bar" ./*.c`: Display 3 lines before match
    - `grep -C 2 "foo" ./*.c`: Display 2 lines around match
    - `grep -r "foo" ./*`: Search recursively
    - `grep -v -e "^foo" -e "foo$" ./*.txt`: Display lines that do not match the given patterns
    - `grep -c "foo" ./*.log`: Count number of matches
    - `grep -l "bar" ./*.py`: Display the file names only
    - `grep -n "foo" ./*.php`: Show line number
- `find`:  Search for files and directories.
- `sed`:  Stream editor for modifying files.
- `awk`:  Pattern scanning and processing language.
- `locate`:  Find files by name quickly.
- `wname`:  Show information about window names.

## System Tools
- `alias`:  Create command shortcuts.
- `tmux`:  Terminal multiplexer.
- `screen`:  Full-screen window manager for terminals.
- `whereis`:  Locate command binary, source, and manual.
- `which`:  Find the location of a command.
- `mount`:  Mount file systems.
- `lsb_release`:  Display Linux distribution information.
- `watch`:  Run a command repeatedly at intervals.
- `cron`:  Schedule jobs to run at specified times
- `export`:  Set environment variables.

## User Management
- `useradd/usermod`:  Add or modify user accounts.
- `passwd`:  Change user passwords.
- `chmod`:  Modify file permissions.
- `chown`:  Change file ownership.

## System Monitoring & Troubleshooting
- `top/htop`:  Monitor system processes and resource usage.
    - `htop -u ram`: Display processes based on username
    - `htop -d 15`: Delay between screen updates to 1.5 sec
    - `htop -p 123,456`: Monitor certain Process IDs
    - `htop -s PERCENT_MEM`: Sort by memory usage
- `ps`:  View currently running processes.
    - `ps -A` | `ps -e`:  View all running processes
    - `ps -ef`| `ps -eF`: View full format listing
    - `ps -aux`: Display processes in BSD format
    - `ps -e --forest`: Display process hierarchy
    - `ps -e -o pid,uname,pmem`: Display selected list of columns
    - `ps -e -o etime`: Display elapsed time
    - `ps -u ram`: Filter based on user
    - `ps -L 426`: View all threads of a process id
    - `ps -U root -u root`: Show all processes running as root
    - `ps -C process_name`: Search based on process name
    - `ps -fG groupID`|`ps -fG group_name`: List all processes of a group id 
    - `ps -T`: View terminal related processes
- `kill/killall`:  Terminate processes.
- `systemctl`:  Manage system services.
    - `systemctl start smb`: Start a service
    - `systemctl stop smb`: Stop a service
    - `systemctl enable smb`: Start automatically at boot
    - `systemctl status smb`: View status of service
    - `systemctl mask smb`: Prevent a service from being started
    - `systemctl list-dependencies smb`: List all dependencies
    - `systemctl set-default gud`: Change the default system target
- `service`:  Start, stop, or restart services.
    - `service smb start`: Start a service
    - `service smb stop`: Stop a service
    - `service smb status`: View status of service
- `df`:  Display disk space usage.
- `du`:  Show directory size.
- `free`:  Show memory usage.
- `dmesg`:  Display kernel logs.
    - `dmesg -T`: Display time in human-readable format
    - `dmesg -f syslog`: To follow updates in real-time
    - `dmesg -l warn,notice`: Filter based on log levels
    - `dmesg -L`: Display output of particular facility
    - `dmesg -L`: Adds color to the output
- `journalctl`:  View system logs.
    - `journalctl -b`: Boot messages
    - `journalctl -r`: Show in reverse chronological order
    - `journalctl --since "1 hour ago"`: Time range
    - `journalctl -u nginx.service`: By service
    - `journalctl -f`: In realtime
    - `journalctl -u nginx.service -f`: In realtime for a particular service
    - `journalctl -o verbose`: Verbose mode
    - `journalctl -o json-pretty`: Display in JSON format
    - `journalctl -p "emerg"`: By priority level
    - `journalctl _UID=108`: By user id 
- `uptime`:  Show system uptime.
- `vmstat`:  Show system performance statistics.
- `rsync`:  Synchronize files between locations.
- `strace`:  Trace system calls made by a process.
- `lsmod`:  Show loaded kernel modules.
- `modinfo`: Display information about kernel module
- `insmod`: Insert a module into kernel
- `lspci`:  List PCI devices.
    - `lspci -mm`: Machine readable format
    - `lspci -vv`: Detailed Format
    - `lspci -s 00:01.0`: Show detailed information of a device
    - `lspci -nn`: Show vendor and device code for each PCI device
    - `lspci -k`: Shows kernel modules in use for each PCI device
- `lshw`:  Display detailed hardware information.
    - `lshw -short`: Short version
    - `lshw -businfo`: To show SCSI, USB, IDE, PCI info
- `lsof`:  List open files.
- `dd`:  Copy and convert data at a low level.

## Networking
- `ssh`:  Secure shell for remote access.
- `ssh-keygen`:  Generate SSH key pairs.
- `scp`:  Securely copy files between systems.
- `curl`:  Transfer data from or to a server.
- `wget`:  Download files from the internet.
- `ftp/sftp`:  File transfer protocol commands.
- `ifconfig/ip`:  Configure network interfaces.
- `dig/nslookup`:  Query DNS records.
    - `dig @8.8.8.8 google.com +short`: Short output
- `ping`:  Test network connectivity.
- `traceroute`:  Trace network routes.
- `iptables/ufw/firewall-cmd`:  Configure firewall rules.
- `netstat/ss`:  Display network statistics.
    - `netstat -a`: List all ports and connections
    - `netstat -at`: List all TCP ports
    - `netstat -au`: List all UDP ports
    - `netstat -l`: List only listening ports
    - `netstat -s`: Display statistics
    - `netstat -i`: To see packet statistics and MTU
    - `netstat -lp`: Display listening programs
    - `netstat -r`: Display kernel routing table
- `nmap`:  Scan networks and detect open ports.
- `ethtool`:  Get or modify network driver settings.
    - `ethtool eth0`: Particular device
    - `ethtool -s eth0 speed 100 autoneg off`: Change NIC parameters
    - `ethtool -i eth0`: Display ethernet driver settings
    - `ethtool -a eth0`: Display rx/tx queues 
    - `ethtool -S eth0`: Display network statistics

## Package Management
- `apt`:
    - `apt update`: Download package information
    - `apt upgrade`: Upgrade all installed packages and security updates
    - `apt --upgradable`: List packages that can be upgraded
    - `apt full-upgrade`: Perform full system upgrade
    - `apt install nginx`: Install new package
    - `apt remove nginx`: Remove a package
    - `apt purge nginx`: Remove both package and config files
    - `apt autoremove`: Removes automatically installed packages that are no longer needed due to dependency changes or package removal.
    - `apt --purge autoremove`: Purge installed packages that are no longer needed
    - `apt search nginx*`: Search installed packages
    - `apt show nginx`: Show info about packages
    - `apt list --installed`: List all installed packages
    - `apt depends nginx`: List all dependencies of a package
    - `apt reinstall nginx`: Reinstall a package
- `yum`:
    - `yum install firefox`: Install a package
    - `yum remove firefox`: Remove a package
    - `yum update firefox`: Update a package
    - `yum search firefox`: Search for a package
    - `yum info firefox`: Get info about a package
    - `yum check-update`: Check for available updates
    - `yum update`: Update system
    - `yum repolist`: List enabled yum repositories
    - `yum --enablerepo=epel install phpmyadmin`: Install a package from specific repository
    - `yum provides /etc/passwd`: Find which package this file belongs to
    - `yum list installed`: List installed packages
    - `yum clean all`: Clean yum cache
- `rpm`: 
    - `rpm -ivh firefox.rpm`: Install the package
    - `rpm -Uvh firefox.rpm`: Upgrade the package
    - `rpm -ev firefox`: Erase/Remove an installed package
    - `rpm -ev --nodeps firefox`: Erase/Remove without checking for dependencies
    - `rpm -qa`: Display or list all installed packages
    - `rpm -qi firefox`: Display information about an installed package
    - `rpm -qf /etc/passwd`: Find out what package a file belongs to
    - `rpm -qc firefox`: Display list of configuration files for a package
    - `rpm -qpR firefox.rpm`: Find all dependencies of a rpm file
    - `rpm -qpR firefox`: Find all dependencies of a package
- `pacman/dnf`:  Package managers for different Linux distributions.
- `dpkg`:
    - `dpkg -i apache2.deb` : Install a package
    - `dpkg -l`: List installed packages
    - `dpkg -l apache2`: Check if a package is installed or not
    - `dpkg -r apache2`: Remove/Uninstall a package 
    - `dpkg -p apache2`: Purge (Uninstall and remove config) a package 
    - `dpkg -c apache2`: View contents of a deb package.
    - `dpkg -L apache2`: List files installed by deb package
    - `dpkg -R apache2 tomcat`: Install multiple deb packages
    - `dpkg --unpack apache2.deb`: Extract contents of .deb package
    - `dpkg --configure apache2`: Configure an unpacked package

## Compression and Archiving
- `tar/zip/gzip`:  File compression utilities.

## Performance Testing
- `iperf/jperf`:  Network performance measurement.
- `perf`:  Performance analysis tool.

## System Paths and Logs
### `/proc/`

- **buddyinfo:**
Info about free memory in the system, specifically how many contiguous blocks (or "buddies") of memory are available in different sizes. 

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s1-proc-topfiles#s2-proc-buddyinfo

```bash
ubuntu:~# cat /proc/buddyinfo
Node 0, zone      DMA      0      0      0      0      0      0      0      0      1      2      2
Node 0, zone    DMA32      1      3      0      2      2      1      1      4      3      5    679
Node 0, zone   Normal  13491  12179   5979   6621   3739    967    144     49     11      6   1549
ubuntu:~# 
```

- **cgroups** displays information about control groups (cgroups) configured on the system.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/resource_management_guide/ch01#sec-How_Control_Groups_Are_Organized
```bash
ubuntu:~# cat /proc/cgroups
#subsys_name    hierarchy       num_cgroups     enabled
cpuset  0       878     1
cpu     0       878     1
cpuacct 0       878     1
blkio   0       878     1
memory  0       878     1
devices 0       878     1
freezer 0       878     1
net_cls 0       878     1
perf_event      0       878     1
net_prio        0       878     1
hugetlb 0       878     1
pids    0       878     1
rdma    0       878     1
misc    0       878     1
ubuntu:~#
//
```
To look into specific cgroup usage in the system:
```bash
ubuntu:~# cat /sys/fs/cgroup/memory.stat 
```

- **cmdline** displays the kernel command line arguments passed to the Linux kernel at boot time.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-cmdline#s2-proc-cmdline

```bash
ubuntu:~# cat /proc/cmdline
BOOT_IMAGE=(hd0,msdos1)/vmlinuz-5.14.0-503.22.1.el9_5.x86_64 root=/dev/mapper/rhel-root ro crashkernel=1G-4G:192M,4G-64G:256M,64G-:512M resume=/dev/mapper/rhel-swap rd.lvm.lv=rhel/root rd.lvm.lv=rhel/swap rhgb quiet net.ifnames=0 biosdevname=0 console=ttyS0,38400n8 console=tty0
ubuntu:~#
```

- **consoles** displays information about the system's console devices that are available for logging and displaying kernel messages.

```bash
ubuntu:~# cat /proc/consoles
tty0                 -WU (EC  p  )    4:1
ttyS0                -W- (E  Np a)    4:64
ubuntu:~#
```
4:1 → tty0 is associated with major device number 4 and minor number 1.

- **cpuinfo** displays detailed information about the CPU(s) in the system.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-cpuinfo

```bash
ubuntu:~# cat /proc/cpuinfo
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 61
model name      : Intel Core Processor (Broadwell, IBRS)
stepping        : 2
microcode       : 0x1
cpu MHz         : 2199.998
cache size      : 16384 KB
physical id     : 0
siblings        : 1
core id         : 0
cpu cores       : 1
apicid          : 0
initial apicid  : 0
fpu             : yes
fpu_exception   : yes
cpuid level     : 13
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl xtopology cpuid tsc_known_freq pni pclmulqdq vmx ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch cpuid_fault pti ssbd ibrs ibpb stibp tpr_shadow flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm rdseed adx smap xsaveopt arat vnmi umip md_clear arch_capabilities
vmx flags       : vnmi preemption_timer posted_intr invvpid ept_x_only ept_ad ept_1gb flexpriority apicv tsc_offset vtpr mtf vapic ept vpid unrestricted_guest vapic_reg vid shadow_vmcs pml
bugs            : cpu_meltdown spectre_v1 spectre_v2 spec_store_bypass l1tf mds swapgs taa srbds mmio_unknown bhi
bogomips        : 4399.99
clflush size    : 64
cache_alignment : 64
address sizes   : 40 bits physical, 48 bits virtual
power management:

ubuntu:~#
```

- **devices**
The file /proc/bus/pci/devices is part of the procfs virtual filesystem and contains details about all PCI devices in the system.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-devices

```bash
ubuntu:~# cat /proc/devices
0009    80867010        0                    1f0                     3f6                     170                     376                    c121                       0                       0                       8                        0                    8                       0                      10                       0                       0        ata_piix
ubuntu:~#
```

- **diskstats** displays disk I/O statistics for all block devices in the system.

https://www.kernel.org/doc/Documentation/ABI/testing/procfs-diskstats
```bash
ubuntu:~# cat /proc/diskstats 
 252       0 vda 112431 164 5524022 124561 298591 62555 17081416 1038176 0 296326 1186204 0 0 0 0 74546 23467
 252       1 vda1 365 0 86486 492 60 4 5208 133 0 422 625 0 0 0 0 0 0
 252       2 vda2 111720 164 5422840 123889 298515 62551 17076208 1038040 0 341717 1161930 0 0 0 0 0 0       
 253       0 dm-0 111621 0 5397024 123834 357592 0 17076208 1259669 0 1297536 1383503 0 0 0 0 0 0
 253       1 dm-1 98 0 4440 44 0 0 0 0 0 28 44 0 0 0 0 0 0
   7       0 loop0 493 0 3826 42 0 0 0 0 0 29 42 0 0 0 0 0 0
   7       1 loop1 303 0 3268 31 0 0 0 0 0 33 31 0 0 0 0 0 0
ubuntu:~#
```

- **dma** displays the DMA (Direct Memory Access) channels currently being used by the system.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-dma

```bash
ubuntu:~# cat /proc/dma
 4: cascade
ubuntu:~#
## Indicates that channel no 4 is used for cascading DMA controllers.
```

- **dynamic_debug** allows you to dynamically enable/disable kernel debug-print code to obtain additional kernel information. If /proc/dynamic_debug/control exists, your kernel has dynamic debug. 

https://docs.kernel.org/admin-guide/dynamic-debug-howto.html

```bash
ubuntu:~# head /proc/dynamic_debug/control
# filename:lineno [module]function flags format
init/main.c:1102 [main]initcall_blacklist =p "blacklisting initcall %s\n"
init/main.c:1144 [main]initcall_blacklisted =p "initcall %s blacklisted\n"
init/main.c:1344 [main]run_init_process =p "  with arguments:\n"
init/main.c:1346 [main]run_init_process =p "    %s\n"
init/main.c:1347 [main]run_init_process =p "  with environment:\n"
init/main.c:1349 [main]run_init_process =p "    %s\n"
init/initramfs.c:500 [initramfs]unpack_to_rootfs =_ "Detected %s compressed data\n"
arch/x86/events/amd/ibs.c:1370 [ibs]setup_ibs_ctl =_ "Failed to setup IBS LVT offset, IBSCTL = 0x%08x\n"     
arch/x86/events/amd/ibs.c:1377 [ibs]setup_ibs_ctl =_ "No CPU node configured for IBS\n"
ubuntu:~#
```
- **filesystems**: displays a list of the file system types currently supported by the kernel.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-filesystems
```bash
ubuntu:~# head /proc/filesystems 
nodev   sysfs
nodev   tmpfs
nodev   bdev
nodev   proc
nodev   cgroup
nodev   cgroup2
nodev   cpuset
nodev   devtmpfs
nodev   configfs
nodev   debugfs
ubuntu:~#
```

- **interrupts**: records the no of interrupts per IRQ. 

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-interrupts
```bash
ubuntu:~# head /proc/interrupts
           CPU0       CPU1       CPU2       CPU3       CPU4       CPU5       CPU6       CPU7
  0:         24          0          0          0          0          0          0          0   IO-APIC   2-edge      timer
  1:          0          0          0          0          9          0          0          0   IO-APIC   1-edge      i8042
  4:          0          0          0          0          0          0        441          0   IO-APIC   4-edge      ttyS0
  8:          0          0          0          0          0          1          0          0   IO-APIC   8-edge      rtc0
  9:          0          0          0          0          0          0          0          0   IO-APIC   9-fasteoi   acpi
 11:          0          0         12          0          0          0          0     636377   IO-APIC  11-fasteoi   uhci_hcd:usb1, virtio2
 12:          0          0          0         15          0          0          0          0   IO-APIC  12-edge      i8042
 14:          0          0          0          0          0          0          0          0   IO-APIC  14-edge      ata_piix
 15:          0          0          0          0          0          0          0          0   IO-APIC  15-edge      ata_piix
ubuntu:~#
```

- **iomem**: current map of system's memory for each physical device.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-iomem
```bash
ubuntu:~# head /proc/iomem
00000000-00000fff : Reserved
00001000-0009fbff : System RAM
0009fc00-0009ffff : Reserved
000a0000-000bffff : PCI Bus 0000:00
000c0000-000c99ff : Video ROM
000ca000-000cadff : Adapter ROM
000cb000-000cbdff : Adapter ROM
000cc000-000ce3ff : Adapter ROM
000f0000-000fffff : Reserved
  000f0000-000fffff : System ROM
ubuntu:~#
```

- **meminfo**:  reports valuable information about the system's RAM usage.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-meminfo#s2-proc-meminfo

```bash
ubuntu:~# head /proc/meminfo
MemTotal:       16112680 kB
MemFree:         9770876 kB
MemAvailable:   13297556 kB
Buffers:            6184 kB
Cached:          3711428 kB
SwapCached:            0 kB
Active:          2427732 kB
Inactive:        2651532 kB
Active(anon):    1582668 kB
Inactive(anon):        0 kB
ubuntu:~#
```

- **mounts**:  list of all mounts in use by the system

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-mounts#s2-proc-mounts

```bash
ubuntu:~# head /proc/mounts
rootfs / rootfs rw 0 0
/proc /proc proc rw,nodiratime 0 0 none
/dev ramfs rw 0 0
/dev/mapper/VolGroup00-LogVol00 / ext3 rw 0 0
none /dev ramfs rw 0 0
/proc /proc proc rw,nodiratime 0 0
/sys /sys sysfs rw 0 0
none /dev/pts devpts rw 0 0
usbdevfs /proc/bus/usb usbdevfs rw 0 0
/dev/hda1 /boot ext3 rw 0 0
none /dev/shm tmpfs rw 0 0
none /proc/sys/fs/binfmt_misc binfmt_misc rw 0 0
sunrpc /var/lib/nfs/rpc_pipefs rpc_pipefs rw 0 0
ubuntu:~#
```

- **stat**:  keeps track of a variety of different statistics about the system since it was last restarted.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-stat#s2-proc-stat

```bash
ubuntu:~# cat /proc/stat
cpu  259246 7001 60190 34250993 137517 772 0
cpu0 259246 7001 60190 34250993 137517 772 0
intr 354133732 347209999 2272 0 4 4 0 0 3 1 1249247 0 0 80143 0 422626 5169433
ctxt 12547729
btime 1093631447
processes 130523
procs_running 1
procs_blocked 0
preempt 5651840
cpu  209841 1554 21720 118519346 72939 154 27168
cpu0 42536 798 4841 14790880 14778 124 3117
cpu1 24184 569 3875 14794524 30209 29 3130
cpu2 28616 11 2182 14818198 4020 1 3493
cpu3 35350 6 2942 14811519 3045 0 3659
cpu4 18209 135 2263 14820076 12465 0 3373
cpu5 20795 35 1866 14825701 4508 0 3615
cpu6 21607 0 2201 14827053 2325 0 3334
cpu7 18544 0 1550 14831395 1589 0 3447
intr 15239682 14857833 6 0 6 6 0 5 0 1 0 0 0 29 0 2 0 0 0 0 0 0 0 94982 0 286812
ctxt 4209609
btime 1078711415
processes 21905
procs_running 1
procs_blocked 0
ubuntu:~#
```
- **swaps**: measures swap space and its utilization.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-swaps#s2-proc-swaps
```bash
ubuntu:~# cat /proc/swaps
Filename                                Type            Size            Used            Priority
/dev/dm-1                               partition       16773116        0               -2
ubuntu:~#
```

### `/var/log`:  System logs directory.
### `/etc/`:  Configuration files.
### `/usr/local/bin`:  User-installed binaries.
### `/usr/bin`:  Standard binaries.
### `/sys/fs/`: 

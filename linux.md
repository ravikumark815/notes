## File and Directory Management
- `ls`:  List files and directories.
```bash
ls -a
```
- `cp`:  Copy files and directories.
- `mv`:  Move or rename files and directories.
- `mkdir`:  Create new directories.
- `cat`:  Concatenate and display file contents.
- `pwd`:  Print the current working directory.
- `cd`:  Change the directory.
- `rm`:  Remove files or directories.
- `ln`:  Create hard and symbolic links.
- `lsns`:  List namespace details.

## Viewing and Manipulating Files
- `less/more`:  View file content page by page.
- `tail/head`:  Display the last or first lines of a file.
- `diff`:  Compare two files line by line.
- `cmp`:  Compare two files byte by byte.
- `grep/egrep/pgrep`:  Search for patterns in files or processes.
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
- `ps`:  View currently running processes.
- `kill/killall`:  Terminate processes.
- `systemctl`:  Manage system services.
- `service`:  Start, stop, or restart services.
- `df`:  Display disk space usage.
- `du`:  Show directory size.
- `free`:  Show memory usage.
- `dmesg`:  Display kernel logs.
- `journalctl`:  View system logs.
- `uptime`:  Show system uptime.
- `vmstat`:  Show system performance statistics.
- `rsync`:  Synchronize files between locations.
- `strace`:  Trace system calls made by a process.
- `lsmod`:  Show loaded kernel modules.
- `lspci`:  List PCI devices.
- `lshw`:  Display detailed hardware information.
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
- `ping`:  Test network connectivity.
- `traceroute`:  Trace network routes.
- `iptables/ufw/firewall-cmd`:  Configure firewall rules.
- `netstat/ss`:  Display network statistics.
- `nmap`:  Scan networks and detect open ports.
- `ethtool`:  Get or modify network driver settings.

## Package Management
- `apt/yum/pacman/rpm/dnf`:  Package managers for different Linux distributions.
- `dpkg`:  Debian package manager.

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
root@s1rtp-nmsc-dev-ravi1:~# cat /proc/buddyinfo
Node 0, zone      DMA      0      0      0      0      0      0      0      0      1      2      2
Node 0, zone    DMA32      1      3      0      2      2      1      1      4      3      5    679
Node 0, zone   Normal  13491  12179   5979   6621   3739    967    144     49     11      6   1549
root@s1rtp-nmsc-dev-ravi1:~# 
```

- **cgroups** displays information about control groups (cgroups) configured on the system.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/resource_management_guide/ch01#sec-How_Control_Groups_Are_Organized
```bash
root@s1rtp-nmsc-dev-ravi1:~# cat /proc/cgroups
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
root@s1rtp-nmsc-dev-ravi1:~#
//
```
To look into specific cgroup usage in the system:
```bash
root@s1rtp-nmsc-dev-ravi1:~# cat /sys/fs/cgroup/memory.stat 
```
- **cmdline** displays the kernel command line arguments passed to the Linux kernel at boot time.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-cmdline#s2-proc-cmdline

```bash
root@s1rtp-nmsc-dev-ravi1:~# cat /proc/cmdline
BOOT_IMAGE=(hd0,msdos1)/vmlinuz-5.14.0-503.22.1.el9_5.x86_64 root=/dev/mapper/rhel-root ro crashkernel=1G-4G:192M,4G-64G:256M,64G-:512M resume=/dev/mapper/rhel-swap rd.lvm.lv=rhel/root rd.lvm.lv=rhel/swap rhgb quiet net.ifnames=0 biosdevname=0 console=ttyS0,38400n8 console=tty0
root@s1rtp-nmsc-dev-ravi1:~#
```
- **consoles** displays information about the system's console devices that are available for logging and displaying kernel messages.

```bash
root@s1rtp-nmsc-dev-ravi1:~# cat /proc/consoles
tty0                 -WU (EC  p  )    4:1
ttyS0                -W- (E  Np a)    4:64
root@s1rtp-nmsc-dev-ravi1:~#
```
4:1 → tty0 is associated with major device number 4 and minor number 1.
- **devices**
The file /proc/bus/pci/devices is part of the procfs virtual filesystem and contains details about all PCI devices in the system.

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-devices

```bash
root@s1rtp-nmsc-dev-ravi1:~# cat /proc/devices
0009    80867010        0                    1f0                     3f6                     170                     376                    c121                       0                       0                       8                        0                    8                       0                      10                       0                       0        ata_piix
root@s1rtp-nmsc-dev-ravi1:~#
```

### `/var/log`:  System logs directory.
### `/etc/`:  Configuration files.
### `/usr/local/bin`:  User-installed binaries.
### `/usr/bin`:  Standard binaries.
### `/sys/fs/`: 


## File and Directory Management
- `ls`:  List files and directories.
    - `ls -l`: Long list with detailed information including permissions, size, date etc.
    - `ls -a`: Show hidden files and directories.
    - `ls -lh`: Display filesize in human readable format.
    - `ls -F`: Distinguish files and directories by adding '/' at the end for directories.
    - `ls -lr`: Sort in reverse order.
    - `ls -lt`: Sort files by modification time.
    - `ls -lS`: Sort files by file size.
    - `ls -lahtr`: List all files, human readable, sorted by time (oldest last).
- `cp`:  Copy files and directories.
    - `cp -r <src> <dest>`: Copy the source directory recursively.
    - `cp -b <src> <dest>`: Create backups for destination files (adds `~`).
    - `cp -f <src> <dest>`: Force replace the file, if it already exists.
    - `cp -n <src> <dest>`: Do not overwrite the file, if it already exists.
    - `cp -v <src> <dest>`: Verbose mode (show files as they are copied).
    - `cp -vni <src> <dest>`: Verbose, prompt before overwrite, do not overwrite if exists.
- `mv`:  Move or rename files and directories.
    - `mv <src> <dest>`: Move or rename file/directory.
    - `mv -f <src> <dest>`: Overwrite if destination file already exists.
    - `mv -v <src> <dest>`: Verbose mode.
    - `mv -n <src> <dest>`: Do not overwrite existing files.
    - `mv -i <src> <dest>`: Prompt before overwrite.
- `mkdir`:  Create new directories.
    - `mkdir <dir>`: Create new directory.
    - `mkdir -p /path/to/your/dir`: Create parent directories as needed.
    - `mkdir -pv path/to/your/dir`: Create parent directories and show what was created.
- `cat`:  Concatenate and display file contents.
    - `cat -n <file>`: Show line numbers.
    - `cat file1 file2`: Display contents of multiple files sequentially.
    - `cat file1 > file2`: Replace contents of file2 with file1.
    - `cat file1 >> file2`: Append contents of file1 to file2.
    - `tac file`: Display in reverse order (last line first).
    - `cat -A file`: Show hidden characters (tabs, EOL).
- `pwd`:  Print the current working directory.
    - `pwd`: Print current directory.
    - `echo "$PWD"`: Print current directory (alternative).
    - `echo "$OLDPWD"`: Print previous working directory.
- `cd`:  Change the directory.
    - `cd`: Home Directory.
    - `cd -`: Switch to previous directory.
    - `cd ..`: Go up one directory.
    - `cd ~user`: Go to another user's home directory.
- `rm`:  Remove files or directories.
    - `rm <file>`: Remove a file.
    - `rm -f <file>`: Force delete (no prompt).
    - `rm -r <dir>`: Delete recursively (for directories).
    - `rm -rf <dir>`: Force, recursively delete directory and contents.
    - `rm -i <file>`: Prompt before delete.
- `ln`:  Create hard and symbolic links.
    - `ln file link`: Creates a hard link (`link` points to `file`).
    - `ln -s file link`: Creates a symbolic (soft) link (`link` points to `file`).
- `lsns`:  List Linux namespaces.
    - `lsns`: Show all Linux namespaces (net, user, mount, etc.) with PIDs.

## Viewing and Manipulating Files
- `less` / `more`:  View file content page by page.
    - `less <file>`: View file with scroll/search.
    - `more <file>`: Simpler pager.
    - `less -N <file>`: Show line numbers.
    - `less -X <file>`: Keep content on screen after quitting.
    - `less -F <file>`: Exit if file fits on one screen.
    - `less +F <file>`: Follow a growing log (like tail -f).
- `tail` / `head`:  Display the last or first lines of a file.
    - `tail -n 20 <file>`: Show last 20 lines.
    - `tail -f <file>`: Monitor the file in real time.
    - `head -n 20 <file>`: Show first 20 lines.
    - `tail -fn 50 <file>`: Follow last 50 lines updating live.
- `diff`:  Compare two files line by line.
    - `diff -c file1 file2`: Context format (shows several lines of context).
    - `diff -u file1 file2`: Unified format (compact, preferred for patches).
    - `diff -i file1 file2`: Ignore case differences.
    - `diff -r dir1 dir2`: Compare directories recursively.
- `cmp`:  Compare two files byte by byte.
    - `cmp file1 file2`: Output first difference, if any.
    - `cmp -s file1 file2`: Suppress output; use exit code only (0 if same).
- `grep` / `egrep` / `pgrep`:  Search for patterns in files or processes.
    - `grep -i "foo" *.txt`: Case insensitive search.
    - `grep -w "foo" *.log`: Match whole words only.
    - `grep -e '^[a-zA-Z]' -e 'foo$' file`: Multiple regexes.
    - `grep -E '^[a-z]|AB CD' file`: Use extended regex (same as `egrep`).
    - `grep -A 5 "foo" *.c`: Show 5 lines after match.
    - `grep -B 3 "bar" *.c`: Show 3 lines before match.
    - `grep -C 2 "foo" *.c`: Show 2 lines around match.
    - `grep -r "foo" .`: Search recursively from current directory.
    - `grep -v -e "^foo" -e "foo$" *.txt`: Show lines not matching patterns.
    - `grep -c "foo" *.log`: Count matches per file.
    - `grep -l "bar" *.py`: Show filenames only if match.
    - `grep -n "foo" *.php`: Show line number for matches.
    - `pgrep <pattern>`: Find process IDs by name.
- `find`:  Search for files and directories.
    - `find . -name "*.sh"`: Find all `.sh` files in current directory and subdirs.
    - `find /var -type d -name "log*"`: Find directories starting with `log` in /var.
    - `find . -size +100M`: Find files larger than 100MB.
    - `find . -mtime -7`: Find files modified in last 7 days.
    - `find . -user <username>`: Find files owned by user.
    - `find . -exec grep -l "pattern" {} +`: Find files containing "pattern".
    - `find . -print0 | xargs -0 <cmd>`: Safe handling for filenames with spaces.
- `sed`:  Stream editor for modifying files.
    - `sed 's/foo/bar/g' file`: Replace all "foo" with "bar" in file (output to stdout).
    - `sed -i 's/foo/bar/g' file`: Replace in-place.
    - `sed -n '5,10p' file`: Print lines 5 to 10.
    - `sed -e 's/old/new/g' -e 's/foo/bar/g' file`: Multiple expressions.
    - `sed -r 's/[0-9]+/num/g' file`: Extended regex.
- `awk`:  Pattern scanning and processing language.
    - `awk '{print $1}' file`: Print first column of each line.
    - `awk -F: '{print $1, $3}' /etc/passwd`: Custom delimiter (colon).
    - `awk '/pattern/ {print $0}' file`: Print lines matching pattern.
    - `awk '{sum+=$1} END {print sum}' file`: Sum first column.
- `locate`:  Find files by name quickly.
    - `locate <filename>`: Search index for files matching name.
    - `locate "*.conf"`: Find all config files.
    - `sudo updatedb`: Update the index.
- `wname`:  Show information about window names.
    - `wname`: Show X11 window names (requires x11-utils or similar).

## System Tools
- `alias`:  Create command shortcuts.
    - `alias ll='ls -lh'`: Example alias for listing files.
    - `unalias ll`: Remove alias.
- `tmux`:  Terminal multiplexer.
    - `tmux`: Start new session.
    - `tmux new -s <name>`: New session with name.
    - `tmux attach -t <name>`: Attach to session.
    - `tmux ls`: List sessions.
    - `tmux kill-session -t <name>`: Kill session.
- `screen`:  Full-screen window manager for terminals.
    - `screen`: Start new screen session.
    - `screen -ls`: List sessions.
    - `screen -r <pid/session>`: Reattach to a session.
    - `Ctrl+a d`: Detach from session.
- `whereis`:  Locate command binary, source, and manual.
    - `whereis ls`: Locate binary, source, and man pages for ls.
- `which`:  Find the location of a command.
    - `which python3`: Show path to python3 binary.
- `mount`:  Mount file systems.
    - `mount /dev/sdb1 /mnt`: Mount device to /mnt.
    - `umount /mnt`: Unmount.
    - `mount -a`: Mount all entries from /etc/fstab.
- `lsb_release`:  Display Linux distribution information.
    - `lsb_release -a`: Show all distribution info.
    - `lsb_release -d`: Description only.
- `watch`:  Run a command repeatedly at intervals.
    - `watch -n 2 'command'`: Run command every 2 seconds.
    - `watch -d -n 1 df -h`: Highlight changes, every 1 second.
- `cron`:  Schedule jobs to run at specified times.
    - `crontab -e`: Edit user cron jobs.
    - `crontab -l`: List current jobs.
    - `crontab -r`: Remove all jobs.
- `export`:  Set environment variables.
    - `export VAR=value`: Set variable for current session.
    - `export PATH=$PATH:/new/path`: Add to PATH.

## User Management
- `useradd/usermod`:  Add or modify user accounts.
    - `useradd <username>`: Add new user.
    - `usermod -aG sudo <username>`: Add user to group.
    - `usermod -l newname oldname`: Change login name.
    - `usermod -d /home/newdir username`: Change home dir.
- `passwd`:  Change user passwords.
    - `passwd`: Change own password.
    - `sudo passwd <user>`: Change other user's password.
- `chmod`:  Modify file permissions.
    - `chmod 755 file`: Set rwxr-xr-x permissions.
    - `chmod -R 755 dir`: Recursive permission change.
    - `chmod +x file`: Make file executable.
- `chown`:  Change file ownership.
    - `chown user:group file`: Change owner and group.
    - `chown -R user:group dir`: Recursive change.

## System Monitoring & Troubleshooting
- `top/htop`:  Monitor system processes and resource usage.
    - `htop -u ram`: Display processes based on username.
    - `htop -d 15`: Delay between screen updates to 1.5 sec.
    - `htop -p 123,456`: Monitor certain Process IDs.
    - `htop -s PERCENT_MEM`: Sort by memory usage.
    - `top -u user`: Filter top by user.
    - `top -o %MEM`: Sort top by memory usage.
    - `top -p 12345`: Show only given PID in top.
- `ps`:  View currently running processes.
    - `ps -A` / `ps -e`: View all running processes.
    - `ps -ef` / `ps -eF`: Full format listing (more columns).
    - `ps aux`: BSD format process list.
    - `ps -e --forest`: Display process hierarchy tree.
    - `ps -e -o pid,uname,pmem`: Select columns to display.
    - `ps -e -o etime`: Display elapsed time for each process.
    - `ps -u ram`: Show processes for user "ram".
    - `ps -L 426`: View all threads of process ID 426.
    - `ps -U root -u root`: Show all processes running as root.
    - `ps -C process_name`: Search based on process name.
    - `ps -fG groupID` / `ps -fG group_name`: List all processes of a group id.
    - `ps -T`: View terminal-related processes.
- `kill/killall`:  Terminate processes.
    - `kill 257`: Kill process ID 257.
    - `kill -9 257`: Force kill process 257 (SIGKILL).
    - `kill -l`: List all signal names.
    - `killall firefox`: Kill all processes named "firefox".
    - `pkill pattern`: Kill processes matching pattern.
- `systemctl`:  Manage systemd system services.
    - `systemctl start smb`: Start a service.
    - `systemctl stop smb`: Stop a service.
    - `systemctl restart smb`: Restart a service.
    - `systemctl enable smb`: Enable service at boot.
    - `systemctl disable smb`: Disable service at boot.
    - `systemctl status smb`: View status of service.
    - `systemctl mask smb`: Prevent a service from being started.
    - `systemctl list-dependencies smb`: List all dependencies for service.
    - `systemctl set-default graphical.target`: Change default boot target.
    - `systemctl is-active smb`: Check if service is running.
    - `systemctl list-units --type=service`: List active services.
- `service`:  Start, stop, or restart services (SysVinit/upstart).
    - `service smb start`: Start a service.
    - `service smb stop`: Stop a service.
    - `service smb restart`: Restart a service.
    - `service smb status`: View status of service.
    - `service --status-all`: List all services and status.
- `df`:  Report file system space usage.
    - `df -m /boot`: Display info about /boot in MB.
    - `df -h`: Display in human readable output.
    - `df -T`: Show filesystem types.
    - `df -a`: Show all mount points (including dummy).
    - `df -i`: Show inode info.
- `du`:  Disk usage summary.
    - `du -h /var`: Show disk usage of every file/dir in /var in human-readable format.
    - `du -sh /var`: Show summary size of /var.
    - `du -a /var`: Show usage including all files.
    - `du -BK /var`: Show disk usage in Kilobytes (`-BM`, `-BG` for MB/GB).
    - `du --max-depth=1 /var`: Size of each sub-directory in /var.
    - `du -h --exclude="*.log" /var`: Exclude .log files from size calculation.
    - `du --total /var`: Show grand total at the end.
- `free`:  Show memory usage.
    - `free -h`: Human readable.
    - `free -m`: Show memory in MB.
    - `free -g`: Show memory in GB.
    - `free -s 5 -c 10`: Show memory every 5s, 10 times.
    - `free -l`: Show low and high memory info.
- `dmesg`:  Display kernel logs.
    - `dmesg -T`: Show human-readable timestamps.
    - `dmesg -w`: Follow logs as they are written (like tail -f).
    - `dmesg -l warn,notice`: Filter by log level.
    - `dmesg -L`: Colorize output (kernel 5.10+).
- `journalctl`:  View systemd logs.
    - `journalctl -b`: Show logs since last boot.
    - `journalctl -r`: Show in reverse time order.
    - `journalctl --since "1 hour ago"`: Show logs from last hour.
    - `journalctl -u nginx.service`: Logs by service.
    - `journalctl -f`: Follow logs in real time.
    - `journalctl -o verbose`: Verbose log output.
    - `journalctl -o json-pretty`: JSON formatted log output.
    - `journalctl -p "emerg"`: By priority level.
    - `journalctl _UID=108`: By user id.
- `uptime`:  Show system uptime.
    - `uptime`: Basic uptime info.
    - `uptime -s`: Show when system was booted.
    - `uptime -p`: Pretty format.
- `vmstat`:  Show virtual memory, processes, I/O, system stats.
    - `vmstat -a`: Show active/inactive memory.
    - `vmstat -s`: Memory stats in summary.
    - `vmstat -f`: Number of forks since boot.
    - `vmstat -d`: Disk stats.
    - `vmstat -p vda1`: Partition stats.
    - `vmstat -S k`: Show in kilobytes.
    - `vmstat -m`: Slab statistics.
- `rsync`:  Copy and synchronize files locally and remotely.
    - `rsync -zvh backup.tar.gz /tmp/backups/`: Copy with compression and verbosity.
    - `rsync -avzh /root/rpmpkgs /tmp/backups/`: Archive mode, compress, verbose.
    - `rsync -avzh /root/rpmpkgs root@10.0.0.1:~/rpms/`: Copy to remote host via SSH.
    - `rsync -avzh root@10.0.0.1:/rpms /root/rpmpkgs`: Copy from remote host.
    - `rsync -e ssh root@10.0.0.1:/rpms /root/rpmpkgs`: Specify SSH as transport.
    - `rsync -avzhe ssh --progress /root/rpmpkgs root@10.0.0.1:/rpms`: Show progress.
    - `rsync -avz --include='*.txt' /root/rpmpkgs /tmp/backups`: Include only txt files.
    - `rsync -avz --exclude='*.txt' /root/rpmpkgs /tmp/backups`: Exclude txt files.
    - `rsync -avz --max-size='200k' /root/rpmpkgs /tmp/backups`: File transfer size limit.
    - `rsync -avz --bwlimit=100 /root/rpmpkgs /tmp/backups`: Bandwidth limit (KB/s).
- `strace`:  Trace system calls and signals.
    - `strace ls`: Trace system calls during `ls`.
    - `strace -e open ls`: Show only "open" syscalls.
    - `strace -o output.txt ls`: Save trace to file.
    - `strace -p 257`: Trace running process by PID.
    - `strace -t ls`: Show timestamps for each line.
    - `strace -c ls`: Show summary statistics.
- `modinfo`:  Display information about kernel modules.
    - `modinfo <module>`: Show info for module.
- `insmod`:  Insert a module into the kernel.
    - `insmod <module.ko>`: Insert module file.
- `lsmod`:  Show loaded kernel modules.
    - `lsmod`: List modules currently loaded.
- `lspci`:  List PCI devices.
    - `lspci -mm`: Machine readable format.
    - `lspci -vv`: Very verbose.
    - `lspci -s 00:01.0`: Info for specific device.
    - `lspci -nn`: Show vendor/device codes.
    - `lspci -k`: Show kernel drivers used.
- `lshw`:  Detailed hardware info.
    - `lshw -short`: Short summary.
    - `lshw -businfo`: Show bus info (SCSI, USB, PCI).
- `lsof`:  List open files and processes.
    - `lsof`: List all open files.
    - `lsof /etc`: Open files in /etc.
    - `lsof -u root`: Files opened by user root.
    - `lsof -p 257`: Files opened by PID 257.
    - `lsof -i`: Files opened by network sockets.
    - `lsof -i 4`: IPv4 sockets.
    - `lsof -i 6`: IPv6 sockets.
    - `lsof -i tcp`: TCP connections.
    - `lsof -i udp`: UDP connections.
    - `lsof -i :3306`: By port number.
    - `lsof -i :80-1024`: By port range.
    - `lsof -t /usr/bin/df`: PIDs holding file.
- `lsblk`:  List block devices and partitions.
    - `lsblk`: Basic list.
    - `lsblk -a`: Include empty devices.
    - `lsblk -m`: Show owner, group, mode.
- `dd`:  Copy and convert data at a low level.
    - `dd if=/tmp/ubuntu.iso of=/dev/sdX bs=4M status=progress`: Make bootable USB.
    - `sudo dd if=/dev/sdX | gzip > backup.img.gz`: Create compressed disk image.
    - `sudo dd if=/dev/sdX | openssl enc -aes-256-cbc -out backup.img.enc`: Encrypted image.
    - `dd if=/dev/nvme0n1 of=/var/backup.img bs=4M status=progress`: Full disk backup.
    - `dd if=/var/backup.img of=/dev/nvme0n1 bs=4M status=progress`: Restore disk image.
    - `dd if=/dev/zero of=/dev/sdX bs=1M status=progress`: Wipe disk.
    - `dd if=/dev/zero of=tempfile bs=1M count=1024 conv=fdatasync status=progress`: Disk write performance.
    - `sudo dd if=/dev/sda of=/dev/null bs=1M status=progress`: Disk read performance.
    - `sudo dd if=/dev/sdX of=mbr_backup.bin bs=512 count=1`: Backup MBR.
    - `sudo dd if=mbr_backup.bin of=/dev/sdX bs=512 count=1`: Restore MBR.
    - `dd if=/dev/sda of=/dev/sdb bs=64k conv=noerror,sync status=progress`: Clone disks.
    - `dd if=/dev/zero of=/swapfile bs=1M count=2048`: Create 2GB swap file.
    - `mkswap /swapfile && sudo swapon /swapfile`: Activate swapfile.

## Networking
- `ssh`:  Secure shell for remote access.
    - `ssh user@host`: Connect to host as user.
    - `ssh -i ~/.ssh/keyfile user@host`: Use custom identity file.
    - `ssh -L 8080:localhost:80 user@host`: Forward local port 8080 to host's port 80.
    - `ssh -N -f -L 2222:localhost:22 user@host`: Background SSH tunnel.
- `ssh-keygen`:  Generate/manage SSH key pairs.
    - `ssh-keygen -t rsa -b 4096 -C "email@example.com"`: Generate RSA key.
    - `ssh-keygen -lf ~/.ssh/id_rsa.pub`: Show key fingerprint.
    - `ssh-keygen -y -f ~/.ssh/id_rsa`: Extract public key from private.
- `scp`:  Securely copy files between systems.
    - `scp file user@host:/path/`: Copy file to remote.
    - `scp -r dir user@host:/path/`: Copy directory recursively.
    - `scp user@host:/file ./`: Copy file from remote.
    - `scp -P 2222 file user@host:/path/`: Use custom SSH port.
- `curl`:  Transfer data from or to a server.
    - `curl -O http://url/file`: Download file.
    - `curl -L http://url`: Follow redirects.
    - `curl -I http://url`: Fetch headers only.
    - `curl -u user:pass http://url`: HTTP authentication.
    - `curl -X POST -d "param=value" http://url`: POST data.
- `wget`:  Download files from the internet.
    - `wget http://url/file`: Download.
    - `wget -c http://url/file`: Continue incomplete download.
    - `wget -r http://url/`: Download recursively.
    - `wget --no-check-certificate https://url/`: Ignore SSL errors.
- `ftp/sftp`:  File transfer protocol commands.
    - `ftp host`: Start FTP session.
    - `sftp user@host`: Secure FTP session.
    - `sftp -i keyfile user@host`: Use custom identity file.
- `ifconfig`:  Configure network interfaces (legacy).
    - `ifconfig`: Show interfaces.
    - `ifconfig eth0 up/down`: Enable/Disable interface.
- `ip`:  Modern network interface management.
    - `ip a`: Show all interfaces and IPs.
    - `ip link set eth0 up/down`: Enable/Disable interface.
    - `ip route`: Show routing table.
    - `ip addr add 192.168.1.10/24 dev eth0`: Add IP to interface.
- `dig/nslookup`:  Query DNS records.
    - `dig google.com`: Lookup domain.
    - `dig @8.8.8.8 google.com +short`: Use custom DNS, short output.
    - `nslookup google.com`: Lookup domain.
- `ping`:  Test network connectivity.
    - `ping 8.8.8.8`: Ping IP address.
    - `ping -c 4 google.com`: Send 4 ping packets.
- `traceroute`:  Trace network routes.
    - `traceroute google.com`: Trace route to domain.
    - `traceroute -I google.com`: Use ICMP instead of UDP.
- `iptables/ufw/firewall-cmd`:  Firewall configuration.
    - `iptables -L`: List rules.
    - `iptables -A INPUT -p tcp --dport 22 -j ACCEPT`: Allow SSH.
    - `ufw enable`: Enable uncomplicated firewall.
    - `ufw allow 80/tcp`: Allow HTTP through firewall.
    - `firewall-cmd --list-all`: Show firewalld status.
    - `firewall-cmd --add-port=8080/tcp`: Open port 8080.
- `netstat/ss`:  Display network statistics.
    - `netstat -a`: List all ports and connections.
    - `netstat -at`: List TCP ports.
    - `netstat -au`: List UDP ports.
    - `netstat -l`: Only listening ports.
    - `netstat -s`: Protocol statistics.
    - `netstat -i`: Packet statistics and MTU.
    - `netstat -lp`: Listening programs with PID.
    - `netstat -r`: Routing table.
    - `ss -tuln`: List TCP/UDP listening ports (modern replacement).
    - `ss -p`: Show process using socket.
- `nmap`:  Network scanner and port detection.
    - `nmap -sS 192.168.1.0/24`: Stealth scan subnet.
    - `nmap -p 80,443 host`: Scan specific ports.
    - `nmap -A host`: OS and version detection.
- `ethtool`:  Network driver and hardware settings.
    - `ethtool eth0`: Show info for device.
    - `ethtool -s eth0 speed 100 autoneg off`: Set speed.
    - `ethtool -i eth0`: Show driver info.
    - `ethtool -a eth0`: Show pause parameters.
    - `ethtool -S eth0`: Show statistics.

## Package Management
- `apt`:
    - `apt update`: Download package information.
    - `apt upgrade`: Upgrade all installed packages and security updates.
    - `apt --upgradable`: List packages that can be upgraded.
    - `apt full-upgrade`: Perform full system upgrade.
    - `apt install nginx`: Install new package.
    - `apt remove nginx`: Remove a package.
    - `apt purge nginx`: Remove both package and config files.
    - `apt autoremove`: Remove automatically installed packages no longer needed.
    - `apt --purge autoremove`: Purge installed packages that are no longer needed.
    - `apt search nginx*`: Search installed packages.
    - `apt show nginx`: Show info about packages.
    - `apt list --installed`: List all installed packages.
    - `apt depends nginx`: List all dependencies of a package.
    - `apt reinstall nginx`: Reinstall a package.
- `yum`:
    - `yum install firefox`: Install a package.
    - `yum remove firefox`: Remove a package.
    - `yum update firefox`: Update a package.
    - `yum search firefox`: Search for a package.
    - `yum info firefox`: Get info about a package.
    - `yum check-update`: Check for available updates.
    - `yum update`: Update system.
    - `yum repolist`: List enabled yum repositories.
    - `yum --enablerepo=epel install phpmyadmin`: Install a package from specific repository.
    - `yum provides /etc/passwd`: Find which package this file belongs to.
    - `yum list installed`: List installed packages.
    - `yum clean all`: Clean yum cache.
- `rpm`: 
    - `rpm -ivh firefox.rpm`: Install the package.
    - `rpm -Uvh firefox.rpm`: Upgrade the package.
    - `rpm -ev firefox`: Erase/Remove an installed package.
    - `rpm -ev --nodeps firefox`: Erase/Remove without checking for dependencies.
    - `rpm -qa`: Display or list all installed packages.
    - `rpm -qi firefox`: Display information about an installed package.
    - `rpm -qf /etc/passwd`: Find out what package a file belongs to.
    - `rpm -qc firefox`: Display list of configuration files for a package.
    - `rpm -qpR firefox.rpm`: Find all dependencies of a rpm file.
    - `rpm -qpR firefox`: Find all dependencies of a package.
- `pacman`:
    - `pacman -Syu`: Update existing packages and install latest package information.
    - `pacman -S htop`:  Install htop tool.
    - `pacman -Ss htop`: Search for a package.
    - `pacman -R htop`: Remove a package.
- `dnf`:  Package managers for different Linux distributions.
    - `dnf install <pkg>`: Install a package.
    - `dnf remove <pkg>`: Remove a package.
    - `dnf update`: Update all packages.
    - `dnf search <pkg>`: Search for a package.
- `dpkg`:
    - `dpkg -i apache2.deb`: Install a package.
    - `dpkg -l`: List installed packages.
    - `dpkg -l apache2`: Check if a package is installed or not.
    - `dpkg -r apache2`: Remove/Uninstall a package.
    - `dpkg -p apache2`: Purge (Uninstall and remove config) a package.
    - `dpkg -c apache2`: View contents of a deb package.
    - `dpkg -L apache2`: List files installed by deb package.
    - `dpkg -R apache2 tomcat`: Install multiple deb packages.
    - `dpkg --unpack apache2.deb`: Extract contents of .deb package.
    - `dpkg --configure apache2`: Configure an unpacked package.

## Compression and Archiving
- `tar/zip/gzip`:  File compression utilities.
    - `tar -czvf file.tar.gz dir/`: Compress directory to tar.gz.
    - `tar -xzvf file.tar.gz`: Extract tar.gz file.
    - `zip -r file.zip dir/`: Compress directory to zip.
    - `unzip file.zip`: Extract zip file.
    - `gzip file`: Compress file to .gz.
    - `gunzip file.gz`: Decompress .gz file.

## Performance Testing
- `iperf/jperf`:  Network performance measurement.
    - `iperf -s`: Start iperf server.
    - `iperf -c <host>`: Run iperf client to host.
    - `iperf -t 60 -c <host>`: Test bandwidth for 60 seconds.
- `perf`:  Performance analysis tool.
    - `perf top`: Real-time system profiling.
    - `perf record ./a.out`: Profile a process.
    - `perf report`: Show profiling report.

## Core Paths & Diagnostic Files

#### `/proc/cpuinfo`: Detailed CPU info per core (model, features, etc.)
- **Key fields:** `model name`, `cpu MHz`, `flags`, `processor`
    ```sh
    cat /proc/cpuinfo
    processor   : 0
    vendor_id   : GenuineIntel
    model name  : Intel(R) Core(TM) i7-8850H CPU @ 2.60GHz
    cpu MHz     : 2600.000
    flags       : fpu vme de pse tsc msr pae mce cx8 ...
    ```
---
#### `/proc/meminfo`: System RAM/swap usage and memory statistics.
- **Key fields:** `MemTotal`, `MemFree`, `MemAvailable`, `Buffers`, `Cached`, `SwapTotal`, `SwapFree`
    ```sh
    cat /proc/meminfo
    MemTotal:       32616656 kB
    MemFree:        12345678 kB
    MemAvailable:   23456789 kB
    Buffers:          123456 kB
    Cached:          2345678 kB
    SwapTotal:      16777212 kB
    SwapFree:       16777212 kB
    ```
---
#### `/proc/uptime`: System uptime and idle time, in seconds.
    ```sh
    cat /proc/uptime
    84212.38 62300.77
    ```
---
#### `/proc/loadavg`: System load averages (1, 5, 15 min), running/total processes, last PID.
    ```sh
    cat /proc/loadavg
    1.02 0.78 0.67 3/456 12567
    ```
---
#### `/proc/stat`: System stats since boot (CPU, context switches, boot time, etc.)
- **Key:** `cpu`, `intr`, `ctxt`, `btime`, `processes`
    ```sh
    head /proc/stat
    cpu  12345 67 8901 2345678 0 0 0 0 0 0
    cpu0 1234 5 678 123456 0 0 0 0 0 0
    intr 123456789 0 0 0 ...
    ctxt 1234567
    btime 1660000000
    processes 23456
    ```
---
#### `/proc/interrupts`: Interrupt counts per IRQ per CPU.
    ```sh
    head /proc/interrupts
               CPU0       CPU1
      0:      12345      12340   IO-APIC   2-edge      timer
      1:          2          0   IO-APIC   1-edge      i8042
    ```
---
#### `/proc/partitions`: List of block devices and their partition sizes.
    ```sh
    cat /proc/partitions
    major minor  #blocks  name
      8        0 488386584 sda
      8        1    8388608 sda1
      8        2 479997952 sda2
    ```
---
#### `/proc/buddyinfo`: Free memory "buddies" per zone/node (memory fragmentation).
    ```sh
    cat /proc/buddyinfo
    Node 0, zone   Normal  1234 567 89 ... 
    ```
---
#### `/proc/cmdline`: Kernel boot parameters.
    ```sh
    cat /proc/cmdline
    BOOT_IMAGE=/vmlinuz root=/dev/sda1 ro quiet splash
    ```
---
#### `/proc/swaps`: Active swap devices and usage.
    ```sh
    cat /proc/swaps
    Filename                                Type            Size    Used    Priority
    /swapfile                               file            2097148 0       -2
    ```
---
#### `/proc/version`: Kernel version and build info.
    ```sh
    cat /proc/version
    Linux version 5.15.0-105-generic (buildd@lcy02-amd64-056) ...
    ```
---
#### `/proc/filesystems`: Supported filesystem types in kernel.
    ```sh
    cat /proc/filesystems
    nodev   sysfs
    nodev   proc
    nodev   devtmpfs
    ext4
    vfat
    ```
---
#### `/proc/net/dev`: Network interface stats (RX/TX bytes, packets, errors).
    ```sh
    cat /proc/net/dev
    Inter-|   Receive                                                |  Transmit
     face |bytes    packets errs drop fifo frame compressed multicast|bytes    packets errs drop fifo colls carrier compressed
        lo: 2872661   17846    0    0    0     0          0         0   2872661   17846    0    0    0     0       0          0
      eth0: 128728532 121125    0    0    0     0          0         0  10758243   96080    0    0    0     0       0          0
    ```
---
#### `/proc/diskstats`: Block device I/O statistics.
    ```sh
    cat /proc/diskstats
    8       0 sda 158631 18245 3532456 128831 269315 12865 2093842 103882 0 97382 232713
    ```
---
#### `/proc/mounts`: All currently mounted filesystems.
    ```sh
    cat /proc/mounts
    /dev/sda1 / ext4 rw,relatime 0 0
    proc /proc proc rw,nosuid,nodev,noexec,relatime 0 0
    ```
---

#### `/sys/class/net/eth0/operstate`: Network interface status ("up" or "down").
    ```sh
    cat /sys/class/net/eth0/operstate
    up
    ```
---
#### `/sys/block/sda/size`: Size of block device in 512-byte sectors.
    ```sh
    cat /sys/block/sda/size
    1953525168
    ```
---
#### `/sys/kernel/debug/`: Kernel debugfs (mount with `mount -t debugfs none /sys/kernel/debug`).
    ```sh
    ls /sys/kernel/debug/
    ```
---

#### `/var/log/syslog` or `/var/log/messages`: System log (general messages, syslog).
    ```sh
    tail -n 10 /var/log/syslog
    Jun 26 09:10:01 ubuntu CRON[12345]: (root) CMD (some job)
    Jun 26 09:10:01 ubuntu kernel: [123456.789] Some kernel message here
    ```
---
#### `/var/log/kern.log`: Kernel messages.
    ```sh
    tail -n 5 /var/log/kern.log
    Jun 26 09:10:01 ubuntu kernel: [123456.789] Some kernel message here
    ```
---
#### `/var/log/auth.log`: Authentication and sudo logs.
    ```sh
    tail -n 3 /var/log/auth.log
    Jun 26 09:10:01 ubuntu sudo:   alice : TTY=pts/0 ; PWD=/home/alice ; USER=root ; COMMAND=/bin/ls
    ```
---
#### `/var/log/dmesg`: Boot-time kernel ring buffer messages.
    ```sh
    head /var/log/dmesg
    [    0.000000] Linux version 5.15.0-105-generic ...
    ```
---

#### `/etc/fstab`: Filesystem mount configuration.
    ```sh
    cat /etc/fstab
    UUID=1234-abcd / ext4 errors=remount-ro 0 1
    /swapfile none swap sw 0 0
    ```
---
#### `/etc/passwd`: User account info.
    ```sh
    head -n 2 /etc/passwd
    root:x:0:0:root:/root:/bin/bash
    alice:x:1000:1000:Alice:/home/alice:/bin/bash
    ```
---
#### `/etc/hostname`: System hostname.
    ```sh
    cat /etc/hostname
    myubuntu
    ```
---

#### `/usr/bin/`, `/usr/local/bin/`: User commands and locally installed binaries.
    ```sh
    ls /usr/bin
    ls /usr/local/bin
    ```
---

#### `/dev/`: Device files (disks, ttys, random, etc)
    ```sh
    ls -l /dev/sda /dev/null /dev/tty /dev/pts/
    ```
---

#### `/tmp/`: Temporary files, cleared on reboot.
    ```sh
    ls /tmp
    ```
---

#### `/run/`: Volatile runtime info (PIDs, sockets, etc.)
    ```sh
    ls /run
    ```
---

#### `/boot/`: Kernel, initrd, and bootloader files.
    ```sh
    ls /boot
    vmlinuz-5.15.0-105-generic  initrd.img-5.15.0-105-generic  grub/
    ```
---

#### `/home/`: User home directories.
    ```sh
    ls /home
    alice  bob
    ```
---

#### `/opt/`: Optional/commercial/large third-party software.
    ```sh
    ls /opt
    google  VirtualBox
    ```
---

#### `/root/`: Root user's home directory.
    ```sh
    ls /root
    .bashrc  .ssh/
    ```
---
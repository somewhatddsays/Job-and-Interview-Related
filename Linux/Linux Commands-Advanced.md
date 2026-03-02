# Linux Complete Cheat Sheet — Advanced

---

## 1. Kernel & System Internals

### 1.1 Kernel Management

| Command | Description | Example |
|--------|-------------|---------|
| `uname -r` | Show kernel version | `uname -r` |
| `sysctl -a` | List all kernel parameters | `sysctl -a` |
| `sysctl <param>` | Read a kernel parameter | `sysctl vm.swappiness` |
| `sysctl -w <param>=<val>` | Set kernel parameter at runtime | `sysctl -w vm.swappiness=10` |
| `sysctl -p` | Reload /etc/sysctl.conf | `sysctl -p` |
| `dmesg -T` | Kernel logs with human timestamps | `dmesg -T \| tail -50` |
| `dmesg -w` | Follow kernel logs live | `dmesg -w` |
| `lsmod` | List loaded kernel modules | `lsmod` |
| `modinfo <module>` | Show info about a module | `modinfo ext4` |
| `modprobe <module>` | Load a kernel module | `sudo modprobe vboxdrv` |
| `modprobe -r <module>` | Unload a kernel module | `sudo modprobe -r vboxdrv` |
| `insmod <module>.ko` | Insert module manually | `sudo insmod mymod.ko` |
| `rmmod <module>` | Remove a module manually | `sudo rmmod mymod` |

### 1.2 /proc & /sys Filesystem

| Path | Description |
|------|-------------|
| `/proc/cpuinfo` | CPU details |
| `/proc/meminfo` | Memory details |
| `/proc/version` | Kernel version info |
| `/proc/<PID>/maps` | Memory map of a process |
| `/proc/<PID>/fd` | Open file descriptors of a process |
| `/proc/net/tcp` | Active TCP connections |
| `/proc/sys/vm/swappiness` | Swappiness kernel param |
| `/sys/class/net/` | Network interface info |
| `/sys/block/` | Block device info |

---

## 2. Advanced Process Management

### 2.1 Process Introspection

| Command | Description | Example |
|--------|-------------|---------|
| `strace <cmd>` | Trace system calls of a process | `strace ls` |
| `strace -p <PID>` | Attach strace to running process | `strace -p 1234` |
| `strace -e trace=file <cmd>` | Trace only file-related syscalls | `strace -e trace=file ls` |
| `ltrace <cmd>` | Trace library calls | `ltrace ls` |
| `lsof -p <PID>` | List files opened by process | `lsof -p 1234` |
| `lsof -u <user>` | List files opened by user | `lsof -u john` |
| `lsof -i` | List all network connections | `lsof -i` |
| `lsof -i :<port>` | What process is on a port | `lsof -i :443` |
| `pmap <PID>` | Show memory map of process | `pmap 1234` |
| `cat /proc/<PID>/status` | Detailed process status | `cat /proc/1234/status` |

### 2.2 cgroups (Control Groups)

| Command | Description | Example |
|--------|-------------|---------|
| `systemd-cgls` | Show cgroup tree | `systemd-cgls` |
| `systemd-cgtop` | Live cgroup resource usage | `systemd-cgtop` |
| `cgcreate -g cpu:/mygroup` | Create a cgroup | `cgcreate -g cpu:/mygroup` |
| `cgexec -g cpu:/mygroup <cmd>` | Run command in cgroup | `cgexec -g cpu:/mygroup stress` |
| `cgset -r cpu.shares=512 mygroup` | Limit CPU shares | `cgset -r cpu.shares=512 mygroup` |

### 2.3 Namespaces

| Command | Description | Example |
|--------|-------------|---------|
| `lsns` | List all namespaces | `lsns` |
| `unshare --pid --fork bash` | Run shell in new PID namespace | `unshare --pid --fork bash` |
| `nsenter -t <PID> --all` | Enter all namespaces of a process | `nsenter -t 1234 --all` |
| `ip netns list` | List network namespaces | `ip netns list` |
| `ip netns add <ns>` | Create network namespace | `ip netns add mynamespace` |
| `ip netns exec <ns> <cmd>` | Run command in network namespace | `ip netns exec mynamespace ip a` |

---

## 3. Advanced Networking

### 3.1 ip Command (Full Reference)

| Command | Description | Example |
|--------|-------------|---------|
| `ip a` | Show all interfaces & IPs | `ip a` |
| `ip link show` | Show link layer info | `ip link show` |
| `ip link set <iface> up/down` | Bring interface up or down | `ip link set eth0 down` |
| `ip addr add <ip/cidr> dev <iface>` | Assign IP to interface | `ip addr add 192.168.1.100/24 dev eth0` |
| `ip addr del <ip/cidr> dev <iface>` | Remove IP from interface | `ip addr del 192.168.1.100/24 dev eth0` |
| `ip route show` | Show routing table | `ip route show` |
| `ip route add <net> via <gw>` | Add static route | `ip route add 10.0.0.0/8 via 192.168.1.1` |
| `ip route del <net>` | Delete a route | `ip route del 10.0.0.0/8` |
| `ip neigh show` | Show ARP table | `ip neigh show` |

### 3.2 Traffic Analysis

| Command | Description | Example |
|--------|-------------|---------|
| `tcpdump -i <iface>` | Capture packets on interface | `tcpdump -i eth0` |
| `tcpdump -i <iface> port <n>` | Capture on specific port | `tcpdump -i eth0 port 443` |
| `tcpdump -w out.pcap` | Write capture to file | `tcpdump -w capture.pcap` |
| `tcpdump -r out.pcap` | Read capture from file | `tcpdump -r capture.pcap` |
| `tcpdump host <ip>` | Filter by host | `tcpdump host 192.168.1.1` |
| `ss -s` | Socket statistics summary | `ss -s` |
| `ss -o state established` | Show established connections | `ss -o state established` |
| `iftop` | Live bandwidth usage per connection | `sudo iftop -i eth0` |
| `nethogs` | Live bandwidth per process | `sudo nethogs eth0` |
| `nstat` | Network stack statistics | `nstat` |

### 3.3 iptables — Firewall

| Command | Description | Example |
|--------|-------------|---------|
| `iptables -L -v -n` | List all rules verbosely | `iptables -L -v -n` |
| `iptables -A INPUT -p tcp --dport 22 -j ACCEPT` | Allow SSH in | — |
| `iptables -A INPUT -p tcp --dport 80 -j ACCEPT` | Allow HTTP in | — |
| `iptables -A INPUT -j DROP` | Drop all other inbound | — |
| `iptables -D INPUT -j DROP` | Delete a rule | — |
| `iptables -F` | Flush all rules | `iptables -F` |
| `iptables-save > rules.v4` | Save rules to file | `iptables-save > /etc/iptables/rules.v4` |
| `iptables-restore < rules.v4` | Restore rules from file | `iptables-restore < rules.v4` |

### 3.4 nftables (Modern Replacement)

| Command | Description | Example |
|--------|-------------|---------|
| `nft list ruleset` | List all nftables rules | `nft list ruleset` |
| `nft add table inet filter` | Create a table | — |
| `nft add chain inet filter input` | Create a chain | — |
| `nft add rule inet filter input tcp dport 22 accept` | Allow SSH | — |
| `nft flush ruleset` | Clear all rules | `nft flush ruleset` |

---

## 4. Storage & Filesystem Internals

### 4.1 LVM (Logical Volume Manager)

| Command | Description | Example |
|--------|-------------|---------|
| `pvdisplay` | Show physical volumes | `pvdisplay` |
| `vgdisplay` | Show volume groups | `vgdisplay` |
| `lvdisplay` | Show logical volumes | `lvdisplay` |
| `pvcreate /dev/sdb` | Initialize disk as PV | `pvcreate /dev/sdb` |
| `vgcreate vg0 /dev/sdb` | Create volume group | `vgcreate vg0 /dev/sdb` |
| `lvcreate -L 10G -n lv0 vg0` | Create 10G logical volume | `lvcreate -L 10G -n lv0 vg0` |
| `lvextend -L +5G /dev/vg0/lv0` | Extend LV by 5G | `lvextend -L +5G /dev/vg0/lv0` |
| `resize2fs /dev/vg0/lv0` | Resize ext4 filesystem | `resize2fs /dev/vg0/lv0` |
| `lvremove /dev/vg0/lv0` | Remove logical volume | `lvremove /dev/vg0/lv0` |

### 4.2 Filesystem Operations

| Command | Description | Example |
|--------|-------------|---------|
| `mkfs.ext4 /dev/sdb1` | Format as ext4 | `mkfs.ext4 /dev/sdb1` |
| `mkfs.xfs /dev/sdb1` | Format as XFS | `mkfs.xfs /dev/sdb1` |
| `fsck /dev/sdb1` | Check and repair filesystem | `fsck /dev/sdb1` |
| `tune2fs -l /dev/sda1` | Show ext4 filesystem info | `tune2fs -l /dev/sda1` |
| `dumpe2fs /dev/sda1` | Dump ext2/3/4 superblock info | `dumpe2fs /dev/sda1` |
| `xfs_info /dev/sdb1` | Show XFS filesystem info | `xfs_info /dev/sdb1` |
| `blkid` | Show UUID and type of block devices | `blkid` |
| `mount -o remount,ro /` | Remount filesystem read-only | `mount -o remount,ro /` |

### 4.3 /etc/fstab

| Field | Description |
|-------|-------------|
| Device | UUID or device path |
| Mount point | Where to mount |
| Type | Filesystem type (ext4, xfs) |
| Options | `defaults`, `ro`, `noexec`, etc. |
| Dump | Backup flag (0 or 1) |
| Pass | fsck order (0, 1, 2) |

---

## 5. Security & Hardening

### 5.1 SELinux

| Command | Description | Example |
|--------|-------------|---------|
| `getenforce` | Show SELinux mode | `getenforce` |
| `setenforce 1` | Set to Enforcing mode | `setenforce 1` |
| `setenforce 0` | Set to Permissive mode | `setenforce 0` |
| `sestatus` | Detailed SELinux status | `sestatus` |
| `ls -Z <file>` | Show SELinux context of file | `ls -Z /var/www` |
| `ps -eZ` | Show SELinux context of processes | `ps -eZ` |
| `chcon -t httpd_sys_content_t <file>` | Change file context | `chcon -t httpd_sys_content_t index.html` |
| `restorecon -Rv <dir>` | Restore default contexts | `restorecon -Rv /var/www` |
| `audit2allow -a` | Generate allow rules from audit log | `audit2allow -a` |
| `setsebool -P httpd_can_network_connect on` | Set SELinux boolean persistently | — |

### 5.2 AppArmor

| Command | Description | Example |
|--------|-------------|---------|
| `aa-status` | Show AppArmor status | `aa-status` |
| `aa-enforce <profile>` | Set profile to enforce mode | `aa-enforce /etc/apparmor.d/usr.bin.nginx` |
| `aa-complain <profile>` | Set profile to complain mode | `aa-complain /etc/apparmor.d/usr.bin.nginx` |
| `aa-disable <profile>` | Disable a profile | `aa-disable /etc/apparmor.d/usr.bin.nginx` |
| `apparmor_parser -r <profile>` | Reload a profile | `apparmor_parser -r /etc/apparmor.d/usr.bin.nginx` |

### 5.3 Auditing

| Command | Description | Example |
|--------|-------------|---------|
| `auditctl -l` | List audit rules | `auditctl -l` |
| `auditctl -w <file> -p rwxa` | Watch a file for all access | `auditctl -w /etc/passwd -p rwxa` |
| `auditctl -a always,exit -F arch=b64 -S execve` | Audit all exec calls | — |
| `ausearch -f <file>` | Search audit log for file | `ausearch -f /etc/passwd` |
| `ausearch -ua <user>` | Search audit log by user | `ausearch -ua john` |
| `aureport --summary` | Audit summary report | `aureport --summary` |
| `aureport -x` | Report on executed programs | `aureport -x` |

### 5.4 Encryption

| Command | Description | Example |
|--------|-------------|---------|
| `gpg --gen-key` | Generate GPG key pair | `gpg --gen-key` |
| `gpg -c <file>` | Encrypt file with passphrase | `gpg -c secret.txt` |
| `gpg <file>.gpg` | Decrypt a file | `gpg secret.txt.gpg` |
| `gpg -e -r <email> <file>` | Encrypt for a recipient | `gpg -e -r john@x.com file.txt` |
| `openssl enc -aes-256-cbc -in f -out f.enc` | Encrypt with AES-256 | — |
| `openssl enc -d -aes-256-cbc -in f.enc -out f` | Decrypt AES-256 | — |
| `openssl genrsa -out key.pem 4096` | Generate RSA private key | — |
| `openssl req -new -key key.pem -out csr.pem` | Generate CSR | — |
| `openssl x509 -in cert.pem -text` | Read a certificate | — |
| `cryptsetup luksFormat /dev/sdb1` | Encrypt disk with LUKS | — |
| `cryptsetup luksOpen /dev/sdb1 secure` | Open LUKS volume | — |

---

## 6. Advanced Shell Scripting

### 6.1 Arrays

| Concept | Syntax | Example |
|---------|--------|---------|
| Declare array | `arr=(a b c)` | `fruits=(apple banana cherry)` |
| Access element | `${arr[0]}` | `echo ${fruits[0]}` |
| All elements | `${arr[@]}` | `echo ${fruits[@]}` |
| Array length | `${#arr[@]}` | `echo ${#fruits[@]}` |
| Append element | `arr+=("d")` | `fruits+=("mango")` |
| Iterate array | `for i in "${arr[@]}"` | `for f in "${fruits[@]}"; do echo $f; done` |

### 6.2 String Manipulation

| Syntax | Description | Example |
|--------|-------------|---------|
| `${#VAR}` | Length of string | `${#NAME}` |
| `${VAR:2:5}` | Substring (offset:length) | `${NAME:0:4}` |
| `${VAR/old/new}` | Replace first occurrence | `${PATH/usr/local}` |
| `${VAR//old/new}` | Replace all occurrences | `${STR//foo/bar}` |
| `${VAR#prefix}` | Remove shortest prefix | `${FILE#*/}` |
| `${VAR##prefix}` | Remove longest prefix | `${FILE##*/}` |
| `${VAR%suffix}` | Remove shortest suffix | `${FILE%.*}` |
| `${VAR%%suffix}` | Remove longest suffix | `${FILE%%.*}` |
| `${VAR:-default}` | Use default if VAR unset | `${NAME:-"anonymous"}` |
| `${VAR:?error}` | Error if VAR unset | `${NAME:?"NAME required"}` |

### 6.3 Advanced Scripting Patterns

| Concept | Syntax |
|---------|--------|
| Strict mode | `set -euo pipefail` |
| Trap on exit | `trap 'cleanup' EXIT` |
| Trap on error | `trap 'echo "Error on line $LINENO"' ERR` |
| Subshell | `(cd /tmp && ls)` |
| Process substitution | `diff <(ls dir1) <(ls dir2)` |
| Here document | `cat <<EOF ... EOF` |
| Here string | `grep "foo" <<< "$VAR"` |
| Named pipe (FIFO) | `mkfifo mypipe` |
| Script debugging | `bash -x script.sh` |
| Check exit code | `echo $?` |

### 6.4 Regular Expressions

| Pattern | Matches |
|---------|---------|
| `.` | Any single character |
| `*` | Zero or more of previous |
| `+` | One or more of previous |
| `?` | Zero or one of previous |
| `^` | Start of line |
| `$` | End of line |
| `[abc]` | Any of a, b, or c |
| `[^abc]` | Not a, b, or c |
| `[a-z]` | Any lowercase letter |
| `\d` | Any digit (in ERE) |
| `\w` | Word character |
| `\s` | Whitespace |
| `(a\|b)` | Either a or b |
| `{n,m}` | Between n and m times |

---

## 7. Containers & Virtualization

### 7.1 Docker (System-Level)

| Command | Description | Example |
|--------|-------------|---------|
| `docker info` | Full Docker system info | `docker info` |
| `docker system df` | Docker disk usage | `docker system df` |
| `docker system prune -af` | Remove all unused resources | `docker system prune -af` |
| `docker inspect <container>` | Full container metadata | `docker inspect myapp` |
| `docker stats` | Live container resource usage | `docker stats` |
| `docker exec -it <c> bash` | Shell into running container | `docker exec -it myapp bash` |
| `docker cp <c>:<path> .` | Copy file from container | `docker cp myapp:/app/log.txt .` |
| `docker network ls` | List Docker networks | `docker network ls` |
| `docker network inspect <n>` | Inspect a network | `docker network inspect bridge` |
| `docker volume ls` | List volumes | `docker volume ls` |
| `docker volume inspect <v>` | Inspect a volume | `docker volume inspect mydata` |

### 7.2 Namespaces & Container Primitives

| Command | Description | Example |
|--------|-------------|---------|
| `unshare -u bash` | New UTS namespace | `unshare -u bash` |
| `unshare -n bash` | New network namespace | `unshare -n bash` |
| `unshare --mount bash` | New mount namespace | `unshare --mount bash` |
| `chroot <dir> bash` | Change root filesystem | `chroot /mnt/ubuntu bash` |
| `pivot_root <new> <old>` | Switch root filesystem | — |

---

## 8. Performance Tuning

### 8.1 CPU

| Command | Description | Example |
|--------|-------------|---------|
| `mpstat -P ALL 1` | Per-CPU stats every 1s | `mpstat -P ALL 1` |
| `taskset -c 0,1 <cmd>` | Pin process to CPU cores | `taskset -c 0,1 ./app` |
| `numactl --hardware` | Show NUMA topology | `numactl --hardware` |
| `numactl --cpunodebind=0 <cmd>` | Run on specific NUMA node | `numactl --cpunodebind=0 ./app` |
| `perf stat <cmd>` | CPU performance counters | `perf stat ls` |
| `perf top` | Live perf stats by symbol | `perf top` |
| `perf record -g <cmd>` | Record perf data with call graph | `perf record -g ./app` |
| `perf report` | Analyze recorded perf data | `perf report` |
| `cpupower frequency-info` | Show CPU frequency info | `cpupower frequency-info` |
| `cpupower frequency-set -g performance` | Set CPU to performance mode | — |

### 8.2 Memory

| Command | Description | Example |
|--------|-------------|---------|
| `free -h` | RAM and swap usage | `free -h` |
| `vmstat -s` | Memory stats summary | `vmstat -s` |
| `slabtop` | Kernel slab cache usage | `slabtop` |
| `cat /proc/meminfo` | Detailed memory info | `cat /proc/meminfo` |
| `echo 3 > /proc/sys/vm/drop_caches` | Drop page/dentry/inode caches | — |
| `valgrind <cmd>` | Memory leak detection | `valgrind ./app` |
| `valgrind --leak-check=full <cmd>` | Full leak analysis | `valgrind --leak-check=full ./app` |

### 8.3 Disk I/O

| Command | Description | Example |
|--------|-------------|---------|
| `iostat -xz 1` | Extended disk stats every 1s | `iostat -xz 1` |
| `iotop` | Live I/O usage per process | `sudo iotop` |
| `blktrace -d /dev/sda` | Block layer I/O tracing | `blktrace -d /dev/sda` |
| `hdparm -tT /dev/sda` | Disk read speed benchmark | `hdparm -tT /dev/sda` |
| `fio --name=test --rw=randread` | Advanced I/O benchmarking | — |
| `dd if=/dev/zero of=test bs=1G count=1` | Write speed test | — |

---

## 9. Advanced SSH

| Command | Description | Example |
|--------|-------------|---------|
| `ssh -L 8080:localhost:80 user@host` | Local port forwarding | `ssh -L 8080:localhost:80 john@server` |
| `ssh -R 8080:localhost:80 user@host` | Remote port forwarding | `ssh -R 8080:localhost:80 john@server` |
| `ssh -D 1080 user@host` | Dynamic SOCKS proxy | `ssh -D 1080 john@server` |
| `ssh -J jumphost user@host` | SSH jump host (bastion) | `ssh -J bastion.com john@internal` |
| `ssh -o StrictHostKeyChecking=no` | Skip host key check | — |
| `ssh -i ~/.ssh/id_rsa user@host` | Use specific key | `ssh -i ~/.ssh/mykey john@server` |
| `ssh-add ~/.ssh/id_rsa` | Add key to SSH agent | `ssh-add ~/.ssh/id_rsa` |
| `ssh-agent bash` | Start SSH agent in shell | `ssh-agent bash` |
| `~/.ssh/config` | SSH client config file | — |

### 9.1 ~/.ssh/config Example

```
Host myserver
    HostName 192.168.1.10
    User john
    Port 2222
    IdentityFile ~/.ssh/id_rsa
    ServerAliveInterval 60

Host bastion
    HostName bastion.example.com
    User ec2-user
    ForwardAgent yes
```

---

## 10. System Boot & Init

### 10.1 Boot Process

| Stage | Description |
|-------|-------------|
| BIOS/UEFI | Hardware init, finds bootloader |
| Bootloader (GRUB) | Loads kernel into memory |
| Kernel | Initializes hardware, mounts root fs |
| initramfs | Temporary root fs for early boot |
| systemd (PID 1) | Starts all services and targets |
| Login | getty / display manager |

### 10.2 GRUB

| Command | Description | Example |
|--------|-------------|---------|
| `grub2-mkconfig -o /boot/grub2/grub.cfg` | Regenerate GRUB config | — |
| `grub2-install /dev/sda` | Install GRUB to disk | — |
| `cat /boot/grub2/grub.cfg` | View GRUB config | — |
| `grep menuentry /boot/grub2/grub.cfg` | List boot entries | — |

### 10.3 systemd Targets (Runlevels)

| Target | Equivalent Runlevel | Description |
|--------|--------------------|----|
| `poweroff.target` | 0 | Shutdown |
| `rescue.target` | 1 | Single-user mode |
| `multi-user.target` | 3 | Multi-user, no GUI |
| `graphical.target` | 5 | Multi-user with GUI |
| `reboot.target` | 6 | Reboot |

| Command | Description | Example |
|--------|-------------|---------|
| `systemctl get-default` | Show default target | `systemctl get-default` |
| `systemctl set-default <target>` | Set default target | `systemctl set-default multi-user.target` |
| `systemctl isolate <target>` | Switch to target now | `systemctl isolate rescue.target` |
| `systemd-analyze` | Boot time analysis | `systemd-analyze` |
| `systemd-analyze blame` | Per-service boot time | `systemd-analyze blame` |
| `systemd-analyze critical-chain` | Critical boot path | `systemd-analyze critical-chain` |

---

## 11. Advanced File Operations

### 11.1 inotify — Filesystem Events

| Command | Description | Example |
|--------|-------------|---------|
| `inotifywait -m <dir>` | Watch directory for changes | `inotifywait -m /var/www` |
| `inotifywait -e modify,create,delete <dir>` | Watch specific events | `inotifywait -e modify /etc` |
| `inotifywatch <dir>` | Count filesystem events | `inotifywatch /var/log` |

### 11.2 Extended Attributes

| Command | Description | Example |
|--------|-------------|---------|
| `getfattr -n user.comment <file>` | Get extended attribute | `getfattr -n user.comment file.txt` |
| `setfattr -n user.comment -v "my note" <file>` | Set extended attribute | `setfattr -n user.comment -v "reviewed" file.txt` |
| `lsattr <file>` | List immutable/append attributes | `lsattr file.txt` |
| `chattr +i <file>` | Make file immutable | `chattr +i /etc/resolv.conf` |
| `chattr -i <file>` | Remove immutable flag | `chattr -i /etc/resolv.conf` |
| `chattr +a <file>` | Make file append-only | `chattr +a app.log` |

### 11.3 Disk Recovery

| Command | Description | Example |
|--------|-------------|---------|
| `testdisk /dev/sda` | Partition recovery tool | `testdisk /dev/sda` |
| `photorec /dev/sda` | File carving/recovery tool | `photorec /dev/sda` |
| `dd if=/dev/sda of=disk.img bs=4M` | Clone disk to image | — |
| `dd if=disk.img of=/dev/sdb bs=4M` | Restore image to disk | — |
| `ddrescue /dev/sda disk.img map.log` | Fault-tolerant disk clone | — |

---

## 12. Observability & Tracing

### 12.1 eBPF & bpftrace

| Command | Description | Example |
|--------|-------------|---------|
| `bpftool prog list` | List loaded BPF programs | `bpftool prog list` |
| `bpftrace -l 'tracepoint:syscalls:*'` | List syscall tracepoints | — |
| `bpftrace -e 'tracepoint:syscalls:sys_enter_open { printf("%s\n", str(args->filename)); }'` | Trace open() calls | — |
| `bpftrace -e 'kprobe:do_sys_open { printf("%d %s\n", pid, str(arg1)); }'` | Trace with kprobe | — |

### 12.2 Classic Tracing Tools

| Command | Description | Example |
|--------|-------------|---------|
| `ftrace` | Kernel function tracing via /sys/kernel/debug/tracing | — |
| `perf trace <cmd>` | Syscall tracer like strace | `perf trace ls` |
| `systemtap` | Advanced kernel instrumentation | — |
| `dtrace` (on supported systems) | Dynamic tracing framework | — |

### 12.3 USE Method Checklist

| Resource | Utilization | Saturation | Errors |
|----------|-------------|------------|--------|
| CPU | `mpstat` | `vmstat r` | `perf stat` |
| Memory | `free` | `vmstat si/so` | `dmesg OOM` |
| Disk I/O | `iostat %util` | `iostat await` | `dmesg` |
| Network | `sar -n DEV` | `ss retrans` | `ip -s link` |

---

## 13. Automation & Configuration Management

### 13.1 Makefile for Shell Automation

```makefile
.PHONY: deploy clean

deploy:
	rsync -avz ./dist/ user@server:/var/www/
	ssh user@server "systemctl restart nginx"

clean:
	rm -rf ./dist
```

### 13.2 Useful One-Liners

| Task | Command |
|------|---------|
| Find and kill process on port | `lsof -ti:8080 \| xargs kill -9` |
| Watch log file for errors | `tail -f app.log \| grep --line-buffered "error"` |
| Recursively find large files | `find / -type f -size +100M 2>/dev/null` |
| Show top 10 largest dirs | `du -h / 2>/dev/null \| sort -rh \| head -10` |
| Count files in directory | `find . -type f \| wc -l` |
| Batch rename files | `for f in *.txt; do mv "$f" "${f%.txt}.md"; done` |
| Monitor file changes live | `while inotifywait -e close_write file.txt; do ./process.sh; done` |
| Extract IPs from log | `grep -oE '[0-9]{1,3}(\.[0-9]{1,3}){3}' access.log \| sort \| uniq -c \| sort -rn` |
| Create RAM disk | `mount -t tmpfs -o size=512m tmpfs /mnt/ramdisk` |
| Benchmark network | `iperf3 -s` (server) / `iperf3 -c <ip>` (client) |
| Run script at exact time | `at 14:30 <<< "./deploy.sh"` |
| Diff two directories | `diff -rq dir1/ dir2/` |
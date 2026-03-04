# 200 Linux Interview Q&A

#### What is Linux
Linux is an open-source, Unix-like operating system kernel developed
by Linus Torvalds. It is widely used in servers, desktops, mobile devices,
and embedded systems.

#### What is the difference between Linux and Unix?
Linux is an open-source Unix-like operating system kernel, while Unix is a proprietary operating system developed by **AT&T Bell Labs**. Unix requires a license, whereas Linux is free and open-source.

#### Explain the Linux file system hierarchy.
The Linux file system hierarchy is structured in a tree-like format starting from the root directory (**/**). Important directories include:

`/bin, /etc, /home, /var, /usr, and /tmp.`

#### What is the root account?
The root account is the superuser account in Linux with unrestricted access to all commands, files, and system resources. It is used for system administration tasks.

#### How do you change file permissions in Linux?
Use the `chmod` command. For example, *to set read, write, and execute permissions* for the owner and read permissions for others, use:

```
chmod 744 filename
```

#### What is the difference between `su` and `sudo`?
`su` switches the user to the **root account**, requiring the root password. `sudo` allows a permitted user to execute a command as the superuser or another user, requiring the user's password.

#### How do you check the current runlevel?
Use the `runlevel` command:

```
runlevel
```

#### How do you list all installed packages in a Debian-based system?
Use the `dpkg` command:

```
dpkg --list
```

#### How do you view running processes in Linux?
Use the `ps` or `top` command.

| Command  | Description        |
|:---------|:-------------------|
| `ps aux` | For a snapshot     |
| `top`    | For a dynamic view |

#### What is the use of the `grep` command?
`grep` searches for patterns within files. For example, to search for "error" in a file:

```
grep "error" filename
```

#### How do you display disk usage of directories?
Use the `du` command:

```
du -sh /path/to/directory
```

#### How do you check free disk space?
Use the `df` command:

```
df -h
```

#### What is a symbolic link?
A symbolic link is a type of file that points to another file or directory. It is created using the `ln -s` command:

```
ln -s /path/to/target /path/to/link
```

#### How do you find files containing a specific string?
Use the grep command with `-r` for recursive search:

```
grep -r "search_string" /path/to/directory
```

#### How do you compress files using tar?
Use the tar command with `-czf` to create a compressed archive:

```
tar -czf archive.tar.gz /path/to/directory
```

#### How do you extract files from a tar archive?
Use the tar command with `-xzf` to extract:

```
tar -xzf archive.tar.gz
```

#### How do you find the IP address of your system?
Use the `ip` or `ifconfig` command:

```
ip addr show
```
or
```
ifconfig
```

#### How do you view the contents of a file?
Use commands like `cat`, `less`, or `more`. For example:

```
cat filename
```

#### How do you change the hostname of a Linux system?
Use the `hostnamectl` command:

```
sudo hostnamectl set-hostname newhostname
```

#### What is the `crontab` command used for?
`crontab` is used to schedule jobs (commands or scripts) to run periodically. For example, to edit the crontab file:

```
crontab -e
```

#### How do you add a user in Linux?
Use the `adduser` command:

```
sudo adduser username
```

#### How do you delete a user in Linux?
Use the `deluser` command:

```
sudo deluser username
```

#### How do you switch to another user account?
Use the `su` command:

```
su - username
```

#### How do you change file ownership?
Use the `chown` command:

```
sudo chown user:group filename
```

#### How do you view system logs?
Use the `journalctl` command for systemd logs or `tail` for log files. For example:

```
journalctl
```
or
```
tail -f /var/log/syslog
```

#### How do you kill a process by its PID?
Use the `kill` command:

```
kill PID
```

#### How do you forcefully kill a process?
Use the `kill -9` command:

```
kill -9 PID
```

#### How do you find the PID of a process by its name?
Use the `pgrep` command:

```
pgrep processname
```

#### What is a package manager?
A package manager automates the process of installing, upgrading, configuring, and removing software packages. Examples include APT for Debian-based systems and YUM/DNF for Red Hat-based systems.

#### How do you update all packages in a Debian-based system?
Use the `apt update` and `apt upgrade` commands:

```
sudo apt update
sudo apt upgrade
```

#### How do you install a package in a Red Hat-based system?
Use the `yum` or `dnf` command:

```
sudo yum install package_name
```
or
```
sudo dnf install package_name
```

#### How do you remove a package in a Debian-based system?
Use the `apt remove` command:

```
sudo apt remove package_name
```

#### What is the difference between apt-get and apt?
`apt` is a higher-level interface for package management, providing a more user-friendly set of commands that include the functionality of `apt-get`, `apt-cache`, and other lower-level tools.

#### What is the find command used for?
`find` is used to search for files and directories based on various criteria. For example, to find all `.txt` files:

```
find /path/to/search -name "*.txt"
```

#### How do you count the number of lines, words, and characters in a file?
Use the `wc` command:

```
wc filename
```

#### What is the purpose of the /etc/passwd file?
The `/etc/passwd` file contains user account information, including username, user ID, group ID, home directory, and shell.

#### What is the /etc/shadow file?
The `/etc/shadow` file contains encrypted user passwords and additional account information like password expiration.

#### How do you display the last 10 lines of a file?
Use the `tail` command:

```
tail filename
```

#### How do you display the first 10 lines of a file?
Use the `head` command:

```
head filename
```

#### How do you combine multiple files into one?
Use the `cat` command:

```
cat file1 file2 > combined_file
```

#### What is the purpose of the /etc/fstab file?
The `/etc/fstab` file contains information about file systems and their mount points, specifying how and where they should be mounted.

#### How do you mount a file system?
Use the `mount` command:

```
sudo mount /dev/sdX1 /mnt
```

#### How do you unmount a file system?
Use the `umount` command:

```
sudo umount /mnt
```

#### What is the purpose of the /proc directory?
The `/proc` directory is a virtual file system providing information about system processes and kernel parameters.

#### How do you change the current directory?
Use the `cd` command:

```
cd /path/to/directory
```

#### How do you display the current directory?
Use the `pwd` command:

```
pwd
```

#### How do you create a new directory?
Use the `mkdir` command:

```
mkdir new_directory
```

#### How do you remove an empty directory?
Use the `rmdir` command:

```
rmdir empty_directory
```

#### How do you remove a directory and its contents?
Use the `rm -r` command:

```
rm -r directory_name
```

#### What is the purpose of the /etc/hosts file?
The `/etc/hosts` file maps hostnames to IP addresses, providing a way to associate names with IP addresses without using DNS.

#### How do you display all open network connections?
Use the `netstat` command:

```
netstat -tuln
```

#### What is the ifconfig command used for?
`ifconfig` is used to configure network interfaces, assign IP addresses, and manage network connections. However, `ip` is recommended for newer systems.

#### How do you configure a network interface using the ip command?
Use the `ip addr` command:

```
ip addr add 192.168.1.100/24 dev eth0
ip link set eth0 up
```

#### What is the ping command used for?
`ping` is used to check the network connectivity between two nodes by sending ICMP echo requests and measuring the response time.

#### How do you check DNS resolution for a domain?
Use the `dig` or `nslookup` command:

```
dig example.com
```
or
```
nslookup example.com
```

#### How do you add a new route in the routing table?
Use the `ip route add` command:

```
sudo ip route add 192.168.2.0/24 via 192.168.1.1
```

#### How do you display the routing table?
Use the `ip route show` command:

```
ip route show
```

#### What is the iptables command used for?
`iptables` is used to set up, maintain, and inspect the tables of IP packet filter rules in the Linux kernel.

#### How do you list the current iptables rules?
Use the `iptables -L` command:

```
sudo iptables -L
```

#### How do you allow incoming SSH connections on iptables?
Use the `iptables -A` command:

```
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

#### How do you save iptables rules?
Use the `iptables-save` command:

```
sudo iptables-save > /etc/iptables/rules.v4
```

#### What is the tcpdump command used for?
`tcpdump` is a packet analyzer that captures and displays the network traffic passing through a network interface.

#### How do you capture packets on a specific interface using tcpdump?
Use the `tcpdump -i` command:

```
sudo tcpdump -i eth0
```

#### What is the ss command used for?
`ss` is used to dump socket statistics and display information about network connections.

#### How do you display listening ports using ss?
Use the `ss -tuln` command:

```
ss -tuln
```

#### What is the hostname command used for?
`hostname` displays or sets the system's hostname.

#### How do you change the system's hostname?
Use the `hostnamectl` command:

```
sudo hostnamectl set-hostname newhostname
```

#### What is a shell in Linux?
A shell is a command-line interpreter that provides a user interface for accessing the operating system's services.

#### What is the difference between bash and sh?
`bash` (Bourne Again Shell) is an enhanced version of `sh` (Bourne Shell) with additional features like command history, tab completion, and improved scripting capabilities.

#### How do you create a shell script?
Create a text file with the `.sh` extension and add shell commands to it. For example:

```bash
#!/bin/bash
echo "Hello, World!"
```

#### How do you make a shell script executable?
Use the `chmod` command:

```
chmod +x script.sh
```

#### How do you run a shell script?
Use the `./` syntax:

```
./script.sh
```

#### What is the purpose of the shebang (#!) in a script?
The shebang specifies the interpreter to be used to execute the script. For example, `#!/bin/bash` tells the system to use bash to run the script.

#### How do you define a variable in a shell script?
Use the `=` operator without spaces:

```bash
variable_name="value"
```

#### How do you access a variable in a shell script?
Use the `$` symbol:

```bash
echo $variable_name
```

#### How do you read user input in a shell script?
Use the `read` command:

```bash
read variable_name
```

#### How do you use an if statement in a shell script?
Use the `if` keyword followed by the condition and `then` keyword. For example:

```bash
if [ condition ]; then
  commands
fi
```

#### How do you use a for loop in a shell script?
Use the `for` keyword followed by the loop variable and `in` keyword. For example:

```bash
for i in 1 2 3; do
  echo $i
done
```

#### How do you use a while loop in a shell script?
Use the `while` keyword followed by the condition. For example:

```bash
while [ condition ]; do
  commands
done
```

#### How do you pass arguments to a shell script?
Use positional parameters `$1`, `$2`, etc. For example:

```
./script.sh arg1 arg2
```

#### How do you display the current date and time?
Use the `date` command:

```
date
```

#### How do you display a calendar for the current month?
Use the `cal` command:

```
cal
```

#### How do you display the current user's username?
Use the `whoami` command:

```
whoami
```

#### How do you display a list of users currently logged in?
Use the `who` command:

```
who
```

#### How do you display information about the system?
Use the `uname` command. For detailed information:

```
uname -a
```

#### What is the uptime command used for?
`uptime` displays how long the system has been running, the number of users, and the load average.

#### How do you display the system's load average?
Use the `uptime` or `top` command.

#### What is the dmesg command used for?
`dmesg` displays the kernel ring buffer messages, useful for debugging hardware and driver issues.

#### How do you clear the terminal screen?
Use the `clear` command:

```
clear
```

#### How do you schedule a one-time job using at?
Use the `at` command followed by the time. For example:

```
echo "command" | at 10:00
```

#### How do you list scheduled at jobs?
Use the `atq` command:

```
atq
```

#### How do you remove a scheduled at job?
Use the `atrm` command followed by the job number:

```
atrm job_number
```

#### How do you schedule a recurring job using cron?
Edit the crontab file using `crontab -e` and add the job with the schedule. For example:

```
0 5 * * * /path/to/script.sh
```

#### How do you list all cron jobs for the current user?
Use the `crontab -l` command:

```
crontab -l
```

#### How do you remove all cron jobs for the current user?
Use the `crontab -r` command:

```
crontab -r
```

#### How do you view the system's scheduled cron jobs?
View the `/etc/crontab` file and files in `/etc/cron.d/`.

#### How do you send a message to all logged-in users?
Use the `wall` command:

```
echo "message" | wall
```

#### How do you display the amount of free and used memory in the system?
Use the `free` command:

```
free -h
```

#### How do you check for available software updates?
For Debian-based systems, use:

```
sudo apt update
```

For Red Hat-based systems, use:

```
sudo yum check-update
```

#### How do you reboot the system?
Use the `reboot` command:

```
sudo reboot
```

#### How do you shut down the system?
Use the `shutdown` command:

```
sudo shutdown now
```

#### How do you schedule a system shutdown?
Use the `shutdown` command with a time argument:

```
sudo shutdown +10  # Shutdown in 10 minutes
```

#### How do you cancel a scheduled shutdown?
Use the `shutdown -c` command:

```
sudo shutdown -c
```

#### How do you enable a service to start at boot?
Use the `systemctl enable` command:

```
sudo systemctl enable service_name
```

#### How do you disable a service from starting at boot?
Use the `systemctl disable` command:

```
sudo systemctl disable service_name
```

#### How do you start a service?
Use the `systemctl start` command:

```
sudo systemctl start service_name
```

#### How do you stop a service?
Use the `systemctl stop` command:

```
sudo systemctl stop service_name
```

#### How do you restart a service?
Use the `systemctl restart` command:

```
sudo systemctl restart service_name
```

#### How do you check the status of a service?
Use the `systemctl status` command:

```
systemctl status service_name
```

#### What is the purpose of the /etc/systemd/system/ directory?
It contains systemd unit files for services and targets that are enabled to start at boot.

#### How do you reload systemd manager configuration?
Use the `systemctl daemon-reload` command:

```
sudo systemctl daemon-reload
```

#### What is the journalctl command used for?
`journalctl` is used to query and display logs from the systemd journal.

#### How do you display the latest system logs using journalctl?
Use the `journalctl -e` command:

```
journalctl -e
```

#### How do you display kernel logs using journalctl?
Use the `journalctl -k` command:

```
journalctl -k
```

#### How do you display logs for a specific service using journalctl?
Use the `journalctl -u` command:

```
journalctl -u service_name
```

#### How do you set up a swap file in Linux?
Use the `dd`, `mkswap`, and `swapon` commands:

```
sudo dd if=/dev/zero of=/swapfile bs=1M count=2048
sudo mkswap /swapfile
sudo swapon /swapfile
sudo chmod 600 /swapfile
```

#### How do you disable a swap file?
Use the `swapoff` command:

```
sudo swapoff /swapfile
```

#### How do you permanently enable a swap file?
Add the swap file entry to `/etc/fstab`:

```
/swapfile swap swap defaults 0 0
```

#### How do you check swap usage?
Use the `swapon -s` or `free -h` command:

```
swapon -s
```
or
```
free -h
```

#### What is the df command used for?
`df` displays the amount of disk space used and available on file systems.

#### What is the du command used for?
`du` estimates file space usage and displays the disk usage of files and directories.

#### How do you check the disk usage of a specific directory?
Use the `du -sh` command:

```
du -sh /path/to/directory
```

#### How do you create a symbolic link?
Use the `ln -s` command:

```
ln -s /path/to/target /path/to/link
```

#### How do you create a hard link?
Use the `ln` command:

```
ln /path/to/target /path/to/link
```

#### What is the difference between a symbolic link and a hard link?
A symbolic link points to a file or directory by name, whereas a hard link points directly to the inode of a file. Symbolic links can cross file system boundaries, while hard links cannot.

#### How do you view the contents of a directory?
Use the `ls` command:

```
ls /path/to/directory
```

#### How do you view hidden files in a directory?
Use the `ls -a` command:

```
ls -a /path/to/directory
```

#### How do you copy files?
Use the `cp` command:

```
cp source_file destination_file
```

#### How do you move or rename files?
Use the `mv` command:

```
mv source_file destination_file
```

#### How do you delete files?
Use the `rm` command:

```
rm filename
```

#### How do you delete directories and their contents?
Use the `rm -r` command:

```
rm -r directory_name
```

#### How do you change file permissions?
Use the `chmod` command:

```
chmod 755 filename
```

#### How do you change file ownership?
Use the `chown` command:

```
sudo chown user:group filename
```

#### How do you change the group ownership of a file?
Use the `chgrp` command:

```
sudo chgrp group filename
```

#### How do you find files by name?
Use the `find` command:

```
find /path/to/search -name "filename"
```

#### How do you search for files containing a specific string?
Use the `grep -r` command:

```
grep -r "search_string" /path/to/search
```

#### What is the locate command used for?
`locate` searches for files in a pre-built database, making it faster than `find`.

#### How do you update the locate database?
Use the `updatedb` command:

```
sudo updatedb
```

#### How do you view the manual page for a command?
Use the `man` command:

```
man command_name
```

#### How do you view the help information for a command?
Use the `--help` option:

```
command_name --help
```

#### How do you display the current environment variables?
Use the `env` command:

```
env
```

#### How do you set an environment variable?
Use the `export` command:

```
export VAR_NAME=value
```

#### How do you add a directory to the PATH variable?
Use the `export` command to modify PATH:

```
export PATH=$PATH:/path/to/directory
```

#### What is the alias command used for?
`alias` creates shortcuts for commands. For example:

```
alias ll='ls -l'
```

#### How do you remove an alias?
Use the `unalias` command:

```
unalias alias_name
```

#### What is the purpose of the /etc/profile file?
The `/etc/profile` file contains system-wide environment and startup programs for login shells.

#### What is the purpose of the .bashrc file?
The `.bashrc` file contains user-specific aliases and functions for non-login shells.

#### How do you reload the bashrc file after making changes?
Use the `source` command:

```
source ~/.bashrc
```

#### How do you check the syntax of a shell script without executing it?
Use the `bash -n` command:

```
bash -n script.sh
```

#### How do you debug a shell script?
Use the `bash -x` command to execute the script in debug mode:

```
bash -x script.sh
```

#### What is the diff command used for?
`diff` compares the contents of two files line by line and displays the differences.

#### How do you display the differences between two files?
Use the `diff` command:

```
diff file1 file2
```

#### What is the patch command used for?
`patch` applies changes to files based on a diff file.
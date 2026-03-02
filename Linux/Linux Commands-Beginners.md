# Linux Complete Cheat Sheet — Beginner

---

## 1. Navigation

### 1.1 Moving Around

| Command | Description | Example |
|--------|-------------|---------|
| `pwd` | Print current working directory | `pwd` |
| `ls` | List files and folders | `ls` |
| `ls -l` | List with details (permissions, size, date) | `ls -l` |
| `ls -a` | List including hidden files | `ls -a` |
| `ls -la` | List all files with details | `ls -la` |
| `cd <dir>` | Change directory | `cd Documents` |
| `cd ..` | Go one level up | `cd ..` |
| `cd ~` | Go to home directory | `cd ~` |
| `cd /` | Go to root directory | `cd /` |
| `cd -` | Go to previous directory | `cd -` |

### 1.2 Exploring Directories

| Command | Description | Example |
|--------|-------------|---------|
| `tree` | Display directory structure as a tree | `tree` |
| `tree -L 2` | Tree up to 2 levels deep | `tree -L 2` |
| `du -sh <dir>` | Show size of a directory | `du -sh Downloads` |
| `df -h` | Show disk space usage | `df -h` |

---

## 2. File & Directory Management

### 2.1 Creating

| Command | Description | Example |
|--------|-------------|---------|
| `touch <file>` | Create an empty file | `touch notes.txt` |
| `mkdir <dir>` | Create a new directory | `mkdir Projects` |
| `mkdir -p <path>` | Create nested directories | `mkdir -p a/b/c` |

### 2.2 Copying & Moving

| Command | Description | Example |
|--------|-------------|---------|
| `cp <src> <dest>` | Copy a file | `cp file.txt backup.txt` |
| `cp -r <src> <dest>` | Copy a directory recursively | `cp -r folder1 folder2` |
| `mv <src> <dest>` | Move or rename a file/directory | `mv old.txt new.txt` |

### 2.3 Deleting

| Command | Description | Example |
|--------|-------------|---------|
| `rm <file>` | Delete a file | `rm notes.txt` |
| `rm -r <dir>` | Delete a directory recursively | `rm -r myfolder` |
| `rm -rf <dir>` | Force delete without prompt (use carefully!) | `rm -rf temp` |
| `rmdir <dir>` | Delete an empty directory | `rmdir emptydir` |

### 2.4 Viewing Files

| Command | Description | Example |
|--------|-------------|---------|
| `cat <file>` | Print entire file content | `cat notes.txt` |
| `less <file>` | View file page by page | `less notes.txt` |
| `head <file>` | Show first 10 lines | `head notes.txt` |
| `head -n 5 <file>` | Show first 5 lines | `head -n 5 notes.txt` |
| `tail <file>` | Show last 10 lines | `tail notes.txt` |
| `tail -n 5 <file>` | Show last 5 lines | `tail -n 5 notes.txt` |
| `tail -f <file>` | Follow file in real time (logs) | `tail -f syslog` |

---

## 3. File Permissions

### 3.1 Understanding Permissions

| Symbol | Meaning |
|--------|---------|
| `r` | Read |
| `w` | Write |
| `x` | Execute |
| `-` | No permission |
| `d` | Directory |

### 3.2 Changing Permissions

| Command | Description | Example |
|--------|-------------|---------|
| `chmod +x <file>` | Add execute permission | `chmod +x script.sh` |
| `chmod 755 <file>` | rwx for owner, rx for others | `chmod 755 script.sh` |
| `chmod 644 <file>` | rw for owner, r for others | `chmod 644 file.txt` |
| `chown user <file>` | Change file owner | `chown john file.txt` |
| `chown user:group <file>` | Change owner and group | `chown john:dev file.txt` |
| `ls -l` | View permissions of files | `ls -l` |

### 3.3 Permission Numbers Reference

| Number | Permission |
|--------|------------|
| `7` | rwx (read + write + execute) |
| `6` | rw- (read + write) |
| `5` | r-x (read + execute) |
| `4` | r-- (read only) |
| `0` | --- (no permission) |

---

## 4. Searching & Finding

### 4.1 Finding Files

| Command | Description | Example |
|--------|-------------|---------|
| `find . -name <file>` | Find file by name in current dir | `find . -name notes.txt` |
| `find / -name <file>` | Find file system-wide | `find / -name passwd` |
| `find . -type f` | Find only files | `find . -type f` |
| `find . -type d` | Find only directories | `find . -type d` |
| `find . -name "*.txt"` | Find all .txt files | `find . -name "*.txt"` |

### 4.2 Searching Inside Files

| Command | Description | Example |
|--------|-------------|---------|
| `grep <pattern> <file>` | Search for a pattern in a file | `grep "error" log.txt` |
| `grep -i <pattern> <file>` | Case-insensitive search | `grep -i "error" log.txt` |
| `grep -r <pattern> <dir>` | Search recursively in directory | `grep -r "TODO" ./src` |
| `grep -n <pattern> <file>` | Show line numbers with results | `grep -n "error" log.txt` |
| `grep -v <pattern> <file>` | Show lines that do NOT match | `grep -v "debug" log.txt` |

---

## 5. Text Editing

### 5.1 Nano (Beginner Friendly)

| Command | Description |
|--------|-------------|
| `nano <file>` | Open file in nano editor |
| `Ctrl + O` | Save the file |
| `Ctrl + X` | Exit nano |
| `Ctrl + K` | Cut a line |
| `Ctrl + U` | Paste a line |
| `Ctrl + W` | Search inside file |

### 5.2 Redirects & Writing to Files

| Command | Description | Example |
|--------|-------------|---------|
| `echo "text" > file` | Write text to file (overwrites) | `echo "hello" > hi.txt` |
| `echo "text" >> file` | Append text to file | `echo "world" >> hi.txt` |
| `cat file1 > file2` | Copy content of file1 to file2 | `cat a.txt > b.txt` |

---

## 6. Process Management

### 6.1 Viewing Processes

| Command | Description | Example |
|--------|-------------|---------|
| `ps` | Show current user processes | `ps` |
| `ps aux` | Show all running processes | `ps aux` |
| `top` | Live view of system processes | `top` |
| `htop` | Interactive process viewer (if installed) | `htop` |

### 6.2 Controlling Processes

| Command | Description | Example |
|--------|-------------|---------|
| `kill <PID>` | Kill a process by PID | `kill 1234` |
| `kill -9 <PID>` | Force kill a process | `kill -9 1234` |
| `pkill <name>` | Kill process by name | `pkill firefox` |
| `Ctrl + C` | Stop a running command | — |
| `Ctrl + Z` | Pause a running command | — |
| `bg` | Resume paused job in background | `bg` |
| `fg` | Bring background job to foreground | `fg` |
| `jobs` | List background jobs | `jobs` |

---

## 7. Networking

### 7.1 Basic Network Commands

| Command | Description | Example |
|--------|-------------|---------|
| `ping <host>` | Check connectivity to a host | `ping google.com` |
| `ifconfig` | Show network interfaces (older) | `ifconfig` |
| `ip a` | Show IP addresses (modern) | `ip a` |
| `ip r` | Show routing table | `ip r` |
| `curl <url>` | Fetch content from a URL | `curl https://example.com` |
| `wget <url>` | Download a file from a URL | `wget https://example.com/file.zip` |
| `netstat -tuln` | Show open ports and connections | `netstat -tuln` |
| `ss -tuln` | Modern replacement for netstat | `ss -tuln` |
| `hostname` | Show system hostname | `hostname` |
| `nslookup <domain>` | DNS lookup for a domain | `nslookup google.com` |

---

## 8. Package Management

### 8.1 Debian / Ubuntu (apt)

| Command | Description | Example |
|--------|-------------|---------|
| `sudo apt update` | Update package list | `sudo apt update` |
| `sudo apt upgrade` | Upgrade all installed packages | `sudo apt upgrade` |
| `sudo apt install <pkg>` | Install a package | `sudo apt install curl` |
| `sudo apt remove <pkg>` | Remove a package | `sudo apt remove curl` |
| `sudo apt purge <pkg>` | Remove package + config files | `sudo apt purge curl` |
| `apt search <pkg>` | Search for a package | `apt search vim` |
| `apt list --installed` | List installed packages | `apt list --installed` |

### 8.2 Red Hat / CentOS (yum / dnf)

| Command | Description | Example |
|--------|-------------|---------|
| `sudo yum install <pkg>` | Install a package | `sudo yum install curl` |
| `sudo dnf install <pkg>` | Install (modern systems) | `sudo dnf install curl` |
| `sudo yum update` | Update all packages | `sudo yum update` |
| `sudo yum remove <pkg>` | Remove a package | `sudo yum remove curl` |

---

## 9. User Management

### 9.1 Users

| Command | Description | Example |
|--------|-------------|---------|
| `whoami` | Show current logged-in user | `whoami` |
| `who` | Show all logged-in users | `who` |
| `id` | Show user ID and group info | `id` |
| `sudo adduser <name>` | Create a new user | `sudo adduser john` |
| `sudo deluser <name>` | Delete a user | `sudo deluser john` |
| `passwd` | Change current user password | `passwd` |
| `su <user>` | Switch to another user | `su john` |
| `sudo <command>` | Run command as superuser | `sudo apt update` |

### 9.2 Groups

| Command | Description | Example |
|--------|-------------|---------|
| `groups` | Show groups of current user | `groups` |
| `sudo groupadd <group>` | Create a new group | `sudo groupadd devs` |
| `sudo usermod -aG <group> <user>` | Add user to a group | `sudo usermod -aG sudo john` |

---

## 10. System Information

| Command | Description | Example |
|--------|-------------|---------|
| `uname -a` | Show system/kernel info | `uname -a` |
| `hostname` | Show hostname | `hostname` |
| `uptime` | Show how long system has been running | `uptime` |
| `date` | Show current date and time | `date` |
| `cal` | Show calendar | `cal` |
| `free -h` | Show RAM usage | `free -h` |
| `df -h` | Show disk usage | `df -h` |
| `lscpu` | Show CPU info | `lscpu` |
| `lsblk` | Show block devices (disks) | `lsblk` |
| `env` | Show environment variables | `env` |
| `echo $PATH` | Show PATH variable | `echo $PATH` |

---

## 11. Compression & Archiving

| Command | Description | Example |
|--------|-------------|---------|
| `tar -cvf archive.tar <dir>` | Create a tar archive | `tar -cvf backup.tar myfolder` |
| `tar -xvf archive.tar` | Extract a tar archive | `tar -xvf backup.tar` |
| `tar -czvf archive.tar.gz <dir>` | Create compressed .tar.gz | `tar -czvf backup.tar.gz myfolder` |
| `tar -xzvf archive.tar.gz` | Extract .tar.gz | `tar -xzvf backup.tar.gz` |
| `zip archive.zip <files>` | Create a zip file | `zip notes.zip *.txt` |
| `unzip archive.zip` | Extract a zip file | `unzip notes.zip` |
| `gzip <file>` | Compress a file with gzip | `gzip log.txt` |
| `gunzip <file>.gz` | Decompress a gzip file | `gunzip log.txt.gz` |

---

## 12. Shortcuts & Productivity

### 12.1 Terminal Shortcuts

| Shortcut | Description |
|----------|-------------|
| `Ctrl + C` | Kill current process |
| `Ctrl + Z` | Pause current process |
| `Ctrl + D` | Logout / close terminal |
| `Ctrl + L` | Clear the screen |
| `Ctrl + A` | Move cursor to start of line |
| `Ctrl + E` | Move cursor to end of line |
| `Ctrl + R` | Search command history |
| `↑ / ↓` | Navigate command history |
| `Tab` | Auto-complete command or filename |
| `!!` | Repeat last command |

### 12.2 Useful Misc Commands

| Command | Description | Example |
|--------|-------------|---------|
| `clear` | Clear terminal screen | `clear` |
| `history` | Show command history | `history` |
| `man <command>` | Open manual for a command | `man ls` |
| `whatis <command>` | One-line description of a command | `whatis grep` |
| `alias` | Show all aliases | `alias` |
| `alias ll='ls -la'` | Create a custom shortcut | `alias ll='ls -la'` |
| `exit` | Exit the terminal session | `exit` |
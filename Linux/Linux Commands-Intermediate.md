# Linux Complete Cheat Sheet — Intermediate

---

## 1. File System Deep Dive

### 1.1 Advanced File Operations

| Command | Description | Example |
|--------|-------------|---------|
| `ln -s <src> <link>` | Create a symbolic (soft) link | `ln -s /var/log logs` |
| `ln <src> <link>` | Create a hard link | `ln file.txt hardlink.txt` |
| `readlink <link>` | Show where a symlink points | `readlink logs` |
| `stat <file>` | Detailed file metadata | `stat file.txt` |
| `file <file>` | Detect file type | `file archive.tar.gz` |
| `wc -l <file>` | Count lines in a file | `wc -l notes.txt` |
| `wc -w <file>` | Count words in a file | `wc -w notes.txt` |
| `diff <f1> <f2>` | Compare two files line by line | `diff a.txt b.txt` |
| `sort <file>` | Sort file contents alphabetically | `sort names.txt` |
| `sort -n <file>` | Sort numerically | `sort -n scores.txt` |
| `sort -r <file>` | Sort in reverse | `sort -r names.txt` |
| `uniq <file>` | Remove duplicate lines | `uniq names.txt` |
| `cut -d: -f1 <file>` | Cut specific field from file | `cut -d: -f1 /etc/passwd` |
| `tr 'a-z' 'A-Z'` | Translate characters (lowercase to upper) | `echo "hello" \| tr 'a-z' 'A-Z'` |
| `tee <file>` | Read from stdin, write to file and stdout | `ls \| tee output.txt` |

### 1.2 File Descriptor & Redirection

| Operator | Description | Example |
|----------|-------------|---------|
| `>` | Redirect stdout (overwrite) | `ls > out.txt` |
| `>>` | Redirect stdout (append) | `ls >> out.txt` |
| `<` | Redirect stdin | `sort < names.txt` |
| `2>` | Redirect stderr | `cmd 2> err.txt` |
| `2>>` | Append stderr | `cmd 2>> err.txt` |
| `&>` | Redirect both stdout and stderr | `cmd &> all.txt` |
| `2>&1` | Merge stderr into stdout | `cmd > out.txt 2>&1` |
| `/dev/null` | Discard output entirely | `cmd > /dev/null 2>&1` |

---

## 2. Piping & Command Chaining

### 2.1 Pipes

| Command | Description | Example |
|--------|-------------|---------|
| `cmd1 \| cmd2` | Pipe output of cmd1 into cmd2 | `ls \| grep ".txt"` |
| `cmd1 \| cmd2 \| cmd3` | Chain multiple pipes | `cat log.txt \| grep "error" \| wc -l` |
| `xargs` | Build commands from stdin input | `find . -name "*.txt" \| xargs rm` |

### 2.2 Command Chaining Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `;` | Run commands sequentially | `cd /tmp; ls` |
| `&&` | Run next only if previous succeeded | `mkdir test && cd test` |
| `\|\|` | Run next only if previous failed | `cd /x \|\| echo "failed"` |
| `&` | Run command in background | `ping google.com &` |

---

## 3. Advanced Text Processing

### 3.1 sed — Stream Editor

| Command | Description | Example |
|--------|-------------|---------|
| `sed 's/old/new/' <file>` | Replace first match per line | `sed 's/foo/bar/' file.txt` |
| `sed 's/old/new/g' <file>` | Replace all matches per line | `sed 's/foo/bar/g' file.txt` |
| `sed -i 's/old/new/g' <file>` | Edit file in place | `sed -i 's/foo/bar/g' file.txt` |
| `sed -n '2,5p' <file>` | Print lines 2 to 5 | `sed -n '2,5p' file.txt` |
| `sed '/pattern/d' <file>` | Delete lines matching pattern | `sed '/debug/d' log.txt` |

### 3.2 awk — Pattern Scanning

| Command | Description | Example |
|--------|-------------|---------|
| `awk '{print $1}' <file>` | Print first column | `awk '{print $1}' data.txt` |
| `awk '{print $1, $3}' <file>` | Print columns 1 and 3 | `awk '{print $1, $3}' data.txt` |
| `awk -F: '{print $1}' <file>` | Use custom delimiter | `awk -F: '{print $1}' /etc/passwd` |
| `awk 'NR==3' <file>` | Print 3rd line | `awk 'NR==3' file.txt` |
| `awk '/pattern/' <file>` | Print lines matching pattern | `awk '/error/' log.txt` |
| `awk '{sum+=$1} END {print sum}' <file>` | Sum a column | `awk '{sum+=$1} END {print sum}' nums.txt` |

### 3.3 grep Advanced

| Command | Description | Example |
|--------|-------------|---------|
| `grep -E <pattern> <file>` | Extended regex | `grep -E "err\|warn" log.txt` |
| `grep -c <pattern> <file>` | Count matching lines | `grep -c "error" log.txt` |
| `grep -l <pattern> <dir>` | List files with matches | `grep -rl "TODO" ./src` |
| `grep -A 3 <pattern> <file>` | Show 3 lines after match | `grep -A 3 "error" log.txt` |
| `grep -B 3 <pattern> <file>` | Show 3 lines before match | `grep -B 3 "error" log.txt` |
| `grep -C 3 <pattern> <file>` | Show 3 lines around match | `grep -C 3 "error" log.txt` |

---

## 4. Process & Job Management

### 4.1 Advanced Process Control

| Command | Description | Example |
|--------|-------------|---------|
| `ps aux --sort=-%mem` | Sort processes by memory | `ps aux --sort=-%mem` |
| `ps aux --sort=-%cpu` | Sort processes by CPU | `ps aux --sort=-%cpu` |
| `pgrep <name>` | Get PID of process by name | `pgrep nginx` |
| `pstree` | Show process tree | `pstree` |
| `nice -n 10 <cmd>` | Run command with lower priority | `nice -n 10 backup.sh` |
| `renice -n 5 -p <PID>` | Change priority of running process | `renice -n 5 -p 1234` |
| `nohup <cmd> &` | Run command immune to hangups | `nohup ./script.sh &` |
| `disown` | Detach background job from terminal | `disown %1` |
| `wait` | Wait for background jobs to finish | `wait` |

### 4.2 Signals

| Signal | Number | Description |
|--------|--------|-------------|
| `SIGTERM` | 15 | Graceful termination (default kill) |
| `SIGKILL` | 9 | Force kill — cannot be caught |
| `SIGHUP` | 1 | Reload config / hangup |
| `SIGINT` | 2 | Interrupt (Ctrl + C) |
| `SIGSTOP` | 19 | Pause process (Ctrl + Z) |
| `SIGCONT` | 18 | Resume paused process |

---

## 5. Shell Scripting Basics

### 5.1 Script Structure

| Concept | Syntax | Example |
|---------|--------|---------|
| Shebang | `#!/bin/bash` | First line of every script |
| Make executable | `chmod +x script.sh` | `chmod +x deploy.sh` |
| Run script | `./script.sh` | `./deploy.sh` |
| Comments | `# comment` | `# This installs packages` |

### 5.2 Variables

| Concept | Syntax | Example |
|---------|--------|---------|
| Define variable | `VAR=value` | `NAME="Linux"` |
| Use variable | `$VAR` | `echo $NAME` |
| Command substitution | `VAR=$(cmd)` | `DATE=$(date)` |
| Read user input | `read VAR` | `read USERNAME` |
| Env variable | `export VAR=value` | `export PATH=$PATH:/usr/local/bin` |

### 5.3 Conditionals

| Concept | Syntax |
|---------|--------|
| if / else | `if [ condition ]; then ... else ... fi` |
| Check file exists | `if [ -f file.txt ]; then` |
| Check dir exists | `if [ -d mydir ]; then` |
| String equals | `if [ "$VAR" == "hello" ]; then` |
| Number comparison | `if [ $NUM -gt 10 ]; then` |

### 5.4 Comparison Operators

| Operator | Meaning |
|----------|---------|
| `-eq` | Equal to |
| `-ne` | Not equal to |
| `-gt` | Greater than |
| `-lt` | Less than |
| `-ge` | Greater than or equal |
| `-le` | Less than or equal |
| `-f` | File exists |
| `-d` | Directory exists |
| `-z` | String is empty |
| `-n` | String is not empty |

### 5.5 Loops

| Concept | Syntax |
|---------|--------|
| for loop | `for i in 1 2 3; do echo $i; done` |
| for range | `for i in {1..5}; do echo $i; done` |
| while loop | `while [ $i -lt 5 ]; do ... done` |
| loop over files | `for f in *.txt; do echo $f; done` |
| break | `break` |
| continue | `continue` |

### 5.6 Functions

| Concept | Syntax |
|---------|--------|
| Define function | `myfunc() { echo "hello"; }` |
| Call function | `myfunc` |
| Function with args | `myfunc() { echo $1; }` |
| Return value | `return 0` |

---

## 6. Networking — Intermediate

### 6.1 SSH

| Command | Description | Example |
|--------|-------------|---------|
| `ssh user@host` | Connect to remote server | `ssh john@192.168.1.10` |
| `ssh -p 2222 user@host` | Connect on custom port | `ssh -p 2222 john@server.com` |
| `ssh-keygen` | Generate SSH key pair | `ssh-keygen -t rsa` |
| `ssh-copy-id user@host` | Copy public key to server | `ssh-copy-id john@server.com` |
| `scp <file> user@host:<path>` | Securely copy file to remote | `scp file.txt john@server.com:/home/john` |
| `scp user@host:<file> .` | Copy file from remote to local | `scp john@server.com:/log.txt .` |
| `rsync -avz <src> user@host:<dest>` | Sync files to remote | `rsync -avz ./src john@server.com:/app` |

### 6.2 Ports & Connections

| Command | Description | Example |
|--------|-------------|---------|
| `ss -tuln` | Show listening ports | `ss -tuln` |
| `ss -tp` | Show connections with process names | `ss -tp` |
| `lsof -i :<port>` | Show process using a port | `lsof -i :8080` |
| `curl -I <url>` | Fetch HTTP headers only | `curl -I https://google.com` |
| `curl -X POST -d 'data' <url>` | Send POST request | `curl -X POST -d 'name=john' http://api.com` |
| `traceroute <host>` | Trace route to a host | `traceroute google.com` |
| `nmap <host>` | Scan open ports on a host | `nmap 192.168.1.1` |

---

## 7. Disk & Storage Management

| Command | Description | Example |
|--------|-------------|---------|
| `lsblk` | List all block devices | `lsblk` |
| `fdisk -l` | List disk partitions | `sudo fdisk -l` |
| `mount <dev> <dir>` | Mount a device | `sudo mount /dev/sdb1 /mnt/usb` |
| `umount <dir>` | Unmount a device | `sudo umount /mnt/usb` |
| `df -h` | Show disk usage (human readable) | `df -h` |
| `du -sh *` | Show size of each item in current dir | `du -sh *` |
| `du -sh * \| sort -h` | Sort items by size | `du -sh * \| sort -h` |
| `ncdu` | Interactive disk usage viewer | `ncdu` |

---

## 8. System Monitoring

| Command | Description | Example |
|--------|-------------|---------|
| `top` | Live process and CPU monitor | `top` |
| `htop` | Enhanced interactive monitor | `htop` |
| `vmstat 1` | CPU, memory, I/O stats every 1s | `vmstat 1` |
| `iostat` | CPU and disk I/O statistics | `iostat` |
| `sar -u 1 5` | CPU usage 5 times every 1s | `sar -u 1 5` |
| `watch -n 2 <cmd>` | Run command every 2 seconds | `watch -n 2 df -h` |
| `dmesg` | Kernel ring buffer / hardware logs | `dmesg \| tail` |
| `journalctl -xe` | View systemd logs | `journalctl -xe` |
| `journalctl -u nginx` | Logs for a specific service | `journalctl -u nginx` |

---

## 9. Service Management (systemd)

| Command | Description | Example |
|--------|-------------|---------|
| `systemctl start <svc>` | Start a service | `sudo systemctl start nginx` |
| `systemctl stop <svc>` | Stop a service | `sudo systemctl stop nginx` |
| `systemctl restart <svc>` | Restart a service | `sudo systemctl restart nginx` |
| `systemctl reload <svc>` | Reload config without restart | `sudo systemctl reload nginx` |
| `systemctl status <svc>` | Check service status | `systemctl status nginx` |
| `systemctl enable <svc>` | Enable service on boot | `sudo systemctl enable nginx` |
| `systemctl disable <svc>` | Disable service on boot | `sudo systemctl disable nginx` |
| `systemctl list-units` | List all active units | `systemctl list-units` |
| `systemctl daemon-reload` | Reload systemd config | `sudo systemctl daemon-reload` |

---

## 10. Scheduling Tasks (cron)

### 10.1 Cron Syntax

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week (0=Sun, 6=Sat)
│ │ │ └──── Month (1–12)
│ │ └────── Day of month (1–31)
│ └──────── Hour (0–23)
└────────── Minute (0–59)
```

### 10.2 Cron Commands

| Command | Description |
|--------|-------------|
| `crontab -e` | Edit current user's cron jobs |
| `crontab -l` | List current user's cron jobs |
| `crontab -r` | Remove all cron jobs |
| `sudo crontab -e` | Edit root cron jobs |

### 10.3 Cron Examples

| Schedule | Cron Expression |
|----------|----------------|
| Every minute | `* * * * *` |
| Every hour | `0 * * * *` |
| Every day at midnight | `0 0 * * *` |
| Every Monday at 9am | `0 9 * * 1` |
| Every 1st of month | `0 0 1 * *` |
| Every 5 minutes | `*/5 * * * *` |

---

## 11. Environment & Shell Configuration

| Command | Description | Example |
|--------|-------------|---------|
| `echo $VAR` | Print an environment variable | `echo $HOME` |
| `export VAR=val` | Set environment variable | `export EDITOR=vim` |
| `unset VAR` | Remove an environment variable | `unset EDITOR` |
| `env` | List all environment variables | `env` |
| `printenv <VAR>` | Print specific variable | `printenv PATH` |
| `source ~/.bashrc` | Reload shell config | `source ~/.bashrc` |
| `~/.bashrc` | User shell config file (bash) | — |
| `~/.bash_profile` | Login shell config file | — |
| `~/.profile` | Generic login profile | — |
| `alias ll='ls -la'` | Create command shortcut | `alias gs='git status'` |
| `unalias ll` | Remove an alias | `unalias gs` |
| `type <cmd>` | Show what a command resolves to | `type ls` |
| `which <cmd>` | Show full path of a command | `which python3` |
| `whereis <cmd>` | Show binary, source, man page | `whereis nginx` |

---

## 12. Compression & Transfer

| Command | Description | Example |
|--------|-------------|---------|
| `tar -czvf out.tar.gz <dir>` | Compress directory to .tar.gz | `tar -czvf backup.tar.gz /var/www` |
| `tar -xzvf file.tar.gz -C <dir>` | Extract to specific directory | `tar -xzvf backup.tar.gz -C /tmp` |
| `tar -tzvf file.tar.gz` | List contents without extracting | `tar -tzvf backup.tar.gz` |
| `zip -r out.zip <dir>` | Zip a directory recursively | `zip -r site.zip ./public` |
| `rsync -avz --progress <src> <dst>` | Sync with progress output | `rsync -avz --progress ./app server:/var/www` |
| `rsync --delete <src> <dst>` | Sync and delete removed files | `rsync --delete ./src server:/app` |

---

## 13. Permissions — Advanced

### 13.1 Special Permissions

| Permission | Octal | Description |
|------------|-------|-------------|
| `setuid` | `4xxx` | Run file as file owner | 
| `setgid` | `2xxx` | Run file as group owner |
| `sticky bit` | `1xxx` | Only owner can delete file in dir |

| Command | Description | Example |
|--------|-------------|---------|
| `chmod u+s <file>` | Set setuid bit | `chmod u+s /usr/bin/passwd` |
| `chmod g+s <dir>` | Set setgid on directory | `chmod g+s /shared` |
| `chmod +t <dir>` | Set sticky bit | `chmod +t /tmp` |
| `umask` | Show default permission mask | `umask` |
| `umask 022` | Set default permission mask | `umask 022` |

### 13.2 ACL (Access Control Lists)

| Command | Description | Example |
|--------|-------------|---------|
| `getfacl <file>` | View ACL of a file | `getfacl file.txt` |
| `setfacl -m u:john:rw <file>` | Give user specific permissions | `setfacl -m u:john:rw file.txt` |
| `setfacl -x u:john <file>` | Remove ACL for a user | `setfacl -x u:john file.txt` |
# Linux Commands Cheat-Sheet

**This cheat sheet covers**:
* System information commands
* Hardware & performance monitoring
* File & directory management 
* Networking & SSH
* Process management
* Disk usage & archives
* Package installation
* Permission & Search

---

## System Information

| Command          | Descriptoon                                      |
|:-----------------|:-------------------------------------------------|
| `uname -a`       | Display Linux system information                 |
| `uname -f`       | Display kernel release information               |
| `lsb_release -a` | Show which version of ubuntu installed           |
| `uptime`         | Show hoe long the system has been running + load |
| `hostname`       | Show system host name                            |
| `hostname -I`    | Display the IP address of the host               |
| `last reboot`    | Show system reboot history                       |
| `date`           | Show the current date and time                   |
| `cal`            | Show this month's calander                       |
| `w`              | Display who is online                            |
| `whoami`         | Who you are logged in as                         |


## Hardware Information

| Command               | Description                                                                |
|:----------------------|:---------------------------------------------------------------------------|
| `cat /proc/cpuinfo`   | Disply CPU information                                                     |
| `cat /proc/meminfo`   | Display memory information                                                 |
| `free -h`             | Display free and used memory (-h for human readable, -m for MB, -g for GB) |
| `lscpi -tv`           | Display PCI devices                                                        |
| `lsusb -tv`           | Display USB devices                                                        |
| `dmidecode`           | Display DMI/SMBIOS (hardware info) from the BIOS                           |
| `hdparm -i /dev/sda`  | Show info about disk sda                                                   |
| `hdparm -tT /dev/sda` | Perform a read speed test on disk sda                                      |


## Performance Monitoring and Statistics

| Command                   | Description                                                                    |
|:--------------------------|:-------------------------------------------------------------------------------|
| `top`                     | Display and manage the top processes                                           |
| `mpstat 1`                | Display processor related statistics                                           |
| `vmstat 1`                | Display virtual memory statistics                                              |
| `iostat 1`                | Display I/O statistics                                                         |
| `tcpdump -i eth0`         | Capture and display all packets on interface eth0                              |
| `tcpdump -i eth0 port 80` | Monitor all traffic on port 80 (HTTP)                                          |
| `lsof`                    | List all of the open files on the system                                       |
| `lsof -u user`            | List files opened by the user                                                  |
| `free -h`                 | Display free and used memory (-h for Human Readable, -m for MB, and -g for GB) |
| `watch df -h`             | Execute **df -h**, showing periodic updates                                    |

## User Inormation and Management

| Command                             | Description                                                                                              |
|:------------------------------------|:---------------------------------------------------------------------------------------------------------|
| `id`                                | Display the user and group ids of your current user                                                      |
| `last`                              | Display the latest users who logged onto the system                                                      |
| `who`                               | Show who is logged into the system                                                                       |
| `w`                                 | Show who logged is logged in and what they're doing                                                      |
| `groupadd test`                     | Create a group named **test**                                                                            |
| `useradd -c "John Smith" -m john`   | Create an account named **john**, with a comment of **John Smith** and create the user's home directory. |
| `userdel john`                      | Delete the john account                                                                                  |
| `usermod -aG sales john`            | Add the john account to the sales group                                                                  |


## File and Directory Commands

| Command                              | Description                                                                                                                                                                         |
|:-------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ls -al`                             | List all files in a long listing (detailed) format                                                                                                                                  |
| `pwd`                                | Display the present working directory                                                                                                                                               |
| `mkdir directory`                    | Create a directory                                                                                                                                                                  |
| `rm file`                            | Remove (delete) file                                                                                                                                                                |
| `rm -r directory`                    | Remove the directory and its contents recursively                                                                                                                                   |
| `rm -f file`                         | Force removal of file without prompting for confirmation                                                                                                                            |
| `rm -rf directory`                   | Forcefully remove directory recursively                                                                                                                                             |
| `rmdir`                              | Delete a file or files                                                                                                                                                              |
| `cp file1 file2`                     | Copy file1 to file2                                                                                                                                                                 |
| `cp -r source_directory destination` | Copy source_directory recursively to destination. If destination exists, copy source_directory into destination, otherwise create destination with the contents of source_directory |
| `mv file1 file2`                     | Rename or move file1 to file2. If file2 is an existing directory, move file1 into directory file2                                                                                   |
| `ln -s /path/to/file linkname`       | Create symbolic link to linkname                                                                                                                                                    |
| `touch file`                         | Create an empty file or update the access and modification times of file                                                                                                            |
| `cat file`                           | View the contents of file                                                                                                                                                           |
| `less file`                          | Browse through a text file                                                                                                                                                          |
| `head file`                          | Display the first 10 lines of file                                                                                                                                                  |
| `tail file`                          | Display the last 10 lines of file                                                                                                                                                   |
| `tail -f file`                       | Display the last 10 lines of file and "follow" the file as it grows                                                                                                                 |
| `lpr`                                | Spool file for line printing                                                                                                                                                        |
| `chgrp`                              | Change file group                                                                                                                                                                   |
| `more, page`                         | Display file data at your terminal                                                                                                                                                  |
| `file`                               | Determine file type                                                                                                                                                                 |
| `vi`                                 | GNOME text editor                                                                                                                                                                   |
| `gedit`                              | Standard text editor                                                                                                                                                                |

##  Manipulating Data

| Command            | Description                                            |
|:-------------------|:-------------------------------------------------------|
| `awk`              | Pattern scanning and processing language               |
| `perl`             | Data manipulation language                             |
| `cmp`              | Compare the contents of two files                      |
| `paste`            | Merge file data                                        |
| `sed`              | Stream text editor                                     |
| `cut`              | Cut out selected fields of each line of a file         |
| `sort`             | Sort file data                                         |
| `diff`             | Differential file comparator                           |
| `split`            | Split file into smaller files                          |
| `expand, unexpand` | Expand tabs to spaces, and vice versa                  |
| `tr`               | Translate characters                                   |
| `uniq`             | Report repeated lines in a file                        |
| `join`             | Join files on some common field                        |
| `look`             | Find lines in sorted data                              |
| `gzip`             | Compress files                                         |
| `zmore`            | File perusal filter for crt viewing of compressed text |
| `uncompress`       | Uncompress files                                       |
| `zcat`             | Cat a compressed file                                  |
| `gunzip`           | Uncompress gzipped files                               |
| `zcmp, zdiff`      | Compare compressed files                               |


## Process Management

| Command                      | Description                                               |
|:-----------------------------|:----------------------------------------------------------|
| `ps`                         | Display your currently running processes                  |
| `ps -ef`                     | Display all the currently running processes on the system |
| `ps -ef \| grep processname` | Display process information for processname               |
| `top`                        | Display and manage the top processes                      |
| `htop`                       | Interactive process viewer (top alternative)              |
| `kill pid`                   | Kill process with process ID of pid                       |
| `killall processname`        | Kill all processes named processname                      |
| `program &`                  | Start program in the background                           |
| `bg`                         | Display stopped or background jobs                        |
| `fg`                         | Brings the most recent background job to foreground       |
| `fg n`                       | Brings job n to the foreground                            |


## File Permissions

| Permission (U G W) | Example              |
|:-------------------|:---------------------|
| `rwx rwx rwx`      | `chmod 777 filename` |
| `rwx rwx r-x`      | `chmod 775 filename` |
| `rwx r-x r-x`      | `chmod 755 filename` |
| `rw- rw- r--`      | `chmod 664 filename` |
| `rw- r-- r--`      | `chmod 644 filename` |

> **File type:** `-` → regular file, `d` → directory
>
> **Permissions:** `r` = Read, `w` = Write, `x` = Execute
>
> **Groups:** `u` = User, `g` = Group, `o` = Other, `a` = All

## Networking

| Command                       | Description                                                    |
|:------------------------------|:---------------------------------------------------------------|
| `ifconfig -a`                 | Display all network interfaces and ip address                  |
| `ifconfig eth0`               | Display eth0 address and details                               |
| `ethtool eth0`                | Query or control network driver and hardware settings          |
| `ping host`                   | Send ICMP echo request to host                                 |
| `whois domain`                | Display whois information for domain                           |
| `dig domain`                  | Display DNS information for domain                             |
| `dig -x IP_ADDRESS`           | Reverse lookup of IP_ADDRESS                                   |
| `host domain`                 | Display DNS ip address for domain                              |
| `hostname -i`                 | Display the network address of the host name                   |
| `hostname -I`                 | Display all local ip addresses                                 |
| `wget http://domain.com/file` | Download http://domain.com/file                                |
| `netstat -nutlp`              | Display listening tcp and udp ports and corresponding programs |
| `ftp`                         | File transfer program                                          |
| `tftp`                        | Trivial file transfer program                                  |
| `sftp`                        | Secure shell file transfer program                             |
| `rcp`                         | Remote file copy                                               |
| `scp`                         | Secure shell remote file copy                                  |
| `wget`                        | Non-interactive network downloader                             |
| `telnet`                      | Make terminal connection to another host                       |
| `ssh`                         | Secure shell terminal or command connection                    |
| `rlogin`                      | Remote login to a Linux host                                   |
| `rsh`                         | Remote shell                                                   |
| `curl`                        | Transfer data from a url                                       |


## Archives (Tar Files)

| Command                             | Description                                            |
|:------------------------------------|:-------------------------------------------------------|
| `tar cf archive.tar directory`      | Create tar named archive.tar containing directory      |
| `tar xf archive.tar`                | Extract the contents from archive.tar                  |
| `tar czf archive.tar.gz directory`  | Create a gzip compressed tar file named archive.tar.gz |
| `tar xzf archive.tar.gz`            | Extract a gzip compressed tar file                     |
| `tar cjf archive.tar.bz2 directory` | Create a tar file with bzip2 compression               |
| `tar xjf archive.tar.bz2`           | Extract a bzip2 compressed tar file                    |


## Installing Packages

| Command                                                                                     | Description                                               |
|:--------------------------------------------------------------------------------------------|:----------------------------------------------------------|
| `yum search keyword`                                                                        | Search for a package by keyword                           |
| `yum install package`                                                                       | Install package                                           |
| `yum info package`                                                                          | Display description and summary information about package |
| `rpm -i package.rpm`                                                                        | Install package from local file named package.rpm         |
| `yum remove package`                                                                        | Remove/uninstall package                                  |
| `tar zxvf sourcecode.tar.gz` then `cd sourcecode` → `./configure` → `make` → `make install` | Install software from source code                         |



## Search

| Command                           | Description                                       |
|:----------------------------------|:--------------------------------------------------|
| `grep pattern file`               | Search for pattern in file                        |
| `grep -r pattern directory`       | Search recursively for pattern in directory       |
| `locate name`                     | Find files and directories by name                |
| `find /home/john -name 'prefix*'` | Find files in /home/john that start with "prefix" |
| `find /home -size +100M`          | Find files larger than 100MB in /home             |



## SSH Logins

| Command                 | Description                            |
|:------------------------|:---------------------------------------|
| `ssh host`              | Connect to host as your local username |
| `ssh user@host`         | Connect to host as user                |
| `ssh -p port user@host` | Connect to host using port             |


## File Transfers

| Command                             | Description                                                                                |
|:------------------------------------|:-------------------------------------------------------------------------------------------|
| `scp server:/var/www/*.html /tmp`   | Copy *.html files from server to the local /tmp folder                                     |
| `scp -r server:/var/www /tmp`       | Copy all files and directories recursively from server to the current system's /tmp folder |
| `rsync -a /home /backups/`          | Synchronize /home to /backups/home                                                         |
| `rsync -avz /home server:/backups/` | Synchronize files/directories between local and remote system with compression enabled     |


## Disk Usage

| Command    | Description                                                               |
|:-----------|:--------------------------------------------------------------------------|
| `df -h`    | Show free and used space on mounted filesystems                           |
| `df -i`    | Show free and used inodes on mounted filesystems                          |
| `fdisk -l` | Display disks partitions sizes and types                                  |
| `du -ah`   | Display disk usage for all files and directories in human readable format |
| `du -sh`   | Display total disk usage off the current directory                        |


## Directory Navigation

| Command   | Description                                                              |
|:----------|:-------------------------------------------------------------------------|
| `cd ..`   | Go up one level of the directory tree (change into the parent directory) |
| `cd`      | Go to the $HOME directory                                                |
| `cd /etc` | Change to the /etc directory                                             |


## Programming

| Command  | Description                             |
|:---------|:----------------------------------------|
| `make`   | Maintain groups of programs             |
| `size`   | Print program's sizes                   |
| `nm`     | Print program's name list               |
| `strip`  | Remove symbol table and relocation bits |
| `bcpp`   | Make C++ beautifier                     |
| `gcc`    | GNU ANSI C Compiler                     |
| `ctrace` | C program debugger                      |
| `indent` | Indent and format C program source      |
| `cxref`  | Generate C program cross reference      |
| `g++`    | GNU C++ Compiler                        |


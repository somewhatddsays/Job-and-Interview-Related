# Introduction to Linux

---

## 1. What is Linux?

Linux is a free, open-source operating system kernel created by **Linus Torvalds** in 1991. It was inspired by UNIX — a powerful OS originally developed at Bell Labs in the 1970s.

Today, Linux powers almost everything around you — from web servers and supercomputers to Android phones, smart TVs, stock exchanges, and NASA spacecraft. It is the backbone of the modern internet.

> **Fun Fact:** Over 96% of the world's top 1 million web servers run on Linux.

---

## 2. Linux vs UNIX vs Windows vs macOS

| Feature | Linux | UNIX | Windows | macOS |
|---------|-------|------|---------|-------|
| Open Source | ✅ Yes | ❌ No | ❌ No | ❌ No |
| Free to Use | ✅ Yes | ❌ Mostly paid | ❌ No | ❌ No |
| Kernel Type | Monolithic | Monolithic | Hybrid | Hybrid (XNU) |
| Primary Use | Servers, Dev, Desktop | Servers, Workstations | Desktop, Enterprise | Desktop, Creative |
| Shell | bash, zsh, fish | sh, ksh, csh | PowerShell, CMD | zsh, bash |
| File System | ext4, XFS, Btrfs | UFS, ZFS | NTFS, FAT32 | APFS, HFS+ |
| Security Model | DAC + MAC (SELinux) | DAC | ACL-based | DAC + SIP |
| Package Manager | apt, yum, pacman | varies | winget, choco | Homebrew |

---

## 3. The Linux Kernel

The **kernel** is the core of Linux. It sits between the hardware and software, managing everything.

```
  ┌─────────────────────────────┐
  │        User Applications     │
  ├─────────────────────────────┤
  │         Shell / CLI          │
  ├─────────────────────────────┤
  │        System Libraries      │
  ├─────────────────────────────┤
  │         Linux Kernel         │  ← Core of the OS
  ├─────────────────────────────┤
  │           Hardware           │
  └─────────────────────────────┘
```

### What the Kernel Does

| Responsibility | Description |
|----------------|-------------|
| Process Management | Creates, schedules, and kills processes |
| Memory Management | Allocates and frees RAM for programs |
| Device Drivers | Talks to hardware (disk, keyboard, GPU) |
| File System | Reads/writes files on storage devices |
| Networking | Manages TCP/IP stack and network interfaces |
| Security | Enforces permissions and access control |

---

## 4. Linux Distributions (Distros)

A **distribution** is Linux kernel + package manager + default tools + desktop environment bundled together. There are 600+ distros — here are the most important ones.

### 4.1 Major Distro Families

```
Linux Kernel
├── Debian
│   ├── Ubuntu
│   │   ├── Linux Mint
│   │   ├── Pop!_OS
│   │   └── Elementary OS
│   └── Kali Linux
├── Red Hat
│   ├── RHEL (Red Hat Enterprise Linux)
│   ├── CentOS / AlmaLinux / Rocky Linux
│   └── Fedora
├── Arch Linux
│   ├── Manjaro
│   └── EndeavourOS
├── SUSE
│   ├── openSUSE
│   └── SLES (SUSE Linux Enterprise Server)
└── Independent
    ├── Alpine Linux
    ├── Gentoo
    └── NixOS
```

### 4.2 Which Distro for What?

| Use Case | Recommended Distro |
|----------|--------------------|
| Beginners / Desktop | Ubuntu, Linux Mint |
| Developers | Ubuntu, Fedora, Pop!_OS |
| Servers / Production | RHEL, Ubuntu Server, Debian |
| Cybersecurity / Pentesting | Kali Linux, Parrot OS |
| Lightweight / Old Hardware | Alpine, Lubuntu, Puppy Linux |
| Power Users / Customization | Arch Linux, Gentoo |
| Containers / Cloud | Alpine Linux, CoreOS |
| Privacy Focused | Tails, Whonix |

---

## 5. The Linux File System Hierarchy

Linux uses a single unified directory tree starting from `/` (root). Everything — files, devices, processes — is a file in Linux.

```
/
├── bin        → Essential user binaries (ls, cp, mv)
├── sbin       → System binaries (fdisk, ifconfig)
├── etc        → Configuration files
├── home       → User home directories (/home/john)
├── root       → Home directory for root user
├── var        → Variable data (logs, databases, mail)
├── tmp        → Temporary files (cleared on reboot)
├── usr        → User programs and libraries
│   ├── bin    → Non-essential user binaries
│   ├── lib    → Libraries for /usr/bin
│   └── local  → Locally compiled software
├── lib        → Essential shared libraries
├── dev        → Device files (disks, terminals)
├── proc       → Virtual filesystem for kernel/process info
├── sys        → Virtual filesystem for hardware/kernel params
├── mnt        → Temporary mount points
├── media      → Auto-mounted removable drives
├── boot       → Bootloader files (GRUB, kernel)
├── opt        → Optional third-party software
└── srv        → Data for services (web, FTP)
```

### Key Principle: Everything is a File

| Type | Example |
|------|---------|
| Regular file | `/etc/hosts` |
| Directory | `/home/john` |
| Symbolic link | `/usr/bin/python → python3` |
| Device file | `/dev/sda` (hard disk) |
| Socket | `/run/docker.sock` |
| Named pipe | `/tmp/mypipe` |
| Virtual file | `/proc/cpuinfo` |

---

## 6. The Shell

The **shell** is a command-line interpreter — it takes your commands and talks to the kernel to execute them.

### 6.1 Popular Shells

| Shell | Full Name | Description |
|-------|-----------|-------------|
| `bash` | Bourne Again Shell | Default on most Linux distros |
| `zsh` | Z Shell | Powerful, highly customizable, default on macOS |
| `fish` | Friendly Interactive Shell | Beginner-friendly, auto-suggestions |
| `sh` | Bourne Shell | Minimal, POSIX-compliant |
| `ksh` | KornShell | Common in enterprise UNIX |
| `dash` | Debian Almquist Shell | Fast, used for boot scripts |

### 6.2 Shell vs Terminal vs Console

| Term | What It Is |
|------|-----------|
| **Shell** | The program that interprets your commands (bash, zsh) |
| **Terminal** | The application window you type in (GNOME Terminal, iTerm2) |
| **Console** | Physical or virtual text interface directly to the system |
| **TTY** | Teletypewriter — the underlying device interface |

---

## 7. Users, Groups & Permissions

Linux is a **multi-user** system. Every file and process is owned by a user and a group.

### 7.1 User Types

| Type | Description |
|------|-------------|
| **Root** (UID 0) | Superuser — has unrestricted access to everything |
| **System Users** (UID 1–999) | Created by services (www-data, mysql, nobody) |
| **Regular Users** (UID 1000+) | Human users with limited access |

### 7.2 Understanding File Permissions

```
-rwxr-xr--  1  john  devs  4096  Jan 1 10:00  script.sh
│││││││││└── Others: read only
│││││││└──── Others: no write
│││││└─────── Group: read + execute
│││└────────── Owner: read + write + execute
││└─────────── File type (- = file, d = dir, l = link)
│└──────────── Number of hard links
└───────────── File type indicator
```

### 7.3 Permission Numeric Reference

| Octal | Binary | Permissions |
|-------|--------|-------------|
| 7 | 111 | rwx |
| 6 | 110 | rw- |
| 5 | 101 | r-x |
| 4 | 100 | r-- |
| 3 | 011 | -wx |
| 2 | 010 | -w- |
| 1 | 001 | --x |
| 0 | 000 | --- |

---

## 8. Package Management

A **package manager** handles installing, updating, and removing software automatically — including dependencies.

### 8.1 Package Managers by Distro

| Distro Family | Package Manager | Command Prefix |
|---------------|----------------|----------------|
| Debian / Ubuntu | apt | `sudo apt` |
| Red Hat / CentOS | yum / dnf | `sudo dnf` |
| Arch Linux | pacman | `sudo pacman` |
| SUSE | zypper | `sudo zypper` |
| Alpine | apk | `sudo apk` |
| Gentoo | portage | `emerge` |
| Any | snap | `snap` |
| Any | flatpak | `flatpak` |

### 8.2 How Package Management Works

```
User Request (apt install nginx)
        ↓
Package Manager
        ↓
Repository (remote server with packages)
        ↓
Downloads .deb / .rpm package + dependencies
        ↓
Installs files to correct locations
        ↓
Registers package in local database
```

---

## 9. Processes & the Boot Process

### 9.1 How Linux Boots

```
Power On
   ↓
BIOS / UEFI
(hardware self-test, finds boot disk)
   ↓
Bootloader — GRUB
(loads the Linux kernel into RAM)
   ↓
Linux Kernel
(initializes CPU, memory, devices)
   ↓
initramfs
(temporary filesystem for early boot tasks)
   ↓
systemd (PID 1)
(starts all services, mounts filesystems)
   ↓
Login Prompt / Desktop
```

### 9.2 Process States

| State | Symbol | Description |
|-------|--------|-------------|
| Running | R | Actively using the CPU |
| Sleeping | S | Waiting for an event or I/O |
| Uninterruptible Sleep | D | Waiting for disk I/O (cannot be killed) |
| Stopped | T | Paused (Ctrl+Z) |
| Zombie | Z | Finished but not yet cleaned up by parent |

---

## 10. Networking Basics in Linux

### 10.1 How Linux Handles Networking

```
Application (curl, browser)
      ↓
Socket API
      ↓
Transport Layer (TCP / UDP)
      ↓
Network Layer (IP)
      ↓
Data Link Layer (Ethernet / Wi-Fi)
      ↓
Physical Hardware (NIC)
```

### 10.2 Important Network Files

| File | Description |
|------|-------------|
| `/etc/hosts` | Static hostname to IP mappings |
| `/etc/resolv.conf` | DNS server configuration |
| `/etc/network/interfaces` | Network interface config (Debian) |
| `/etc/NetworkManager/` | NetworkManager config directory |
| `/etc/hostname` | System hostname |
| `/etc/services` | Port number to service name mappings |

---

## 11. Why Learn Linux?

| Reason | Details |
|--------|---------|
| **It runs the world** | 96% of web servers, 100% of top 500 supercomputers, all major cloud platforms |
| **Developer standard** | Docker, Kubernetes, and most dev tools are Linux-native |
| **Career value** | Required for DevOps, SRE, Cloud, Cybersecurity, Backend roles |
| **Free & open** | No licensing costs — full access to source code |
| **Stability** | Linux servers routinely run for years without rebooting |
| **Security** | Fine-grained permissions, SELinux, open-source auditability |
| **Customization** | Everything from the kernel to the desktop is configurable |
| **Community** | Massive global community, endless free learning resources |

---

## 12. Key Concepts to Always Remember

| Concept | Rule |
|---------|------|
| Everything is a file | Devices, processes, sockets — all represented as files |
| Case sensitive | `File.txt` and `file.txt` are different files |
| Root is everything | `/` is the top — everything branches from here |
| Root user is god | UID 0 bypasses all permission checks |
| Permissions are layered | Owner → Group → Others |
| No undo for `rm` | Deleted files don't go to a trash bin by default |
| Dot files are hidden | Files starting with `.` are hidden (`ls -a` to see them) |
| Processes inherit env | Child processes inherit variables from parent shell |
| stdout / stderr / stdin | Every process has 3 default streams (0, 1, 2) |
| man is your best friend | `man <command>` has documentation for everything |

---

## 13. Learning Path Recommendation

```
Beginner
   ↓
Learn basic navigation, file management, permissions, and package management
   ↓
Intermediate
   ↓
Shell scripting, text processing (sed/awk), networking, process management, cron
   ↓
Advanced
   ↓
Kernel internals, performance tuning, security hardening, eBPF, LVM, containers
   ↓
Expert
   ↓
Kernel development, custom distro building, systems programming (C), eBPF programs
```

---

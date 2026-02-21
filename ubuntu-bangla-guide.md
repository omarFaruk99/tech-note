# 🐧 Ubuntu Linux — Complete Guide (Beginner to Advanced)

## Cyber Security, DevOps, এবং AWS Server Management এর জন্য প্রস্তুতি

> **Target:** Linux এ fluent এবং confident হওয়া যাতে পরবর্তীতে Ubuntu Server, AWS EC2, Cyber Security, DevOps সহজে adopt করা যায়।
>
> **Study Time:** প্রতিদিন ২-৩ ঘণ্টা
>
> **Version:** 2.0 | **Last Updated:** February 2026 | **For:** Ubuntu 24.04 LTS

---

## 📑 Master Table of Contents

### Section 1: Linux Foundation (Beginner)

- [Phase 1.1: Linux ও Ubuntu পরিচিতি](#phase-11-linux-ও-ubuntu-পরিচিতি)
- [Phase 1.2: Desktop Environment (GNOME)](#phase-12-desktop-environment-gnome)
- [Phase 1.3: File System Architecture](#phase-13-file-system-architecture)
- [Phase 1.4: File Manager ও GUI Operations](#phase-14-file-manager-ও-gui-operations)
- [Phase 1.5: Software Management](#phase-15-software-management)

### Section 2: Command Line Mastery

- [Phase 2.1: Terminal Basics ও Navigation](#phase-21-terminal-basics-ও-navigation)
- [Phase 2.2: File ও Directory Operations](#phase-22-file-ও-directory-operations)
- [Phase 2.3: File Content ও Text Processing](#phase-23-file-content-ও-text-processing)
- [Phase 2.4: I/O Redirection ও Pipes](#phase-24-io-redirection-ও-pipes)
- [Phase 2.5: File Permissions ও Ownership](#phase-25-file-permissions-ও-ownership)
- [Phase 2.6: Search ও Find](#phase-26-search-ও-find)
- [Phase 2.7: Text Editors Deep Dive](#phase-27-text-editors-deep-dive)

### Section 3: System Administration

- [Phase 3.1: User ও Group Management](#phase-31-user-ও-group-management)
- [Phase 3.2: Process Management](#phase-32-process-management)
- [Phase 3.3: Service Management (systemd)](#phase-33-service-management-systemd)
- [Phase 3.4: Disk ও Storage Management](#phase-34-disk-ও-storage-management)
- [Phase 3.5: Package Management (Advanced)](#phase-35-package-management-advanced)
- [Phase 3.6: System Monitoring ও Performance](#phase-36-system-monitoring-ও-performance)
- [Phase 3.7: Log Management](#phase-37-log-management)
- [Phase 3.8: Cron Jobs ও Task Scheduling](#phase-38-cron-jobs-ও-task-scheduling)

### Section 4: Networking ও Security

- [Phase 4.1: Networking Fundamentals](#phase-41-networking-fundamentals)
- [Phase 4.2: Network Configuration ও Tools](#phase-42-network-configuration-ও-tools)
- [Phase 4.3: SSH (Secure Shell)](#phase-43-ssh-secure-shell)
- [Phase 4.4: Firewall (UFW ও iptables)](#phase-44-firewall-ufw-ও-iptables)
- [Phase 4.5: Network Diagnostics](#phase-45-network-diagnostics)
- [Phase 4.6: Security Hardening](#phase-46-security-hardening)
- [Phase 4.7: SSL/TLS ও Certificates](#phase-47-ssltls-ও-certificates)

### Section 5: Shell Scripting ও Automation

- [Phase 5.1: Bash Basics](#phase-51-bash-basics)
- [Phase 5.2: Control Structures](#phase-52-control-structures)
- [Phase 5.3: Functions ও Arguments](#phase-53-functions-ও-arguments)
- [Phase 5.4: String ও Array Operations](#phase-54-string-ও-array-operations)
- [Phase 5.5: Practical Scripts](#phase-55-practical-scripts)
- [Phase 5.6: Advanced Scripting](#phase-56-advanced-scripting)

### Section 6: Server Administration

- [Phase 6.1: Ubuntu Server vs Desktop](#phase-61-ubuntu-server-vs-desktop)
- [Phase 6.2: Remote Server Management](#phase-62-remote-server-management)
- [Phase 6.3: Web Server Setup](#phase-63-web-server-setup)
- [Phase 6.4: Database Server Basics](#phase-64-database-server-basics)
- [Phase 6.5: Application Deployment](#phase-65-application-deployment)
- [Phase 6.6: Server Maintenance](#phase-66-server-maintenance)

### Section 7: Advanced Linux ও Cloud Readiness

- [Phase 7.1: Environment ও Configuration](#phase-71-environment-ও-configuration)
- [Phase 7.2: Containers Introduction](#phase-72-containers-introduction)
- [Phase 7.3: Version Control (Git on Linux)](#phase-73-version-control-git-on-linux)
- [Phase 7.4: System Virtualization](#phase-74-system-virtualization)
- [Phase 7.5: Cloud ও AWS Preparation](#phase-75-cloud-ও-aws-preparation)

---

---

# 📘 Section 1: Linux Foundation (Beginner)

> **🎯 এই Section এর লক্ষ্য:** Linux কি, কিভাবে কাজ করে, Desktop পরিচিতি, File System বোঝা এবং Software install করা শেখা।
>
> **⏱ আনুমানিক সময়:** ১ সপ্তাহ (প্রতিদিন ২-৩ ঘণ্টা)
>
> **🔮 Future Path Connection:** এই foundation ছাড়া কোনো advanced topic শেখা সম্ভব না। Cyber Security, DevOps, AWS — সবকিছুর শুরু এখান থেকে।

---

## Phase 1.1: Linux ও Ubuntu পরিচিতি

### Linux কি?

**Linux** হলো একটি **open-source operating system kernel** যেটা ১৯৯১ সালে **Linus Torvalds** তৈরি করেছিলেন।

**সহজ ভাষায়:** Windows যেমন Microsoft এর OS, Linux তেমনি একটি OS — তবে এটি **বিনামূল্যে**, **open-source**, এবং **অনেক বেশি secure ও flexible**।

### কেন Linux শিখবেন?

| কারণ                   | ব্যাখ্যা                                                                     |
| ---------------------- | ---------------------------------------------------------------------------- |
| **Server Market**      | বিশ্বের ৯৬%+ server Linux এ চলে (AWS, Google, Facebook সব Linux ব্যবহার করে) |
| **Cyber Security**     | Kali Linux, Parrot OS — সব security tools Linux based                        |
| **DevOps**             | Docker, Kubernetes, CI/CD — সব Linux environment এ কাজ করে                   |
| **Free & Open Source** | কোনো licence fee নেই, code দেখতে ও পরিবর্তন করতে পারবেন                      |
| **Career**             | Linux skill থাকলে salary ২০-৪০% বেশি হতে পারে IT sector এ                    |

### Linux Architecture (কিভাবে কাজ করে)

```
┌─────────────────────────────────┐
│      Applications               │ ← আপনি যা ব্যবহার করেন (Chrome, VS Code)
├─────────────────────────────────┤
│      Shell (Bash/Zsh)           │ ← Command interpreter (আপনার command বোঝে)
├─────────────────────────────────┤
│      Kernel                     │ ← Linux এর হৃদপিণ্ড (hardware manage করে)
├─────────────────────────────────┤
│      Hardware                   │ ← CPU, RAM, Disk, Network
└─────────────────────────────────┘
```

- **Kernel:** Hardware এর সাথে কথা বলে। Memory, CPU, devices — সব manage করে
- **Shell:** আপনার command নিয়ে kernel কে বলে কাজ করতে। Bash হলো সবচেয়ে popular shell
- **Applications:** Firefox, Terminal, Files — যেসব program আপনি ব্যবহার করেন

### Linux Distribution (Distro) কি?

Linux kernel এর উপর ভিত্তি করে বিভিন্ন company/community বিভিন্ন OS তৈরি করেছে — এগুলোকে **Distribution** বা **Distro** বলে।

| Distro                 | ভিত্তি       | ব্যবহার                              |
| ---------------------- | ------------ | ------------------------------------ |
| **Ubuntu**             | Debian-based | সবচেয়ে জনপ্রিয়, beginner-friendly  |
| **Debian**             | Independent  | Stable, server-focused               |
| **CentOS/Rocky Linux** | RHEL-based   | Enterprise server                    |
| **Kali Linux**         | Debian-based | Cyber Security ও Penetration Testing |
| **Arch Linux**         | Independent  | Advanced users, highly customizable  |
| **Fedora**             | RHEL-based   | Latest features, developer-friendly  |

### Ubuntu 24.04 LTS বিশেষত্ব

- **LTS (Long Term Support):** ৫ বছরের security update ও support (২০২৯ পর্যন্ত)
- **GNOME 46 Desktop Environment**
- **Kernel 6.8** — latest hardware support
- Production server এর জন্য সবসময় **LTS version** ব্যবহার করবেন

### Windows vs Linux — Key Differences

| বিষয়                | Windows                   | Linux (Ubuntu)             |
| -------------------- | ------------------------- | -------------------------- |
| **মূল্য**            | Paid licence              | সম্পূর্ণ বিনামূল্যে        |
| **Source Code**      | Closed (দেখা যায় না)     | Open (যে কেউ দেখতে পারে)   |
| **Virus/Malware**    | বেশি ঝুঁকি                | খুবই কম ঝুঁকি              |
| **File System**      | NTFS, C:\, D:\            | ext4, সব `/` থেকে শুরু     |
| **Software Install** | .exe download             | apt, snap, repository থেকে |
| **Updates**          | জোরপূর্বক restart         | আপনার নিয়ন্ত্রণে          |
| **Terminal**         | Optional (PowerShell/CMD) | Primary tool (Bash)        |
| **Customization**    | সীমিত                     | সম্পূর্ণ স্বাধীনতা         |
| **Server Usage**     | ~4% market                | ~96% market                |

### 📝 Practice (Phase 1.1)

1. আপনার Ubuntu version check করুন: Settings → About
2. Terminal খুলুন (Ctrl+Alt+T) এবং `uname -a` লিখুন — output এর প্রতিটি part বোঝার চেষ্টা করুন
3. `lsb_release -a` command দিন এবং আপনার Ubuntu version ও codename note করুন

---

## Phase 1.2: Desktop Environment (GNOME)

### Desktop Environment (DE) কি?

Desktop Environment হলো সেই GUI (Graphical User Interface) যা আপনি screen এ দেখেন — icons, wallpaper, taskbar, menus সব মিলিয়ে। Ubuntu 24.04 এ **GNOME 46** ব্যবহৃত হয়।

> **🎯 Why This Matters:** Desktop এ কাজ করা শিখলে Linux এ comfortable হবেন। তবে মনে রাখবেন, server এ কোনো GUI থাকে না — তাই terminal ও শিখতে হবে (Section 2 তে)।

### GNOME Desktop এর মূল উপাদান

**১. Top Bar (উপরের বার)**

- **বাম পাশে:** Activities বাটন — সব open window দেখায়
- **মাঝখানে:** তারিখ ও সময় (click করলে calendar + notifications দেখায়)
- **ডান পাশে:** System tray — Volume, Wi-Fi, Battery, Power Menu

**২. Activities Overview (Super Key চাপুন)**

- সব open windows একসাথে দেখায়
- উপরে **Search Bar** — যেকোনো app, file, setting খুঁজতে পারবেন
- ডানে **Workspaces** — বিভিন্ন virtual desktop

**৩. Dash/Dock (বাম পাশের Application Bar)**

- Favorite apps এর shortcut
- Running apps গুলোতে dot দেখায়
- **App pin করতে:** app এ right-click → "Add to Favorites"
- **App unpin করতে:** right-click → "Remove from Favorites"

**৪. Application Grid (Super + A)**

- সব installed application দেখায়
- Windows এর Start Menu এর মতো
- Apps drag করে Dock এ রাখতে পারবেন

### Keyboard Shortcuts (অবশ্যই মুখস্ত করুন!)

#### 🔴 Must-Know Shortcuts

| Shortcut               | কাজ (Purpose)                |
| ---------------------- | ---------------------------- |
| `Super` (Windows Key)  | Activities Overview খুলুন    |
| `Ctrl + Alt + T`       | Terminal খুলুন               |
| `Super + A`            | Application Grid (সব apps)   |
| `Super + L`            | Screen Lock করুন             |
| `Alt + Tab`            | Open apps এর মধ্যে switch    |
| `Alt + F4`             | বর্তমান window বন্ধ          |
| `Super + D`            | Desktop দেখান (minimize all) |
| `Ctrl + C / Ctrl + V`  | Copy / Paste (GUI তে)        |
| `Ctrl + Shift + C / V` | Copy / Paste (Terminal এ)    |
| `Ctrl + Z`             | Undo                         |

#### 📸 Screenshot Shortcuts

| Shortcut         | কাজ                               |
| ---------------- | --------------------------------- |
| `PrtScn`         | পুরো screen capture               |
| `Shift + PrtScn` | নির্দিষ্ট area select করে capture |
| `Alt + PrtScn`   | শুধুমাত্র active window capture   |

#### 🖥 Workspace Shortcuts

| Shortcut                       | কাজ                             |
| ------------------------------ | ------------------------------- |
| `Super + Page Up/Down`         | Workspace পরিবর্তন              |
| `Shift + Super + Page Up/Down` | Window কে অন্য workspace এ সরান |
| `Super + Home`                 | প্রথম workspace এ যান           |

### Custom Shortcut তৈরি করা

1. Settings → Keyboard → View and Customize Shortcuts
2. নিচে scroll করুন → Custom Shortcuts
3. `+` button click করুন
4. Name, Command দিন এবং key combination set করুন

### Workspaces কি ও কেন ব্যবহার করবেন?

Workspace হলো **virtual desktop**। মনে করুন আপনার ৩টা আলাদা desk আছে:

- **Workspace 1:** Browser + Research
- **Workspace 2:** Code Editor + Terminal
- **Workspace 3:** Communication (Slack, Email)

এভাবে কাজ organized থাকে এবং clutter কমে।

### 📝 Practice (Phase 1.2)

1. `Super` key চেপে Activities Overview explore করুন
2. ৩টি app খুলুন এবং `Alt + Tab` দিয়ে switch করুন
3. একটি app কে Dock এ pin করুন
4. ২টি ভিন্ন Workspace তৈরি করুন এবং window move করুন
5. `Ctrl + Alt + T` দিয়ে Terminal খুলুন, বন্ধ করুন, আবার খুলুন — যতক্ষণ shortcut মনে না হচ্ছে

---

## Phase 1.3: File System Architecture

> **🎯 Why This Matters:** Linux file system বোঝা **অত্যন্ত গুরুত্বপূর্ণ**। Server manage করতে, log check করতে, config edit করতে, deploy করতে — সবকিছুতে file system এর জ্ঞান লাগবে। AWS EC2 তে কাজ করতে গেলে `/var/log`, `/etc`, `/opt` — এসব regularly ব্যবহার করবেন।

### Windows vs Linux File System

```
Windows:                          Linux:
C:\Users\omar\Documents           /home/omar/Documents
D:\Projects                       /home/omar/Projects
C:\Program Files                  /usr/bin  বা  /opt
C:\Windows\System32               /usr/sbin
```

**Key পার্থক্য:**

- Windows এ **drive letters** (C:, D:) থাকে; Linux এ সবকিছু **একটি root `/`** থেকে শুরু
- Windows এ `\` (backslash); Linux এ `/` (forward slash)
- Linux এ **everything is a file** — device, process, socket — সবকিছু file হিসেবে represent হয়

### Linux File System Hierarchy (FHS)

```
/                          ← Root directory (সবকিছুর শুরু)
├── /home/                 ← Users এর personal files
│   └── /home/omar/        ← আপনার home directory (~)
│       ├── Desktop/
│       ├── Documents/
│       ├── Downloads/
│       ├── Music/
│       ├── Pictures/
│       └── Videos/
│
├── /etc/                  ← System configuration files
│                            (সব settings এখানে থাকে)
│
├── /var/                  ← Variable data
│   ├── /var/log/          ← System logs (!!! খুবই important)
│   ├── /var/www/          ← Web server files
│   └── /var/cache/        ← Cached data
│
├── /usr/                  ← User programs & utilities
│   ├── /usr/bin/          ← Common commands (ls, cp, grep)
│   ├── /usr/sbin/         ← System admin commands
│   ├── /usr/lib/          ← Libraries
│   └── /usr/share/        ← Shared data (docs, icons)
│
├── /bin/                  ← Essential commands (boot এ লাগে)
├── /sbin/                 ← Essential system admin commands
├── /boot/                 ← Boot loader files (kernel আছে)
├── /dev/                  ← Device files (hardware represent করে)
├── /proc/                 ← Process info (virtual filesystem)
├── /sys/                  ← System hardware info (virtual)
├── /tmp/                  ← Temporary files (reboot এ মুছে যায়)
├── /opt/                  ← Optional/third-party software
├── /root/                 ← Root user এর home directory
├── /mnt/                  ← Manual mount point
├── /media/                ← Auto-mounted drives (USB, CD)
└── /srv/                  ← Service data (web, FTP)
```

### প্রতিটি Directory এর বিস্তারিত ব্যাখ্যা

| Directory | পূর্ণরূপ/অর্থ             | কাজ                    | কখন ব্যবহার করবেন           |
| --------- | ------------------------- | ---------------------- | --------------------------- |
| `/`       | Root                      | সবকিছুর parent         | Linux এর শুরু               |
| `/home`   | Home                      | User এর personal files | প্রতিদিন                    |
| `/etc`    | Et Cetera / Configuration | সব config files        | Server config, app settings |
| `/var`    | Variable                  | পরিবর্তনশীল data       | Logs দেখতে, web files       |
| `/usr`    | Unix System Resources     | Programs ও libraries   | Software related            |
| `/tmp`    | Temporary                 | সাময়িক files          | Auto-delete হয়             |
| `/opt`    | Optional                  | Third-party software   | Custom software install     |
| `/dev`    | Devices                   | Hardware device files  | Disk mount, device access   |
| `/proc`   | Process                   | Running process info   | System monitoring           |
| `/boot`   | Boot                      | Startup files          | Kernel, GRUB                |
| `/root`   | Root Home                 | Admin user এর home     | Admin কাজে                  |
| `/mnt`    | Mount                     | Manual mount point     | External disk mount         |
| `/media`  | Media                     | Auto-mount             | USB, CD automatically       |

### Home Directory (`~`) — আপনার প্রধান কাজের জায়গা

- Full path: `/home/your-username/`
- Shortcut: `~` (tilde)
- এখানে আপনার সব personal files, settings, downloads থাকে

**Hidden files ও folders:**

- `.` দিয়ে শুরু হলে file/folder hidden
- উদাহরণ: `.bashrc`, `.config/`, `.ssh/`
- এগুলো important config files — delete করবেন না!

### 📝 Practice (Phase 1.3)

1. Terminal খুলুন ও `ls /` command দিন — root directory এর contents দেখুন
2. `ls /home` দিয়ে আপনার username দেখুন
3. `ls /etc` দিয়ে config files explore করুন
4. `ls -la ~` দিয়ে আপনার home এর hidden files দেখুন
5. `cat /etc/hostname` দিয়ে আপনার computer এর নাম দেখুন
6. `cat /etc/os-release` দিয়ে Ubuntu version details দেখুন

---

## Phase 1.4: File Manager ও GUI Operations

### Files (Nautilus) — Ubuntu এর File Manager

**খোলার উপায়:**

- Dock থেকে folder icon click করুন
- Activities → "Files" type করুন
- Terminal: `nautilus .` (current directory খুলবে)

### Files App Layout

```
┌─────────────────────────────────────────┐
│  ← → 🏠  /home/omar/Documents    🔍 ☰  │  ← Navigation Bar
├──────────┬──────────────────────────────┤
│ ⭐ Starred │                            │
│ 🏠 Home    │     [Files & Folders        │
│ 📁 Desktop │      appear here]           │
│ 📁 Documents│                            │
│ 📁 Downloads│                            │
│ 📁 Music   │                            │
│ 📁 Pictures│                            │
│ 📁 Videos  │                            │
│            │                            │
│ 💾 Other   │                            │
│  Locations │                            │
├──────────┴──────────────────────────────┤
│  3 items                                │  ← Status Bar
└─────────────────────────────────────────┘
```

### File Operations (GUI)

| কাজ                 | Shortcut           | Mouse                       |
| ------------------- | ------------------ | --------------------------- |
| Copy                | `Ctrl + C`         | Right-click → Copy          |
| Cut                 | `Ctrl + X`         | Right-click → Cut           |
| Paste               | `Ctrl + V`         | Right-click → Paste         |
| Delete (Trash)      | `Delete`           | Right-click → Move to Trash |
| Delete (Permanent)  | `Shift + Delete`   | —                           |
| Rename              | `F2`               | Right-click → Rename        |
| Select All          | `Ctrl + A`         | —                           |
| New Folder          | `Ctrl + Shift + N` | Right-click → New Folder    |
| Properties          | `Alt + Enter`      | Right-click → Properties    |
| Hidden Files Toggle | `Ctrl + H`         | Menu → Show Hidden Files    |
| Undo                | `Ctrl + Z`         | —                           |
| Search              | `Ctrl + F`         | Click 🔍 icon               |

### File Properties (Right-click → Properties)

**৩টি Tab:**

1. **Basic:** Name, Type, Size, Location, Modified date
2. **Permissions:** Owner, Group, Others — Read/Write/Execute
3. **Open With:** কোন program দিয়ে file খুলবে সেটা set করুন

### Drives ও USB Management

**USB/External Drive Connect করলে:**

1. Automatically `/media/username/drive-name` এ mount হবে
2. Files app এর sidebar এ দেখা যাবে
3. কাজ শেষে **Safely Eject করুন** → sidebar এ ⏏ icon click

### 📝 Practice (Phase 1.4)

1. Files app খুলুন এবং Documents folder এ ৩টি test folder তৈরি করুন
2. একটি folder এ right-click → New Document → Empty Document
3. File rename করুন `F2` দিয়ে
4. File copy করে অন্য folder এ paste করুন
5. `Ctrl + H` দিয়ে hidden files দেখুন — কি কি আছে note করুন
6. Terminal থেকে `nautilus /etc` দিয়ে system config folder explore করুন (ভোলো কিছু delete করবেন না!)

---

## Phase 1.5: Software Management

> **🎯 Why This Matters:** Linux এ software management Windows থেকে অনেক ভিন্ন। **Repository** concept বুঝলে server এ software deploy করা, Docker image তৈরি করা, automation script লেখা — সব সহজ হবে।

### Software Install এর ৪টি উপায়

```
Install Method        সহজতা     Speed    Use Case
──────────────────────────────────────────────────
1. Software Center    ⭐⭐⭐⭐⭐    🐢      Beginner, GUI-only
2. APT (Terminal)     ⭐⭐⭐⭐     🚀      সবচেয়ে standard, server এও কাজ করে
3. Snap              ⭐⭐⭐⭐     🐢      Sandboxed, cross-distro
4. .deb File         ⭐⭐⭐       🚀      Third-party software
```

### ১. Ubuntu Software Center (GUI)

- Activities → "Software" বা "Ubuntu Software"
- Search করুন → Install button → Password দিন
- **ভালো দিক:** সহজ, safe
- **খারাপ দিক:** ধীর, সব software থাকে না

### ২. APT — Advanced Package Tool (সবচেয়ে গুরুত্বপূর্ণ!)

APT হলো Ubuntu/Debian র **default package manager**। Server এ এটাই ব্যবহার করবেন।

**Repository কি?**
Repository হলো software এর online storage/warehouse। APT সেখান থেকে software download ও install করে।

```bash
# ──────────────────────────────────────────
# 📦 APT Commands — প্রতিটি command এর ব্যাখ্যা
# ──────────────────────────────────────────

# 1. Package list update করুন
#    কাজ: Repository থেকে latest software list নিয়ে আসে
#    অর্থ: "নতুন কি কি আছে check করো"
#    কখন: যেকোনো install/upgrade এর আগে
sudo apt update

# 2. Installed software upgrade করুন
#    কাজ: সব installed software এর নতুন version install করে
#    অর্থ: "যা আছে সব latest version এ update করো"
#    -y flag: automatically "Yes" বলে (confirm না চেয়ে)
sudo apt upgrade -y

# 3. Full system upgrade
#    কাজ: upgrade + kernel ও dependencies ও update করে
#    অর্থ: "পুরো system কে latest এ নিয়ে যাও"
sudo apt full-upgrade -y

# 4. Software install করুন
#    কাজ: নতুন software install করে
#    syntax: sudo apt install <package-name>
sudo apt install vlc               # VLC media player
sudo apt install gimp              # Image editor
sudo apt install htop              # System monitor

# 5. একসাথে অনেক software install
sudo apt install vlc gimp htop curl wget

# 6. Software remove করুন
#    কাজ: Software uninstall করে (config files থাকে)
sudo apt remove vlc

# 7. Software পুরোপুরি remove (config সহ)
#    কাজ: Software + তার config files সব মুছে দেয়
sudo apt purge vlc

# 8. অব্যবহৃত packages মুছুন
#    কাজ: যেসব dependency আর কোনো software ব্যবহার করে না, সেগুলো মুছে দেয়
sudo apt autoremove -y

# 9. Package cache clean করুন
#    কাজ: Downloaded .deb files মুছে disk space free করে
sudo apt clean

# 10. Software search করুন
#     কাজ: Repository তে software খুঁজুন
apt search "video player"
apt search nginx

# 11. Software details দেখুন
#     কাজ: Package এর version, size, description দেখায়
apt show vlc
apt show nginx

# 12. Installed packages এর list
#     কাজ: কি কি install আছে দেখুন
apt list --installed

# 13. কোনো specific package installed কিনা check
apt list --installed | grep nginx

# ──────────────────────────────────────────
# 🔄 All-in-one update command (মুখস্ত করুন!)
# ──────────────────────────────────────────
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```

### `sudo` কি?

- **Super User DO** — admin/root হিসেবে command চালায়
- System-level পরিবর্তন করতে `sudo` লাগে
- Password চাইবে (আপনার login password দিন)
- **সাবধানতা:** `sudo` দিয়ে ভুল command দিলে system damage হতে পারে!

### ৩. Snap Packages

Snap হলো **sandboxed** package system। প্রতিটি snap নিজের dependencies সাথে নিয়ে আসে।

```bash
# Snap install
sudo snap install vlc
sudo snap install code --classic      # VS Code (--classic = full system access)
sudo snap install spotify

# Installed snaps দেখুন
snap list

# Snap update
sudo snap refresh

# Snap remove
sudo snap remove vlc

# Snap search
snap find "text editor"
```

**APT vs Snap:**

| Feature     | APT        | Snap                  |
| ----------- | ---------- | --------------------- |
| Speed       | দ্রুত      | একটু ধীর              |
| Size        | ছোট        | বড় (dependencies সহ) |
| Auto-update | না         | হ্যাঁ                 |
| Isolation   | না         | হ্যাঁ (sandboxed)     |
| Server Use  | Primary ✅ | Secondary             |

### ৪. `.deb` File Install

কিছু software (Chrome, VS Code) তাদের website থেকে `.deb` file download দেয়।

```bash
# Method 1: dpkg দিয়ে install
#   dpkg = Debian Package Manager (low-level)
cd ~/Downloads
sudo dpkg -i google-chrome-stable_current_amd64.deb

# Dependency error আসলে fix করুন
sudo apt install -f

# Method 2: apt দিয়ে install (recommended)
sudo apt install ./google-chrome-stable_current_amd64.deb
```

### ৫. PPA (Personal Package Archive)

PPA হলো **third-party repository**। Official repository তে নেই এমন software এখান থেকে install করা যায়।

```bash
# PPA add করুন
#   কাজ: নতুন software source যোগ করে
sudo add-apt-repository ppa:graphics-drivers/ppa

# Update করুন (নতুন PPA থেকে list আনার জন্য)
sudo apt update

# PPA remove করুন
sudo add-apt-repository --remove ppa:graphics-drivers/ppa
```

> ⚠️ **সাবধানতা:** অপরিচিত PPA add করবেন না — malware/virus হতে পারে!

### System Update Best Practice

```bash
# প্রতি সপ্তাহে এই commands গুলো চালান:
sudo apt update               # 1. Latest list আনো
sudo apt upgrade -y            # 2. Software update করো
sudo apt full-upgrade -y       # 3. System upgrade করো
sudo apt autoremove -y         # 4. অপ্রয়োজনীয় packages মুছো
sudo apt clean                 # 5. Cache clean করো
sudo snap refresh              # 6. Snap apps update করো
```

### Essential Software Install (নতুন Ubuntu Setup এর পরে)

```bash
# System tools
sudo apt install curl wget git htop net-tools vim nano

# Build essentials (programming এর জন্য)
sudo apt install build-essential

# Media codecs (video/audio চালানোর জন্য)
sudo apt install ubuntu-restricted-extras

# Archive tools
sudo apt install unrar p7zip-full p7zip-rar

# Browser
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb

# VS Code
sudo snap install code --classic

# VLC
sudo apt install vlc
```

### 📝 Practice (Phase 1.5)

1. `sudo apt update` চালান এবং output বুঝুন (কতগুলো package update আছে)
2. `apt search "text editor"` দিয়ে text editors খুঁজুন
3. `sudo apt install htop` দিয়ে htop install করুন
4. `apt show htop` দিয়ে package details দেখুন
5. `htop` command দিয়ে চালান (exit: `q`)
6. `apt list --installed | wc -l` দিয়ে মোট কতগুলো package installed আছে গণনা করুন
7. `snap list` দিয়ে installed snaps দেখুন

---

---

# 📗 Section 2: Command Line Mastery

> **🎯 এই Section এর লক্ষ্য:** Terminal এ fluent হওয়া। Linux এর আসল power terminal এ। Server, AWS EC2, Docker — কোথাও GUI নেই, সব command line।
>
> **⏱ আনুমানিক সময়:** ২ সপ্তাহ (প্রতিদিন ২-৩ ঘণ্টা)
>
> **🔮 Future Path Connection:** Terminal mastery ছাড়া Cyber Security, DevOps, Server Management — কিছুই করা সম্ভব না। এটি **সবচেয়ে গুরুত্বপূর্ণ Section**।

---

## Phase 2.1: Terminal Basics ও Navigation

### Terminal কি?

Terminal (বা Console/Shell) হলো একটি text-based interface যেখানে আপনি command লিখে computer কে instruction দেন।

**Terminal খোলার উপায়:**

- `Ctrl + Alt + T` — সবচেয়ে দ্রুত (মুখস্ত করুন!)
- Activities → "Terminal" search

### Terminal Prompt বোঝা

```bash
omar@ubuntu-pc:~$
│     │          │ │
│     │          │ └── $ = Normal user (# হলে root/admin)
│     │          └──── ~ = Current location (~ = home)
│     └──────────────── Computer/hostname
└────────────────────── Your username
```

### Navigation Commands

```bash
# ── pwd — Print Working Directory ──
# কাজ: আপনি এখন কোথায় আছেন দেখায়
pwd
# Output: /home/omar

# ── ls — List ──
# কাজ: Directory র ভিতরে কি আছে দেখায়
ls                    # Basic listing
ls -l                 # Long format (permissions, size, date সহ)
ls -a                 # All files (hidden সহ)
ls -la                # Long + All (সবচেয়ে বেশি ব্যবহৃত!)
ls -lh                # Human readable size (KB, MB, GB)
ls -lah               # সবকিছু একসাথে
ls -lt                # Time sort (newest first)
ls -ltr               # Time reverse sort (oldest first)
ls -R                 # Recursive (subfolder সহ)
ls /etc               # নির্দিষ্ট directory দেখুন

# ls -l output বোঝা:
# -rw-rw-r-- 1 omar omar 4096 Feb 20 10:30 file.txt
# │            │ │    │    │    │              └── File name
# │            │ │    │    │    └── Modified date
# │            │ │    │    └── Size
# │            │ │    └── Group
# │            │ └── Owner
# │            └── Hard links
# └── Permissions

# ── cd — Change Directory ──
# কাজ: Directory পরিবর্তন করে
cd Documents          # Documents folder এ যান
cd /var/log           # Absolute path দিয়ে যান
cd ..                 # এক level উপরে
cd ../..              # দুই level উপরে
cd ~                  # Home directory তে যান
cd                    # Home directory (shortcut)
cd -                  # আগের directory তে ফিরে যান
cd /                  # Root directory
```

### Path — Absolute vs Relative

```bash
# Absolute Path: / থেকে শুরু, সম্পূর্ণ address
cd /home/omar/Documents/Projects

# Relative Path: বর্তমান location থেকে
cd Documents/Projects

# Special symbols:
#  .   = Current directory
#  ..  = Parent directory
#  ~   = Home directory
#  -   = Previous directory
```

### Essential Terminal Skills

```bash
# clear — Screen clear
clear                 # or Ctrl + L

# history — আগের commands
history               # সব commands
history 20            # শেষ ২০টি
!!                    # শেষ command আবার চালান
sudo !!               # শেষ command sudo দিয়ে চালান

# Tab Completion — সবচেয়ে useful!
# "Doc" + Tab → "Documents/" auto-complete

# man — Manual page
man ls                # ls এর manual (q দিয়ে exit)

# --help — Quick help
ls --help

# which — Command কোথায়
which python3         # Python location
```

### Terminal Control Shortcuts

| Shortcut        | কাজ                           |
| --------------- | ----------------------------- |
| `Ctrl + C`      | Running command বন্ধ (cancel) |
| `Ctrl + D`      | Terminal exit/logout          |
| `Ctrl + L`      | Screen clear                  |
| `Ctrl + A`      | Cursor → line এর শুরু         |
| `Ctrl + E`      | Cursor → line এর শেষ          |
| `Ctrl + U`      | Cursor এর বামের সব মুছুন      |
| `Ctrl + K`      | Cursor এর ডানের সব মুছুন      |
| `Ctrl + W`      | আগের word মুছুন               |
| `Ctrl + R`      | History search (reverse)      |
| `Up/Down Arrow` | আগের/পরের command             |

### 📝 Practice (Phase 2.1)

1. Terminal খুলুন → `pwd` → `ls -lah` → output এর columns বুঝুন
2. `cd /var/log` → `pwd` → `ls` → `cd ~` — sequence practice
3. `cd -` দিয়ে toggle করুন
4. `man ls` পড়ুন (q exit)
5. Tab completion: `cd Doc` + Tab
6. `Ctrl + R` → "cd" search
7. `history 10` দিয়ে recent commands দেখুন

---

## Phase 2.2: File ও Directory Operations

### Directory তৈরি

```bash
# ── mkdir — Make Directory ──
# কাজ: নতুন folder তৈরি করে
mkdir projects                     # একটি folder
mkdir test1 test2 test3            # একসাথে ৩টি
mkdir -p projects/web/frontend     # -p: Nested folders (parent সহ তৈরি)
mkdir -v projects/backend          # -v: Verbose, কি তৈরি হলো দেখায়
```

### File তৈরি

```bash
# ── touch — File তৈরি / timestamp update ──
# কাজ: Empty file তৈরি, বা existing file এর timestamp update
touch file.txt                     # একটি empty file
touch file1.txt file2.txt          # ২টি file
touch .hidden-file                 # Hidden file (. দিয়ে শুরু)
echo "Hello World" > hello.txt     # Content সহ file
```

### Copy

```bash
# ── cp — Copy ──
# Syntax: cp [options] source destination
cp file.txt backup.txt             # File copy
cp file.txt ~/Documents/           # অন্য directory তে copy
cp -r projects projects_backup     # -r: Directory copy (recursive)
cp -rv src/ dest/                  # -v: verbose
cp -i file.txt dest/               # -i: overwrite আগে confirm চায়
```

### Move / Rename

```bash
# ── mv — Move / Rename ──
mv old.txt new.txt                 # Rename
mv file.txt ~/Documents/           # Move
mv file.txt ~/Documents/report.txt # Move + rename
mv *.txt ~/Documents/              # সব .txt move
mv -i source dest                  # -i: confirm চায়
```

### Delete (⚠️ সাবধান!)

```bash
# ── rm — Remove ──
# ⚠️ Linux এ Recycle Bin নেই! rm = permanent delete!
rm file.txt                        # File delete
rm -i file.txt                     # -i: confirm চায় (safe!)
rm -r folder/                      # -r: Directory delete (recursive)
rm -ri folder/                     # Safe! Interactive + recursive
rm -rf folder/                     # ⚠️ Force delete! No confirm!

# ⛔ NEVER: rm -rf /     (পুরো system মুছে যাবে!)
# ⛔ NEVER: rm -rf ~     (পুরো home মুছে যাবে!)

# rmdir — শুধু empty folder মুছে
rmdir empty_folder
```

### Symbolic Links (Shortcuts)

```bash
# ── ln -s — Symbolic Link ──
# কাজ: Shortcut/link তৈরি (Windows shortcut এর মতো)
ln -s /path/to/original /path/to/link
ln -s ~/Documents/project ~/Desktop/project-link

# Link দেখা: ls -la তে -> দিয়ে দেখায়
# Link remove: rm link-name (original file থাকে)
```

### Wildcards / Globbing

```bash
# * = যেকোনো কিছু
ls *.txt                           # সব .txt files
cp *.jpg ~/Pictures/

# ? = ঠিক একটি character
ls file?.txt                       # file1.txt YES, file10.txt NO

# [] = নির্দিষ্ট characters
ls file[123].txt                   # file1, file2, file3

# {} = Brace expansion
mkdir {frontend,backend,database}  # ৩টি folder
touch file{1..5}.txt               # file1-5.txt
```

### 📝 Practice (Phase 2.2)

1. `mkdir -p ~/linux-practice/web/{html,css,js}` দিয়ে structure তৈরি
2. `touch ~/linux-practice/web/html/index.html` files তৈরি
3. `cp -r web web-backup` backup নিন
4. `mv web-backup web-archive` rename
5. `ls -R ~/linux-practice` structure দেখুন
6. `rm -ri web-archive` interactive delete
7. `touch file{1..10}.txt` তারপর wildcard practice

---

## Phase 2.3: File Content ও Text Processing

> **🎯 Why This Matters:** Log analysis, config check, data processing — DevOps ও Cyber Security তে এসব tools ছাড়া অসম্ভব।

### File Content দেখা

```bash
# ── cat — Concatenate ──
# কাজ: File এর সম্পূর্ণ content দেখায়
cat file.txt                       # Content দেখুন
cat -n file.txt                    # Line number সহ
cat file1.txt file2.txt > merged.txt  # ২ file merge

# ── less — Page by Page (বড় file এর জন্য সেরা) ──
less file.txt
# Space = next page, b = previous, /text = search, q = quit

# ── head — শুরু দেখুন ──
head file.txt                      # প্রথম 10 lines
head -n 5 file.txt                 # প্রথম 5 lines

# ── tail — শেষ দেখুন ──
tail file.txt                      # শেষ 10 lines
tail -n 5 file.txt                 # শেষ 5 lines
tail -f /var/log/syslog            # ⭐ Live monitoring! Real-time log
#  -f = follow mode. নতুন log আসলে automatic দেখায়
#  DevOps/Server এ constantly ব্যবহার করবেন!
#  Ctrl+C বন্ধ করুন

# ── wc — Word Count ──
wc file.txt                        # lines words characters
wc -l file.txt                     # শুধু line count
wc -w file.txt                     # শুধু word count
```

### Text Processing Tools

```bash
# ── grep — Search text in files ──
# সবচেয়ে ব্যবহৃত Linux tools এর একটি!
grep "error" log.txt               # "error" খুঁজুন
grep -i "error" log.txt            # -i: case insensitive
grep -n "error" log.txt            # -n: line number সহ
grep -c "error" log.txt            # -c: count
grep -v "debug" log.txt            # -v: invert (যেখানে "debug" নেই)
grep -r "TODO" ~/projects/         # -r: recursive, সব subfolder
grep -w "error" file.txt           # -w: whole word ("errors" না)
grep -A 3 "error" file.txt         # -A: match এর পরের 3 lines
grep -B 2 "error" file.txt         # -B: match এর আগের 2 lines
grep -E "error|warning" file.txt   # -E: regex, | = OR

# Regex সহ grep
grep "^Error" file.txt             # ^ = line শুরুতে
grep "error$" file.txt             # $ = line শেষে

# ── sort — Lines sort করুন ──
sort file.txt                      # Alphabetical
sort -r file.txt                   # Reverse
sort -n numbers.txt                # Numeric sort
sort -u file.txt                   # Unique (duplicate বাদ)

# ── cut — Columns extract ──
cut -d':' -f1 /etc/passwd          # : separator, 1st field
cut -d',' -f2,3 data.csv           # CSV from 2nd,3rd column

# ── uniq — Duplicate remove ──
# ⚠️ sort এর পরে ব্যবহার করুন!
sort file.txt | uniq               # Duplicate remove
sort file.txt | uniq -c            # Count সহ

# ── diff — File তুলনা ──
diff file1.txt file2.txt           # পার্থক্য দেখুন
diff -u file1.txt file2.txt        # Git style format

# ── sed — Stream Editor (find & replace) ──
# Server config modify করতে অনেক ব্যবহৃত
sed 's/old/new/' file.txt          # প্রথম match replace
sed 's/old/new/g' file.txt         # g: সব replace
sed -i 's/old/new/g' file.txt      # -i: file এ সরাসরি পরিবর্তন!
sed '3d' file.txt                  # 3rd line delete
sed -n '5,10p' file.txt            # 5-10 line দেখাও

# ── awk — Column-based processing ──
# Log analysis এ অত্যন্ত useful!
awk '{print $1}' file.txt          # 1st column
awk '{print $1, $3}' file.txt      # 1st ও 3rd column
awk -F':' '{print $1}' /etc/passwd # Custom separator
awk '/error/ {print}' log.txt      # Pattern match lines
```

### 📝 Practice (Phase 2.3)

1. `cat /etc/passwd` → output বুঝুন
2. `grep "root" /etc/passwd` → root user খুঁজুন
3. `grep -c "bash" /etc/passwd` → bash user count
4. `cut -d':' -f1 /etc/passwd | sort` → sorted users
5. `wc -l /etc/passwd` → total users
6. Test file তৈরি করে `sed 's/hello/world/g'` practice
7. `tail -f /var/log/syslog` → live log (Ctrl+C exit)

---

## Phase 2.4: I/O Redirection ও Pipes

> **🎯 Why This Matters:** Redirection ও Pipes হলো Linux এর superpower। ছোট commands connect করে complex কাজ করা যায়।

### Standard Streams

```
stdin (0)  → [Program] → stdout (1) = normal output
                       → stderr (2) = error output
```

### Output Redirection

```bash
# > — Overwrite (আগের content মুছে যায়!)
echo "Hello" > file.txt            # Save to file
ls -la > listing.txt               # Directory listing save

# >> — Append (শেষে যোগ করে)
echo "Line 1" > notes.txt          # Create
echo "Line 2" >> notes.txt         # Append
echo "Line 3" >> notes.txt         # Append more

# 2> — Error redirect
ls /nonexistent 2> errors.txt      # Error save
find / -name "*.conf" 2> /dev/null # Error ignore

# &> — stdout + stderr redirect
command &> all_output.txt

# /dev/null — "Black Hole"
command > /dev/null                 # Output ফেলে দাও
command &> /dev/null                # সব silent
```

### Input Redirection ও Here Document

```bash
# < — File থেকে input
sort < names.txt

# << — Here Document (multi-line input)
cat << EOF > config.txt
server_name=myserver
port=8080
debug=false
EOF
```

### Pipes (|) — Linux এর সবচেয়ে powerful feature!

```bash
# | (Pipe): একটি command এর output → পরের command এর input

# User list sort
cat /etc/passwd | cut -d':' -f1 | sort

# Process count
ps aux | wc -l

# Process search
ps aux | grep "firefox"

# Top 5 বড় files
du -ah ~ | sort -rh | head -5

# Log এ error count
cat /var/log/syslog | grep -i "error" | wc -l

# tee — Screen + file দুই জায়গায়
ls -la | tee listing.txt
ls -la | tee -a listing.txt        # -a: append

# xargs — pipe output → arguments
find . -name "*.tmp" | xargs rm
echo "f1 f2 f3" | xargs touch
```

### Real-world Pipe Examples

```bash
# Open ports
sudo ss -tlnp | grep "LISTEN"

# Disk usage top 10
du -ah /home | sort -rh | head -10

# Config without comments
cat config.file | grep -v "^#" | grep -v "^$"

# Running services
systemctl list-units --type=service --state=running | grep ".service"
```

### 📝 Practice (Phase 2.4)

1. `echo "Hello" > test.txt` → `echo "World" >> test.txt` → `cat test.txt`
2. `ls /nonexistent 2> error.txt` → `cat error.txt`
3. `ls -la | head -5` → first 5 items
4. `ps aux | grep "bash" | wc -l`
5. `history | grep "ls" | wc -l`
6. `du -sh ~/* | sort -rh | head -5`
7. `ls -la | tee listing.txt` screen + file output

---

## Phase 2.5: File Permissions ও Ownership

> **🎯 Why This Matters:** Linux security এর মূল ভিত্তি হলো permissions। Server এ wrong permission = security breach। AWS EC2, web server, SSH key — সবকিছুতে correct permissions জানতে হবে।

### Permission System বোঝা

```bash
ls -l file.txt
# -rw-r--r-- 1 omar developers 4096 Feb 20 10:30 file.txt
#  │││ │││ │││
#  │││ │││ └┴┴── Others (বাকি সবাই): r-- (read only)
#  │││ └┴┴────── Group (developers): r-- (read only)
#  └┴┴────────── Owner (omar): rw- (read + write)
#
# First character: file type
#  -  = regular file
#  d  = directory
#  l  = symbolic link
```

### Permission Types

| Symbol | Number | অর্থ          | File এ           | Directory তে             |
| ------ | ------ | ------------- | ---------------- | ------------------------ |
| `r`    | 4      | Read          | File পড়া        | `ls` দিয়ে contents দেখা |
| `w`    | 2      | Write         | File edit/delete | Files তৈরি/delete        |
| `x`    | 1      | Execute       | Program চালানো   | `cd` দিয়ে ঢোকা          |
| `-`    | 0      | No permission | —                | —                        |

### chmod — Permission পরিবর্তন

```bash
# ── chmod — Change Mode ──
# কাজ: File/directory এর permissions পরিবর্তন করে

# === Symbolic Method (সহজ) ===
# u = user/owner, g = group, o = others, a = all
# + = add, - = remove, = = set exactly
chmod u+x script.sh               # Owner কে execute permission দিন
chmod g+w file.txt                 # Group কে write permission
chmod o-r file.txt                 # Others থেকে read remove
chmod a+r file.txt                 # সবাইকে read
chmod u+rwx,g+rx,o+r file.txt     # Multiple at once

# === Numeric Method (professional — মুখস্ত করুন!) ===
# r=4, w=2, x=1 → যোগ করুন
# 7 = rwx (4+2+1)
# 6 = rw- (4+2)
# 5 = r-x (4+1)
# 4 = r-- (4)
# 0 = --- (no permission)

chmod 755 script.sh                # rwxr-xr-x (owner:full, others:read+execute)
chmod 644 file.txt                 # rw-r--r-- (owner:read+write, others:read)
chmod 600 private.key              # rw------- (শুধু owner read+write — SSH key!)
chmod 700 secret_folder/           # rwx------ (শুধু owner full access)
chmod 777 file.txt                 # ⚠️ rwxrwxrwx — সবাই সব করতে পারে (AVOID!)

# Common permission patterns:
# 755 — Executable scripts, directories
# 644 — Regular files (documents, configs)
# 600 — Private files (SSH keys, passwords)
# 700 — Private directories
# 400 — Read-only sensitive files
```

### chown — Owner পরিবর্তন

```bash
# ── chown — Change Owner ──
# কাজ: File/directory এর owner ও group পরিবর্তন করে
# Syntax: sudo chown user:group file
sudo chown omar file.txt           # Owner পরিবর্তন
sudo chown omar:developers file.txt # Owner + group পরিবর্তন
sudo chown :developers file.txt    # শুধু group পরিবর্তন
sudo chown -R omar:omar folder/    # -R: Recursive (folder + সব contents)
```

### Special Permissions

```bash
# umask — Default permission mask
umask                              # Current mask দেখুন (সাধারণত 0022)
# File default: 666 - 022 = 644 (rw-r--r--)
# Dir default: 777 - 022 = 755 (rwxr-xr-x)

# SUID (Set User ID) — Program owner হিসেবে চলে
chmod u+s program                  # passwd command এভাবে root হিসেবে চলে
# SGID (Set Group ID) — Group inherit করে
chmod g+s folder/
# Sticky Bit — শুধু owner delete করতে পারে (/tmp তে ব্যবহৃত)
chmod +t folder/
```

### 📝 Practice (Phase 2.5)

1. `touch test-perm.txt` → `ls -l test-perm.txt` → default permissions দেখুন
2. `chmod 755 test-perm.txt` → `ls -l` → পরিবর্তন দেখুন
3. `chmod 600 test-perm.txt` → `ls -l` → শুধু owner access
4. `mkdir test-dir` → `ls -ld test-dir` → directory permissions
5. `touch script.sh` → `chmod +x script.sh` → executable করুন
6. `ls -l /etc/passwd` ও `ls -l /etc/shadow` তুলনা করুন — কেন shadow restricted?
7. `umask` command দিয়ে default mask দেখুন

---

## Phase 2.6: Search ও Find

> **🎯 Why This Matters:** Server এ log file, config file, কোনো specific file খুঁজতে হলে find/locate ব্যবহার করবেন। Security audit এ unauthorized files খুঁজতেও এগুলো লাগে।

```bash
# ── find — File/Directory search (সবচেয়ে powerful!) ──
# কাজ: Real-time file system search
# Syntax: find [where] [criteria] [action]

# নাম দিয়ে খুঁজুন
find ~ -name "*.txt"               # Home এ সব .txt files
find /etc -name "*.conf"           # /etc এ সব config files
find . -name "*.log"               # Current directory তে log files
find / -name "myfile" 2>/dev/null  # পুরো system এ (errors ignore)

# -iname: Case insensitive
find ~ -iname "readme*"            # README, readme, Readme সব

# Type দিয়ে খুঁজুন
find ~ -type f                     # শুধু files (f)
find ~ -type d                     # শুধু directories (d)
find ~ -type l                     # শুধু symlinks (l)

# Size দিয়ে খুঁজুন
find ~ -size +100M                 # 100MB এর বড় files
find ~ -size +1G                   # 1GB এর বড় files
find /var/log -size +50M           # বড় log files খুঁজুন
find ~ -size -1k                   # 1KB এর ছোট files
find ~ -empty                      # Empty files/directories

# Time দিয়ে খুঁজুন
find ~ -mtime -7                   # গত ৭ দিনে modified
find ~ -mtime +30                  # ৩০ দিনের বেশি আগে modified
find ~ -mmin -60                   # গত ৬০ মিনিটে modified
find /var/log -newer /var/log/syslog  # syslog এর পরে modify হওয়া files

# Permission দিয়ে খুঁজুন
find / -perm 777 2>/dev/null       # 777 permission files (security risk!)
find / -perm -u+s 2>/dev/null      # SUID files (security audit)

# Find + Action
find ~ -name "*.tmp" -delete       # .tmp files খুঁজে delete
find ~ -name "*.log" -exec rm {} \;  # -exec: command চালান
find . -type f -name "*.txt" -exec grep "error" {} \;  # Text search in found files
find . -name "*.sh" -exec chmod +x {} \;  # সব .sh কে executable করুন

# ── locate — Database-based search (দ্রুত!) ──
# কাজ: Pre-built database থেকে search (find এর চেয়ে দ্রুত)
sudo apt install mlocate           # Install
sudo updatedb                      # Database update (প্রথমবার)
locate myfile.txt                  # File search
locate -i "readme"                 # -i: case insensitive
locate "*.conf" | head -20         # First 20 config files

# ── which — Command location ──
which python3                      # /usr/bin/python3
which nginx                        # Nginx কোথায়

# ── whereis — Binary, source, man page location ──
whereis python3                    # Binary + man page location
whereis ls
```

### 📝 Practice (Phase 2.6)

1. `find ~ -name "*.txt"` → home এ সব txt files খুঁজুন
2. `find ~ -size +10M` → 10MB+ files খুঁজুন
3. `find ~ -mtime -1` → আজকে modified files
4. `find ~ -empty` → empty files/folders
5. `find /etc -name "*.conf" | wc -l` → কতগুলো config file আছে
6. `which bash` ও `which python3` → locations দেখুন
7. `find ~ -type d -name ".*"` → hidden directories খুঁজুন

---

## Phase 2.7: Text Editors Deep Dive

> **🎯 Why This Matters:** Server এ GUI নেই। Config file edit করতে, script লিখতে — terminal-based editor জানা mandatory। `vim` হলো industry standard, AWS EC2 তে by default থাকে।

### Nano — Beginner Friendly Editor

```bash
# nano — সহজ terminal editor
nano file.txt                      # File খুলুন (নতুন হলে তৈরি হবে)

# Nano Shortcuts (নিচে দেখায়):
# Ctrl + O → Save (Write Out)
# Ctrl + X → Exit
# Ctrl + K → Line cut
# Ctrl + U → Paste
# Ctrl + W → Search
# Ctrl + \ → Find and replace
# Ctrl + G → Help
# Alt + U  → Undo
# Ctrl + _ → Go to line number
```

### Vim — Professional Editor (অবশ্যই শিখুন!)

```bash
# vim install (Ubuntu তে vi/vim থাকে)
sudo apt install vim

# Vim খুলুন
vim file.txt

# ═══════════════════════════════════
# Vim এর ৩টি Mode (সবচেয়ে গুরুত্বপূর্ণ concept!)
# ═══════════════════════════════════
#
# 1. NORMAL MODE (default) — Navigation ও commands
#    Vim খুললেই Normal mode এ থাকে
#
# 2. INSERT MODE — Text লেখা
#    Normal mode এ "i" চাপলে Insert mode
#    Esc চাপলে Normal mode এ ফিরে আসে
#
# 3. COMMAND MODE — Save, quit, search
#    Normal mode এ ":" চাপলে Command mode
#
# ═══════════════════════════════════

# === Normal Mode Commands ===

# Navigation:
# h = বামে, j = নিচে, k = উপরে, l = ডানে
# gg = File এর শুরুতে
# G  = File এর শেষে
# 0  = Line এর শুরুতে
# $  = Line এর শেষে
# w  = পরের word এ
# b  = আগের word এ

# Edit:
# x  = একটি character delete
# dd = পুরো line delete (cut)
# yy = পুরো line copy
# p  = paste (নিচে)
# P  = paste (উপরে)
# u  = undo
# Ctrl+r = redo
# dw = word delete
# D  = cursor থেকে line শেষ পর্যন্ত delete

# Insert Mode এ ঢোকার উপায়:
# i = cursor এর আগে insert
# I = line এর শুরুতে insert
# a = cursor এর পরে insert
# A = line এর শেষে insert
# o = নতুন line নিচে তৈরি করে insert
# O = নতুন line উপরে তৈরি করে insert

# === Command Mode (: চাপুন) ===
# :w          → Save
# :q          → Quit
# :wq         → Save and Quit
# :q!         → Quit without saving (force!)
# :x          → Save and Quit (shortcut)
# ZZ          → Save and Quit (Normal mode থেকে)
# :%s/old/new/g → Find and Replace (সব)
# :set number  → Line numbers দেখান
# :set nonumber → Line numbers বন্ধ
# /search-term → Text search (n = next, N = previous)
```

### Vim Survival Guide (মুখস্ত করুন!)

```
1. vim file.txt     → File খুলুন
2. i                → Insert mode (লেখা শুরু)
3. [Type your text]
4. Esc              → Normal mode এ ফিরুন
5. :wq              → Save and quit
```

**Vim এ আটকে গেলে:**

- `Esc` চাপুন (একাধিকবার চাপুন)
- `:q!` লিখে Enter চাপুন (save না করে বের হবেন)

### vimtutor — Vim শেখার সেরা উপায়

```bash
vimtutor              # Built-in interactive tutorial!
# এটা ৩০ মিনিটের tutorial — অবশ্যই complete করুন!
```

### 📝 Practice (Phase 2.7)

1. `nano test-nano.txt` → কিছু লিখুন → Ctrl+O save → Ctrl+X exit
2. `vim test-vim.txt` → `i` → কিছু লিখুন → Esc → `:wq`
3. `vimtutor` চালান এবং Lesson 1, 2 complete করুন
4. Vim এ `/search` দিয়ে text search practice করুন
5. Vim এ `dd` দিয়ে line delete, `u` দিয়ে undo, `yy` + `p` দিয়ে copy-paste practice
6. `vim /etc/hostname` দিয়ে read-only file দেখুন (`:q!` দিয়ে exit — edit করবেন না!)

---

---

# 📙 Section 3: System Administration

> **🎯 এই Section এর লক্ষ্য:** Linux system manage করা শেখা — users, processes, services, disks, packages, logs, scheduled tasks। এগুলো জানলে আপনি একজন **Linux System Administrator** হিসেবে কাজ করতে পারবেন।
>
> **⏱ আনুমানিক সময়:** ২-৩ সপ্তাহ (প্রতিদিন ২-৩ ঘণ্টা)
>
> **🔮 Future Path Connection:** DevOps এবং AWS Server Management এর core skill। Server maintain, deploy, monitor — সবকিছুতে এই knowledge লাগবে।

---

## Phase 3.1: User ও Group Management

> **🎯 Why This Matters:** Server এ multiple users থাকে। কে কি access পাবে তা নিয়ন্ত্রণ করতে user/group management জানতে হবে। AWS EC2 তে user create, SSH access দেওয়া — এসব daily task।

### User Information Files

```bash
# গুরুত্বপূর্ণ system files:
cat /etc/passwd    # সব users এর list
# Format: username:x:UID:GID:comment:home_dir:shell
# omar:x:1000:1000:Omar Faruk:/home/omar:/bin/bash

cat /etc/shadow    # Password hashes (restricted! sudo লাগবে)
sudo cat /etc/shadow

cat /etc/group     # সব groups এর list
# Format: group_name:x:GID:members

cat /etc/sudoers   # কারা sudo ব্যবহার করতে পারে
sudo cat /etc/sudoers
```

### User Management Commands

```bash
# ── whoami — Current user ──
whoami                             # আপনার username

# ── id — User details ──
id                                 # UID, GID, groups দেখুন
id omar                            # নির্দিষ্ট user এর details

# ── useradd — নতুন user তৈরি ──
# কাজ: System এ নতুন user account তৈরি করে
sudo useradd devuser               # Basic user তৈরি (home dir ছাড়া)
sudo useradd -m devuser            # -m: Home directory সহ তৈরি
sudo useradd -m -s /bin/bash devuser  # -s: Shell specify (bash)
sudo useradd -m -s /bin/bash -c "Developer User" devuser  # -c: Comment/full name
sudo useradd -m -G sudo,docker devuser  # -G: Groups এ add করো

# ── adduser — Interactive user creation (সহজতর) ──
sudo adduser newuser               # Interactive: password, name সব চাইবে

# ── passwd — Password পরিবর্তন ──
passwd                             # নিজের password পরিবর্তন
sudo passwd devuser                # অন্য user এর password

# ── usermod — User modify ──
# কাজ: Existing user এর settings পরিবর্তন করে
sudo usermod -aG sudo devuser      # -aG: sudo group এ add (-a = append!)
sudo usermod -aG docker devuser    # Docker group এ add
sudo usermod -s /bin/zsh devuser   # Shell পরিবর্তন
sudo usermod -L devuser            # -L: Account lock
sudo usermod -U devuser            # -U: Account unlock
# ⚠️ -aG তে -a না দিলে আগের groups মুছে যাবে!

# ── userdel — User delete ──
sudo userdel devuser               # User delete (home dir থাকবে)
sudo userdel -r devuser            # -r: Home directory সহ delete

# ── su — Switch User ──
su - devuser                       # অন্য user হিসেবে login
su -                               # Root user হিসেবে login
exit                               # আগের user এ ফিরে আসুন
```

### Group Management

```bash
# ── groupadd — Group তৈরি ──
sudo groupadd developers           # নতুন group
sudo groupadd -g 1500 webteam      # -g: specific GID সহ

# ── groupdel — Group delete ──
sudo groupdel developers

# ── gpasswd — Group member management ──
sudo gpasswd -a omar developers    # -a: user add to group
sudo gpasswd -d omar developers    # -d: user remove from group

# User এর groups দেখুন
groups                             # নিজের groups
groups omar                        # নির্দিষ্ট user এর groups
```

### sudo Configuration

```bash
# sudo access দেওয়া
sudo usermod -aG sudo username     # sudo group এ add

# sudoers file edit (safe way!)
sudo visudo                        # ⚠️ সরাসরি nano/vim দিয়ে edit করবেন না!
# যোগ করুন:
# devuser ALL=(ALL:ALL) ALL        # Full sudo access
# devuser ALL=(ALL) NOPASSWD: ALL  # Password ছাড়া sudo (⚠️ risky)

# Sudo session
sudo -i                            # Root shell (interactive)
sudo -s                            # Root shell (same directory)
sudo -k                            # Sudo session expire করুন
```

### 📝 Practice (Phase 3.1)

1. `whoami` → `id` → আপনার user info দেখুন
2. `cat /etc/passwd | cut -d':' -f1` → সব users দেখুন
3. `groups` → আপনার groups দেখুন
4. `sudo adduser testuser` → নতুন user তৈরি করুন
5. `su - testuser` → switch করুন → `whoami` → `exit`
6. `sudo userdel -r testuser` → user delete করুন
7. `sudo visudo` → sudoers file দেখুন (edit না করে `:q!` exit)

---

## Phase 3.2: Process Management

> **🎯 Why This Matters:** Server hang হলে, কোনো app crash করলে, resource বেশি খাচ্ছে — process manage করা জানতে হবে। DevOps এ application monitoring, Cyber Security তে suspicious process detect — সব process management।

### Process কি?

Process হলো একটি running program। যখন আপনি কোনো command বা app চালান, সেটা একটি process হিসেবে run হয় এবং একটি unique **PID (Process ID)** পায়।

### Process দেখা

```bash
# ── ps — Process Status ──
# কাজ: Running processes দেখায়
ps                                 # শুধু current terminal এর processes
ps aux                             # ALL processes (সবচেয়ে বেশি ব্যবহৃত!)
#  a = all users
#  u = user-friendly format
#  x = processes without terminal

# ps aux output:
# USER  PID %CPU %MEM  VSZ  RSS TTY STAT START TIME COMMAND
# root    1  0.0  0.1 16844 4788 ?   Ss   10:00 0:01 /sbin/init

ps aux | grep nginx                # নির্দিষ্ট process খুঁজুন
ps aux | sort -nrk 3 | head -10   # Top 10 CPU-hungry processes
ps aux | sort -nrk 4 | head -10   # Top 10 Memory-hungry processes
ps -ef                             # Full format listing
ps -u omar                        # নির্দিষ্ট user এর processes

# ── top — Real-time process monitor ──
# কাজ: Live CPU, memory, process information দেখায়
top
# Shortcuts:
#  P = CPU sort
#  M = Memory sort
#  k = PID দিয়ে process kill
#  q = quit
#  h = help

# ── htop — Better process monitor (install করুন!) ──
sudo apt install htop
htop
# Features: Color coded, mouse support, tree view
# F3 = Search, F5 = Tree view, F9 = Kill, F10 = Quit

# ── pgrep — Process ID search ──
pgrep firefox                      # Firefox এর PID(s)
pgrep -u omar                     # User এর সব PIDs
```

### Process Control

```bash
# ── kill — Process বন্ধ করুন ──
# কাজ: PID দিয়ে process terminate/kill করে
kill PID                           # Graceful termination (SIGTERM)
kill -9 PID                        # Force kill (SIGKILL) — emergency!
kill -15 PID                       # Normal termination (SIGTERM)

# ── killall — নাম দিয়ে kill ──
killall firefox                    # সব firefox processes kill
killall -9 firefox                 # Force kill all firefox

# ── pkill — Pattern দিয়ে kill ──
pkill firefox                      # firefox নামে match করা processes
pkill -u testuser                  # User এর সব processes kill

# ── Signals (গুরুত্বপূর্ণ) ──
# SIGTERM (15) — Graceful stop (default, cleanup করে বন্ধ হয়)
# SIGKILL (9)  — Immediate stop (force, cleanup করে না)
# SIGSTOP (19) — Pause
# SIGCONT (18) — Resume
# SIGHUP (1)   — Restart/reload config
```

### Background ও Foreground

```bash
# ── Background এ command চালানো ──
long_command &                     # & = background এ চালাও
sleep 100 &                        # Example

# ── jobs — Background jobs দেখুন ──
jobs                               # Running background jobs

# ── fg — Foreground এ আনুন ──
fg                                 # Last background job foreground এ
fg %1                              # Job #1 foreground এ

# ── bg — Paused job কে background এ চালান ──
# Step 1: Ctrl+Z (running command pause হবে)
# Step 2: bg (background এ resume)

# ── nohup — Terminal বন্ধ করলেও চলবে ──
# কাজ: Terminal close করলেও process চলতে থাকবে
nohup long_command &               # Background + terminal-independent
nohup ./script.sh > output.log 2>&1 &  # Output file এ save

# ── nice / renice — Priority set করুন ──
# কাজ: Process এর CPU priority নির্ধারণ (-20 highest to 19 lowest)
nice -n 10 command                 # Low priority তে চালান
sudo renice -5 -p PID             # Running process এর priority পরিবর্তন
```

### 📝 Practice (Phase 3.2)

1. `ps aux | head -10` → process list দেখুন, columns বুঝুন
2. `ps aux | grep "bash"` → আপনার bash sessions খুঁজুন
3. `top` চালান → `P` (CPU sort) → `M` (Memory sort) → `q` (quit)
4. `htop` install ও চালান → F5 (tree view) → F10 (quit)
5. `sleep 300 &` → `jobs` → `fg` → `Ctrl+C`
6. `pgrep bash` → bash PID(s) দেখুন
7. `ps aux | sort -nrk 3 | head -5` → top CPU processes

---

## Phase 3.3: Service Management (systemd)

> **🎯 Why This Matters:** Modern Linux এর service management system হলো **systemd**। Nginx, MySQL, Docker, SSH — সব services systemd দিয়ে manage হয়। AWS EC2 তে app deploy করতে, server services manage করতে — systemd essential।

### systemd কি?

systemd হলো Linux এর **init system** এবং **service manager**। Computer boot হলে systemd সব services start করে এবং manage করে।

### systemctl — Service Control

```bash
# ── systemctl — Service manage করুন ──
# কাজ: Services start, stop, enable, disable, check status

# Service Status চেক
sudo systemctl status nginx        # Nginx এর status
sudo systemctl status ssh          # SSH service status
sudo systemctl status docker       # Docker status
# Output এ দেখবেন:
#  Active: active (running) ← চলছে
#  Active: inactive (dead)  ← বন্ধ
#  Active: failed           ← error হয়ে বন্ধ

# Service Start / Stop / Restart
sudo systemctl start nginx         # Service চালু করুন
sudo systemctl stop nginx          # Service বন্ধ করুন
sudo systemctl restart nginx       # Restart (stop + start)
sudo systemctl reload nginx        # Config reload (বন্ধ না করে)

# Boot এ Auto-start
sudo systemctl enable nginx        # Boot এ automatically চালু হবে
sudo systemctl disable nginx       # Boot এ চালু হবে না
sudo systemctl enable --now nginx  # Enable + immediate start

# Service List
systemctl list-units --type=service              # সব running services
systemctl list-units --type=service --state=running  # শুধু running
systemctl list-unit-files --type=service         # সব services (enabled/disabled)
systemctl list-units --failed                     # Failed services

# Service কি enabled?
systemctl is-enabled nginx
systemctl is-active nginx
```

### journalctl — System Logs (systemd logs)

```bash
# ── journalctl — System log viewer ──
# কাজ: systemd services এর logs দেখায়

sudo journalctl                    # সব logs
sudo journalctl -u nginx           # নির্দিষ্ট service এর logs
sudo journalctl -u nginx -f        # Live logs (tail -f এর মতো)
sudo journalctl -u nginx --since "1 hour ago"  # শেষ ১ ঘণ্টা
sudo journalctl -u nginx --since today         # আজকের logs
sudo journalctl -u nginx -n 50    # শেষ ৫০ lines
sudo journalctl -p err            # শুধু errors
sudo journalctl -b                # Last boot থেকে logs
sudo journalctl --disk-usage      # Log size দেখুন
```

### Custom Service তৈরি (Advanced)

```bash
# নিজের application কে service হিসেবে চালান
sudo nano /etc/systemd/system/myapp.service

# Content:
# [Unit]
# Description=My Node.js Application
# After=network.target
#
# [Service]
# Type=simple
# User=omar
# WorkingDirectory=/home/omar/myapp
# ExecStart=/usr/bin/node server.js
# Restart=on-failure
# RestartSec=10
#
# [Install]
# WantedBy=multi-user.target

# Service register ও চালু
sudo systemctl daemon-reload       # নতুন service file load
sudo systemctl enable myapp        # Boot এ auto-start
sudo systemctl start myapp         # চালু করুন
sudo systemctl status myapp        # Status check
```

### 📝 Practice (Phase 3.3)

1. `sudo systemctl status ssh` → SSH service status দেখুন
2. `systemctl list-units --type=service --state=running` → running services
3. `sudo journalctl -u ssh -n 20` → SSH logs দেখুন
4. `systemctl is-enabled ssh` → SSH enabled কিনা check
5. `systemctl list-units --failed` → failed services দেখুন
6. `sudo journalctl --disk-usage` → log size
7. `systemctl list-unit-files --type=service | grep enabled | wc -l` → enabled services count

---

## Phase 3.4: Disk ও Storage Management

> **🎯 Why This Matters:** Server এ disk full হলে application crash করে। AWS EBS volume manage, partition, mount — সব জানতে হবে। DevOps এ storage monitoring critical।

### Disk Information

```bash
# ── df — Disk Free space ──
# কাজ: Filesystem এর available space দেখায়
df -h                              # -h: Human readable (KB, MB, GB)
df -h /                            # Root partition
df -h /home                        # Home partition
df -hT                             # -T: Filesystem type সহ

# ── du — Disk Usage ──
# কাজ: File/directory কতটুকু space নিচ্ছে দেখায়
du -sh ~/Documents                 # -s: summary, -h: human readable
du -sh /var/log                    # Log folder size
du -sh ~/*                         # Home এর প্রতিটি folder
du -ah ~ | sort -rh | head -20    # সবচেয়ে বড় files/folders

# ── lsblk — Block devices list ──
# কাজ: সব disks/partitions দেখায়
lsblk                              # All block devices
lsblk -f                           # Filesystem info সহ

# ── fdisk — Partition info ──
sudo fdisk -l                      # সব disk ও partition details
sudo fdisk -l /dev/sda             # নির্দিষ্ট disk
```

### Mount / Unmount

```bash
# ── mount — Device/partition attach করুন ──
# কাজ: Disk/partition কে filesystem এ connect করে
mount                              # সব mounted filesystems দেখুন
sudo mount /dev/sdb1 /mnt          # USB/disk mount
sudo mount /dev/sdb1 /mnt/usb     # নির্দিষ্ট folder এ mount

# ── umount — Unmount (safely remove) ──
sudo umount /mnt                   # Unmount
sudo umount /dev/sdb1              # Device দিয়ে unmount

# Permanent mount (boot এ automatic mount)
# /etc/fstab file edit করুন:
sudo blkid                         # UUID দেখুন
sudo nano /etc/fstab
# যোগ করুন:
# UUID=xxxx-xxxx /mnt/data ext4 defaults 0 2
```

### Swap Management

```bash
# Swap কি? — RAM ভরে গেলে disk কে temporary RAM হিসেবে ব্যবহার
swapon --show                      # Swap info
free -h                            # RAM + Swap দেখুন

# Swap file তৈরি (AWS EC2 তে প্রায়ই লাগে!)
sudo fallocate -l 2G /swapfile     # 2GB swap file তৈরি
sudo chmod 600 /swapfile           # Permission set
sudo mkswap /swapfile              # Swap format
sudo swapon /swapfile              # Swap activate

# Permanent swap (reboot এও থাকবে)
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# Swappiness (কখন swap ব্যবহার করবে)
cat /proc/sys/vm/swappiness        # Current value (default 60)
sudo sysctl vm.swappiness=10       # SSD তে 10 recommended
# Permanent: echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
```

### LVM Basics (Logical Volume Management)

```bash
# LVM কি? — Flexible disk management system
# Physical Volume (PV) → Volume Group (VG) → Logical Volume (LV)
# AWS EBS resize করতে LVM জ্ঞান লাগে

# LVM info দেখুন
sudo pvs                           # Physical Volumes
sudo vgs                           # Volume Groups
sudo lvs                           # Logical Volumes
sudo lvdisplay                     # Detailed LV info
```

### 📝 Practice (Phase 3.4)

1. `df -h` → disk space দেখুন, কোন partition কতটুকু used
2. `du -sh ~/*` → home folders এর size
3. `du -ah ~ | sort -rh | head -10` → biggest files
4. `lsblk` → সব disks/partitions
5. `free -h` → RAM ও Swap usage
6. `swapon --show` → Swap details
7. `cat /proc/sys/vm/swappiness` → swappiness value

---

## Phase 3.5: Package Management (Advanced)

> **🎯 Why This Matters:** শুধুমাত্র `apt install` জানলে হবে না। Dependency সমস্যা সমাধান করা, custom repository (PPA) manage করা, এবং underlying system (`dpkg`) বোঝা একজন sysadmin বা DevOps engineer এর জন্য আবশ্যিক।

### APT Internals (কিভাবে কাজ করে)

- **Config Files:** `/etc/apt/sources.list` এবং `/etc/apt/sources.list.d/`
- **Cache:** `/var/lib/apt/lists/` (package lists) এবং `/var/cache/apt/archives/` (downloaded .deb files)

```bash
# ── Repository Management ──
# Repository list এ নতুন source যোগ করা
sudo add-apt-repository ppa:obsproject/obs-studio
sudo apt update

# Repository remove করা
sudo add-apt-repository --remove ppa:obsproject/obs-studio

# ── Troubleshooting APT ──
# Broken dependencies fix করা
sudo apt --fix-broken install

# Configure unfinished packages
sudo dpkg --configure -a

# Clear locks (যদি অন্য process apt ব্যবহার করে আটকে থাকে)
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock*

# ── Advanced searching ──
# শুধু installed packages এর মধ্যে খোঁজা
apt list --installed | grep nginx

# নির্দিষ্ট file কোন package থেকে এসেছে তা বের করা
sudo apt install apt-file
sudo apt-file update
apt-file search /etc/nginx/nginx.conf
```

### dpkg — Low-level Package Tool

`apt` আসলে `dpkg` এর উপরে কাজ করে। সরাসরি `.deb` file handle করতে এটি লাগে।

```bash
# .deb file install
sudo dpkg -i package_name.deb

# Package list দেখা
dpkg -l | grep nginx

# Package এর সব files এর list দেখা
dpkg -L nginx

# Install করা package remove (config থাকে)
sudo dpkg -r package_name

# Package পুরোপুরি remove (purge)
sudo dpkg -P package_name
```

---

## Phase 3.6: System Monitoring & Performance

> **🎯 Why This Matters:** Server slow হলে বা crash করলে bottleneck কোথায় সেটা খুঁজে বের করা একজন DevOps বা Admin এর প্রধান কাজ। CPU, RAM, Disk I/O, Network — এই ৪টি জিনিসের health monitor করতে জানতে হবে।

### Real-time Monitoring

```bash
# ── Resources Check ──
# CPU ও overall load (top এর আধুনিক বিকল্প)
sudo apt install htop
htop

# RAM usage (Human readable)
free -h

# Disk Space
df -h

# Disk I/O (Disk কি slow কাজ করছে?)
sudo apt install sysstat
iostat -xz 1

# Network Usage (Real-time bandwidth)
sudo apt install nethogs
sudo nethogs eth0  # specific interface
```

### Performance Analysis Tools

```bash
# ── uptime ──
# কতক্ষণ ধরে server চলছে এবং load average কত
uptime
# Load average: 0.05, 0.03, 0.01 (1, 5, 15 minute average)

# ── vmstat ──
# Virtual memory, processes, paging, trap ও CPU activity
vmstat 1 5  # প্রতি ১ সেকেন্ডে ৫ বার update

# ── lsof ──
# List of Open Files (কোন app কোন file ব্যবহার করছে)
lsof -i :80         # Port 80 কে ব্যবহার করছে
lsof -u omar        # omar user এর open files

# ── dmesg ──
# Kernel ring buffer (Hardware বা boot errors দেখার জন্য সেরা)
dmesg | tail -20
dmesg | grep -i "error"
```

---

## Phase 3.7: Log Management

> **🎯 Why This Matters:** Linux এ যা কিছু ঘটে তার প্রমাণ থাকে Logs এ। Troubleshoot করার জন্য log পড়া শিখলে আপনি অর্ধেক সমস্যা নিজেই সমাধান করতে পারবেন। AWS CloudWatch বা ELK stack এর foundation হলো এই logs।

### গুরুত্বপূর্ণ Log Locations (`/var/log/`)

| Log File            | কি থাকে                                   |
| ------------------- | ----------------------------------------- |
| `/var/log/syslog`   | General system messages (central log)     |
| `/var/log/auth.log` | Login, sudo, and authentication events    |
| `/var/log/dmesg`    | Kernel ring buffer (hardware/driver info) |
| `/var/log/apache2/` | Apache web server logs                    |
| `/var/log/nginx/`   | Nginx web server logs                     |
| `/var/log/mysql/`   | MySQL database logs                       |

### Logs দেখার পদ্ধতি

```bash
# Real-time log monitoring (Golden Command!)
tail -f /var/log/syslog

# Error খোঁজা
grep -i "error" /var/log/syslog

# ── logrotate ──
# Logs যেন disk full না করে দেয় সেজন্য automatic compress/delete করে
cat /etc/logrotate.conf
```

---

## Phase 3.8: Cron Jobs & Task Scheduling

> **🎯 Why This Matters:** DevOps এর মানেই automation। প্রতিদিন রাত ১২টায় backup নেওয়া, প্রতি রবিবার system update করা — এই automation গুলো Cron দিয়ে করা হয়।

### Crontab — Task Schedule করা

```bash
# User এর crontab file edit করা
crontab -e

# Crontab এর Syntax:
# * * * * * command_to_execute
# │ │ │ │ │
# │ │ │ │ └── Day of week (0-6) (Sunday=0)
# │ │ │ └──── Month (1-12)
# │ │ └────── Day of month (1-31)
# │ └──────── Hour (0-23)
# └────────── Minute (0-59)
```

### প্রয়োজনীয় Cron উদাহরণ

```bash
# প্রতিদিন রাত ৩টায় backup script চালানো
0 3 * * * /home/omar/scripts/backup.sh

# প্রতি রবিবার ভোর ৪টায় system update ও upgrade
0 4 * * 0 sudo apt update && sudo apt upgrade -y

# প্রতি ১৫ মিনিট অন্তর log clean করা
*/15 * * * * /path/to/script.sh

# Boot হওয়ার সময় চালানো
@reboot /home/omar/my_app.sh
```

### Crontab Management

```bash
# Crontab list দেখা
crontab -l

# Crontab পুরোপুরি মুছে ফেলা (⚠️ সাবধান!)
crontab -r
```

### 📝 Practice (Section 3)

1. একটি নতুন user তৈরি করুন `sudo adduser developer` এবং তাকে `sudo` group এ add করুন।
2. `htop` চালিয়ে দেখুন কোন process সবচেয়ে বেশি RAM নিচ্ছে।
3. একটি background process (`sleep 500 &`) চালান এবং `kill` command দিয়ে তাকে বন্ধ করুন।
4. একটা cron job তৈরি করুন যেটা প্রতি মিনিটে একটা output file এ current time এবং date লিখে রাখবে। (`date >> ~/time_log.txt`)
5. `/var/log/auth.log` check করে দেখুন কেউ ভুল password দিয়ে login করার চেষ্টা করেছে কিনা।

---

---

# 📕 Section 4: Networking ও Security

> **🎯 এই Section এর লক্ষ্য:** Linux networking বোঝা এবং system secure করা। যেকোনো server internet এ connected, তাই networking ও security জ্ঞান ছাড়া server manage করা বিপদজনক।
>
> **⏱ আনুমানিক সময়:** ২-৩ সপ্তাহ (প্রতিদিন ২-৩ ঘণ্টা)
>
> **🔮 Future Path Connection:** Cyber Security এর মূল ভিত্তি। AWS Security Groups, VPC, firewall — সব এখান থেকে শুরু। DevOps এ container networking, service discovery — সবকিছুতে networking লাগে।

---

## Phase 4.1: Networking Fundamentals

> **🎯 Why This Matters:** Server কিভাবে internet এ কাজ করে, IP address কি, port কি — এগুলো না বুঝলে SSH, firewall, AWS VPC কিছুই বুঝবেন না।

### Network Basics

```
Internet কিভাবে কাজ করে (simplified):

আপনার PC ──→ Router ──→ ISP ──→ Internet ──→ Server (AWS EC2)

প্রতিটি device এর একটি unique IP address থাকে, এবং
প্রতিটি service একটি port number ব্যবহার করে।
```

### IP Address

```bash
# IP Address = Network এ device এর address
# দুই ধরনের:
#   IPv4: 192.168.1.100 (32-bit, সবচেয়ে বেশি ব্যবহৃত)
#   IPv6: 2001:0db8:85a3::8a2e:0370:7334 (128-bit, নতুন)

# Private IP ranges (LAN/Internal network):
#   10.0.0.0    - 10.255.255.255    (Class A)
#   172.16.0.0  - 172.31.255.255    (Class B — AWS VPC default!)
#   192.168.0.0 - 192.168.255.255   (Class C — Home router)

# Public IP: Internet এ unique address (ISP দেয়)
# Loopback: 127.0.0.1 (localhost — নিজের machine)
```

### গুরুত্বপূর্ণ Port Numbers (মুখস্ত করুন!)

| Port  | Service    | কাজ                                     |
| ----- | ---------- | --------------------------------------- |
| 22    | SSH        | Remote login (⭐ সবচেয়ে বেশি ব্যবহৃত!) |
| 80    | HTTP       | Web traffic (non-secure)                |
| 443   | HTTPS      | Web traffic (secure/SSL)                |
| 21    | FTP        | File transfer                           |
| 25    | SMTP       | Email sending                           |
| 53    | DNS        | Domain name resolution                  |
| 3306  | MySQL      | MySQL database                          |
| 5432  | PostgreSQL | PostgreSQL database                     |
| 3000  | Dev Server | React/Node dev (custom)                 |
| 8080  | Alt HTTP   | Alternative web port                    |
| 27017 | MongoDB    | MongoDB database                        |

### TCP vs UDP

```
TCP (Transmission Control Protocol):
  - Reliable: Data lost হলে আবার পাঠায়
  - Ordered: ক্রমানুসারে আসে
  - ব্যবহার: HTTP, SSH, FTP, Email
  - ধীর কিন্তু নির্ভরযোগ্য

UDP (User Datagram Protocol):
  - Unreliable: Data lost হলে আবার পাঠায় না
  - Unordered: যেকোনো ক্রমে আসতে পারে
  - ব্যবহার: DNS, Video streaming, Gaming
  - দ্রুত কিন্তু data loss হতে পারে
```

### DNS (Domain Name System)

```bash
# DNS = Domain name কে IP address এ convert করে
# google.com → 142.250.185.46

# DNS resolution order:
# 1. /etc/hosts (local file)
# 2. DNS server (/etc/resolv.conf)
# 3. ISP DNS → Root DNS → TLD DNS → Auth DNS

# Local hosts file দেখুন/edit করুন
cat /etc/hosts
sudo nano /etc/hosts
# Custom entry যোগ করুন:
# 192.168.1.50  myserver.local

# DNS server config
cat /etc/resolv.conf

# DNS lookup tools
nslookup google.com                # Domain → IP
dig google.com                     # Detailed DNS info
dig google.com +short              # শুধু IP
host google.com                    # Simple lookup
```

### 📝 Practice (Phase 4.1)

1. আপনার computer এর IP address লিখুন (private ও public আলাদা করুন)
2. `cat /etc/hosts` → local DNS entries দেখুন
3. `dig google.com +short` → Google এর IP দেখুন
4. `nslookup facebook.com` → Facebook এর DNS info
5. Port number chart থেকে ৫টি port মুখস্ত করুন (22, 80, 443, 3306, 27017)

---

## Phase 4.2: Network Configuration ও Tools

> **🎯 Why This Matters:** Server এর IP configure করা, network troubleshoot করা — DevOps ও AWS admin এর দৈনন্দিন কাজ।

### Network Interface দেখা ও Configure

```bash
# ── ip — Modern network tool (ifconfig এর replacement) ──
# কাজ: Network interface, IP address, routing দেখা ও configure করা

# IP address দেখুন
ip addr show                       # সব interfaces (বা ip a)
ip addr show eth0                  # নির্দিষ্ট interface
# Output এ গুরুত্বপূর্ণ:
#   inet 192.168.1.100/24 ← IPv4 address
#   ether aa:bb:cc:dd:ee:ff ← MAC address
#   state UP ← Interface active

# ── ifconfig — Legacy tool (এখনো ব্যবহৃত) ──
sudo apt install net-tools
ifconfig                           # সব interfaces
ifconfig eth0                      # নির্দিষ্ট interface

# Network interface up/down
sudo ip link set eth0 up           # Interface চালু
sudo ip link set eth0 down         # Interface বন্ধ

# Temporary IP assign (reboot এ চলে যায়)
sudo ip addr add 192.168.1.200/24 dev eth0

# Routing table দেখুন
ip route show                      # বা ip r
# default via 192.168.1.1 ← Gateway (router)
```

### Network Testing Tools

```bash
# ── ping — Connectivity test ──
# কাজ: কোনো host reachable কিনা check করে
ping google.com                    # Continuous ping (Ctrl+C exit)
ping -c 4 google.com               # -c 4: শুধু ৪ বার ping
ping -c 4 192.168.1.1              # Gateway/router ping
# Output:
# 64 bytes from 142.250.185.46: icmp_seq=1 ttl=117 time=12.3 ms
#  time = latency (কম = ভালো)
#  ttl = Time To Live

# ── traceroute — Path দেখুন ──
# কাজ: Packet কোন কোন router দিয়ে যাচ্ছে দেখায়
sudo apt install traceroute
traceroute google.com

# ── mtr — ping + traceroute combined ──
sudo apt install mtr
mtr google.com                     # Real-time path analysis

# ── wget — File download ──
wget https://example.com/file.zip
wget -O custom-name.zip https://example.com/file.zip  # Custom filename
wget -c https://example.com/big-file.zip  # -c: Resume download

# ── curl — URL request ──
# কাজ: HTTP request পাঠায় (API test এ অনেক ব্যবহৃত!)
curl https://api.ipify.org         # আপনার public IP দেখুন
curl -I https://google.com         # -I: শুধু headers
curl -o file.html https://google.com  # Download
curl -X POST -d "data=value" https://api.example.com  # POST request
```

### Network Status ও Connections

```bash
# ── ss — Socket Statistics (netstat এর replacement) ──
# কাজ: Active connections ও listening ports দেখায়
ss -tlnp                           # TCP listening ports সহ process
#  -t = TCP
#  -l = Listening
#  -n = Numeric (port name না, number)
#  -p = Process name

ss -ulnp                           # UDP listening ports
ss -tunap                          # সব connections (established + listening)

# ── netstat — Legacy but still useful ──
sudo apt install net-tools
netstat -tlnp                      # TCP listening ports
netstat -an                        # সব connections

# কোন process কোন port ব্যবহার করছে
sudo lsof -i :80                   # Port 80
sudo lsof -i :3000                 # Port 3000

# নির্দিষ্ট port available কিনা
sudo ss -tlnp | grep ":80"
```

### 📝 Practice (Phase 4.2)

1. `ip addr show` → আপনার IP address ও interfaces দেখুন
2. `ping -c 4 google.com` → connectivity check
3. `curl https://api.ipify.org` → public IP
4. `ss -tlnp` → কোন ports open আছে দেখুন
5. `traceroute google.com` → path trace
6. `ip route show` → routing table ও default gateway
7. `dig bangla.bdnews24.com +short` → DNS lookup practice

---

## Phase 4.3: SSH (Secure Shell)

> **🎯 Why This Matters:** SSH হলো remote server access এর **সবচেয়ে গুরুত্বপূর্ণ tool**। AWS EC2 তে connect, GitHub/GitLab এ push, server manage — সবকিছু SSH দিয়ে হয়। SSH ছাড়া server admin অসম্ভব।

### SSH কি?

SSH (Secure Shell) হলো encrypted protocol যা দিয়ে আপনি remote server এ safely login করতে পারেন। Password বা key-based authentication ব্যবহার করে।

### SSH Client (অন্য server এ connect)

```bash
# ── ssh — Remote login ──
# Basic syntax: ssh username@server-ip
ssh omar@192.168.1.50              # Password দিয়ে login
ssh omar@myserver.com              # Hostname দিয়ে
ssh -p 2222 omar@server.com        # -p: Custom port (default 22)

# AWS EC2 তে connect (key file দিয়ে):
ssh -i ~/.ssh/my-key.pem ubuntu@ec2-xx-xx-xx-xx.compute.amazonaws.com
# -i = identity file (private key)
# ubuntu = EC2 এর default user

# ── Remote command execution ──
# Login না করে command চালান:
ssh omar@server "ls -la /var/www"
ssh omar@server "df -h && free -h"

# ── scp — Secure Copy (SSH দিয়ে file transfer) ──
# কাজ: Local ↔ Remote server এ file copy করে
# Local → Remote:
scp file.txt omar@server:/home/omar/
scp -r folder/ omar@server:/home/omar/  # -r: Directory copy

# Remote → Local:
scp omar@server:/var/log/syslog ./
scp -r omar@server:/home/omar/project ./

# ── rsync — Better file sync (scp এর চেয়ে smart!) ──
# কাজ: শুধু changed files copy করে (bandwidth বাঁচায়)
rsync -avz folder/ omar@server:/backup/
#  -a = archive (permissions, timestamps রাখে)
#  -v = verbose
#  -z = compress (faster transfer)
rsync -avz --delete source/ omar@server:/dest/  # --delete: source এ নেই = dest থেকে delete
```

### SSH Key-based Authentication (⭐ অবশ্যই শিখুন!)

Password এর চেয়ে key-based authentication **অনেক বেশি secure** এবং **সুবিধাজনক** (password টাইপ করতে হয় না)।

```bash
# Step 1: SSH Key Pair তৈরি করুন
ssh-keygen -t ed25519 -C "omar@example.com"
# -t ed25519: Algorithm (সবচেয়ে secure ও দ্রুত)
# -C: Comment (আপনার email)
# Enter চাপুন → default location (~/.ssh/id_ed25519)
# Passphrase: optional but recommended

# Key pair তৈরি হবে:
# ~/.ssh/id_ed25519       ← Private key (⛔ কাউকে দেবেন না!)
# ~/.ssh/id_ed25519.pub   ← Public key (server এ দেবেন)

# Step 2: Public key server এ copy করুন
ssh-copy-id omar@server
# বা manually:
cat ~/.ssh/id_ed25519.pub | ssh omar@server "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

# Step 3: এখন password ছাড়া login!
ssh omar@server                    # No password needed!

# Key permissions (⚠️ গুরুত্বপূর্ণ! Wrong permission এ SSH কাজ করবে না!)
chmod 700 ~/.ssh                   # Directory
chmod 600 ~/.ssh/id_ed25519        # Private key
chmod 644 ~/.ssh/id_ed25519.pub    # Public key
chmod 600 ~/.ssh/authorized_keys   # Authorized keys (server এ)
```

### SSH Server Configuration

```bash
# SSH server config file:
sudo nano /etc/ssh/sshd_config

# গুরুত্বপূর্ণ settings:
# Port 22                          # Custom port (e.g., 2222) — security!
# PermitRootLogin no               # ⚠️ Root login বন্ধ করুন!
# PasswordAuthentication no        # ⚠️ শুধু key-based login (server secure করুন!)
# MaxAuthTries 3                   # Max login attempts
# PubkeyAuthentication yes         # Key-based auth চালু

# Config পরিবর্তনের পরে restart:
sudo systemctl restart ssh
# বা
sudo systemctl restart sshd
```

### SSH Config File (Shortcut!)

```bash
# ~/.ssh/config — SSH shortcuts তৈরি করুন
nano ~/.ssh/config

# Content:
Host myserver
    HostName 192.168.1.50
    User omar
    Port 22
    IdentityFile ~/.ssh/id_ed25519

Host aws-production
    HostName ec2-xx-xx-xx-xx.compute.amazonaws.com
    User ubuntu
    Port 22
    IdentityFile ~/.ssh/aws-key.pem

# এখন সংক্ষেপে connect:
ssh myserver                       # ssh omar@192.168.1.50 এর বদলে!
ssh aws-production                 # Long AWS command এর বদলে!
```

### 📝 Practice (Phase 4.3)

1. `ssh-keygen -t ed25519 -C "your-email"` → key pair তৈরি করুন
2. `ls -la ~/.ssh/` → key files দেখুন ও permissions check
3. `cat ~/.ssh/id_ed25519.pub` → public key দেখুন
4. `~/.ssh/config` file তৈরি করুন with a Host entry
5. যদি অন্য Linux machine থাকে, `ssh-copy-id` দিয়ে key copy করুন
6. `scp` দিয়ে local ↔ remote file transfer practice করুন

---

## Phase 4.4: Firewall (UFW ও iptables)

> **🎯 Why This Matters:** Firewall হলো server এর দরজার তালা। কোন port open থাকবে, কে access পাবে — সব firewall নিয়ন্ত্রণ করে। AWS Security Groups ও আসলে firewall rules। Server deploy করলে firewall configure করা **mandatory**।

### UFW — Uncomplicated Firewall (Ubuntu default, সহজ!)

```bash
# UFW install ও status
sudo apt install ufw
sudo ufw status                    # Status দেখুন
sudo ufw status verbose            # বিস্তারিত status
sudo ufw status numbered           # Rule numbers সহ

# ── Firewall চালু/বন্ধ ──
sudo ufw enable                    # Firewall চালু (⚠️ SSH allow আগে করুন!)
sudo ufw disable                   # Firewall বন্ধ
sudo ufw reset                     # সব rules মুছে reset

# ── Allow (অনুমতি দিন) ──
sudo ufw allow ssh                 # SSH (port 22) allow
sudo ufw allow 22                  # Same thing (port number দিয়ে)
sudo ufw allow 80                  # HTTP
sudo ufw allow 443                 # HTTPS
sudo ufw allow 3000               # Dev server

# Service name দিয়ে
sudo ufw allow 'Nginx Full'        # Nginx HTTP + HTTPS
sudo ufw allow 'OpenSSH'

# নির্দিষ্ট IP থেকে allow
sudo ufw allow from 192.168.1.100
sudo ufw allow from 192.168.1.0/24 to any port 22  # Subnet থেকে SSH

# ── Deny (block করুন) ──
sudo ufw deny 3306                 # MySQL port block (public থেকে)
sudo ufw deny from 10.0.0.5       # নির্দিষ্ট IP block

# ── Rule delete করুন ──
sudo ufw status numbered           # Rule number দেখুন
sudo ufw delete 3                  # Rule #3 delete
sudo ufw delete allow 80           # Rule by specification

# ── Default Policy (গুরুত্বপূর্ণ!) ──
sudo ufw default deny incoming     # ⚠️ সব incoming block (recommend!)
sudo ufw default allow outgoing    # সব outgoing allow

# ═══════════════════════════════════════════════
# ⭐ Standard Server Firewall Setup (মুখস্ত করুন!)
# ═══════════════════════════════════════════════
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh                 # SSH — always first!
sudo ufw allow 80                  # HTTP
sudo ufw allow 443                 # HTTPS
sudo ufw enable                    # Activate!
```

### iptables — Advanced Firewall (Low-level)

```bash
# iptables হলো Linux kernel-level firewall
# UFW আসলে iptables এর উপরে কাজ করে (simpler interface)

# Current rules দেখুন
sudo iptables -L -n -v             # List all rules
sudo iptables -L -n --line-numbers

# Allow SSH
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow HTTP/HTTPS
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Block specific IP
sudo iptables -A INPUT -s 10.0.0.5 -j DROP

# Default deny all incoming
sudo iptables -P INPUT DROP

# ⚠️ Note: iptables rules reboot এ চলে যায়!
# Save করতে:
sudo apt install iptables-persistent
sudo netfilter-persistent save
```

### 📝 Practice (Phase 4.4)

1. `sudo ufw status` → current firewall status
2. `sudo ufw allow ssh` → SSH allow করুন (enable আগে!)
3. `sudo ufw default deny incoming` → default policy set
4. `sudo ufw allow 80` → HTTP allow
5. `sudo ufw status numbered` → rules দেখুন
6. `sudo iptables -L -n` → kernel-level rules দেখুন
7. **⚠️ সাবধান:** Remote server এ SSH allow না করে `ufw enable` করলে locked out হবেন!

---

## Phase 4.5: Network Diagnostics

> **🎯 Why This Matters:** Server connect হচ্ছে না, website load হচ্ছে না — এসব সমস্যা solve করার জন্য network diagnosing tools জানা আবশ্যিক।

### Diagnostic Commands

```bash
# ── nmap — Network/Port Scanner ──
# কাজ: কোন ports open আছে এবং কোন services চলছে তা scan করে
# ⚠️ শুধু নিজের server এ ব্যবহার করুন! অন্যের server scan করা illegal!
sudo apt install nmap

nmap localhost                     # নিজের machine scan
nmap 192.168.1.1                   # Router scan
nmap -sV 192.168.1.50              # Service version detection
nmap -p 22,80,443 server-ip        # নির্দিষ্ট ports scan
nmap -p- server-ip                 # সব ports scan (1-65535)
nmap -sn 192.168.1.0/24            # Network এ কোন devices আছে

# ── tcpdump — Packet capture (Advanced) ──
# কাজ: Network traffic capture ও analyze করে (Wireshark CLI version)
sudo tcpdump -i eth0               # Interface এ traffic দেখুন
sudo tcpdump -i eth0 port 80       # শুধু HTTP traffic
sudo tcpdump -i eth0 -w capture.pcap  # File এ save (Wireshark এ open করা যায়)
sudo tcpdump -i any -c 50          # -c: 50 packets capture করে stop

# ── netcat (nc) — Network Swiss Army Knife ──
# কাজ: Port test, simple server/client, data transfer
nc -zv server-ip 22                # Port open কিনা check
nc -zv server-ip 80                # HTTP port check
nc -zv server-ip 20-100            # Port range scan

# ── arp — ARP table (LAN devices) ──
arp -a                             # Local network এ connected devices
ip neigh                           # Modern alternative
```

### Network Troubleshooting Workflow

```
Website load হচ্ছে না? এই sequence ফলো করুন:

1. ping google.com          → Internet আছে?
2. ping 8.8.8.8             → DNS problem নাকি connectivity problem?
3. dig mysite.com           → DNS resolve হচ্ছে?
4. traceroute mysite.com    → কোথায় block হচ্ছে?
5. curl -I https://mysite.com → Server respond করছে?
6. ss -tlnp                 → Service listen করছে?
7. sudo ufw status          → Firewall block করছে?
8. sudo journalctl -u nginx → Service error আছে?
```

### 📝 Practice (Phase 4.5)

1. `nmap localhost` → নিজের machine এর open ports দেখুন
2. `nc -zv google.com 80` → Google এর port 80 open কিনা check
3. `nc -zv google.com 443` → HTTPS port check
4. `arp -a` → local network devices
5. Troubleshooting workflow মুখস্ত করুন — server problem হলে step by step follow করুন

---

## Phase 4.6: Security Hardening

> **🎯 Why This Matters:** Server internet এ expose থাকলে hackers attack করবেই। Server secure করা (hardening) default task। AWS EC2 deploy করলে দিনেই automated attacks আসে। তাই সুরক্ষা জানা mandatory।

### Essential Security Measures

```bash
# ═══════════════════════════════════════════════
# ⭐ Server Security Checklist (প্রতিটি server এ করুন!)
# ═══════════════════════════════════════════════

# 1. System Update (সব সময় updated রাখুন!)
sudo apt update && sudo apt upgrade -y

# 2. Automatic Security Updates চালু করুন
sudo apt install unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades
# Security patches automatic install হবে

# 3. Root login বন্ধ করুন
sudo nano /etc/ssh/sshd_config
# PermitRootLogin no
sudo systemctl restart ssh

# 4. Password authentication বন্ধ (SSH key ব্যবহার করুন)
# PasswordAuthentication no (sshd_config এ)

# 5. SSH port পরিবর্তন করুন (optional, but helps)
# Port 2222 (sshd_config এ)

# 6. Firewall configure করুন
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw enable

# 7. Fail2Ban — Brute force attack প্রতিরোধ
sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
# Config:
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo nano /etc/fail2ban/jail.local
# [sshd]
# enabled = true
# port = ssh
# maxretry = 3
# bantime = 3600    ← ১ ঘণ্টা ban
# findtime = 600    ← ১০ মিনিটে ৩ বার fail = ban

# Fail2Ban status check
sudo fail2ban-client status sshd   # Banned IPs দেখুন
```

### User Security

```bash
# Strong password policy
sudo apt install libpam-pwquality
sudo nano /etc/security/pwquality.conf
# minlen = 12
# ucredit = -1 (minimum 1 uppercase)
# lcredit = -1 (minimum 1 lowercase)
# dcredit = -1 (minimum 1 digit)

# Sudo timeout কমান
sudo visudo
# Defaults timestamp_timeout=5     ← ৫ মিনিট পরে আবার password চাইবে

# Login attempts check করুন
sudo cat /var/log/auth.log | grep "Failed password"
sudo lastb                         # Failed login attempts
sudo last                          # Successful logins
who                                # Currently logged in users
w                                  # বিস্তারিত logged in info
```

### AppArmor — Application Security

```bash
# AppArmor কি? — Application কে restrict করে (কোন application কি access পাবে)
# Ubuntu তে by default চালু থাকে

sudo aa-status                     # AppArmor status
sudo apt install apparmor-utils

# Profile modes:
#  enforce — Rule ভাঙলে block করে
#  complain — Rule ভাঙলে শুধু log করে
```

### 📝 Practice (Phase 4.6)

1. `sudo cat /var/log/auth.log | grep "Failed" | tail -10` → failed logins
2. `sudo last -10` → recent logins
3. `who` ও `w` → currently logged in users
4. `sudo apt install fail2ban` → install করুন
5. `sudo fail2ban-client status` → status check
6. `sudo aa-status` → AppArmor check

---

## Phase 4.7: SSL/TLS ও Certificates

> **🎯 Why This Matters:** কোনো website HTTPS ছাড়া চলে না — browser "Not Secure" দেখায়। SSL certificate setup করা web server admin এর basic কাজ।

### SSL/TLS Basics

```
HTTP  → Port 80  → Unencrypted (data plain text এ যায়)
HTTPS → Port 443 → Encrypted (SSL/TLS দিয়ে secure)

SSL Certificate কাজ:
1. Data encryption (man-in-the-middle attack prevention)
2. Identity verification (website আসল কিনা)
3. Trust (browser এ 🔒 icon দেখায়)
```

### Let's Encrypt — Free SSL Certificate

```bash
# Certbot install (Let's Encrypt client)
sudo apt install certbot python3-certbot-nginx
# or for Apache:
sudo apt install certbot python3-certbot-apache

# Nginx এর জন্য certificate install
sudo certbot --nginx -d example.com -d www.example.com
# Interactive: email দিন, terms agree করুন
# Automatic: Nginx config update করে SSL setup করে দেয়!

# Apache এর জন্য
sudo certbot --apache -d example.com

# Certificate renewal (৯০ দিনে expire হয়)
sudo certbot renew                 # Manual renew
sudo certbot renew --dry-run       # Test run (actual renew না করে)

# Auto-renewal (cron/timer)
# Certbot install করলে automatic timer setup হয়ে যায়:
sudo systemctl status certbot.timer
```

### Certificate Management

```bash
# Certificate দেখুন
sudo certbot certificates          # Installed certificates

# Certificate delete
sudo certbot delete --cert-name example.com

# OpenSSL দিয়ে certificate info দেখুন
openssl s_client -connect google.com:443 -brief
openssl x509 -in cert.pem -noout -text   # Certificate details
openssl x509 -in cert.pem -noout -dates  # Expiry dates
```

### Self-signed Certificate (Development/Testing)

```bash
# Self-signed certificate তৈরি (production এ ব্যবহার করবেন না!)
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/selfsigned.key \
  -out /etc/ssl/certs/selfsigned.crt
```

### 📝 Practice (Phase 4.7)

1. `openssl s_client -connect google.com:443 -brief` → Google এর SSL info
2. Web browser এ যেকোনো website এর 🔒 icon click করে certificate দেখুন
3. Let's Encrypt এর process steps মুখস্ত করুন
4. `sudo systemctl status certbot.timer` → auto-renewal timer check (যদি installed থাকে)

---

---

# 📒 Section 5: Shell Scripting ও Automation

> **🎯 এই Section এর লক্ষ্য:** Bash scripting শিখে Linux এ কাজ automate করা। একই কাজ বারবার করতে হলে script লিখে একবারেই শেষ করুন। DevOps এর মূল ভিত্তি হলো automation।
>
> **⏱ আনুমানিক সময়:** ২-৩ সপ্তাহ (প্রতিদিন ২-৩ ঘণ্টা)
>
> **🔮 Future Path Connection:** DevOps এ CI/CD scripts, AWS automation, deployment pipelines — সবকিছু shell scripting ছাড়া অসম্ভব। Cyber Security তে automation scripts, scanning scripts — Bash সবখানে।
>
> **📌 Note:** আপনি JavaScript/Python জানেন, তাই programming concepts familiar লাগবে। Bash এর syntax একটু ভিন্ন, কিন্তু logic একই।

---

## Phase 5.1: Bash Basics

> **🎯 Why This Matters:** প্রথম script লেখা — "Hello World" থেকে variables, input/output পর্যন্ত। এটা foundation।

### প্রথম Script

```bash
# Step 1: Script file তৈরি করুন
nano hello.sh

# Step 2: Content লিখুন:
#!/bin/bash
# ↑ Shebang line — Linux কে বলে "এই script bash দিয়ে চালাও"
# এটা প্রথম line এ থাকা আবশ্যিক!

# এটা একটি comment (bash ignore করে)
echo "Hello, World!"
echo "আমি Linux শিখছি!"

# Step 3: Executable করুন
chmod +x hello.sh

# Step 4: চালান
./hello.sh
# বা
bash hello.sh
```

### Variables

```bash
#!/bin/bash

# ═══════════════════════════════
# Variables — data store করার জায়গা
# ═══════════════════════════════

# Variable assign (⚠️ = এর আগে-পরে space দেবেন না!)
name="Omar"                        # ✅ সঠিক
# name = "Omar"                    # ❌ ভুল! (space দিলে error)

age=25
city="Dhaka"

# Variable ব্যবহার ($ prefix লাগে)
echo "Name: $name"
echo "Age: $age"
echo "City: ${city}"               # ${} = safer way (recommend)

# ── Variable types (সব string, bash এ আলাদা type নেই) ──
number=42                          # Integer (internally string)
price=99.99                        # Float (bash proper float support করে না)
message="Hello World"              # String

# ── Read-only variable ──
readonly PI=3.14159
# PI=3.14                          # ❌ Error! Read-only

# ── Environment variables ──
echo $HOME                         # Home directory
echo $USER                         # Username
echo $PWD                          # Current directory
echo $PATH                         # Command search paths
echo $SHELL                        # Current shell
echo $HOSTNAME                     # Computer name
echo $RANDOM                       # Random number (0-32767)

# ── Variable export (child process এ available করা) ──
export MY_VAR="hello"
# এখন এই terminal থেকে run করা সব program MY_VAR access করতে পারবে
```

### User Input

```bash
#!/bin/bash

# ── read — User থেকে input নেওয়া ──
echo "আপনার নাম কি?"
read username
echo "Hello, $username!"

# একই line এ prompt + input (-p flag)
read -p "আপনার বয়স কত? " age
echo "আপনার বয়স: $age"

# Password input (text দেখা যাবে না, -s = silent)
read -sp "Password: " password
echo ""
echo "Password received!"

# Multiple values
read -p "First Last: " first last
echo "First: $first, Last: $last"

# Default value সহ
read -p "Port [default 8080]: " port
port=${port:-8080}                 # Input না দিলে 8080
echo "Using port: $port"
```

### Quoting (গুরুত্বপূর্ণ!)

```bash
name="Omar"

# Double quotes: Variable expand হয়
echo "Hello $name"                 # Output: Hello Omar
echo "Home is $HOME"               # Output: Home is /home/omar

# Single quotes: সবকিছু literal (variable expand হয় না!)
echo 'Hello $name'                 # Output: Hello $name
echo 'Home is $HOME'               # Output: Home is $HOME

# Backticks / $(): Command substitution
echo "Today is $(date)"            # date command এর output
echo "Files: $(ls | wc -l)"        # File count
echo "IP: $(hostname -I)"          # IP address

# Escaping
echo "He said \"Hello\""           # \" = literal quote
echo "Price: \$100"                # \$ = literal dollar sign
echo "Backslash: \\"               # \\ = literal backslash
```

### Arithmetic

```bash
#!/bin/bash

# ── (( )) — Arithmetic operations ──
a=10
b=3

echo $(( a + b ))                  # 13
echo $(( a - b ))                  # 7
echo $(( a * b ))                  # 30
echo $(( a / b ))                  # 3 (integer division!)
echo $(( a % b ))                  # 1 (remainder/modulo)
echo $(( a ** 2 ))                 # 100 (power)

# Variable এ store
result=$(( a + b ))
echo "Result: $result"

# Increment / Decrement
(( a++ ))                          # a = 11
(( b-- ))                          # b = 2
(( a += 5 ))                       # a = 16

# ── bc — Float calculation ──
# Bash integer শুধু support করে, float এর জন্য bc ব্যবহার করুন
echo "10 / 3" | bc -l              # 3.33333333333...
echo "scale=2; 10/3" | bc          # 3.33 (2 decimal places)
```

### 📝 Practice (Phase 5.1)

1. `hello.sh` script তৈরি করুন → `chmod +x` → `./hello.sh`
2. Script এ name, age variable declare করুন → `echo` দিয়ে print
3. `read -p` দিয়ে user input নিন → greeting print করুন
4. Double quotes vs single quotes থেকে variable expand test করুন
5. $(( )) দিয়ে calculator script তৈরি করুন (দুটি সংখ্যা input → যোগ/বিয়োগ/গুণ/ভাগ output)

---

## Phase 5.2: Control Structures

> **🎯 Why This Matters:** if/else, loops — এগুলো ছাড়া meaningful script লেখা সম্ভব না। JavaScript এ যেমন `if`, `for`, `while` আছে, Bash এও আছে — syntax ভিন্ন।

### If-Else Conditions

```bash
#!/bin/bash

# ═══════════════════════════════
# if statement
# ═══════════════════════════════

# Basic if
age=18
if [ $age -ge 18 ]; then
    echo "আপনি adult"
fi

# if-else
if [ $age -ge 18 ]; then
    echo "Adult"
else
    echo "Minor"
fi

# if-elif-else
score=75
if [ $score -ge 80 ]; then
    echo "Grade: A"
elif [ $score -ge 70 ]; then
    echo "Grade: B"
elif [ $score -ge 60 ]; then
    echo "Grade: C"
else
    echo "Grade: F"
fi
```

### Comparison Operators

```bash
# ═══════════════════════════════
# Number comparison ([ ] এর ভিতরে)
# ═══════════════════════════════
# -eq    Equal to          [ $a -eq $b ]
# -ne    Not equal         [ $a -ne $b ]
# -gt    Greater than      [ $a -gt $b ]
# -lt    Less than         [ $a -lt $b ]
# -ge    Greater or equal  [ $a -ge $b ]
# -le    Less or equal     [ $a -le $b ]

# ═══════════════════════════════
# String comparison
# ═══════════════════════════════
# =      Equal             [ "$a" = "$b" ]
# !=     Not equal         [ "$a" != "$b" ]
# -z     Empty string      [ -z "$a" ]
# -n     Not empty         [ -n "$a" ]

# ↕ (( )) দিয়ে: JavaScript style operators ব্যবহার করতে পারেন!
if (( age >= 18 )); then
    echo "Adult"
fi

# ═══════════════════════════════
# File/Directory checks (⭐ অনেক ব্যবহৃত!)
# ═══════════════════════════════
# -f     File exists        [ -f "/path/file" ]
# -d     Directory exists   [ -d "/path/dir" ]
# -e     কিছু exists        [ -e "/path" ]
# -r     Readable           [ -r "/path/file" ]
# -w     Writable           [ -w "/path/file" ]
# -x     Executable         [ -x "/path/file" ]
# -s     File not empty     [ -s "/path/file" ]

# উদাহরণ:
if [ -f "/etc/nginx/nginx.conf" ]; then
    echo "Nginx installed!"
else
    echo "Nginx not found"
fi

if [ -d "$HOME/projects" ]; then
    echo "Projects folder exists"
else
    mkdir "$HOME/projects"
    echo "Projects folder created"
fi
```

### Logical Operators

```bash
# AND: &&  বা -a
if [ $age -ge 18 ] && [ $age -le 65 ]; then
    echo "Working age"
fi

# OR: ||  বা -o
if [ "$role" = "admin" ] || [ "$role" = "root" ]; then
    echo "Full access"
fi

# NOT: !
if [ ! -f "config.txt" ]; then
    echo "Config file missing!"
fi
```

### For Loop

```bash
#!/bin/bash

# ── Basic for loop ──
for i in 1 2 3 4 5; do
    echo "Number: $i"
done

# ── Range ──
for i in {1..10}; do
    echo "Count: $i"
done

# Step value
for i in {0..100..10}; do          # 0, 10, 20, ..., 100
    echo "$i"
done

# ── C-style for loop (JavaScript এর মতো!) ──
for (( i=0; i<10; i++ )); do
    echo "Index: $i"
done

# ── Files loop (⭐ অনেক useful!) ──
for file in *.txt; do
    echo "Processing: $file"
done

for file in /var/log/*.log; do
    echo "Log: $file, Size: $(du -sh $file | cut -f1)"
done

# ── Array loop ──
servers=("web1" "web2" "db1" "cache1")
for server in "${servers[@]}"; do
    echo "Checking $server..."
done

# ── Command output loop ──
for user in $(cut -d':' -f1 /etc/passwd); do
    echo "User: $user"
done
```

### While Loop

```bash
#!/bin/bash

# ── Basic while ──
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    (( count++ ))
done

# ── File line-by-line read (⭐ log processing!) ──
while IFS= read -r line; do
    echo "Line: $line"
done < /etc/hostname

# ── Infinite loop (server monitoring script) ──
# while true; do
#     echo "$(date): Server is running"
#     sleep 60
# done

# ── Until loop (while এর opposite) ──
count=1
until [ $count -gt 5 ]; do
    echo "Count: $count"
    (( count++ ))
done
```

### Case Statement (Switch)

```bash
#!/bin/bash

# case = JavaScript এর switch
read -p "Enter fruit: " fruit
case $fruit in
    "apple"|"Apple")
        echo "🍎 It's an apple!"
        ;;
    "banana")
        echo "🍌 It's a banana!"
        ;;
    "orange")
        echo "🍊 It's an orange!"
        ;;
    *)                             # default case
        echo "Unknown fruit: $fruit"
        ;;
esac

# Real-world example: Service control script
read -p "Action (start/stop/restart/status): " action
case $action in
    start)   sudo systemctl start nginx ;;
    stop)    sudo systemctl stop nginx ;;
    restart) sudo systemctl restart nginx ;;
    status)  sudo systemctl status nginx ;;
    *)       echo "Usage: start|stop|restart|status" ;;
esac
```

### 📝 Practice (Phase 5.2)

1. Script: User এর বয়স input নিন → adult/minor বলুন
2. Script: File path input → file/directory/not found check করুন
3. Script: 1-10 পর্যন্ত for loop → শুধু even number print
4. Script: Server list array → for loop দিয়ে ping check
5. Script: Menu-based program case statement দিয়ে

---

## Phase 5.3: Functions ও Arguments

> **🎯 Why This Matters:** Code reuse করতে functions লাগে। Script কে arguments দিয়ে flexible করতে হয়। DevOps scripts এ functions ব্যবহার করে modular code লেখা standard practice।

### Functions

```bash
#!/bin/bash

# ── Function define করা ──
# পদ্ধতি ১:
greet() {
    echo "Hello, World!"
}

# পদ্ধতি ২ (function keyword):
function say_goodbye() {
    echo "Goodbye!"
}

# Function call:
greet
say_goodbye

# ── Parameters সহ Function ──
greet_user() {
    local name=$1                  # local = function scope variable
    local time=$2
    echo "Good $time, $name!"
}
greet_user "Omar" "morning"        # Output: Good morning, Omar!
# $1 = 1st argument, $2 = 2nd, $3 = 3rd...
# $@ = সব arguments
# $# = arguments এর count

# ── Return value ──
# Bash function সরাসরি value return করে না (শুধু exit code 0-255)
# Value pass করতে echo ব্যবহার করুন:
add() {
    local sum=$(( $1 + $2 ))
    echo $sum                      # "Return" value
}
result=$(add 10 20)                # Command substitution দিয়ে capture
echo "Sum: $result"                # Sum: 30

# ── Exit code check ──
check_file() {
    if [ -f "$1" ]; then
        return 0                   # Success
    else
        return 1                   # Failure
    fi
}
check_file "/etc/passwd"
if [ $? -eq 0 ]; then             # $? = last command এর exit code
    echo "File exists!"
fi
```

### Script Arguments (Command Line)

```bash
#!/bin/bash
# File: deploy.sh

# Script arguments:
# $0 = Script name itself
# $1 = 1st argument
# $2 = 2nd argument
# $@ = All arguments (as separate words)
# $* = All arguments (as single string)
# $# = Number of arguments

echo "Script: $0"
echo "First arg: $1"
echo "Second arg: $2"
echo "All args: $@"
echo "Total args: $#"

# Usage: ./deploy.sh production web-server

# ── Argument validation ──
if [ $# -lt 1 ]; then
    echo "Usage: $0 <environment>"
    echo "Example: $0 production"
    exit 1                         # Exit with error
fi

environment=$1
echo "Deploying to: $environment"

# ── shift — Arguments shift করুন ──
# shift এর পরে $2 → $1 হয়ে যায়
echo "Before shift: $1 $2"
shift
echo "After shift: $1 $2"
```

### Real-world Function Examples

```bash
#!/bin/bash

# ── Logging function (সব script এ ব্যবহার করুন!) ──
log() {
    local level=$1
    local message=$2
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] [$level] $message"
}

log "INFO" "Script started"
log "WARN" "Disk space low"
log "ERROR" "Connection failed"

# ── Error handling ──
die() {
    log "ERROR" "$1"
    exit 1
}

# Usage:
[ -f "config.txt" ] || die "Config file not found!"

# ── Colors function ──
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m'                       # No Color

success() { echo -e "${GREEN}✅ $1${NC}"; }
warning() { echo -e "${YELLOW}⚠️ $1${NC}"; }
error()   { echo -e "${RED}❌ $1${NC}"; }

success "Installation complete"
warning "Low disk space"
error "Service failed to start"
```

### 📝 Practice (Phase 5.3)

1. `greet()` function তৈরি → name argument নিয়ে greeting দিন
2. `calculate()` function → দুটি number ও operator (+, -, \*, /) নিয়ে result দিন
3. Script তৈরি করুন যা command line argument check করে — insufficient হলে usage message দেখায়
4. logging function তৈরি করুন → log file এ output redirect করুন
5. Color output function গুলো নিজের script এ ব্যবহার করুন

---

## Phase 5.4: String ও Array Operations

> **🎯 Why This Matters:** Text manipulation ও data lists handle করতে string ও array operations জানতে হবে। Config file parse, log extract, server list manage — সবকিছুতে এগুলো লাগে।

### String Operations

```bash
#!/bin/bash

str="Hello World Linux"

# String length
echo ${#str}                       # 17

# Substring (offset, length)
echo ${str:0:5}                    # Hello (index 0 থেকে 5টি)
echo ${str:6:5}                    # World
echo ${str:6}                      # World Linux (6 থেকে শেষ)

# Replace
echo ${str/World/Ubuntu}           # Hello Ubuntu Linux (প্রথমটি)
echo ${str//l/L}                   # HeLLo WorLd Linux (সব 'l' → 'L')

# Delete pattern
filename="document.backup.tar.gz"
echo ${filename%.gz}               # document.backup.tar (শেষ থেকে remove)
echo ${filename%%.*}               # document (প্রথম . থেকে সব remove)
echo ${filename#*.}                # backup.tar.gz (শুরু থেকে remove)
echo ${filename##*.}               # gz (শেষ extension)

# Default values
echo ${undefined_var:-"default"}   # Variable না থাকলে default ব্যবহার
echo ${undefined_var:="set_default"}  # না থাকলে set ও করে দেয়

# Uppercase / Lowercase
str="hello world"
echo ${str^^}                      # HELLO WORLD (all upper)
echo ${str^}                       # Hello world (first upper)
str="HELLO WORLD"
echo ${str,,}                      # hello world (all lower)
```

### Arrays

```bash
#!/bin/bash

# ── Array declare ──
fruits=("Apple" "Banana" "Orange" "Mango")
servers=("web1" "web2" "db1" "cache1")

# ── Access ──
echo ${fruits[0]}                  # Apple (0-indexed!)
echo ${fruits[2]}                  # Orange
echo ${fruits[@]}                  # সব elements
echo ${fruits[*]}                  # সব elements (string হিসেবে)

# ── Array info ──
echo ${#fruits[@]}                 # Length (4)
echo ${!fruits[@]}                 # Indices (0 1 2 3)

# ── Add / Modify / Delete ──
fruits+=("Grape")                  # Add to end
fruits[1]="Pineapple"              # Modify index 1
unset fruits[3]                    # Delete index 3

# ── Loop ──
for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done

# With index:
for i in "${!fruits[@]}"; do
    echo "Index $i: ${fruits[$i]}"
done

# ── Associative Arrays (Key-Value, like JS objects) ──
declare -A config
config[host]="192.168.1.50"
config[port]="8080"
config[user]="admin"

echo "Host: ${config[host]}"
echo "Port: ${config[port]}"

# Loop associative array
for key in "${!config[@]}"; do
    echo "$key = ${config[$key]}"
done
```

### 📝 Practice (Phase 5.4)

1. String variable তৈরি → substring, replace, length practice
2. Filename থেকে extension extract করুন (`${filename##*.}`)
3. Server names এর array তৈরি → loop দিয়ে print
4. Associative array দিয়ে একটি config store/display system তৈরি করুন

---

## Phase 5.5: Practical Scripts

> **🎯 Why This Matters:** এখন পর্যন্ত যা শিখেছেন তা দিয়ে real-world কাজের scripts লিখবেন। এগুলো আপনি সরাসরি server এ ব্যবহার করতে পারবেন।

### Script 1: System Health Check

```bash
#!/bin/bash
# system_health.sh — Server health check report

echo "════════════════════════════════════════"
echo "   System Health Check Report"
echo "   $(date '+%Y-%m-%d %H:%M:%S')"
echo "════════════════════════════════════════"

# Hostname & Uptime
echo -e "\n📌 Hostname: $(hostname)"
echo "⏰ Uptime: $(uptime -p)"

# CPU Load
echo -e "\n🔧 CPU Load Average:"
uptime | awk -F'load average:' '{print "  " $2}'

# Memory
echo -e "\n💾 Memory Usage:"
free -h | grep Mem | awk '{printf "  Used: %s / %s (%s)\n", $3, $2, $3/$2*100"%"}'

# Disk
echo -e "\n💿 Disk Usage:"
df -h / | tail -1 | awk '{printf "  Used: %s / %s (%s)\n", $3, $2, $5}'

# Top Processes
echo -e "\n📊 Top 5 CPU Processes:"
ps aux --sort=-%cpu | head -6 | tail -5 | awk '{printf "  %-10s %5s%% CPU  %s\n", $1, $3, $11}'

echo -e "\n════════════════════════════════════════"
```

### Script 2: Automated Backup

```bash
#!/bin/bash
# backup.sh — Directory backup script

# ── Configuration ──
SOURCE_DIR=${1:-"$HOME/projects"}
BACKUP_DIR="$HOME/backups"
DATE=$(date '+%Y%m%d_%H%M%S')
BACKUP_FILE="backup_${DATE}.tar.gz"
MAX_BACKUPS=7                      # পুরনো ৭টির বেশি রাখবে না

# ── Functions ──
log() { echo "[$(date '+%H:%M:%S')] $1"; }

# ── Pre-checks ──
if [ ! -d "$SOURCE_DIR" ]; then
    log "❌ Source directory not found: $SOURCE_DIR"
    exit 1
fi

mkdir -p "$BACKUP_DIR"

# ── Backup ──
log "📦 Starting backup: $SOURCE_DIR → $BACKUP_DIR/$BACKUP_FILE"
tar -czf "$BACKUP_DIR/$BACKUP_FILE" -C "$(dirname $SOURCE_DIR)" "$(basename $SOURCE_DIR)"

if [ $? -eq 0 ]; then
    SIZE=$(du -sh "$BACKUP_DIR/$BACKUP_FILE" | cut -f1)
    log "✅ Backup complete! Size: $SIZE"
else
    log "❌ Backup failed!"
    exit 1
fi

# ── Cleanup old backups ──
BACKUP_COUNT=$(ls -1 "$BACKUP_DIR"/backup_*.tar.gz 2>/dev/null | wc -l)
if [ "$BACKUP_COUNT" -gt "$MAX_BACKUPS" ]; then
    REMOVE_COUNT=$((BACKUP_COUNT - MAX_BACKUPS))
    log "🗑️  Removing $REMOVE_COUNT old backup(s)..."
    ls -1t "$BACKUP_DIR"/backup_*.tar.gz | tail -n $REMOVE_COUNT | xargs rm -f
fi

log "📁 Current backups: $(ls -1 "$BACKUP_DIR"/backup_*.tar.gz | wc -l)"
```

### Script 3: Service Monitor

```bash
#!/bin/bash
# monitor.sh — Service monitoring (cron দিয়ে চালান)

SERVICES=("nginx" "mysql" "ssh")
LOG_FILE="/var/log/service_monitor.log"

log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

for service in "${SERVICES[@]}"; do
    if systemctl is-active --quiet "$service"; then
        log "✅ $service is running"
    else
        log "❌ $service is DOWN! Attempting restart..."
        sudo systemctl restart "$service"
        if systemctl is-active --quiet "$service"; then
            log "✅ $service restarted successfully"
        else
            log "🚨 CRITICAL: $service failed to restart!"
        fi
    fi
done
```

### Script 4: Simple Deployment Script

```bash
#!/bin/bash
# deploy.sh — Basic deployment script

# ── Argument check ──
if [ $# -lt 1 ]; then
    echo "Usage: $0 <environment>"
    echo "  Environments: staging, production"
    exit 1
fi

ENV=$1
PROJECT_DIR="/var/www/myapp"

RED='\033[0;31m'
GREEN='\033[0;32m'
NC='\033[0m'

log() { echo -e "[$(date '+%H:%M:%S')] $1"; }

# ── Deploy ──
log "${GREEN}🚀 Deploying to $ENV...${NC}"

# Step 1: Pull latest code
log "📥 Pulling latest code..."
cd "$PROJECT_DIR" && git pull origin main

# Step 2: Install dependencies
log "📦 Installing dependencies..."
npm install --production

# Step 3: Build
log "🔨 Building..."
npm run build

# Step 4: Restart service
log "🔄 Restarting service..."
sudo systemctl restart myapp

# Step 5: Health check
sleep 3
if curl -sf http://localhost:3000/health > /dev/null; then
    log "${GREEN}✅ Deployment successful!${NC}"
else
    log "${RED}❌ Health check failed!${NC}"
    exit 1
fi
```

### 📝 Practice (Phase 5.5)

1. `system_health.sh` script তৈরি করুন → চালিয়ে output দেখুন
2. `backup.sh` script তৈরি → আপনার projects folder backup নিন
3. Cron job setup: প্রতিদিন `backup.sh` চালানো
4. `monitor.sh` customize করুন — আপনার installed services দিয়ে

---

## Phase 5.6: Advanced Scripting

> **🎯 Why This Matters:** Professional scripts এ error handling, debugging, এবং best practices follow করা জরুরি। Production server এ faulty script চলানো মানে disaster।

### Error Handling

```bash
#!/bin/bash

# ── set options (Script এর শুরুতে ব্যবহার করুন!) ──
set -e              # Error হলে script বন্ধ (exit on error)
set -u              # Undefined variable error (না বলে ব্যবহার করলে error)
set -o pipefail     # Pipe এ error হলেও catch হবে

# সবগুলো একসাথে (⭐ Best Practice!):
set -euo pipefail

# ── trap — Cleanup on exit ──
# Script শেষ হোক বা error হোক — cleanup চলবে!
cleanup() {
    echo "🧹 Cleaning up temp files..."
    rm -f /tmp/myapp_*.tmp
}
trap cleanup EXIT                  # EXIT = যেভাবেই শেষ হোক

# ── Error handling function ──
handle_error() {
    echo "❌ Error on line $1"
    exit 1
}
trap 'handle_error $LINENO' ERR    # ERR = error হলে
```

### Debugging

```bash
# ── Debug mode ──
# পদ্ধতি ১: Command line থেকে
bash -x script.sh                  # প্রতিটি command execute আগে print করে

# পদ্ধতি ২: Script এর ভিতরে
set -x              # Debug mode on (এখান থেকে সব command print হবে)
# ... code ...
set +x              # Debug mode off

# পদ্ধতি ৩: Shebang এ
#!/bin/bash -x
```

### Script Best Practices

```bash
#!/bin/bash
# ═══════════════════════════════════════════════
# Script Name: example_best_practice.sh
# Description: Best practices demonstration
# Author: Omar
# Date: 2026-02-21
# Version: 1.0
# ═══════════════════════════════════════════════

set -euo pipefail

# ── Constants (UPPERCASE) ──
readonly SCRIPT_DIR="$(cd "$(dirname "$0")" && pwd)"
readonly LOG_FILE="/var/log/myapp.log"
readonly VERSION="1.0"

# ── Functions (lowercase, descriptive names) ──
usage() {
    cat << EOF
Usage: $(basename "$0") [OPTIONS] <command>
Options:
    -h, --help      Show this help
    -v, --version   Show version
    -d, --debug     Enable debug mode
Commands:
    start           Start the service
    stop            Stop the service
EOF
}

log() {
    local level=$1; shift
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] [$level] $*" | tee -a "$LOG_FILE"
}

# ── Argument parsing ──
while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)    usage; exit 0 ;;
        -v|--version) echo "Version: $VERSION"; exit 0 ;;
        -d|--debug)   set -x; shift ;;
        *)            COMMAND=$1; shift ;;
    esac
done

# ── Main logic ──
main() {
    log "INFO" "Script started"
    # ... your code here ...
    log "INFO" "Script completed"
}

main "$@"
```

### 📝 Practice (Phase 5.6)

1. আপনার আগের scripts এ `set -euo pipefail` যোগ করুন
2. `trap cleanup EXIT` দিয়ে cleanup function practice
3. `bash -x script.sh` দিয়ে debug mode test
4. Best practices template ব্যবহার করে একটি complete script লিখুন (argument parsing সহ)

### 📝 Section 5 Final Project

**প্রজেক্ট: Server Setup Script তৈরি করুন**

একটি script লিখুন যেটা:

1. ✅ Arguments নেয় (hostname, user)
2. ✅ System update করে
3. ✅ Essential packages install করে (git, nginx, ufw, fail2ban)
4. ✅ Firewall configure করে (SSH, HTTP, HTTPS)
5. ✅ একটি user তৈরি করে sudo access দিয়ে
6. ✅ প্রতিটি step log করে
7. ✅ Error handling আছে
8. ✅ Color output ব্যবহার করে

---

---

# 📓 Section 6: Server Administration

> **🎯 এই Section এর লক্ষ্য:** Ubuntu Server setup, configure, এবং maintain করা শেখা। Web server, database, application deploy — production server manage করার complete knowledge।
>
> **⏱ আনুমানিক সময়:** ৩-৪ সপ্তাহ (প্রতিদিন ২-৩ ঘণ্টা)
>
> **🔮 Future Path Connection:** এটাই real-world DevOps ও AWS এর foundation। EC2 instance launch করে web app deploy করা — exactly এই Section এর কাজ।
>
> **📌 Environment:** VirtualBox এ Ubuntu Server install করে practice করুন, অথবা AWS Free Tier EC2 ব্যবহার করুন।

---

## Phase 6.1: Ubuntu Server vs Desktop

> **🎯 Why This Matters:** Server ও Desktop — দুটোই Ubuntu কিন্তু আলাদা purpose। Server এ কোনো GUI নেই — সব terminal দিয়ে করতে হয়।

### পার্থক্য বোঝা

```
┌─────────────────────┬──────────────────────┬──────────────────────┐
│ Feature             │ Ubuntu Desktop       │ Ubuntu Server        │
├─────────────────────┼──────────────────────┼──────────────────────┤
│ GUI                 │ ✅ GNOME Desktop     │ ❌ No GUI (CLI only) │
│ Target              │ Personal use         │ Production hosting   │
│ Resource Usage      │ বেশি (GUI heavy)      │ কম (efficient)       │
│ Default Packages    │ Browser, Office etc  │ Minimal (SSH, APT)   │
│ Kernel              │ Desktop optimized    │ Server optimized     │
│ Use Case            │ Coding, browsing     │ Web hosting, DB, API │
│ Access              │ Keyboard + Mouse     │ SSH (remote)         │
│ Boot                │ GUI login screen     │ Text login prompt    │
└─────────────────────┴──────────────────────┴──────────────────────┘
```

### Server Installation Options

```bash
# Option 1: VirtualBox এ Ubuntu Server install (Recommended for practice!)
# 1. VirtualBox download: https://www.virtualbox.org
# 2. Ubuntu Server ISO download: https://ubuntu.com/download/server
# 3. New VM create → ISO attach → Install
# 4. Installation এ OpenSSH server select করুন!

# Option 2: AWS EC2 Free Tier
# 1. AWS account create (free tier: 1 year)
# 2. EC2 → Launch Instance → Ubuntu 24.04 LTS
# 3. Instance type: t2.micro (free tier)
# 4. Key pair download → SSH connect

# Option 3: WSL (Windows Subsystem for Linux)
# PowerShell (Admin) এ:
# wsl --install -d Ubuntu-24.04

# Server এ first login হলে:
sudo apt update && sudo apt upgrade -y
sudo hostnamectl set-hostname myserver    # Hostname set
```

### Server First Steps

```bash
# ── Server এ প্রথম কি করবেন? ──
# ═══════════════════════════════════════════════
# ⭐ New Server Checklist (AWS EC2 / VPS / VirtualBox)
# ═══════════════════════════════════════════════

# 1. System update
sudo apt update && sudo apt upgrade -y

# 2. Hostname set
sudo hostnamectl set-hostname web-server-01

# 3. Timezone set
sudo timedatectl set-timezone Asia/Dhaka
timedatectl                                # Verify

# 4. New user create (root ব্যবহার করবেন না!)
sudo adduser deploy
sudo usermod -aG sudo deploy

# 5. SSH key setup (নতুন user এর জন্য)
sudo mkdir -p /home/deploy/.ssh
sudo cp ~/.ssh/authorized_keys /home/deploy/.ssh/
sudo chown -R deploy:deploy /home/deploy/.ssh
sudo chmod 700 /home/deploy/.ssh
sudo chmod 600 /home/deploy/.ssh/authorized_keys

# 6. Firewall setup
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow OpenSSH
sudo ufw enable

# 7. SSH hardening
sudo nano /etc/ssh/sshd_config
# PermitRootLogin no
# PasswordAuthentication no
sudo systemctl restart ssh

# 8. Fail2Ban install
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
```

### 📝 Practice (Phase 6.1)

1. VirtualBox এ Ubuntu Server install করুন (বা AWS EC2 launch)
2. SSH দিয়ে connect করুন
3. New Server Checklist follow করে server configure করুন
4. `hostnamectl`, `timedatectl` → server info check

---

## Phase 6.2: Remote Server Management

> **🎯 Why This Matters:** Production server physically আপনার সামনে নেই — সব কিছু remotely manage করতে হয়। SSH session management, file transfer, system monitoring — remote admin skills।

### SSH Session Management

```bash
# ── tmux — Terminal Multiplexer (⭐ Server এ must-have!) ──
# কাজ: SSH disconnect হলেও session চালু থাকে!
sudo apt install tmux

# Basic usage
tmux                               # নতুন session
tmux new -s deploy                 # Named session
tmux ls                            # Running sessions
tmux attach -t deploy              # Session এ ফিরে যান
tmux kill-session -t deploy        # Session বন্ধ

# Keyboard shortcuts (Ctrl+B first, then):
# c     → New window
# n     → Next window
# p     → Previous window
# d     → Detach (session চলতে থাকবে!)
# %     → Vertical split
# "     → Horizontal split
# Arrow → Move between panes

# ⭐ Real scenario:
# 1. SSH → Server এ login
# 2. tmux new -s deploy → Session start
# 3. Long deployment start
# 4. Ctrl+B, d → Detach (SSH close করলেও deployment চলবে!)
# 5. পরে: ssh server → tmux attach -t deploy → ফিরে আসলেন!

# ── screen — Alternative to tmux ──
sudo apt install screen
screen -S deploy                   # Named session
screen -ls                         # List sessions
screen -r deploy                   # Reattach
# Ctrl+A, d  → Detach
```

### Remote File Transfer (Advanced)

```bash
# ── rsync (Best for deployment!) ──
# Local → Server (deploy করার সময়):
rsync -avz --exclude='node_modules' --exclude='.git' \
  ./project/ deploy@server:/var/www/myapp/

# Server → Local (backup নেওয়ার সময়):
rsync -avz deploy@server:/var/www/myapp/uploads/ ./backup/uploads/

# ── sftp — Interactive file transfer ──
sftp deploy@server
# sftp> ls                         # Remote files
# sftp> cd /var/www                # Remote directory change
# sftp> put file.txt               # Upload
# sftp> get remote-file.txt        # Download
# sftp> exit
```

### Remote System Monitoring

```bash
# ── Real-time monitoring commands ──
# SSH login করে এগুলো চালান:

# System overview
htop                               # Interactive process monitor
df -h                              # Disk usage
free -h                            # Memory usage
uptime                             # Load average

# Network connections
ss -tunap                          # Active connections
ss -s                              # Connection summary

# Recent logs
sudo journalctl -f                 # Follow live logs
sudo tail -f /var/log/syslog       # System log live
sudo tail -f /var/log/auth.log     # Auth log live

# ── Quick one-liner health check (SSH দিয়ে remote এ) ──
ssh deploy@server "uptime && free -h && df -h /"
```

### 📝 Practice (Phase 6.2)

1. `sudo apt install tmux` → tmux install করুন
2. `tmux new -s practice` → session start → কিছু command চালান → `Ctrl+B, d` detach → `tmux attach -t practice` reattach
3. `rsync` দিয়ে local folder server এ sync করুন
4. `ssh server "uptime && free -h"` → one-liner check

---

## Phase 6.3: Web Server Setup

> **🎯 Why This Matters:** Web server ছাড়া কোনো website বা API internet এ serve করা যায় না। **Nginx** আজকের সবচেয়ে জনপ্রিয় web server — AWS, Docker, Kubernetes সবখানে Nginx।

### Nginx — Modern Web Server

```bash
# ── Install ──
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx        # Boot এ auto-start
sudo systemctl status nginx

# ✅ Browser এ http://server-ip → "Welcome to nginx!" page দেখা যাবে!

# ── Important directories ──
# /etc/nginx/               ← Config directory
# /etc/nginx/nginx.conf     ← Main config
# /etc/nginx/sites-available/ ← Site configs
# /etc/nginx/sites-enabled/   ← Active sites (symlinks)
# /var/www/html/            ← Default web root
# /var/log/nginx/           ← Log files

# ── Commands ──
sudo nginx -t                      # Config test (⭐ deploy আগে always test!)
sudo systemctl reload nginx        # Config reload (downtime ছাড়া!)
sudo systemctl restart nginx       # Full restart
```

### Static Website Deploy করা

```bash
# Step 1: Website directory তৈরি
sudo mkdir -p /var/www/mysite
sudo chown -R $USER:$USER /var/www/mysite

# Step 2: HTML file তৈরি
cat > /var/www/mysite/index.html << 'EOF'
<!DOCTYPE html>
<html>
<head><title>My Site</title></head>
<body>
    <h1>🎉 My First Server Page!</h1>
    <p>Successfully deployed on Ubuntu Server!</p>
</body>
</html>
EOF

# Step 3: Nginx config তৈরি
sudo nano /etc/nginx/sites-available/mysite

# Content:
server {
    listen 80;
    server_name mysite.com www.mysite.com;
    # IP দিয়ে access করলে: server_name _;

    root /var/www/mysite;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # Access ও Error logs
    access_log /var/log/nginx/mysite.access.log;
    error_log /var/log/nginx/mysite.error.log;
}

# Step 4: Site enable করুন
sudo ln -s /etc/nginx/sites-available/mysite /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default    # Default site remove

# Step 5: Test ও reload
sudo nginx -t                      # Config check
sudo systemctl reload nginx        # Apply changes!

# ✅ Browser → http://server-ip → আপনার site!
```

### Nginx Reverse Proxy (⭐ React/Node App এর জন্য!)

```bash
# React/Node app port 3000 এ চলে
# Nginx reverse proxy দিয়ে port 80 → 3000 redirect করে

sudo nano /etc/nginx/sites-available/myapp

server {
    listen 80;
    server_name myapp.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_cache_bypass $http_upgrade;
    }
}

# Enable:
sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
```

### Apache — Alternative Web Server

```bash
# Apache install (যদি Nginx না ব্যবহার করেন)
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2

# Config location:
# /etc/apache2/sites-available/
# /etc/apache2/sites-enabled/
# /var/www/html/

# Virtual host create
sudo nano /etc/apache2/sites-available/mysite.conf

<VirtualHost *:80>
    ServerName mysite.com
    DocumentRoot /var/www/mysite
    <Directory /var/www/mysite>
        AllowOverride All
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/mysite.error.log
    CustomLog ${APACHE_LOG_DIR}/mysite.access.log combined
</VirtualHost>

# Enable site
sudo a2ensite mysite.conf
sudo a2dissite 000-default.conf    # Default disable
sudo systemctl reload apache2

# ⚠️ Note: Nginx ও Apache দুটো একসাথে port 80 ব্যবহার করতে পারবে না!
```

### 📝 Practice (Phase 6.3)

1. `sudo apt install nginx -y` → Nginx install
2. Browser এ `http://server-ip` → default page দেখুন
3. `/var/www/mysite/index.html` তৈরি → custom site config → deploy
4. `sudo nginx -t` → config test করার অভ্যাস তৈরি করুন
5. Reverse proxy config তৈরি করুন (port 3000 → 80)

---

## Phase 6.4: Database Server Basics

> **🎯 Why This Matters:** প্রায় প্রতিটি web application এর পেছনে একটি database আছে। MySQL ও PostgreSQL — দুটোই Linux server এ widely ব্যবহৃত। AWS RDS ও এই same databases ব্যবহার করে।

### MySQL

```bash
# ── Install ──
sudo apt install mysql-server -y
sudo systemctl start mysql
sudo systemctl enable mysql

# ── Security Setup (ইনস্টল এর পরে অবশ্যই করুন!) ──
sudo mysql_secure_installation
# - Root password set
# - Remove anonymous users: Yes
# - Disallow root login remotely: Yes
# - Remove test database: Yes
# - Reload privilege tables: Yes

# ── MySQL Login ──
sudo mysql                         # Root login (first time)
sudo mysql -u root -p              # Password দিয়ে

# ── Basic SQL Commands ──
# MySQL prompt (mysql>) এ:

# Database তৈরি
CREATE DATABASE myapp_db;
SHOW DATABASES;

# User তৈরি ও permission দিন
CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'StrongPassword123!';
GRANT ALL PRIVILEGES ON myapp_db.* TO 'appuser'@'localhost';
FLUSH PRIVILEGES;

# User দিয়ে login
mysql -u appuser -p myapp_db

# Exit
EXIT;

# ── Backup ও Restore ──
# Backup (dump):
mysqldump -u root -p myapp_db > backup_myapp.sql
mysqldump -u root -p --all-databases > backup_all.sql

# Restore:
mysql -u root -p myapp_db < backup_myapp.sql

# ── Config ──
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
# bind-address = 127.0.0.1    ← শুধু localhost (secure!)
# bind-address = 0.0.0.0      ← Remote access (⚠️ firewall setup করুন!)
sudo systemctl restart mysql
```

### PostgreSQL

```bash
# ── Install ──
sudo apt install postgresql postgresql-contrib -y
sudo systemctl start postgresql
sudo systemctl enable postgresql

# ── Login (postgres user দিয়ে) ──
sudo -u postgres psql              # PostgreSQL shell

# ── Basic Commands ──
# psql prompt (postgres=#) এ:

# Database তৈরি
CREATE DATABASE myapp_db;
\l                                  -- List databases

# User তৈরি
CREATE USER appuser WITH PASSWORD 'StrongPassword123!';
GRANT ALL PRIVILEGES ON DATABASE myapp_db TO appuser;

# Exit
\q

# ── Command line থেকে ──
sudo -u postgres createdb myapp_db
sudo -u postgres createuser --interactive  # Interactive user creation

# ── User দিয়ে login ──
psql -U appuser -d myapp_db -h localhost

# ── Backup ও Restore ──
sudo -u postgres pg_dump myapp_db > backup_myapp.sql
sudo -u postgres psql myapp_db < backup_myapp.sql
# Full backup:
sudo -u postgres pg_dumpall > backup_all.sql

# ── Config ──
# /etc/postgresql/16/main/postgresql.conf  ← Main config
# /etc/postgresql/16/main/pg_hba.conf      ← Authentication config
sudo systemctl restart postgresql
```

### 📝 Practice (Phase 6.4)

1. MySQL install → `sudo mysql_secure_installation`
2. Database ও user তৈরি করুন
3. `mysqldump` দিয়ে backup নিন
4. PostgreSQL install → database ও user তৈরি
5. দুটোর command syntax compare করুন

---

## Phase 6.5: Application Deployment

> **🎯 Why This Matters:** Code লেখার পরে সেটা server এ deploy করাই final goal। React build serve, Node.js API চালানো, process management — এটাই production deployment।

### Node.js Install (Server এ)

```bash
# ── NodeSource থেকে install (LTS version) ──
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install nodejs -y
node -v                            # v20.x
npm -v                             # 10.x

# বা nvm দিয়ে (recommended!):
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install --lts
nvm use --lts
```

### React (Vite) App Deploy

```bash
# ── Step-by-step React deployment ──

# Step 1: Code server এ নিয়ে আসুন
cd /var/www
sudo git clone https://github.com/user/myapp.git
sudo chown -R deploy:deploy myapp
cd myapp

# Step 2: Dependencies install ও build
npm install
npm run build
# Build output: dist/ folder (Vite), build/ folder (CRA)

# Step 3: Nginx দিয়ে serve করুন
sudo nano /etc/nginx/sites-available/myapp

server {
    listen 80;
    server_name myapp.com;

    root /var/www/myapp/dist;
    index index.html;

    # SPA routing (React Router support!)
    location / {
        try_files $uri $uri/ /index.html;
    }

    # Cache static assets
    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
        expires 30d;
        add_header Cache-Control "public, immutable";
    }
}

sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
```

### Node.js API Deploy (PM2 দিয়ে)

```bash
# ── PM2 — Production Process Manager ──
# কাজ: Node.js app background এ চালায়, crash হলে restart করে!
sudo npm install -g pm2

# App চালান
cd /var/www/myapi
pm2 start server.js --name "myapi"

# ── PM2 Commands ──
pm2 list                           # Running apps দেখুন
pm2 status                         # Status
pm2 logs myapi                     # Logs দেখুন
pm2 logs myapi --lines 50         # Last 50 lines
pm2 restart myapi                  # Restart
pm2 stop myapi                    # Stop
pm2 delete myapi                  # Remove
pm2 monit                          # Real-time monitor

# ── Boot এ auto-start ──
pm2 startup                        # Auto-start command দেখাবে
# ↑ Output command copy করে paste করুন (sudo সহ)
pm2 save                           # Current apps save

# ── Ecosystem file (⭐ Professional approach!) ──
nano ecosystem.config.js

module.exports = {
    apps: [{
        name: "myapi",
        script: "server.js",
        instances: "max",          // CPU cores অনুযায়ী
        exec_mode: "cluster",      // Cluster mode (load balance)
        env: {
            NODE_ENV: "production",
            PORT: 3000
        },
        max_memory_restart: "300M",
        log_date_format: "YYYY-MM-DD HH:mm:ss"
    }]
};

pm2 start ecosystem.config.js
```

### Nginx + PM2 Together (Complete Setup)

```bash
# ═══════════════════════════════════════════════
# ⭐ Complete Production Setup:
# Nginx (port 80/443) → PM2/Node.js (port 3000)
# ═══════════════════════════════════════════════

# 1. PM2 দিয়ে API চালান (port 3000)
pm2 start server.js --name myapi

# 2. Nginx reverse proxy setup
sudo nano /etc/nginx/sites-available/myapi
# (Phase 6.3 এ দেখানো reverse proxy config ব্যবহার করুন)

# 3. SSL certificate (Let's Encrypt)
sudo certbot --nginx -d api.myapp.com

# 4. Firewall
sudo ufw allow 80
sudo ufw allow 443

# Complete flow:
# Browser → https://api.myapp.com (port 443)
#   → Nginx (SSL terminate) → http://localhost:3000
#   → PM2 → Node.js app → Response
```

### 📝 Practice (Phase 6.5)

1. Server এ Node.js install করুন (nvm recommend)
2. Simple Express API তৈরি → PM2 দিয়ে চালান
3. `pm2 list`, `pm2 logs`, `pm2 monit` → monitoring practice
4. React app build করে Nginx দিয়ে serve করুন
5. Nginx reverse proxy → PM2 API setup

---

## Phase 6.6: Server Maintenance

> **🎯 Why This Matters:** Server deploy করলেই শেষ না — maintain ও করতে হয়। Backups, updates, monitoring, log management — এগুলো regular কাজ।

### Automated Backup Strategy

```bash
#!/bin/bash
# server_backup.sh — Complete server backup

BACKUP_DIR="/backup/$(date '+%Y%m%d')"
mkdir -p "$BACKUP_DIR"

log() { echo "[$(date '+%H:%M:%S')] $1"; }

# 1. Database backup
log "📦 Database backup..."
mysqldump -u root --all-databases > "$BACKUP_DIR/mysql_all.sql"
sudo -u postgres pg_dumpall > "$BACKUP_DIR/postgres_all.sql"

# 2. Application files
log "📦 App files backup..."
tar -czf "$BACKUP_DIR/www.tar.gz" /var/www/

# 3. Config files
log "📦 Config backup..."
tar -czf "$BACKUP_DIR/configs.tar.gz" \
    /etc/nginx/ \
    /etc/ssh/sshd_config \
    /etc/ufw/

# 4. Upload to remote (optional)
# rsync -avz "$BACKUP_DIR/" backup-server:/backups/

log "✅ Backup complete: $BACKUP_DIR"

# Cron: প্রতিদিন রাত ২টায়
# crontab -e:
# 0 2 * * * /home/deploy/scripts/server_backup.sh >> /var/log/backup.log 2>&1
```

### Server Monitoring Setup

```bash
# ── Essential monitoring commands ──

# Disk space alert check
DISK_USAGE=$(df -h / | awk 'NR==2{print $5}' | tr -d '%')
if [ "$DISK_USAGE" -gt 80 ]; then
    echo "⚠️ Disk usage: ${DISK_USAGE}%"
fi

# Memory check
FREE_MEM=$(free -m | awk 'NR==2{printf "%.0f", $3/$2*100}')
echo "Memory usage: ${FREE_MEM}%"

# Failed services check
systemctl --failed

# ── Monitoring script (cron দিয়ে চালান) ──
#!/bin/bash
# health_check.sh
THRESHOLD_DISK=80
THRESHOLD_MEM=90

disk=$(df -h / | awk 'NR==2{print $5}' | tr -d '%')
mem=$(free | awk 'NR==2{printf "%.0f", $3/$2*100}')

[ "$disk" -gt "$THRESHOLD_DISK" ] && echo "⚠️ DISK: ${disk}%"
[ "$mem" -gt "$THRESHOLD_MEM" ] && echo "⚠️ MEM: ${mem}%"
```

### Update Strategy

```bash
# ── Regular Updates ──
# Security updates: automatic (unattended-upgrades)
# Package updates: weekly manual

# Weekly update routine:
sudo apt update
sudo apt list --upgradable        # কি update আছে দেখুন
sudo apt upgrade -y               # Update
sudo apt autoremove -y             # Cleanup

# ── Kernel update হলে reboot প্রয়োজন ──
# Check:
cat /var/run/reboot-required 2>/dev/null
# Output "*** System restart required ***" থাকলে reboot করুন

# Scheduled reboot (maintenance window এ):
sudo shutdown -r 02:00             # আজ রাত ২টায় reboot
```

### Log Rotation ও Cleanup

```bash
# ── logrotate — Automatic log management ──
# Log files বড় হলে automatic rotate, compress, delete করে
# Config: /etc/logrotate.d/

# Custom app এর জন্য logrotate config:
sudo nano /etc/logrotate.d/myapp

/var/log/myapp/*.log {
    daily                          # প্রতিদিন rotate
    missingok                      # File না থাকলে error না
    rotate 14                      # ১৪ দিনের log রাখবে
    compress                       # gzip compress
    delaycompress                  # পরবর্তী rotation এ compress
    notifempty                     # Empty file rotate না
    create 0640 deploy deploy      # নতুন file এর permission
    postrotate
        systemctl reload myapp > /dev/null 2>&1 || true
    endscript
}

# Manual cleanup
sudo journalctl --vacuum-time=7d   # ৭ দিনের পুরনো journal delete
sudo journalctl --vacuum-size=500M # ৫০০MB এর বেশি হলে delete
sudo apt clean                     # APT cache clean
```

### 📝 Practice (Phase 6.6)

1. Backup script তৈরি করুন → cron দিয়ে schedule
2. Health check script → disk ও memory threshold alert
3. `sudo apt update && apt list --upgradable` → update check
4. `sudo journalctl --vacuum-time=7d` → log cleanup
5. `/etc/logrotate.d/` → custom logrotate config তৈরি

---

---

# 📔 Section 7: Advanced Linux ও Cloud Readiness

> **🎯 এই Section এর লক্ষ্য:** Linux এ advanced topics শেখা এবং Cloud (AWS), Containers (Docker), ও DevOps এ transition এর জন্য তৈরি হওয়া। এই Section শেষ করলে আপনি Linux এ **confident** এবং cloud journey শুরু করার জন্য **ready**।
>
> **⏱ আনুমানিক সময়:** ২-৩ সপ্তাহ (প্রতিদিন ২-৩ ঘণ্টা)
>
> **🔮 Future Path Connection:** এটাই final bridge — এখান থেকে সোজা AWS, Docker, Kubernetes, CI/CD এ ঢুকতে পারবেন।

---

## Phase 7.1: Environment ও Configuration

> **🎯 Why This Matters:** Environment variables ও system configuration — প্রতিটি application এগুলোর উপর নির্ভর করে। Docker, AWS, CI/CD — সবখানে environment variables ব্যবহৃত হয়।

### Environment Variables Deep Dive

```bash
# ── Environment Variables কি? ──
# Key-value pairs যা OS ও applications ব্যবহার করে
# Application এর behavior change করতে ব্যবহৃত
# Example: NODE_ENV=production → Node.js production mode এ চলবে

# ── Current environment দেখুন ──
env                                # সব environment variables
printenv                           # Same thing
echo $HOME                         # Specific variable
printenv PATH                      # Specific variable

# ── Temporary set (current session only) ──
export MY_APP_PORT=3000
export DATABASE_URL="postgresql://user:pass@localhost/mydb"
echo $MY_APP_PORT                  # 3000

# ── Permanent set — User level ──
# ~/.bashrc (interactive shell এর জন্য)
# ~/.profile (login shell এর জন্য)
nano ~/.bashrc
# শেষে যোগ করুন:
export EDITOR="nano"
export MY_APP_ENV="development"
export PATH="$HOME/.local/bin:$PATH"

# Apply changes:
source ~/.bashrc                   # বা logout/login

# ── Permanent set — System level ──
sudo nano /etc/environment
# PATH="/usr/local/sbin:..."
# MY_GLOBAL_VAR="value"
# (শুধু KEY="VALUE" format, export লাগে না)

# ── .env file (Application level — ⭐ Docker ও Node.js এ ব্যবহৃত!) ──
# .env file তৈরি:
cat > .env << 'EOF'
NODE_ENV=production
PORT=3000
DATABASE_URL=postgresql://user:pass@localhost/mydb
JWT_SECRET=my-super-secret-key
EOF

# .env load করতে:
export $(grep -v '^#' .env | xargs)

# ⚠️ .env file git এ push করবেন না!
echo ".env" >> .gitignore
```

### System Configuration Files

```bash
# ── গুরুত্বপূর্ণ System Config Files ──
# (এগুলো জানা = Linux admin হওয়া)

# Network:
/etc/hostname                      # System hostname
/etc/hosts                         # Local DNS
/etc/resolv.conf                   # DNS servers
/etc/netplan/*.yaml                # Network config (Ubuntu 18+)

# Users & Auth:
/etc/passwd                        # User accounts
/etc/shadow                        # Password hashes
/etc/group                         # Groups
/etc/sudoers                       # Sudo rules

# System:
/etc/fstab                         # Disk mount config
/etc/crontab                       # System cron jobs
/etc/environment                   # System environment
/etc/timezone                      # Timezone
/etc/locale.conf                   # Locale settings

# Services:
/etc/ssh/sshd_config               # SSH server
/etc/nginx/                        # Nginx
/etc/mysql/                        # MySQL
/etc/systemd/system/               # Custom services

# ── Netplan — Network config (Ubuntu modern way) ──
cat /etc/netplan/*.yaml            # Current config

# Static IP set করা:
sudo nano /etc/netplan/01-netcfg.yaml
# network:
#   version: 2
#   ethernets:
#     eth0:
#       addresses:
#         - 192.168.1.100/24
#       gateway4: 192.168.1.1
#       nameservers:
#         addresses: [8.8.8.8, 8.8.4.4]

sudo netplan apply                 # Apply changes
```

### 📝 Practice (Phase 7.1)

1. `env | head -20` → environment variables দেখুন
2. `.bashrc` এ custom PATH ও alias যোগ করুন
3. `.env` file তৈরি করুন → `export $(grep -v '^#' .env | xargs)` → load
4. `/etc/hosts` এ custom entry যোগ → `ping custom-hostname`
5. Important config files list মুখস্ত করুন

---

## Phase 7.2: Containers Introduction (Docker)

> **🎯 Why This Matters:** Docker হলো modern software distribution ও deployment এর standard। "Works on my machine" problem solve করে। DevOps, AWS ECS, Kubernetes — সবখানে Docker।

### Docker কি?

```
Traditional Deployment:
  App → Depends on OS, versions, libraries → 💥 Conflicts!

Docker Deployment:
  App + Dependencies → Container (isolated) → ✅ Runs anywhere!

┌──────────────────────────────────────────┐
│              Host Machine                │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐   │
│  │ Container│ │ Container│ │ Container│   │
│  │  Node.js │ │  MySQL  │ │  Nginx  │   │
│  │  App     │ │  DB     │ │  Server │   │
│  └─────────┘ └─────────┘ └─────────┘   │
│              Docker Engine               │
│              Ubuntu Server               │
└──────────────────────────────────────────┘
```

### Docker Install

```bash
# ── Official Docker Install (Ubuntu) ──
# Step 1: Prerequisites
sudo apt update
sudo apt install ca-certificates curl gnupg -y

# Step 2: Docker GPG key
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Step 3: Docker repository
echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo $VERSION_CODENAME) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Step 4: Install
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io \
  docker-buildx-plugin docker-compose-plugin -y

# Step 5: User কে docker group এ যোগ (sudo ছাড়া docker চালাতে)
sudo usermod -aG docker $USER
# Logout → Login করুন

# Verify:
docker --version
docker run hello-world             # Test container!
```

### Docker Basic Commands

```bash
# ═══════════════════════════════
# Docker Essential Commands
# ═══════════════════════════════

# ── Images (Blueprint) ──
docker images                      # Downloaded images
docker pull nginx                  # Image download
docker pull node:20-alpine         # Specific version
docker rmi nginx                   # Image delete

# ── Containers (Running instances) ──
docker run nginx                   # Run (foreground)
docker run -d nginx                # -d: Background (detached)
docker run -d -p 80:80 nginx       # -p: Port mapping (host:container)
docker run -d --name web nginx     # --name: Custom name
docker run -d -p 3000:3000 -v $(pwd):/app node:20  # -v: Volume mount

# Container management
docker ps                          # Running containers
docker ps -a                       # All containers (stopped সহ)
docker stop web                    # Stop
docker start web                   # Start
docker restart web                 # Restart
docker rm web                      # Delete (stopped container)
docker rm -f web                   # Force delete (running ও)

# Inspect & Logs
docker logs web                    # Container logs
docker logs -f web                 # Follow logs (live)
docker exec -it web bash           # Container এর ভিতরে যান!
docker inspect web                 # Detailed info

# ── Cleanup ──
docker system prune                # Unused সব delete
docker image prune -a              # Unused images delete
```

### Dockerfile (নিজের Image তৈরি)

```dockerfile
# Dockerfile — React/Node app এর জন্য
FROM node:20-alpine

WORKDIR /app

# Dependencies install (cache friendly!)
COPY package*.json ./
RUN npm install --production

# App code copy
COPY . .

# Build (React)
RUN npm run build

# Port expose
EXPOSE 3000

# Start command
CMD ["node", "server.js"]
```

```bash
# Image build:
docker build -t myapp:1.0 .
# -t = tag (name:version)
# . = current directory (Dockerfile location)

# Run:
docker run -d -p 3000:3000 --name myapp myapp:1.0
```

### Docker Compose (Multi-container)

```yaml
# docker-compose.yml — Full stack app
version: '3.8'

services:
  app:
    build: .
    ports:
      - '3000:3000'
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://user:pass@db/myapp
    depends_on:
      - db

  db:
    image: postgres:16-alpine
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
      - POSTGRES_DB=myapp
    volumes:
      - postgres_data:/var/lib/postgresql/data

  nginx:
    image: nginx:alpine
    ports:
      - '80:80'
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - app

volumes:
  postgres_data:
```

```bash
# Docker Compose commands:
docker compose up -d               # Start all services
docker compose down                # Stop all
docker compose ps                  # Status
docker compose logs -f             # Follow logs
docker compose build               # Rebuild images
```

### 📝 Practice (Phase 7.2)

1. Docker install করুন
2. `docker run hello-world` → test
3. `docker run -d -p 8080:80 nginx` → browser এ `localhost:8080`
4. `docker exec -it <container-id> bash` → container ভিতরে ঢুকুন
5. Simple Dockerfile তৈরি করুন (Node.js app)
6. `docker-compose.yml` তৈরি → `docker compose up -d`

---

## Phase 7.3: Version Control (Git on Linux)

> **🎯 Why This Matters:** Git ছাড়া আধুনিক software development অসম্ভব। Code collaboration, deployment pipeline, CI/CD — সবকিছু Git based। Server এ `git pull` দিয়ে deploy করা standard practice।

### Git Setup

```bash
# ── Install ──
sudo apt install git -y
git --version

# ── Configuration ──
git config --global user.name "Omar Faruk"
git config --global user.email "omar@example.com"
git config --global init.defaultBranch main
git config --global core.editor nano

# Config দেখুন:
git config --list

# ── SSH key for GitHub/GitLab ──
ssh-keygen -t ed25519 -C "omar@example.com"
cat ~/.ssh/id_ed25519.pub
# ↑ Copy করে GitHub → Settings → SSH Keys এ paste করুন

# Test connection:
ssh -T git@github.com              # "Hi username!" → Success!
```

### Essential Git Commands (Linux Terminal)

```bash
# ═══════════════════════════════
# Daily Git Workflow
# ═══════════════════════════════

# ── Repository ──
git init                           # নতুন repo
git clone git@github.com:user/repo.git  # Clone

# ── Basic workflow ──
git status                         # Current state
git add .                          # সব changes stage
git add file.txt                   # নির্দিষ্ট file
git commit -m "Add login feature"  # Commit
git push origin main               # Push to remote

# ── Branching ──
git branch                         # Branches দেখুন
git branch feature/login           # নতুন branch
git checkout feature/login         # Branch switch
git checkout -b feature/login      # Create + switch
git merge feature/login            # Merge

# ── Pull ো sync ──
git pull origin main               # Latest code pull
git fetch origin                   # Fetch without merge
git log --oneline -10              # Last 10 commits

# ── Stash — Temporary save ──
git stash                          # Changes সরিয়ে রাখুন
git stash pop                      # ফিরিয়ে আনুন
git stash list                     # Stash list

# ── Reset ──
git checkout -- file.txt           # File restore
git reset HEAD~1                   # Last commit undo (keeps changes)
git reset --hard HEAD~1            # Last commit undo (⚠️ changes delete!)
```

### Git on Server (Deployment)

```bash
# ── Server এ deploy workflow ──

# Method 1: Direct git pull
ssh deploy@server
cd /var/www/myapp
git pull origin main
npm install
npm run build
pm2 restart myapp

# Method 2: Git hooks (auto-deploy!)
# Server এ bare repo:
mkdir -p /home/deploy/repos/myapp.git
cd /home/deploy/repos/myapp.git
git init --bare

# Post-receive hook:
nano hooks/post-receive
#!/bin/bash
git --work-tree=/var/www/myapp --git-dir=/home/deploy/repos/myapp.git checkout -f
cd /var/www/myapp
npm install
npm run build
pm2 restart myapp
echo "✅ Deployed!"

chmod +x hooks/post-receive

# Local এ remote add:
git remote add production deploy@server:/home/deploy/repos/myapp.git
git push production main           # Push = auto deploy!
```

### 📝 Practice (Phase 7.3)

1. `git config` → name, email set
2. SSH key তৈরি → GitHub এ add
3. Repository clone → branch create → commit → push
4. `git log --oneline --graph` → history দেখুন
5. Server deployment workflow (git pull → build → restart) practice

---

## Phase 7.4: System Virtualization

> **🎯 Why This Matters:** Virtualization হলো cloud computing এর মূল ভিত্তি। AWS EC2 instances মূলত virtual machines। VirtualBox দিয়ে practice করলে AWS এ transition সহজ হবে।

### Virtualization বোঝা

```
Physical Machine (Bare Metal):
┌──────────────────────────────┐
│         Hardware             │
│  ┌────────────────────────┐  │
│  │    Operating System    │  │
│  │  ┌──────┐ ┌──────┐    │  │
│  │  │ App1 │ │ App2 │    │  │
│  │  └──────┘ └──────┘    │  │
│  └────────────────────────┘  │
└──────────────────────────────┘

Virtual Machines:
┌──────────────────────────────┐
│         Hardware             │
│  ┌────────────────────────┐  │
│  │   Host OS + Hypervisor │  │
│  │  ┌──────┐ ┌──────┐    │  │
│  │  │ VM 1 │ │ VM 2 │    │  │
│  │  │Ubuntu│ │CentOS│    │  │
│  │  └──────┘ └──────┘    │  │
│  └────────────────────────┘  │
└──────────────────────────────┘

Containers (Docker):
┌──────────────────────────────┐
│         Hardware             │
│  ┌────────────────────────┐  │
│  │   Host OS + Docker     │  │
│  │  ┌────┐┌────┐┌────┐   │  │
│  │  │C1  ││C2  ││C3  │   │  │
│  │  │Node││MySQL││Nginx│  │  │
│  │  └────┘└────┘└────┘   │  │
│  └────────────────────────┘  │
└──────────────────────────────┘
```

### VirtualBox (Practice Environment)

```bash
# ── VirtualBox install (Ubuntu Host) ──
sudo apt install virtualbox virtualbox-ext-pack -y

# ── Command line VM management ──
VBoxManage list vms                # VM list
VBoxManage startvm "MyVM"          # Start
VBoxManage controlvm "MyVM" poweroff  # Stop
VBoxManage showvminfo "MyVM"       # Info

# ── Vagrant — VM automation (VirtualBox + Vagrant) ──
sudo apt install vagrant -y

# Vagrantfile তৈরি:
vagrant init ubuntu/jammy64        # Ubuntu 22.04 VM
vagrant up                         # VM start
vagrant ssh                        # VM এ SSH
vagrant halt                       # VM stop
vagrant destroy                    # VM delete
```

### VM vs Container পার্থক্য

```
┌──────────────────┬──────────────────┬──────────────────┐
│ Feature          │ Virtual Machine  │ Container        │
├──────────────────┼──────────────────┼──────────────────┤
│ Size             │ GB (full OS)     │ MB (lightweight) │
│ Start time       │ Minutes          │ Seconds          │
│ Isolation        │ Full (separate   │ Process-level    │
│                  │ OS kernel)       │ (shared kernel)  │
│ Resource usage   │ Heavy            │ Light            │
│ Use case         │ Different OS,    │ Microservices,   │
│                  │ full isolation   │ deployment       │
│ Example          │ AWS EC2          │ Docker, K8s      │
│ Portability      │ Less portable    │ Highly portable  │
└──────────────────┴──────────────────┴──────────────────┘
```

### 📝 Practice (Phase 7.4)

1. VM vs Container comparison chart মুখস্ত করুন
2. VirtualBox/Vagrant ব্যবহার করে Ubuntu Server VM তৈরি করুন
3. VM এ SSH করুন → web server setup practice
4. Docker container vs VM — resource usage compare (`docker stats` vs `htop`)

---

## Phase 7.5: Cloud ও AWS Preparation

> **🎯 Why This Matters:** এই পুরো গাইড এর ultimate goal — Cloud ও AWS এ কাজ করার জন্য প্রস্তুত হওয়া। এই Phase এ আপনি দেখবেন আগের সব Section এর knowledge কিভাবে AWS তে connect হয়।

### Linux → AWS Skill Mapping

```
┌────────────────────────────────┬──────────────────────────────────┐
│ আপনি যা শিখেছেন (Linux)        │ AWS তে কোথায় লাগবে              │
├────────────────────────────────┼──────────────────────────────────┤
│ File system, Permissions       │ EC2 instance management         │
│ SSH, Key-based auth            │ EC2 SSH access, Key Pairs       │
│ UFW Firewall                   │ Security Groups                 │
│ Nginx, Reverse proxy           │ EC2 + Application Load Balancer │
│ MySQL, PostgreSQL              │ RDS (Managed Database)          │
│ systemd services               │ EC2 app management              │
│ Cron jobs                      │ EventBridge / Lambda scheduled  │
│ Environment variables          │ Parameter Store, Secrets Manager│
│ Docker, Compose                │ ECS, ECR, Fargate               │
│ Shell scripts                  │ User Data, Automation           │
│ Log management                 │ CloudWatch Logs                 │
│ System monitoring              │ CloudWatch Metrics & Alarms     │
│ Networking, DNS                │ VPC, Route 53                   │
│ SSL/TLS certificates           │ ACM (Certificate Manager)       │
│ Backup                         │ S3, EBS Snapshots               │
│ Git                            │ CodeCommit, CodePipeline        │
└────────────────────────────────┴──────────────────────────────────┘
```

### AWS EC2 Quick Start

```bash
# ═══════════════════════════════════════════════
# ⭐ AWS EC2 Instance Launch → Setup → Deploy
# (আপনি already সব commands জানেন!)
# ═══════════════════════════════════════════════

# Step 1: AWS Console → EC2 → Launch Instance
# - AMI: Ubuntu 24.04 LTS
# - Instance type: t2.micro (free tier!)
# - Key pair: Download .pem file → chmod 400
# - Security Group: SSH (22), HTTP (80), HTTPS (443)

# Step 2: SSH Connect
chmod 400 my-key.pem
ssh -i my-key.pem ubuntu@ec2-xx-xx-xx-xx.compute.amazonaws.com

# Step 3: Server setup (Section 6.1 Checklist!)
sudo apt update && sudo apt upgrade -y
sudo hostnamectl set-hostname production-server
sudo timedatectl set-timezone Asia/Dhaka

# Step 4: Security (Section 4.6!)
sudo adduser deploy
sudo usermod -aG sudo deploy
# SSH key copy, firewall setup, fail2ban...

# Step 5: Web server (Section 6.3!)
sudo apt install nginx -y
sudo ufw allow 'Nginx Full'

# Step 6: App deploy (Section 6.5!)
# Git clone → npm install → npm build → PM2 start → Nginx reverse proxy

# Step 7: SSL (Section 4.7!)
sudo certbot --nginx -d myapp.com

# ✅ Production-ready app on AWS! 🎉
```

### AWS CLI (Command Line)

```bash
# ── AWS CLI Install ──
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version

# ── Configure ──
aws configure
# AWS Access Key ID: XXXXXXXXXX
# AWS Secret Access Key: YYYYYYYYYY
# Default region: ap-southeast-1
# Default output format: json

# ── Basic commands ──
aws s3 ls                          # S3 buckets list
aws s3 cp file.txt s3://my-bucket/ # Upload to S3
aws s3 sync ./dist s3://my-bucket/ # Sync folder

aws ec2 describe-instances         # EC2 instances
aws ec2 start-instances --instance-ids i-xxxxx
aws ec2 stop-instances --instance-ids i-xxxxx
```

### Next Steps — আপনার Learning Path

```
🎓 আপনি এখন Linux এ Confident!
আপনার পরবর্তী Journey:

├── 🔒 Cyber Security Path
│   ├── Kali Linux
│   ├── Penetration Testing
│   ├── Network Security
│   └── OWASP, Burp Suite
│
├── ⚙️ DevOps Path
│   ├── Docker (Advanced) ← আপনি basics জানেন!
│   ├── Kubernetes (K8s)
│   ├── CI/CD (GitHub Actions, Jenkins)
│   ├── Terraform (Infrastructure as Code)
│   └── Ansible (Configuration Management)
│
└── ☁️ AWS Path
    ├── EC2, S3, RDS ← আপনি ready!
    ├── VPC, IAM, CloudWatch
    ├── ECS/Fargate (Docker on AWS)
    ├── Lambda (Serverless)
    ├── CloudFormation/CDK
    └── AWS Certified Solutions Architect
```

### 📝 Practice (Phase 7.5)

1. AWS Free Tier account তৈরি করুন
2. EC2 instance launch → SSH connect → server setup
3. Nginx + React app deploy করুন AWS EC2 তে
4. AWS CLI install → `aws configure` → `aws s3 ls`
5. **Final Challenge:** Complete production deployment: EC2 → Nginx → PM2 → SSL → Domain

---

### 📝 Section 7 Final Project

**প্রজেক্ট: Complete Production Deployment**

আপনার React + Node.js app কে AWS EC2 তে deploy করুন:

1. ✅ EC2 instance launch (Ubuntu 24.04)
2. ✅ SSH connect → server setup (checklist follow)
3. ✅ Firewall configure (UFW)
4. ✅ Node.js install (nvm)
5. ✅ Git clone → npm install → build
6. ✅ PM2 দিয়ে API চালান
7. ✅ Nginx reverse proxy setup
8. ✅ SSL certificate (Let's Encrypt)
9. ✅ Domain point করুন
10. ✅ Monitoring ও backup setup

---

# 🎉 অভিনন্দন! গাইড সম্পূর্ণ!

আপনি এই গাইড থেকে যা শিখেছেন:

| Section   | বিষয়                            | Phases |
| --------- | -------------------------------- | ------ |
| 1         | Linux Foundation                 | 5      |
| 2         | Command Line Mastery             | 7      |
| 3         | System Administration            | 8      |
| 4         | Networking & Security            | 7      |
| 5         | Shell Scripting & Automation     | 6      |
| 6         | Server Administration            | 6      |
| 7         | Advanced Linux & Cloud Readiness | 5      |
| **Total** | **Complete Linux Knowledge**     | **44** |

> **💡 মনে রাখুন:** Linux শেখা একটি journey, destination না। প্রতিদিন terminal ব্যবহার করুন, scripts লিখুন, server manage করুন — এভাবেই fluency আসবে।
>
> **🚀 আপনার পরবর্তী step:** AWS Free Tier এ EC2 launch করুন এবং এই গাইডের সব knowledge apply করুন। Real-world experience ই সবচেয়ে বড় শিক্ষক।

---

_Guide Version: 2.0 | Last Updated: February 2026 | Created for: Ubuntu 24.04 LTS_
_Total Phases: 44 | Estimated Completion: ৩-৪ মাস (প্রতিদিন ২-৩ ঘণ্টা)_

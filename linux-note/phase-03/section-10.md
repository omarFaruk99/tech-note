# 📖 Section 10: System Information ও Monitoring

---

## 🎯 এই Section-এ যা শিখবেন

- সিস্টেমের সম্পূর্ণ তথ্য সংগ্রহ করা
- CPU, RAM, Disk, Network-এর তথ্য দেখা
- System uptime ও load average বোঝা
- Hardware তথ্য দেখা
- Performance Monitoring

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড      |  Ubuntu 24 LTS-এ   | মন্তব্য                     |
| ----------- | :----------------: | --------------------------- |
| `uname`     |  ✅ Pre-installed  | Kernel/OS তথ্য              |
| `hostname`  |  ✅ Pre-installed  | কম্পিউটারের নাম             |
| `uptime`    |  ✅ Pre-installed  | কতক্ষণ ধরে চালু             |
| `free`      |  ✅ Pre-installed  | RAM তথ্য                    |
| `df`        |  ✅ Pre-installed  | Disk space                  |
| `du`        |  ✅ Pre-installed  | ফোল্ডারের আকার              |
| `lscpu`     |  ✅ Pre-installed  | CPU তথ্য                    |
| `lsblk`     |  ✅ Pre-installed  | Block device (disk) তালিকা  |
| `lsusb`     |  ✅ Pre-installed  | USB device তালিকা           |
| `lspci`     |  ✅ Pre-installed  | PCI device তালিকা           |
| `lshw`      |  ✅ Pre-installed  | সম্পূর্ণ hardware তথ্য      |
| `dmidecode` |  ✅ Pre-installed  | BIOS/hardware details       |
| `vmstat`    |  ✅ Pre-installed  | Virtual memory stats        |
| `iostat`    | ❌ ইন্সটল করতে হবে | `sudo apt install sysstat`  |
| `neofetch`  | ❌ ইন্সটল করতে হবে | `sudo apt install neofetch` |
| `inxi`      | ❌ ইন্সটল করতে হবে | `sudo apt install inxi`     |
| `nmon`      | ❌ ইন্সটল করতে হবে | `sudo apt install nmon`     |

---

## 1️⃣ OS ও Kernel তথ্য

### `uname` — System Information

```bash
# সব তথ্য দেখুন
uname -a
# Linux ubuntu 6.8.0-41-generic #41-Ubuntu SMP ... x86_64 GNU/Linux
```

| Flag | কাজ                      | উদাহরণ আউটপুট      |
| ---- | ------------------------ | ------------------ |
| `-a` | **a**ll — সব তথ্য        | সম্পূর্ণ লাইন      |
| `-s` | Kernel নাম               | `Linux`            |
| `-r` | Kernel **r**elease       | `6.8.0-41-generic` |
| `-m` | **m**achine type         | `x86_64`           |
| `-n` | **n**ode name (hostname) | `ubuntu`           |
| `-o` | **o**perating system     | `GNU/Linux`        |

### OS-এর বিস্তারিত তথ্য:

```bash
# Ubuntu version ও release তথ্য
cat /etc/os-release

# সংক্ষিপ্তে
lsb_release -a
```

### `hostname` — কম্পিউটারের নাম

```bash
hostname
# ubuntu

# IP address সহ
hostname -I
# 192.168.1.100
```

### `neofetch` — সুন্দর System Info

```bash
# ইন্সটল করুন (প্রথমবার)
sudo apt install -y neofetch

# চালান
neofetch
```

> 💡 `neofetch` রঙিন ASCII art সহ আপনার সিস্টেমের সব তথ্য দেখায় — OS, Kernel, CPU, RAM, GPU, Shell, Terminal, Resolution সব!

---

## 2️⃣ `uptime` — কতক্ষণ ধরে চালু

```bash
uptime
# 02:15:00 up  3:30,  1 user,  load average: 0.52, 0.34, 0.28
```

**ব্যাখ্যা:**

```
02:15:00    → বর্তমান সময়
up 3:30     → ৩ ঘণ্টা ৩০ মিনিট ধরে চালু আছে
1 user      → ১ জন logged in
load average: 0.52, 0.34, 0.28
              │     │     └── শেষ ১৫ মিনিটের গড় ভার
              │     └── শেষ ৫ মিনিটের গড় ভার
              └── শেষ ১ মিনিটের গড় ভার
```

### Load Average বোঝা:

| CPU Cores | Load = 1.0 মানে | Load = 2.0 মানে   |
| --------- | --------------- | ----------------- |
| 1 core    | ১০০% ব্যস্ত ⚠️  | ২০০% — সমস্যা! 🔴 |
| 2 cores   | ৫০% ব্যস্ত ✅   | ১০০% ব্যস্ত ⚠️    |
| 4 cores   | ২৫% ব্যস্ত ✅   | ৫০% ব্যস্ত ✅     |

> 💡 **নিয়ম:** Load average < CPU core সংখ্যা হলে ভালো। বেশি হলে সিস্টেম ধীর হয়ে যাচ্ছে।

---

## 3️⃣ `free` — RAM তথ্য

```bash
# Human-readable format-এ
free -h
```

**আউটপুট:**

```
               total        used        free      shared  buff/cache   available
Mem:           7.7Gi       2.8Gi       3.3Gi       256Mi       1.6Gi       4.6Gi
Swap:          2.0Gi          0B       2.0Gi
```

| কলাম           | অর্থ                                |
| -------------- | ----------------------------------- |
| **total**      | মোট RAM                             |
| **used**       | ব্যবহৃত                             |
| **free**       | সম্পূর্ণ ফাঁকা                      |
| **buff/cache** | Buffer/cache (দরকার হলে ছেড়ে দেবে) |
| **available**  | আসলে কতটুকু ব্যবহারযোগ্য ✅         |
| **Swap**       | Hard disk-এ অতিরিক্ত "RAM"          |

> 💡 **গুরুত্বপূর্ণ:** `free` কলাম নয়, **`available`** কলাম দেখুন। `buff/cache` এর মেমরি দরকার হলে স্বয়ংক্রিয়ভাবে ছেড়ে দেয়।

| Flag   | কাজ                              |
| ------ | -------------------------------- |
| `-h`   | **h**uman readable (GB, MB)      |
| `-m`   | **M**egabytes-এ                  |
| `-g`   | **G**igabytes-এ                  |
| `-s 2` | প্রতি **2** সেকেন্ডে আপডেট দেখাও |

```bash
# প্রতি ২ সেকেন্ডে RAM দেখুন (Ctrl+C দিয়ে বন্ধ)
free -h -s 2
```

### Swap কী?

**Swap** = Hard disk-এর একটি অংশ যেটি RAM ভরে গেলে অতিরিক্ত "RAM" হিসেবে ব্যবহৃত হয়।

> 🐌 Swap ব্যবহার হচ্ছে মানে RAM কম। Swap ব্যবহার হলে কম্পিউটার **ধীর** হয়ে যায়, কারণ Hard disk RAM-এর চেয়ে অনেক ধীর।

---

## 4️⃣ `df` — Disk Space দেখা

**কাজ:** Disk-এ কতটুকু জায়গা আছে/ব্যবহৃত হচ্ছে দেখায়।

**মনে রাখুন:** "**D**isk **F**ree" = "ডিস্ক খালি কতটুকু"

```bash
df -h
```

**আউটপুট:**

```
Filesystem      Size  Used  Avail Use%  Mounted on
/dev/sda1       100G   25G    70G  26%  /
tmpfs           3.9G   12M   3.9G   1%  /dev/shm
/dev/sda2       500G  120G   355G  26%  /home
```

| কলাম       | অর্থ                 |
| ---------- | -------------------- |
| Filesystem | ডিস্ক/পার্টিশনের নাম |
| Size       | মোট আকার             |
| Used       | ব্যবহৃত              |
| Avail      | খালি আছে             |
| Use%       | ব্যবহারের শতকরা হার  |
| Mounted on | কোথায় সংযুক্ত       |

> ⚠️ **সতর্কতা:** `Use%` ৯০%-এর উপরে গেলে সতর্ক হোন। ১০০% হলে সিস্টেম সঠিকভাবে কাজ করবে না!

```bash
# নির্দিষ্ট directory-র তথ্য
df -h /home

# ফাইল সিস্টেম type সহ
df -hT
```

---

## 5️⃣ `du` — ফোল্ডারের আকার

**কাজ:** কোনো ফোল্ডার বা ফাইল কতটুকু জায়গা নিচ্ছে দেখায়।

**মনে রাখুন:** "**D**isk **U**sage" = "ডিস্ক ব্যবহার"

```bash
# Home directory-র আকার (সারসংক্ষেপ)
du -sh ~
# 5.2G    /home/the-king

# Home-এর ভিতরের প্রতিটি ফোল্ডারের আকার
du -sh ~/*
# 1.2G    /home/the-king/Downloads
# 500M    /home/the-king/Documents
# 200M    /home/the-king/Pictures
# ...

# সবচেয়ে বড় ১০টি ফোল্ডার খুঁজুন
du -sh ~/* | sort -rh | head -10
```

| Flag            | অর্থ                      |
| --------------- | ------------------------- |
| `-s`            | **s**ummary — শুধু মোট    |
| `-h`            | **h**uman readable        |
| `--max-depth=1` | শুধু প্রথম স্তরের ফোল্ডার |

### df vs du:

| কমান্ড | কী দেখায়                        | কখন ব্যবহার                 |
| ------ | -------------------------------- | --------------------------- |
| `df`   | পুরো **disk/partition**-এর space | "ডিস্কে কতটুকু জায়গা আছে?" |
| `du`   | নির্দিষ্ট **ফোল্ডারের** আকার     | "এই ফোল্ডার কত বড়?"        |

---

## 6️⃣ Hardware তথ্য

### `lscpu` — CPU তথ্য

```bash
lscpu
```

**গুরুত্বপূর্ণ তথ্য:**

```
Architecture:          x86_64        ← ৬৪-বিট
CPU(s):                8             ← মোট ৮টি CPU thread
Model name:            Intel i7-...  ← প্রসেসরের নাম
CPU max MHz:           4500.0000     ← সর্বোচ্চ গতি
```

### `lsblk` — Disk/Storage Device

```bash
lsblk
```

```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0   500G  0 disk
├─sda1   8:1    0   100G  0 part /
├─sda2   8:2    0   398G  0 part /home
└─sda3   8:3    0     2G  0 part [SWAP]
```

### `lsusb` — USB Device তালিকা

```bash
lsusb
# Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
# Bus 001 Device 003: ID 046d:c52b Logitech Wireless Mouse
```

### `lspci` — PCI Device (GPU, WiFi card, etc.)

```bash
lspci
# 00:02.0 VGA compatible controller: Intel Corporation...
# 02:00.0 Network controller: Intel Corporation WiFi...
```

```bash
# শুধু GPU দেখুন
lspci | grep -i vga

# শুধু Network দেখুন
lspci | grep -i network
```

### `lshw` — সম্পূর্ণ Hardware তথ্য

```bash
# সংক্ষিপ্ত তালিকা
sudo lshw -short
```

---

## 7️⃣ `/proc` — Virtual Filesystem

`/proc` হলো একটি বিশেষ ফোল্ডার যেখানে সিস্টেমের **real-time** তথ্য থাকে:

```bash
# CPU-র বিস্তারিত তথ্য
cat /proc/cpuinfo

# RAM-এর তথ্য
cat /proc/meminfo

# Kernel version
cat /proc/version

# System uptime (সেকেন্ডে)
cat /proc/uptime

# Mount করা file system
cat /proc/mounts
```

> 💡 `/proc` এর ফাইলগুলো আসল ফাইল নয় — Kernel এগুলো **গতিশীলভাবে তৈরি** করে। প্রতিবার পড়লে নতুন তথ্য পাবেন!

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কমান্ড     | কী দেখায়       | উদাহরণ            |
| ---------- | --------------- | ----------------- |
| `uname -a` | OS/Kernel তথ্য  | Kernel version    |
| `hostname` | কম্পিউটারের নাম | `ubuntu`          |
| `uptime`   | কতক্ষণ ধরে চালু | `up 3:30`         |
| `free -h`  | RAM তথ্য        | ৭.৭ GB total      |
| `df -h`    | Disk space      | ১০০ GB partition  |
| `du -sh`   | ফোল্ডারের আকার  | ৫.২ GB home       |
| `lscpu`    | CPU তথ্য        | Intel i7, 8 cores |
| `lsblk`    | Disk/partition  | sda, 500GB        |
| `lsusb`    | USB devices     | Mouse, keyboard   |
| `lspci`    | PCI devices     | GPU, WiFi         |
| `neofetch` | সুন্দর summary  | সব কিছু একসাথে    |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: সিস্টেম তথ্য সংগ্রহ

নিচের সব কমান্ড চালিয়ে আপনার সিস্টেমের তথ্য সংগ্রহ করুন:

```bash
# 1. OS ও Kernel
uname -a

# 2. Ubuntu version
lsb_release -a

# 3. Hostname ও IP
hostname
hostname -I

# 4. Uptime
uptime

# 5. CPU
lscpu | head -15

# 6. RAM
free -h

# 7. Disk
df -h

# 8. Home ফোল্ডারের আকার
du -sh ~

# 9. USB devices
lsusb

# 10. (Optional) neofetch
sudo apt install -y neofetch && neofetch
```

### অনুশীলন ২: Disk Analysis

```bash
# 1. কোন partition-এ সবচেয়ে বেশি জায়গা ব্যবহৃত?
df -h

# 2. Home-এর কোন ফোল্ডার সবচেয়ে বড়?
du -sh ~/* 2>/dev/null | sort -rh | head -5

# 3. Downloads-এ কত জায়গা নিচ্ছে?
du -sh ~/Downloads
```

### অনুশীলন ৩: RAM Monitoring

```bash
# 1. RAM দেখুন
free -h

# 2. বর্তমানে available কত?
free -h | grep Mem

# 3. Swap ব্যবহার হচ্ছে কি?
free -h | grep Swap
```

---

## ➡️ পরবর্তী Section

[Section 11: Service Management (systemd) →](section-11.md)

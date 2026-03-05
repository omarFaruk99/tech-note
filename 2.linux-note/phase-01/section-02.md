# 📖 Section 02: Terminal পরিচিতি ও Basic Navigation

---

## 🎯 এই Section-এ যা শিখবেন

- Terminal কী এবং কেন গুরুত্বপূর্ণ
- Terminal খোলার উপায়
- Shell কী (Bash)
- Prompt চেনা ও বোঝা
- Linux File System Structure
- pwd, ls, cd — Navigation-এর মূল কমান্ড
- Absolute Path vs Relative Path
- `clear`, `history`, `whoami` এবং আরও কিছু সহায়ক কমান্ড

---

## 🖥️ Terminal কী?

**Terminal** (বা **Terminal Emulator**) হলো একটি অ্যাপ্লিকেশন যেখানে আপনি **টেক্সট কমান্ড** লিখে কম্পিউটারকে নির্দেশ দেন।

### সহজ উদাহরণ:

GUI (মাউস) দিয়ে একটি ফোল্ডার তৈরি করতে:

1. Files app খুলুন
2. Right click করুন
3. "New Folder" ক্লিক করুন
4. নাম লিখুন
5. Enter চাপুন

Terminal-এ একই কাজ:

```bash
mkdir my-folder
```

**ব্যাস! একটি কমান্ডেই কাজ শেষ!** ⚡

---

## 🚀 Terminal খোলার উপায়

| পদ্ধতি                | কিভাবে                                             |
| --------------------- | -------------------------------------------------- |
| **Keyboard Shortcut** | `Ctrl + Alt + T` (সবচেয়ে দ্রুত ✅)                |
| **Activities Menu**   | উপরে-বাঁয়ে "Activities" → "Terminal" সার্চ করুন   |
| **Right Click**       | Desktop-এ/Files-এ Right Click → "Open in Terminal" |

> 💡 **পরামর্শ:** `Ctrl + Alt + T` মুখস্থ করে ফেলুন। এটি সবচেয়ে বেশি ব্যবহার হবে।

---

## 🐚 Shell কী?

**Shell** হলো একটি **Command Interpreter** — এটি আপনার লেখা কমান্ড পড়ে, বোঝে এবং Kernel-এর কাছে পাঠায়।

### Shell-এর কাজের ধাপ:

```
আপনি কমান্ড লিখলেন → Shell পড়ল → Kernel-এর কাছে পাঠাল → Kernel কাজ করল → ফলাফল দেখাল
```

### বিভিন্ন Shell:

| Shell    | পুরো নাম                   | বিবরণ                           |
| -------- | -------------------------- | ------------------------------- |
| **bash** | Bourne Again SHell         | Ubuntu-র default shell ✅       |
| **zsh**  | Z Shell                    | macOS-এর default, বেশি features |
| **sh**   | Bourne Shell               | সবচেয়ে পুরনো, basic            |
| **fish** | Friendly Interactive Shell | User-friendly, colorful         |

> আপনি Ubuntu 24-তে **bash** ব্যবহার করছেন। এই গাইডের সব কমান্ড bash-এ চলবে।

### আপনার Shell দেখুন:

```bash
echo $SHELL
```

**ব্যাখ্যা:**

- `echo` = পর্দায় কিছু প্রিন্ট/দেখানো
- `$SHELL` = একটি **environment variable** যেটি বর্তমান shell-এর পথ ধারণ করে

**আউটপুট:**

```
/bin/bash
```

---

## 📟 Terminal Prompt বোঝা

Terminal খুললে আপনি এরকম কিছু দেখবেন:

```
the-king@ubuntu:~$
```

এটিকে বলে **Prompt**। আসুন প্রতিটি অংশ বুঝি:

```
the-king  @  ubuntu  :  ~  $
   │      │    │     │  │  │
   │      │    │     │  │  └── $ = সাধারণ user (# হলে root/admin)
   │      │    │     │  └──── ~ = আপনি Home directory-তে আছেন
   │      │    │     └──────── : = বিভাজক
   │      │    └────────────── ubuntu = কম্পিউটারের নাম (hostname)
   │      └─────────────────── @ = "at" — কোন কম্পিউটারে
   └────────────────────────── the-king = আপনার username
```

### গুরুত্বপূর্ণ চিহ্ন:

| চিহ্ন | অর্থ                                              |
| ----- | ------------------------------------------------- |
| `$`   | আপনি সাধারণ (normal) user                         |
| `#`   | আপনি **root** (superuser/admin) — সর্বোচ্চ ক্ষমতা |
| `~`   | Home directory (`/home/your-username`)            |

> ⚠️ **সতর্কতা:** `#` দেখলে সাবধান! Root user হিসেবে ভুল কমান্ড দিলে পুরো সিস্টেম নষ্ট হতে পারে।

---

## 📁 Linux File System Structure

Windows-এ `C:\`, `D:\` ড্রাইভ থাকে। কিন্তু Linux-এ সব কিছু **একটি গাছের (tree) মতো** structure-এ থাকে, যেখানে root হলো `/`।

```
/ (root — সবকিছুর শুরু)
├── home/          ← ব্যবহারকারীদের ব্যক্তিগত ফোল্ডার
│   └── the-king/  ← আপনার Home directory (~)
│       ├── Desktop/
│       ├── Documents/
│       ├── Downloads/
│       ├── Music/
│       ├── Pictures/
│       └── Videos/
├── etc/           ← সিস্টেমের সব configuration ফাইল
├── var/           ← পরিবর্তনশীল ডেটা (logs, cache)
├── tmp/           ← অস্থায়ী ফাইল (reboot-এ মুছে যায়)
├── usr/           ← User programs ও libraries
│   ├── bin/       ← User commands
│   ├── lib/       ← Libraries
│   └── share/     ← Shared data
├── bin/           ← অত্যাবশ্যক কমান্ড (ls, cp, mv)
├── sbin/          ← System/admin কমান্ড
├── dev/           ← Device files (hardware-এর প্রতিনিধি)
├── proc/          ← চলমান process-এর তথ্য
├── opt/           ← তৃতীয় পক্ষের সফটওয়্যার
├── root/          ← Root user-এর Home directory
├── boot/          ← বুটিং সম্পর্কিত ফাইল
└── mnt/ ও media/  ← বাহ্যিক ডিভাইস mount হয় এখানে
```

### প্রতিটি ফোল্ডারের বিস্তারিত:

| ফোল্ডার  | পুরো নাম              | কাজ                              | উদাহরণ                   |
| -------- | --------------------- | -------------------------------- | ------------------------ |
| `/`      | Root                  | সবকিছুর শুরু বিন্দু              | পুরো file system         |
| `/home`  | Home                  | ব্যবহারকারীদের ব্যক্তিগত ফোল্ডার | `/home/the-king`         |
| `/etc`   | Et Cetera             | সিস্টেম সেটিংস ফাইল              | `/etc/hostname`          |
| `/var`   | Variable              | পরিবর্তনশীল ডেটা                 | `/var/log/syslog`        |
| `/tmp`   | Temporary             | অস্থায়ী ফাইল                    | Reboot-এ মুছে যায়       |
| `/usr`   | Unix System Resources | প্রোগ্রাম ও লাইব্রেরি            | `/usr/bin/python3`       |
| `/bin`   | Binaries              | অত্যাবশ্যক কমান্ড                | `ls`, `cp`, `mv`         |
| `/sbin`  | System Binaries       | Admin কমান্ড                     | `fdisk`, `reboot`        |
| `/dev`   | Devices               | হার্ডওয়্যার ডিভাইস ফাইল         | `/dev/sda` (হার্ড ডিস্ক) |
| `/proc`  | Processes             | চলমান প্রক্রিয়ার তথ্য           | `/proc/cpuinfo`          |
| `/boot`  | Boot                  | বুটিং ফাইল                       | Kernel image             |
| `/media` | Media                 | USB/CD auto-mount                | পেনড্রাইভ                |
| `/mnt`   | Mount                 | ম্যানুয়াল mount                 | বাহ্যিক ডিস্ক            |
| `/opt`   | Optional              | তৃতীয় পক্ষের software           | Google Chrome            |
| `/root`  | Root Home             | Root user-এর ঘর                  | শুধু root-এর জন্য        |

### Windows vs Linux তুলনা:

| Windows               | Linux                       | ব্যাখ্যা              |
| --------------------- | --------------------------- | --------------------- |
| `C:\`                 | `/`                         | মূল ড্রাইভ            |
| `C:\Users\the-king`   | `/home/the-king`            | ব্যক্তিগত ফোল্ডার     |
| `C:\Program Files`    | `/usr/bin` বা `/opt`        | ইন্সটল করা সফটওয়্যার |
| `C:\Windows\System32` | `/bin` ও `/sbin`            | সিস্টেম কমান্ড        |
| `D:\` (আলাদা ড্রাইভ)  | `/mnt/data` বা `/media/...` | অতিরিক্ত ড্রাইভ mount |

> 💡 **Linux-এ সব কিছুই ফাইল!** — এমনকি আপনার কীবোর্ড, মাউস, হার্ডডিস্কও `/dev/` ফোল্ডারে ফাইল হিসেবে থাকে। এটি Linux-এর মৌলিক দর্শন।

---

## 🧭 Navigation কমান্ড — pwd, ls, cd

এই তিনটি কমান্ড Linux-এর সবচেয়ে বেশি ব্যবহৃত কমান্ড। এগুলো ছাড়া Linux ব্যবহার করাই সম্ভব না।

---

### 1️⃣ `pwd` — Print Working Directory

**কাজ:** আপনি এই মুহূর্তে কোন ফোল্ডারে আছেন তা দেখায়।

**মনে রাখুন:** "**P**rint **W**orking **D**irectory" = "কাজের ডিরেক্টরি প্রিন্ট করো"

```bash
pwd
```

**আউটপুট:**

```
/home/the-king
```

**Real-Life তুলনা:**

> GPS-এ "আমি এখন কোথায়?" জিজ্ঞেস করার মতো। `pwd` আপনাকে বলে দেয় আপনি file system-এর ঠিক কোথায় দাঁড়িয়ে আছেন।

---

### 2️⃣ `ls` — List

**কাজ:** বর্তমান ফোল্ডারের ভিতরে কী কী আছে তা দেখায়।

**মনে রাখুন:** "**L**i**s**t" = "তালিকা দেখাও"

#### মৌলিক ব্যবহার:

```bash
ls
```

**আউটপুট:**

```
Desktop  Documents  Downloads  Music  Pictures  Videos
```

#### গুরুত্বপূর্ণ Options/Flags:

| কমান্ড   | Flag-এর অর্থ              | কাজ                                  |
| -------- | ------------------------- | ------------------------------------ |
| `ls -l`  | **l**ong format           | বিস্তারিত তথ্য সহ দেখায়             |
| `ls -a`  | **a**ll                   | লুকানো ফাইলও দেখায় (`.` দিয়ে শুরু) |
| `ls -la` | long + all                | সব ফাইল বিস্তারিতভাবে                |
| `ls -lh` | long + **h**uman readable | ফাইল সাইজ সহজে পড়া যায় (KB, MB)    |
| `ls -lt` | long + **t**ime sorted    | সময় অনুযায়ী সাজায় (নতুন আগে)      |
| `ls -lS` | long + **S**ize sorted    | আকার অনুযায়ী সাজায় (বড় আগে)       |
| `ls -R`  | **R**ecursive             | সব sub-folder-এর ভিতরেও দেখায়       |

#### `ls -la` এর আউটপুট বোঝা:

```bash
ls -la
```

```
total 40
drwxr-xr-x 5 the-king the-king 4096 Mar  5 01:00 .
drwxr-xr-x 3 root     root     4096 Mar  4 20:00 ..
-rw-r--r-- 1 the-king the-king  220 Mar  4 20:00 .bashrc
drwxr-xr-x 2 the-king the-king 4096 Mar  5 01:00 Desktop
drwxr-xr-x 2 the-king the-king 4096 Mar  5 01:00 Documents
-rw-r--r-- 1 the-king the-king  807 Mar  4 20:00 .profile
```

**প্রতিটি কলামের ব্যাখ্যা:**

```
-rw-r--r--  1  the-king  the-king  807  Mar 5 01:00  .profile
│            │     │         │      │       │           │
│            │     │         │      │       │           └── ফাইলের নাম
│            │     │         │      │       └── শেষ পরিবর্তনের তারিখ ও সময়
│            │     │         │      └── ফাইলের আকার (bytes)
│            │     │         └── Group (গোষ্ঠী)
│            │     └── Owner (মালিক)
│            └── Hard links-এর সংখ্যা
└── Permission (অনুমতি) — পরে বিস্তারিত শিখব
```

#### নির্দিষ্ট ফোল্ডারের ভিতর দেখা:

```bash
# Downloads ফোল্ডারের ভিতর দেখুন
ls -la Downloads/

# /etc ফোল্ডার দেখুন
ls /etc
```

> 💡 **লুকানো ফাইল:** Linux-এ যে ফাইল/ফোল্ডারের নাম `.` (ডট) দিয়ে শুরু হয় সেগুলো লুকানো থাকে। যেমন `.bashrc`, `.profile`। এগুলো দেখতে `ls -a` লাগবে।

---

### 3️⃣ `cd` — Change Directory

**কাজ:** এক ফোল্ডার থেকে অন্য ফোল্ডারে যাওয়া।

**মনে রাখুন:** "**C**hange **D**irectory" = "ডিরেক্টরি বদলাও"

#### মৌলিক ব্যবহার:

```bash
# Documents ফোল্ডারে যান
cd Documents

# আপনি কোথায় আছেন দেখুন
pwd
# আউটপুট: /home/the-king/Documents
```

#### গুরুত্বপূর্ণ cd shortcuts:

| কমান্ড     | কাজ                        | ব্যাখ্যা                |
| ---------- | -------------------------- | ----------------------- |
| `cd`       | Home directory-তে ফিরে যান | যেকোনো জায়গা থেকে      |
| `cd ~`     | Home directory-তে ফিরে যান | `cd` এর মতোই            |
| `cd ..`    | এক ধাপ পিছনে (parent) যান  | `..' = parent directory |
| `cd ../..` | দুই ধাপ পিছনে যান          | —                       |
| `cd -`     | আগের ফোল্ডারে ফিরে যান     | "undo" এর মতো           |
| `cd /`     | Root directory-তে যান      | সবার উপরে               |

#### ধাপে ধাপে উদাহরণ:

```bash
# Home-এ আছেন
pwd
# /home/the-king

# Documents-এ যান
cd Documents
pwd
# /home/the-king/Documents

# এক ধাপ পিছনে (Home-এ ফিরুন)
cd ..
pwd
# /home/the-king

# Downloads-এ যান
cd Downloads
pwd
# /home/the-king/Downloads

# আগের ফোল্ডারে (Home-এ) ফিরুন
cd -
# /home/the-king

# যেকোনো জায়গা থেকে Home-এ ফিরুন
cd
pwd
# /home/the-king
```

---

## 🛤️ Absolute Path vs Relative Path

এটি Linux-এর একটি **অত্যন্ত গুরুত্বপূর্ণ** concept।

### Absolute Path (পূর্ণ পথ):

- সবসময় **`/`** দিয়ে শুরু হয়
- **Root থেকে সম্পূর্ণ ঠিকানা**
- আপনি যেখানেই থাকুন, এটি সবসময় কাজ করবে

```bash
cd /home/the-king/Documents
```

**Real-Life তুলনা:**

> এটি Google Maps-এ পুরো ঠিকানা দেওয়ার মতো: "বাসা ৫, রোড ৩, ব্লক ডি, মিরপুর, ঢাকা, বাংলাদেশ"

### Relative Path (আপেক্ষিক পথ):

- **`/`** দিয়ে শুরু হয় **না**
- **বর্তমান অবস্থান থেকে পথ**
- আপনি কোথায় আছেন তার উপর নির্ভর করে

```bash
# ধরুন আপনি /home/the-king তে আছেন
cd Documents
# এটি আসলে যায় /home/the-king/Documents তে
```

**Real-Life তুলনা:**

> এটি কাউকে পথ বলার মতো: "এই রাস্তা দিয়ে সোজা যান, তারপর ডানে ঘুরুন" — আপনি কোথায় দাঁড়িয়ে আছেন তার উপর নির্ভর করে!

### তুলনা:

| Absolute Path              | Relative Path                        |
| -------------------------- | ------------------------------------ |
| `/home/the-king/Documents` | `Documents` (Home থেকে)              |
| `/home/the-king/Downloads` | `../Downloads` (Documents থেকে)      |
| `/etc/hostname`            | আপনি `/etc`-তে থাকলে শুধু `hostname` |

### বিশেষ চিহ্ন:

| চিহ্ন | অর্থ                          | উদাহরণ                              |
| ----- | ----------------------------- | ----------------------------------- |
| `.`   | বর্তমান ফোল্ডার               | `./script.sh` (এই ফোল্ডারের script) |
| `..`  | parent (এক ধাপ উপরের) ফোল্ডার | `cd ..`                             |
| `~`   | Home directory                | `cd ~/Documents`                    |
| `/`   | Root directory                | `cd /`                              |

---

## 🛠️ আরও প্রয়োজনীয় কমান্ড

### `clear` — Terminal পরিষ্কার করা

```bash
clear
```

**কাজ:** Terminal-এর সব লেখা পরিষ্কার করে ফেলে (তথ্য মুছে যায় না, শুধু স্ক্রিন পরিষ্কার হয়)

**Shortcut:** `Ctrl + L` (আরও দ্রুত ✅)

---

### `whoami` — আমি কে?

```bash
whoami
```

**আউটপুট:**

```
the-king
```

**কাজ:** বর্তমানে কোন user হিসেবে logged in তা দেখায়।

**মনে রাখুন:** "**Who am I?**" = "আমি কে?"

---

### `history` — কমান্ড ইতিহাস

```bash
history
```

**কাজ:** আপনি আগে যতগুলো কমান্ড লিখেছেন তার তালিকা দেখায়।

```bash
# শেষ ১০টি কমান্ড দেখুন
history 10

# ইতিহাস থেকে কমান্ড পুনরায় চালান
!5          # ৫ নম্বর কমান্ড আবার চালান
!!          # সবশেষ কমান্ড আবার চালান
```

**Tip:** `↑` (উপর তীর) চাপলে আগের কমান্ড আসে। `↓` চাপলে পরের।

---

### `man` — Manual (সাহায্য)

```bash
man ls
```

**কাজ:** যেকোনো কমান্ডের সম্পূর্ণ manual/ডকুমেন্টেশন দেখায়।

**মনে রাখুন:** "**Man**ual" = "ব্যবহারকারী নির্দেশিকা"

**Manual-এ নেভিগেশন:**
| Key | কাজ |
|-----|-----|
| `↑` / `↓` | উপরে/নিচে স্ক্রল |
| `Space` | এক পৃষ্ঠা নিচে |
| `b` | এক পৃষ্ঠা উপরে (**b**ack) |
| `/search-term` | কিছু সার্চ করুন |
| `q` | বের হোন (**q**uit) |

> 💡 **Tip:** `man` পড়তে ভয় লাগলে `--help` ব্যবহার করুন — এটি সংক্ষিপ্ত সাহায্য দেখায়:
>
> ```bash
> ls --help
> ```

---

### `which` — কমান্ড কোথায় আছে?

```bash
which ls
```

**আউটপুট:**

```
/usr/bin/ls
```

**কাজ:** কোনো কমান্ডের executable ফাইল কোথায় আছে তা দেখায়।

---

## ⌨️ Terminal Shortcuts (অবশ্যই মুখস্থ করুন!)

| Shortcut   | কাজ                                     |
| ---------- | --------------------------------------- |
| `Ctrl + C` | চলমান কমান্ড বন্ধ করুন                  |
| `Ctrl + L` | Terminal পরিষ্কার করুন (`clear` এর মতো) |
| `Ctrl + A` | লাইনের শুরুতে যান                       |
| `Ctrl + E` | লাইনের শেষে যান                         |
| `Ctrl + U` | কার্সরের আগের সব মুছুন                  |
| `Ctrl + K` | কার্সরের পরের সব মুছুন                  |
| `Ctrl + W` | আগের একটি শব্দ মুছুন                    |
| `Ctrl + R` | কমান্ড ইতিহাসে সার্চ করুন               |
| `Ctrl + D` | Terminal বন্ধ করুন (exit)               |
| `Tab`      | Auto-complete (নাম স্বয়ংক্রিয় পূরণ)   |
| `Tab Tab`  | সব সম্ভাব্য option দেখান                |
| `↑` / `↓`  | আগের/পরের কমান্ড দেখুন                  |

> ⚡ **সবচেয়ে গুরুত্বপূর্ণ:** `Tab` key! এটি কমান্ড, ফাইলের নাম, ফোল্ডারের নাম — সব কিছু auto-complete করে। ভুল টাইপ কমে, গতি বাড়ে। **প্রতিটি কমান্ডে Tab ব্যবহার করুন!**

**Tab ব্যবহারের উদাহরণ:**

```bash
# "Doc" লিখে Tab চাপুন
cd Doc[Tab]
# স্বয়ংক্রিয়ভাবে হয়ে যাবে:
cd Documents/

# যদি একাধিক match থাকে, Tab দুবার চাপুন:
cd D[Tab][Tab]
# দেখাবে: Desktop/ Documents/ Downloads/
```

---

## 🏋️ Practice Exercise

### অনুশীলন ১: Navigation Practice

Terminal খুলুন (`Ctrl + Alt + T`) এবং নিচের কমান্ডগুলো ক্রমানুসারে চালান:

```bash
# 1. আপনি কোথায় আছেন দেখুন
pwd

# 2. Home directory-তে কী আছে দেখুন
ls

# 3. বিস্তারিতভাবে দেখুন (লুকানো ফাইলসহ)
ls -la

# 4. Human-readable format-এ দেখুন
ls -lah

# 5. Documents-এ যান
cd Documents

# 6. আপনি কোথায় আছেন confirm করুন
pwd

# 7. এক ধাপ পিছনে যান
cd ..

# 8. /etc ফোল্ডারে যান (Absolute path)
cd /etc

# 9. সেখানে কী আছে দেখুন
ls

# 10. Home-এ ফিরে আসুন
cd ~

# 11. Downloads-এ যান
cd Downloads

# 12. আগের ফোল্ডারে (Home) ফিরুন
cd -

# 13. Root directory-তে যান
cd /

# 14. Root-এ কী কী ফোল্ডার আছে দেখুন
ls

# 15. Home-এ ফিরুন
cd
```

### অনুশীলন ২: তথ্য সংগ্রহ

নিচের কমান্ডগুলো চালান এবং আউটপুট লক্ষ্য করুন:

```bash
# আপনার username
whoami

# আপনার shell
echo $SHELL

# আপনার kernel version
uname -r

# কমান্ড ইতিহাস (শেষ ৫টি)
history 5

# ls কমান্ড কোথায় আছে
which ls

# pwd কমান্ড কোথায় আছে
which pwd
```

### অনুশীলন ৩: Tab Auto-Complete অভ্যাস

```bash
# Home-এ যান
cd ~

# "Desk" লিখে Tab চাপুন — কী হয়?
cd Desk[Tab]

# পিছনে আসুন
cd ..

# "D" লিখে Tab দুবার চাপুন — কী দেখায়?
cd D[Tab][Tab]
```

### অনুশীলন ৪: প্রশ্নোত্তর

1. `pwd` আর `whoami` এর পার্থক্য কী?
2. `ls -a` তে দেখা `.` আর `..` কী বোঝায়?
3. `cd ..` আর `cd -` এর পার্থক্য কী?
4. Absolute path ও Relative path-এর মধ্যে কোনটি কখন ব্যবহার করবেন?
5. `/home` ফোল্ডার আর `/root` ফোল্ডারের মধ্যে পার্থক্য কী?

---

## ➡️ পরবর্তী Section

[Section 03: File ও Directory Management →](section-03.md)

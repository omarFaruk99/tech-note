# 📖 Section 07: Package Management (apt)

---

## 🎯 এই Section-এ যা শিখবেন

- Package কী এবং Package Manager কেন দরকার
- APT কিভাবে কাজ করে
- Repository কী
- সফটওয়্যার ইন্সটল, আপডেট, আনইন্সটল করা
- `.deb` ফাইল থেকে ইন্সটল করা
- Snap Package Manager
- সফটওয়্যার খোঁজা ও তথ্য দেখা

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড                       |  Ubuntu 24 LTS-এ   | মন্তব্য                                  |
| ---------------------------- | :----------------: | ---------------------------------------- |
| `apt`                        |  ✅ Pre-installed  | Ubuntu-র প্রধান package manager          |
| `apt-get`                    |  ✅ Pre-installed  | apt-এর পুরনো version                     |
| `apt-cache`                  |  ✅ Pre-installed  | Package তথ্য খোঁজা                       |
| `dpkg`                       |  ✅ Pre-installed  | Low-level .deb package manager           |
| `snap`                       |  ✅ Pre-installed  | Snap package manager (Ubuntu-তে default) |
| `flatpak`                    | ❌ ইন্সটল করতে হবে | `sudo apt install flatpak`               |
| `aptitude`                   | ❌ ইন্সটল করতে হবে | `sudo apt install aptitude`              |
| `software-properties-common` |  ✅ Pre-installed  | PPA যোগ করতে সাহায্য করে                 |

---

## 📦 Package কী?

**Package** হলো একটি সফটওয়্যারের **ইন্সটলেশন প্যাকেজ** — এতে থাকে:

- সফটওয়্যারের সব ফাইল
- কোথায় কোন ফাইল রাখতে হবে তার তথ্য
- কী কী অন্য সফটওয়্যার আগে থাকতে হবে (dependencies)

### সহজ উদাহরণ:

কল্পনা করুন IKEA-র আসবাবপত্র:

- **Package** = একটি বাক্স যাতে আসবাবের সব টুকরো আছে
- **Package Manager** = সেই কর্মী যিনি বাক্স খুলে সব ঠিকমতো জোড়া লাগান
- **Dependencies** = কিছু tool লাগবে (screwdriver, hammer) — সেগুলোও Package Manager এনে দেবে!

### Windows vs Linux:

| Windows                             | Linux (Ubuntu)                     |
| ----------------------------------- | ---------------------------------- |
| Google-এ search করো                 | `apt search firefox`               |
| Website থেকে .exe ডাউনলোড করো       | `sudo apt install firefox`         |
| Installer চালাও                     | Package Manager নিজেই করে ✅       |
| আপডেট? প্রতিটি সফটওয়্যার আলাদাভাবে | `sudo apt upgrade` — সব একসাথে! ✅ |
| আনইন্সটল? Control Panel             | `sudo apt remove firefox`          |

> 💡 Linux-এ Package Manager থাকায় **সব সফটওয়্যার একটি কমান্ডে** ইন্সটল/আপডেট/আনইন্সটল হয়। Website থেকে ডাউনলোড করার দরকার নেই!

---

## 🏪 Repository কী?

**Repository (Repo)** হলো একটি **অনলাইন ভাণ্ডার** যেখানে হাজার হাজার Package রাখা আছে।

### সহজ উদাহরণ:

```
Repository = App Store (কিন্তু সব FREE!)
├── Main       → Canonical (Ubuntu-র প্রতিষ্ঠাতা কোম্পানি) সমর্থিত
├── Universe   → Community সমর্থিত
├── Restricted → প্রোপ্রাইটারি ড্রাইভার (NVIDIA, etc.)
└── Multiverse → Copyright-যুক্ত সফটওয়্যার
```

### Repository তালিকা দেখা:

```bash
cat /etc/apt/sources.list.d/ubuntu.sources
```

### PPA (Personal Package Archive) — তৃতীয় পক্ষের Repo:

```bash
# PPA যোগ করা
sudo add-apt-repository ppa:user/ppa-name

# PPA মুছে ফেলা
sudo add-apt-repository --remove ppa:user/ppa-name
```

> ⚠️ **সতর্কতা:** শুধু বিশ্বস্ত PPA যোগ করুন। অজানা PPA থেকে ক্ষতিকর সফটওয়্যার আসতে পারে!

---

## 📥 APT — মূল Package Manager

**APT = Advanced Package Tool**

### 1️⃣ Package তালিকা আপডেট করা

```bash
sudo apt update
```

**কী করে:** Repository থেকে সর্বশেষ Package-এর তালিকা ডাউনলোড করে। **সফটওয়্যার ইন্সটল করে না**, শুধু তালিকা আপডেট করে।

**মনে রাখুন:** মুদি দোকানের **মূল্য তালিকা** আপডেট করার মতো — পণ্য কেনা হচ্ছে না, শুধু দাম জানা হচ্ছে।

> 💡 **নিয়ম:** যেকোনো সফটওয়্যার ইন্সটল করার **আগে** সবসময় `sudo apt update` চালান!

---

### 2️⃣ সফটওয়্যার ইন্সটল করা

```bash
sudo apt install <package-name>
```

**উদাহরণ:**

```bash
# VLC media player ইন্সটল
sudo apt install vlc

# একাধিক software একসাথে ইন্সটল
sudo apt install git curl wget htop

# বিনা প্রশ্নে ইন্সটল (-y = yes to all)
sudo apt install -y neofetch
```

| Flag                      | অর্থ                            |
| ------------------------- | ------------------------------- |
| `-y`                      | "**Y**es" — সব প্রশ্নে yes বলো  |
| `--no-install-recommends` | শুধু আবশ্যক packages ইন্সটল করো |

### কী ইন্সটল হবে তা আগে দেখা (Dry Run):

```bash
sudo apt install --dry-run vlc
# আসলে ইন্সটল করবে না, শুধু দেখাবে কী কী হবে
```

---

### 3️⃣ সফটওয়্যার আপডেট/Upgrade করা

```bash
# সব ইন্সটল করা package আপডেট করুন
sudo apt upgrade

# বিনা প্রশ্নে আপডেট
sudo apt upgrade -y
```

**`update` vs `upgrade` — গুরুত্বপূর্ণ পার্থক্য:**

| কমান্ড        | কী করে                       | তুলনা            |
| ------------- | ---------------------------- | ---------------- |
| `apt update`  | Package **তালিকা** আপডেট করে | মেনু কার্ড দেখা  |
| `apt upgrade` | **সফটওয়্যার** আপডেট করে     | খাবার অর্ডার করা |

> ⚠️ **সবসময় আগে `update`, তারপর `upgrade`!**
>
> ```bash
> sudo apt update && sudo apt upgrade -y
> ```
>
> `&&` মানে = প্রথমটি সফল হলে তবেই দ্বিতীয়টি চালাও

### Full Upgrade:

```bash
sudo apt full-upgrade
```

**পার্থক্য:** `upgrade` পুরনো package মুছে না, `full-upgrade` দরকার হলে পুরনো package মুছে নতুনটি ইন্সটল করে।

---

### 4️⃣ সফটওয়্যার আনইন্সটল করা

```bash
# Package আনইন্সটল করুন (config ফাইল থাকবে)
sudo apt remove vlc

# Package + config সব মুছুন (সম্পূর্ণ পরিষ্কার)
sudo apt purge vlc

# অব্যবহৃত dependencies মুছুন
sudo apt autoremove
```

| কমান্ড       | কী মুছে               | Config ফাইল  |
| ------------ | --------------------- | ------------ |
| `remove`     | সফটওয়্যার            | ✅ থাকে      |
| `purge`      | সফটওয়্যার + config   | ❌ মুছে যায় |
| `autoremove` | অব্যবহৃত dependencies | —            |

> 💡 **পরামর্শ:** `purge` ব্যবহার করুন যদি সফটওয়্যার আবার ইন্সটল করার ইচ্ছা না থাকে।

---

### 5️⃣ Package খোঁজা

```bash
# নাম দিয়ে খুঁজুন
apt search video player

# নির্দিষ্ট নামে খুঁজুন
apt search ^vlc

# ইন্সটল করা package-এর তালিকা
apt list --installed

# আপগ্রেড পাওয়া যায় এমন package
apt list --upgradable
```

---

### 6️⃣ Package-এর তথ্য দেখা

```bash
# Package-এর বিস্তারিত তথ্য
apt show vlc

# Package ইন্সটল আছে কিনা দেখুন
apt list --installed | grep vlc

# কোন package কোন ফাইল ইন্সটল করেছে
dpkg -L vlc

# একটি ফাইল কোন package-এর অংশ
dpkg -S /usr/bin/vim
```

---

## 📀 `.deb` ফাইল থেকে ইন্সটল — `dpkg`

কিছু সফটওয়্যার (.deb ফাইল) website থেকে ডাউনলোড করে ইন্সটল করতে হয় (যেমন Google Chrome, VS Code):

```bash
# .deb ফাইল ইন্সটল করুন
sudo dpkg -i package-name.deb

# Dependencies error হলে ঠিক করুন
sudo apt install -f
```

### Real-Life উদাহরণ — Google Chrome ইন্সটল:

```bash
# 1. Chrome ডাউনলোড করুন
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb

# 2. ইন্সটল করুন
sudo dpkg -i google-chrome-stable_current_amd64.deb

# 3. কোনো dependency সমস্যা হলে
sudo apt install -f
```

| dpkg Flag | কাজ                                    |
| --------- | -------------------------------------- |
| `-i`      | **i**nstall — ইন্সটল করো               |
| `-r`      | **r**emove — আনইন্সটল করো              |
| `-l`      | **l**ist — ইন্সটল করা packages দেখাও   |
| `-L`      | **L**ist files — package-এর ফাইল দেখাও |
| `-S`      | **S**earch — ফাইল কোন package-এর       |

---

## 📱 Snap — আরেকটি Package Manager

**Snap** হলো Canonical (Ubuntu-র নির্মাতা)-এর তৈরি Package Manager। Ubuntu 24-এ **আগে থেকেই ইন্সটল আছে**।

### Snap এর সুবিধা:

- Dependencies নিজে আনে (dependency hell নেই!)
- স্বয়ংক্রিয়ভাবে আপডেট হয়
- Sandbox-এ চলে (নিরাপদ)
- সব Linux distro-তে চলে

### Snap ব্যবহার:

```bash
# Package খুঁজুন
snap find vlc

# ইন্সটল করুন
sudo snap install vlc

# তালিকা দেখুন
snap list

# আনইন্সটল করুন
sudo snap remove vlc

# তথ্য দেখুন
snap info vlc
```

### APT vs Snap:

| বিষয়        | APT (.deb)            | Snap                     |
| ------------ | --------------------- | ------------------------ |
| গতি          | ✅ দ্রুত চালু হয়     | ❌ একটু ধীর              |
| আকার         | ✅ ছোট                | ❌ বড় (dependencies সহ) |
| Auto-update  | ❌ ম্যানুয়াল         | ✅ স্বয়ংক্রিয়          |
| Sandboxed    | ❌ না                 | ✅ হ্যাঁ (নিরাপদ)        |
| সব distro-তে | ❌ শুধু Debian/Ubuntu | ✅ সব Linux              |

> 💡 **পরামর্শ:** যদি APT-তে package পাওয়া যায়, APT ব্যবহার করুন। না পেলে Snap ব্যবহার করুন।

---

## 🔄 সিস্টেম রক্ষণাবেক্ষণ (Maintenance) কমান্ড

```bash
# সম্পূর্ণ আপডেট প্রক্রিয়া (নিয়মিত চালান!)
sudo apt update          # তালিকা আপডেট
sudo apt upgrade -y      # সফটওয়্যার আপডেট
sudo apt autoremove -y   # অব্যবহৃত packages মুছুন
sudo apt autoclean       # পুরনো cache মুছুন

# অথবা একলাইনে:
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y && sudo apt autoclean
```

> 💡 **পরামর্শ:** সপ্তাহে অন্তত একবার এই কমান্ডগুলো চালান আপনার সিস্টেম আপডেট ও সুস্থ রাখতে।

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কমান্ড                    | কাজ                      |
| ------------------------- | ------------------------ |
| `sudo apt update`         | Package তালিকা আপডেট     |
| `sudo apt install <pkg>`  | Package ইন্সটল           |
| `sudo apt remove <pkg>`   | Package আনইন্সটল         |
| `sudo apt purge <pkg>`    | Package + config মুছা    |
| `sudo apt upgrade`        | সব package আপডেট         |
| `sudo apt autoremove`     | অব্যবহৃত dependency মুছা |
| `sudo apt autoclean`      | Cache পরিষ্কার           |
| `apt search <name>`       | Package খোঁজা            |
| `apt show <pkg>`          | Package-এর তথ্য          |
| `apt list --installed`    | ইন্সটল করা packages      |
| `sudo dpkg -i <file.deb>` | .deb ফাইল ইন্সটল         |
| `sudo snap install <pkg>` | Snap package ইন্সটল      |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: Package তথ্য দেখা

```bash
# 1. Package তালিকা আপডেট করুন
sudo apt update

# 2. ইন্সটল করা packages কতগুলো দেখুন
apt list --installed | wc -l

# 3. upgradable packages দেখুন
apt list --upgradable

# 4. "git" package-এর তথ্য দেখুন
apt show git
```

### অনুশীলন ২: সফটওয়্যার ইন্সটল ও আনইন্সটল

```bash
# 1. neofetch ইন্সটল করুন (সুন্দর system info দেখায়)
sudo apt install -y neofetch

# 2. চালান
neofetch

# 3. htop ইন্সটল করুন (system monitor)
sudo apt install -y htop

# 4. চালান (q দিয়ে বেরোন)
htop

# 5. tree ইন্সটল করুন (folder structure দেখায়)
sudo apt install -y tree

# 6. চালান
tree ~/linux-practice

# 7. (ঐচ্ছিক) আনইন্সটল করুন
sudo apt remove neofetch
```

### অনুশীলন ৩: Snap ব্যবহার

```bash
# 1. ইন্সটল করা snap packages দেখুন
snap list

# 2. snap-এ vlc খুঁজুন
snap find vlc

# 3. snap-এ vlc-র তথ্য দেখুন
snap info vlc
```

### অনুশীলন ৪: Maintenance

```bash
# সম্পূর্ণ maintenance চালান
sudo apt update
sudo apt upgrade -y
sudo apt autoremove -y
sudo apt autoclean
```

---

## ➡️ পরবর্তী Section

[Section 08: Text Editor (nano, vim) →](section-08.md)

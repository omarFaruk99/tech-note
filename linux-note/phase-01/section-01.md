# 📖 Section 01: Linux কী? ইতিহাস, Distribution ও Ubuntu পরিচিতি

---

## 🎯 এই Section-এ যা শিখবেন

- Linux কী এবং এটি কেন গুরুত্বপূর্ণ
- Linux-এর ইতিহাস ও জন্মকথা
- Kernel কী এবং এটি কিভাবে কাজ করে
- Linux Distribution কী
- Ubuntu কেন বেছে নেবেন
- Open Source-এর ধারণা

---

## 📚 Linux কী?

**Linux** হলো একটি **Operating System (OS)** — ঠিক যেমন Windows বা macOS। কম্পিউটার চালানোর জন্য একটি Operating System দরকার হয়। OS হলো সেই সফটওয়্যার যেটি:

- আপনার হার্ডওয়্যার (RAM, CPU, Hard Disk) পরিচালনা করে
- আপনাকে সফটওয়্যার চালাতে দেয়
- আপনার ও কম্পিউটারের মধ্যে সেতু হিসেবে কাজ করে

### সহজ উদাহরণ দিয়ে বুঝুন:

কল্পনা করুন একটি রেস্তোরাঁ:

- **আপনি (User)** = খাবার অর্ডার দেন
- **ওয়েটার (Operating System)** = আপনার অর্ডার রান্নাঘরে পৌঁছায় এবং খাবার আপনার কাছে আনে
- **রান্নাঘর (Hardware)** = আসল কাজ করে

Linux হলো সেই **ওয়েটারের** মতো — আপনি যখন কোনো কাজ করতে চান (ফাইল খুলুন, ব্রাউজার চালান), Linux সেই কাজটি Hardware-এর কাছে পৌঁছে দেয়।

---

## 🕰️ Linux-এর ইতিহাস

### শুরুর গল্প

| সাল      | ঘটনা                                                                        |
| -------- | --------------------------------------------------------------------------- |
| **1969** | AT&T Bell Labs-এ **Unix** তৈরি হয় — এটিই Linux-এর পূর্বসূরি                |
| **1983** | **Richard Stallman** GNU Project শুরু করেন — Free Software আন্দোলনের জন্ম   |
| **1991** | **Linus Torvalds** (ফিনল্যান্ডের ২১ বছর বয়সী ছাত্র) Linux Kernel তৈরি করেন |
| **1993** | প্রথম Linux distributions আসে — Debian, Slackware                           |
| **2004** | **Ubuntu** আসে — "Linux for Human Beings" স্লোগান নিয়ে                     |
| **2024** | Ubuntu 24.04 LTS রিলিজ হয় — আপনি এটাই ইন্সটল করেছেন!                       |

### Linus Torvalds কে?

Linus Torvalds হলেন একজন ফিনিশ-আমেরিকান সফটওয়্যার ইঞ্জিনিয়ার। ১৯৯১ সালে তিনি Helsinki University-তে পড়াকালীন একটি ছোট Operating System তৈরি করেন নিজের ব্যক্তিগত ব্যবহারের জন্য। পরে সেটি ইন্টারনেটে শেয়ার করেন এবং সারা বিশ্বের ডেভেলপাররা এতে অবদান রাখতে শুরু করেন।

> 💡 **মজার তথ্য:** "Linux" নামটি এসেছে **Linus + Unix** = **Linux** থেকে।

---

## 🧠 Kernel কী?

**Kernel** হলো Operating System-এর **হৃৎপিণ্ড**। এটি OS-এর সবচেয়ে গুরুত্বপূর্ণ অংশ।

### Kernel-এর কাজ:

```
┌─────────────────────────────────────────┐
│           Applications                   │
│    (Browser, Terminal, File Manager)     │
├─────────────────────────────────────────┤
│           Shell (Bash/Zsh)               │
│    (আপনার কমান্ড Kernel-এ পাঠায়)        │
├─────────────────────────────────────────┤
│           🫀 KERNEL (Linux)              │
│  • CPU Management (প্রসেসর পরিচালনা)     │
│  • Memory Management (RAM পরিচালনা)      │
│  • Device Drivers (হার্ডওয়্যার নিয়ন্ত্রণ) │
│  • File System (ফাইল ব্যবস্থাপনা)        │
├─────────────────────────────────────────┤
│           Hardware                       │
│    (CPU, RAM, HDD, Keyboard, Mouse)     │
└─────────────────────────────────────────┘
```

### সহজ ভাষায়:

> আপনি যখন Terminal-এ কিছু টাইপ করেন, সেটি **Shell**-এর কাছে যায়। Shell সেটি **Kernel**-এ পাঠায়। Kernel **Hardware**-কে কাজ করতে বলে। Hardware কাজ শেষ করে Kernel-কে জানায়। Kernel আপনাকে ফলাফল দেখায়।

### আপনার Kernel Version দেখুন:

```bash
uname -r
```

**ব্যাখ্যা:**

- `uname` = **U**nix **Name** — সিস্টেমের তথ্য দেখায়
- `-r` = **r**elease — Kernel-এর version নম্বর দেখায়

**উদাহরণ আউটপুট:**

```
6.8.0-41-generic
```

এখানে:

- `6` = Major version
- `8` = Minor version
- `0-41` = Patch/revision number
- `generic` = সাধারণ ব্যবহারের জন্য তৈরি

---

## 📦 Linux Distribution কী?

**Linux Distribution (Distro)** হলো Linux Kernel-এর উপর ভিত্তি করে তৈরি সম্পূর্ণ Operating System।

### সহজ উদাহরণ:

কল্পনা করুন **Kernel** হলো একটি গাড়ির **Engine**:

- একই Engine দিয়ে Toyota Corolla বানানো যায় (= Ubuntu)
- একই Engine দিয়ে Toyota Camry বানানো যায় (= Fedora)
- একই Engine দিয়ে Toyota Land Cruiser বানানো যায় (= Arch Linux)

Engine (Kernel) একই, কিন্তু বাকি জিনিসপত্র (Desktop, Software, Package Manager) আলাদা!

### জনপ্রিয় Linux Distributions:

| Distribution     | বৈশিষ্ট্য                                       | কাদের জন্য                         |
| ---------------- | ----------------------------------------------- | ---------------------------------- |
| **Ubuntu**       | সহজ, user-friendly, বিশাল community             | Beginners, General users           |
| **Debian**       | অত্যন্ত স্থিতিশীল, Ubuntu-র মূল ভিত্তি          | Server, Advanced users             |
| **Fedora**       | সর্বশেষ প্রযুক্তি, Red Hat-এর community version | Developers                         |
| **Linux Mint**   | Ubuntu-ভিত্তিক, Windows-এর মতো দেখতে            | Windows থেকে আসা users             |
| **Arch Linux**   | সম্পূর্ণ কাস্টমাইজেবল, DIY approach             | Expert users                       |
| **Kali Linux**   | Security testing tools সমৃদ্ধ                   | Cybersecurity, Penetration Testers |
| **CentOS/Rocky** | Enterprise-grade, সার্ভারে ব্যবহৃত              | Server admins                      |

### Distribution Family Tree:

```
Linux Kernel
├── Debian Family
│   ├── Debian
│   ├── Ubuntu ← (আপনি এখানে আছেন! ✅)
│   │   ├── Linux Mint
│   │   ├── Pop!_OS
│   │   └── Kubuntu, Xubuntu...
│   └── Kali Linux
├── Red Hat Family
│   ├── Fedora
│   ├── CentOS / Rocky Linux
│   └── RHEL (Red Hat Enterprise Linux)
├── Arch Family
│   ├── Arch Linux
│   └── Manjaro
└── Other
    ├── openSUSE
    └── Gentoo
```

---

## 🟠 Ubuntu কেন?

আপনি Ubuntu 24.04 LTS ইন্সটল করেছেন — চমৎকার সিদ্ধান্ত! কারণ:

### LTS মানে কী?

**LTS = Long Term Support**

| Version Type                 | Support Period | কাদের জন্য              |
| ---------------------------- | -------------- | ----------------------- |
| Regular Release (যেমন 23.10) | ৯ মাস          | যারা নতুন features চায় |
| **LTS Release (যেমন 24.04)** | **৫ বছর**      | যারা stability চায় ✅  |

> 💡 **24.04** মানে = **2024** সালের **April** মাসে রিলিজ হয়েছে

### Ubuntu-র সুবিধা:

1. **বিশাল Community** — সমস্যা হলে সাহায্য পেতে সহজ
2. **সহজ ব্যবহার** — নতুনদের জন্য সবচেয়ে friendly
3. **বিশাল Software Repository** — হাজার হাজার free software
4. **Regular Updates** — নিরাপত্তা আপডেট নিয়মিত আসে
5. **Professional Use** — অনেক কোম্পানি Ubuntu ব্যবহার করে
6. **Free** — সম্পূর্ণ বিনামূল্যে

---

## 🔓 Open Source কী?

**Open Source** মানে হলো এমন সফটওয়্যার যার **source code** সবার জন্য উন্মুক্ত।

### তুলনা:

| বিষয়       | Closed Source (Windows)        | Open Source (Linux)             |
| ----------- | ------------------------------ | ------------------------------- |
| Source Code | লুকানো, দেখা যায় না           | সবার জন্য উন্মুক্ত              |
| দাম         | সাধারণত টাকা লাগে              | সাধারণত বিনামূল্যে              |
| পরিবর্তন    | করা যায় না                    | যে কেউ পরিবর্তন করতে পারে       |
| নিরাপত্তা   | কোম্পানি দেখভাল করে            | হাজার হাজার ডেভেলপার দেখভাল করে |
| গোপনীয়তা   | কোম্পানি ডেটা সংগ্রহ করতে পারে | আপনার ডেটা আপনার কাছে           |

### Real-Life Use Case:

> 🌍 **আপনি জানেন কি?**
>
> - Google-এর সমস্ত সার্ভার Linux-এ চলে
> - Android ফোনের ভিতরে Linux Kernel আছে
> - Netflix, Amazon, Facebook — সব Linux-এ চলে
> - বিশ্বের Top 500 Supercomputer-এর **100%** Linux ব্যবহার করে
> - International Space Station-এও Linux চলে!

---

## 🖥️ Ubuntu-তে কী কী আছে?

আপনার Ubuntu 24.04 LTS-এ ইন্সটলের সাথেই যা আসে:

| Component           | নাম                   | কাজ                                        |
| ------------------- | --------------------- | ------------------------------------------ |
| Desktop Environment | **GNOME**             | গ্রাফিক্যাল ইন্টারফেস (যেটা দেখতে পাচ্ছেন) |
| File Manager        | **Nautilus (Files)**  | ফাইল ব্রাউজ করা                            |
| Terminal            | **GNOME Terminal**    | কমান্ড লেখার জায়গা                        |
| Web Browser         | **Firefox**           | ইন্টারনেট ব্রাউজ করা                       |
| Text Editor         | **GNOME Text Editor** | টেক্সট ফাইল এডিট করা                       |
| Package Manager     | **APT**               | সফটওয়্যার ইন্সটল/আনইন্সটল                 |
| Software Store      | **Ubuntu Software**   | GUI-তে সফটওয়্যার ইন্সটল                   |

### GUI vs CLI:

| বিষয়       | GUI (Graphical)          | CLI (Command Line)                 |
| ----------- | ------------------------ | ---------------------------------- |
| কী?         | মাউস দিয়ে ক্লিক করে কাজ | কমান্ড টাইপ করে কাজ                |
| সুবিধা      | সহজ, চোখে দেখা যায়      | দ্রুত, শক্তিশালী, automation সম্ভব |
| উদাহরণ      | Files app-এ ফোল্ডার তৈরি | `mkdir new-folder` কমান্ড          |
| কখন ব্যবহার | দৈনন্দিন কাজে            | Server management, scripting-এ     |

> ⚡ **গুরুত্বপূর্ণ:** Linux-এ professional হতে হলে **CLI (Terminal)** শেখা আবশ্যক। এই গাইডে আমরা মূলত CLI-তে কাজ শিখব, কারণ এটিই Linux-এর আসল শক্তি।

---

## ✅ গুরুত্বপূর্ণ শব্দকোষ (Glossary)

| শব্দ                      | অর্থ                                                            |
| ------------------------- | --------------------------------------------------------------- |
| **OS (Operating System)** | কম্পিউটার চালানোর মূল সফটওয়্যার                                |
| **Kernel**                | OS-এর মূল অংশ যেটি Hardware-এর সাথে যোগাযোগ করে                 |
| **Shell**                 | ব্যবহারকারীর কমান্ড Kernel-এ পাঠানোর মাধ্যম                     |
| **Terminal**              | Shell ব্যবহার করার জন্য যে window/app                           |
| **Distribution (Distro)** | Kernel + অতিরিক্ত software = সম্পূর্ণ OS                        |
| **GUI**                   | Graphical User Interface — চোখে দেখা যায়, মাউসে ক্লিক করা যায় |
| **CLI**                   | Command Line Interface — কমান্ড টাইপ করে কাজ করা                |
| **Open Source**           | যে software-এর code সবার জন্য উন্মুক্ত                          |
| **LTS**                   | Long Term Support — দীর্ঘমেয়াদি সমর্থন                         |
| **Repository**            | সফটওয়্যারের ভাণ্ডার/গুদাম                                      |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: নিচের প্রশ্নগুলোর উত্তর দিন (মুখে বলুন বা লিখুন)

1. Linux আর Windows-এর মধ্যে ৩টি পার্থক্য বলুন
2. Kernel কী কী কাজ করে?
3. Ubuntu কোন Distribution Family-র অংশ?
4. LTS মানে কী এবং এটি কেন গুরুত্বপূর্ণ?
5. Open Source software-এর ২টি সুবিধা বলুন

### অনুশীলন ২: Terminal-এ এই কমান্ডগুলো চালান

```bash
# আপনার Kernel version দেখুন
uname -r

# আপনার OS-এর সম্পূর্ণ তথ্য দেখুন
uname -a

# আপনার Ubuntu version দেখুন
lsb_release -a

# আপনার কম্পিউটারের hostname দেখুন
hostname
```

> 🔑 **Terminal খুলতে:** `Ctrl + Alt + T` চাপুন

### অনুশীলন ৩: চিন্তা করুন

- আপনার Android ফোনেও Linux Kernel আছে — এটি কি আপনাকে অবাক করেছে?
- কেন মনে করেন বিশ্বের বড় বড় কোম্পানি (Google, Amazon) Linux ব্যবহার করে Windows নয়?

---

## ➡️ পরবর্তী Section

[Section 02: Terminal পরিচিতি ও Basic Navigation →](section-02.md)

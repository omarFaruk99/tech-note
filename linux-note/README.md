# 🐧 Linux শেখার সম্পূর্ণ গাইড (বাংলায়)

> **Ubuntu 24 LTS** ভিত্তিক — Beginner থেকে Advanced পর্যন্ত

---

## 📚 সূচিপত্র

---

### 🟢 Phase 1: Linux ভিত্তি (Foundation)

> **কী শিখবেন:** Linux কী, Terminal চেনা, ফাইল-ফোল্ডার তৈরি-মুছা-কপি, ফাইলের ভিতর দেখা ও খোঁজা। এটি Linux-এর ABC — এই ভিত্তি ছাড়া আর কিছু শেখা সম্ভব নয়।
>
> 🎯 **কাদের জন্য:** 🔒 Cybersecurity · 🚀 DevOps · 🖥️ System Admin · 🧑‍💻 Developer · 📝 Daily Use — **সবার জন্য আবশ্যক!**

| Section | বিষয়                                           | ফাইল                                    |
| ------- | ----------------------------------------------- | --------------------------------------- |
| 01      | Linux কী? ইতিহাস, Distribution ও Ubuntu পরিচিতি | [section-01.md](phase-01/section-01.md) |
| 02      | Terminal পরিচিতি ও Basic Navigation             | [section-02.md](phase-01/section-02.md) |
| 03      | File ও Directory Management                     | [section-03.md](phase-01/section-03.md) |
| 04      | File Content দেখা ও Text Processing Basics      | [section-04.md](phase-01/section-04.md) |

---

### 🟡 Phase 2: Permission, User ও Package Management

> **কী শিখবেন:** কে কোন ফাইলে কী করতে পারবে (permissions), ব্যবহারকারী ও গোষ্ঠী পরিচালনা, সফটওয়্যার ইন্সটল/আনইন্সটল (apt), এবং Terminal-এ ফাইল edit করা। Linux-এর নিরাপত্তা ও ব্যবস্থাপনার মূল ভিত্তি।
>
> 🎯 **কাদের জন্য:** 🔒 Cybersecurity · 🚀 DevOps · 🖥️ System Admin · 🧑‍💻 Developer — **সবার জন্য আবশ্যক!**

| Section | বিষয়                        | ফাইল                                    |
| ------- | ---------------------------- | --------------------------------------- |
| 05      | File Permissions ও Ownership | [section-05.md](phase-02/section-05.md) |
| 06      | User ও Group Management      | [section-06.md](phase-02/section-06.md) |
| 07      | Package Management (apt)     | [section-07.md](phase-02/section-07.md) |
| 08      | Text Editor (nano, vim)      | [section-08.md](phase-02/section-08.md) |

---

### 🟠 Phase 3: System Management

> **কী শিখবেন:** চলমান প্রোগ্রাম (process) নিয়ন্ত্রণ, RAM-CPU-Disk মনিটরিং, systemd দিয়ে service পরিচালনা, এবং ডিস্ক-পার্টিশন ব্যবস্থাপনা। সিস্টেম সচল ও সুস্থ রাখতে এই জ্ঞান অপরিহার্য।
>
> 🎯 **সবচেয়ে বেশি দরকার:** 🖥️ System Admin · 🚀 DevOps · 🔒 Cybersecurity
> 💡 **কাজে লাগবে:** 🧑‍💻 Developer · 📝 Daily Use (সমস্যা সমাধানে)

| Section | বিষয়                           | ফাইল                                    |
| ------- | ------------------------------- | --------------------------------------- |
| 09      | Process Management              | [section-09.md](phase-03/section-09.md) |
| 10      | System Information ও Monitoring | [section-10.md](phase-03/section-10.md) |
| 11      | Service Management (systemd)    | [section-11.md](phase-03/section-11.md) |
| 12      | Disk ও Storage Management       | [section-12.md](phase-03/section-12.md) |

---

### 🔵 Phase 4: Input/Output ও Scripting

> **কী শিখবেন:** Pipe (`|`) দিয়ে কমান্ড জোড়া লাগানো, grep/sed/awk দিয়ে ডেটা ফিল্টার ও প্রক্রিয়াকরণ, Shell Script লিখে কাজ স্বয়ংক্রিয় করা, এবং Cron দিয়ে scheduled task সেট করা। এই Phase-ই আপনাকে "Linux ব্যবহারকারী" থেকে **"Linux Power User"**-এ রূপান্তরিত করবে।
>
> 🎯 **সবচেয়ে বেশি দরকার:** 🚀 DevOps · 🖥️ System Admin · 🔒 Cybersecurity (log analysis, automation)
> 💡 **কাজে লাগবে:** 🧑‍💻 Developer (build scripts, data processing)

| Section | বিষয়                                     | ফাইল                                    |
| ------- | ----------------------------------------- | --------------------------------------- |
| 13      | I/O Redirection ও Piping                  | [section-13.md](phase-04/section-13.md) |
| 14      | grep, sed, awk — Advanced Text Processing | [section-14.md](phase-04/section-14.md) |
| 15      | Shell Scripting Basics                    | [section-15.md](phase-04/section-15.md) |
| 16      | Cron Jobs ও Automation                    | [section-16.md](phase-04/section-16.md) |

---

### 🔴 Phase 5: Networking ও Security

> **কী শিখবেন:** নেটওয়ার্কিং-এর মূল ধারণা (IP, DNS, ports), SSH দিয়ে দূর থেকে সার্ভারে ঢোকা, Firewall দিয়ে সিস্টেম সুরক্ষিত করা, এবং Log analyze করে সমস্যা ও আক্রমণ চিহ্নিত করা। **Cybersecurity এবং Server Management-এর হৃৎপিণ্ড।**
>
> 🎯 **সবচেয়ে বেশি দরকার:** 🔒 Cybersecurity (অত্যাবশ্যক!) · 🖥️ System Admin · 🚀 DevOps
> 💡 **কাজে লাগবে:** 🧑‍💻 Developer (deployment, remote work)

| Section | বিষয়                           | ফাইল                                    |
| ------- | ------------------------------- | --------------------------------------- |
| 17      | Networking Basics               | [section-17.md](phase-05/section-17.md) |
| 18      | SSH ও Remote Access             | [section-18.md](phase-05/section-18.md) |
| 19      | Firewall (ufw) ও Basic Security | [section-19.md](phase-05/section-19.md) |
| 20      | Log Management                  | [section-20.md](phase-05/section-20.md) |

---

### 🟣 Phase 6: Advanced ও Real-World Skills

> **কী শিখবেন:** Environment Variable ও সিস্টেম কনফিগারেশন, ডেটা Backup ও Recovery, ফাইল Compression (tar, zip, gzip), এবং প্রফেশনাল Linux Tips ও Best Practices। এই Phase আপনাকে **প্রোডাকশন-রেডি** করবে — চাকরিতে বা নিজের সার্ভারে Linux সামলাতে পারবেন।
>
> 🎯 **সবচেয়ে বেশি দরকার:** 🖥️ System Admin · 🚀 DevOps
> 💡 **কাজে লাগবে:** 🔒 Cybersecurity · 🧑‍💻 Developer · 📝 Daily Use

| Section | বিষয়                                  | ফাইল                                    |
| ------- | -------------------------------------- | --------------------------------------- |
| 21      | Environment Variables ও `~/.bashrc`    | [section-21.md](phase-06/section-21.md) |
| 22      | Archive ও Compression (tar, gzip, zip) | [section-22.md](phase-06/section-22.md) |
| 23      | Backup ও Restore Strategies            | [section-23.md](phase-06/section-23.md) |
| 24      | Linux Troubleshooting Best Practices   | [section-24.md](phase-06/section-24.md) |

---

### 🟤 Phase 7: Daily and Frequent Uses

> **কী শিখবেন:** প্রতিদিনের লিনাক্স ব্যবহারে কাজে লাগা অত্যন্ত প্রয়োজনীয় টুল ও শর্টকাট। কীভাবে পিসি মেইনটেইন করতে হয়, দ্রুত টার্মিনাল নেভিগেশন, হিস্ট্রি সার্চ এবং উবুন্টু ডেস্কটপের নানা প্রো-লেভেলের শর্টকাট।
>
> 🎯 **সবচেয়ে বেশি দরকার:** 📝 Daily Use · 🧑‍💻 Developer

| Section | বিষয়                                    | ফাইল                                    |
| ------- | ---------------------------------------- | --------------------------------------- |
| 25      | Daily System Maintenance & Tending       | [section-25.md](phase-07/section-25.md) |
| 26      | Fast Navigation & File Searching         | [section-26.md](phase-07/section-26.md) |
| 27      | Everyday Terminal Productivity Tricks    | [section-27.md](phase-07/section-27.md) |
| 28      | Ubuntu Desktop Mastery & Daily Shortcuts | [section-28.md](phase-07/section-28.md) |

---

## 🗺️ আপনার লক্ষ্য অনুযায়ী কোন Phase পড়বেন?

| আপনার লক্ষ্য                           | আবশ্যক Phase | গুরুত্বপূর্ণ Phase | ঐচ্ছিক Phase |
| -------------------------------------- | :----------: | :----------------: | :----------: |
| 🔒 **Cybersecurity / Ethical Hacking** |  1, 2, 4, 5  |        3, 6        |      —       |
| 🚀 **DevOps / Cloud Engineering**      |  1, 2, 3, 4  |        5, 6        |      —       |
| 🖥️ **System Administration**           |   1, 2, 3    |      4, 5, 6       |      —       |
| 🧑‍💻 **Software Developer**              |     1, 2     |         4          |   3, 5, 6    |
| 📝 **দৈনন্দিন ব্যবহার (Daily Use)**    |     1, 2     |   3 (Section 7)    |   4, 5, 6    |

> 💡 **পরামর্শ:** আপনি যে পথেই যেতে চান, **Phase 1 ও Phase 2 সবার আগে পড়ুন** — এটি সকল পথের ভিত্তি। তারপর উপরের টেবিল দেখে আপনার লক্ষ্য অনুযায়ী এগিয়ে যান। তবে **সব Phase পড়লেই সবচেয়ে ভালো!**

---

## 🎯 কিভাবে এই গাইড ব্যবহার করবেন?

1. **ক্রমানুসারে পড়ুন** — Phase 1 থেকে শুরু করুন
2. **প্রতিটি কমান্ড নিজে চালান** — শুধু পড়লে শেখা হয় না, হাতে-কলমে করতে হবে
3. **Practice Exercise করুন** — প্রতিটি section-এর শেষে exercise আছে, সেগুলো অবশ্যই করুন
4. **ভুল করতে ভয় পাবেন না** — ভুল থেকেই সবচেয়ে ভালো শেখা হয়

---

> 📅 **তৈরি:** মার্চ ২০২৬  
> 💻 **প্ল্যাটফর্ম:** Ubuntu 24.04 LTS  
> 📝 **ভাষা:** বাংলা

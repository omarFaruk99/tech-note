# 📖 Section 11: Service Management (systemd)

---

## 🎯 এই Section-এ যা শিখবেন

- Service কী এবং কেন দরকার
- systemd কী
- Service শুরু, বন্ধ, restart করা
- Service enable/disable (বুটে স্বয়ংক্রিয়)
- Service-এর অবস্থা দেখা
- Systemd Timer ও Target
- Boot log দেখা

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড        | Ubuntu 24 LTS-এ  | মন্তব্য                  |
| ------------- | :--------------: | ------------------------ |
| `systemctl`   | ✅ Pre-installed | systemd-এর প্রধান কমান্ড |
| `journalctl`  | ✅ Pre-installed | systemd log দেখা         |
| `timedatectl` | ✅ Pre-installed | সময় ও timezone সেট করা  |
| `hostnamectl` | ✅ Pre-installed | Hostname সেট করা         |
| `loginctl`    | ✅ Pre-installed | Login session দেখা       |

> ✅ এই section-এর **সব কমান্ড** Ubuntu 24 LTS-এ **আগে থেকেই ইন্সটল করা আছে**।

---

## ⚙️ Service কী?

**Service** (বা **Daemon**) হলো **ব্যাকগ্রাউন্ডে চলা প্রোগ্রাম** — এগুলো আপনার দেখার দরকার ছাড়াই নীরবে কাজ করে যায়।

### সহজ উদাহরণ:

| Service          | কী করে                   | তুলনা                   |
| ---------------- | ------------------------ | ----------------------- |
| `NetworkManager` | WiFi/Internet সংযোগ রাখে | বিদ্যুৎ সংযোগ রক্ষাকারী |
| `ssh`            | দূর থেকে লগইন করতে দেয়  | দরজার তালা ব্যবস্থা     |
| `apache2`        | ওয়েবসাইট সার্ভ করে      | রেস্তোরাঁর ওয়েটার      |
| `cron`           | নির্ধারিত সময়ে কাজ করে  | অ্যালার্ম ঘড়ি          |
| `cups`           | প্রিন্টিং পরিচালনা করে   | ডাকঘর                   |

> 💡 **Daemon** শব্দটি গ্রিক পৌরাণিক কাহিনী থেকে এসেছে — "অদৃশ্য সাহায্যকারী আত্মা"। নাম শেষে `d` থাকলে সেটি সাধারণত daemon (যেমন: `sshd`, `httpd`, `crond`)

---

## 🏗️ systemd কী?

**systemd** হলো Ubuntu সহ বেশিরভাগ আধুনিক Linux-এর **init system** এবং **service manager**।

### systemd-এর কাজ:

```
কম্পিউটার চালু হলো
      ↓
BIOS → GRUB Bootloader → Linux Kernel
      ↓
Kernel প্রথম যাকে চালায় → systemd (PID 1)
      ↓
systemd সব service চালু করে:
├── NetworkManager (ইন্টারনেট)
├── gdm (Login screen)
├── ssh (Remote access)
├── cron (Scheduled tasks)
└── ... আরও অনেক
```

> 💡 `systemd` হলো **PID 1** — সিস্টেমের প্রথম process। সব process-এর "পূর্বপুরুষ"।

```bash
# PID 1 দেখুন
ps -p 1
#     PID TTY          TIME CMD
#       1 ?        00:00:05 systemd
```

---

## 1️⃣ `systemctl` — Service নিয়ন্ত্রণ

**systemctl** হলো systemd নিয়ন্ত্রণের **প্রধান কমান্ড**।

**মনে রাখুন:** "**System** **C**on**t**ro**l**" = "সিস্টেম নিয়ন্ত্রণ"

### Service-এর অবস্থা দেখা:

```bash
# SSH service-এর অবস্থা
systemctl status ssh
```

**আউটপুট:**

```
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Thu 2026-03-05 01:00:00 +06; 2h ago
       Docs: man:sshd(8)
   Main PID: 789 (sshd)
      Tasks: 1 (limit: 9324)
     Memory: 5.4M
        CPU: 124ms
     CGroup: /system.slice/ssh.service
             └─789 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
```

**গুরুত্বপূর্ণ তথ্য পড়া:**

| ফিল্ড                           | অর্থ                         |
| ------------------------------- | ---------------------------- |
| **Active: active (running)** 🟢 | চলছে                         |
| **Active: inactive (dead)** ⚫  | বন্ধ আছে                     |
| **Active: failed** 🔴           | কাজ করতে ব্যর্থ              |
| **enabled**                     | Boot-এ স্বয়ংক্রিয় শুরু হবে |
| **disabled**                    | Boot-এ শুরু হবে না           |
| **Main PID**                    | Process ID                   |

### Service শুরু ও বন্ধ করা:

```bash
# Service শুরু করুন
sudo systemctl start ssh

# Service বন্ধ করুন
sudo systemctl stop ssh

# Service restart করুন (বন্ধ করে আবার শুরু)
sudo systemctl restart ssh

# Service reload করুন (বন্ধ না করেই config পুনরায় পড়ো)
sudo systemctl reload ssh
```

| কমান্ড    | কাজ                 | কখন ব্যবহার          |
| --------- | ------------------- | -------------------- |
| `start`   | শুরু করো            | Service বন্ধ থাকলে   |
| `stop`    | বন্ধ করো            | Service চালু থাকলে   |
| `restart` | বন্ধ করে আবার শুরু  | Config পরিবর্তনের পর |
| `reload`  | Config পুনরায় পড়ো | Service না থামিয়েই  |

### Boot-এ Enable/Disable করা:

```bash
# Boot-এ স্বয়ংক্রিয় শুরু হোক
sudo systemctl enable ssh

# Boot-এ শুরু হোক না
sudo systemctl disable ssh

# Enable + এখনই Start
sudo systemctl enable --now ssh

# Disable + এখনই Stop
sudo systemctl disable --now ssh
```

| কমান্ড         | কাজ                          |
| -------------- | ---------------------------- |
| `enable`       | Boot-এ স্বয়ংক্রিয় শুরু হবে |
| `disable`      | Boot-এ শুরু হবে না           |
| `enable --now` | Boot-এ enable + এখনই start   |

### চলমান সব Service দেখা:

```bash
# সব চলমান service
systemctl list-units --type=service --state=running

# সব service (চলমান + বন্ধ)
systemctl list-units --type=service --all

# শুধু failed services
systemctl --failed
```

### Service আছে কিনা দেখা:

```bash
# Service চলছে কি?
systemctl is-active ssh
# active

# Service enabled কি?
systemctl is-enabled ssh
# enabled
```

---

## 2️⃣ `journalctl` — System Logs দেখা

**journalctl** হলো systemd-এর **log দেখার কমান্ড**।

**মনে রাখুন:** "**Journal** **C**on**t**ro**l**" = "জার্নাল/লগ নিয়ন্ত্রণ"

### মৌলিক ব্যবহার:

```bash
# সব log দেখুন (খুব বড়!)
journalctl

# শেষের log দেখুন (সবচেয়ে নতুন আগে)
journalctl -r

# আজকের log
journalctl --since today

# শেষ ১ ঘণ্টার log
journalctl --since "1 hour ago"

# নির্দিষ্ট সময়কালের log
journalctl --since "2026-03-05 01:00" --until "2026-03-05 02:00"
```

### নির্দিষ্ট Service-এর Log:

```bash
# SSH service-এর log
journalctl -u ssh

# SSH-এর সর্বশেষ ২০টি log
journalctl -u ssh -n 20

# SSH-এর log live দেখুন (tail -f এর মতো)
journalctl -u ssh -f
```

| Flag     | অর্থ          | কাজ                      |
| -------- | ------------- | ------------------------ |
| `-u`     | **u**nit      | নির্দিষ্ট service-এর log |
| `-n 20`  | **n**umber    | শেষ ২০টি entry           |
| `-f`     | **f**ollow    | Live/real-time log       |
| `-r`     | **r**everse   | নতুন আগে                 |
| `-p err` | **p**riority  | শুধু error দেখাও         |
| `-b`     | **b**oot      | বর্তমান boot-এর log      |
| `-b -1`  | previous boot | আগের boot-এর log         |

### Log Priority Levels:

```bash
# শুধু error দেখুন
journalctl -p err

# Warning ও তার উপরের সব
journalctl -p warning
```

| Priority | সংখ্যা | অর্থ                 |
| -------- | ------ | -------------------- |
| emerg    | 0      | জরুরি — সিস্টেম অচল! |
| alert    | 1      | এখনই পদক্ষেপ নিন     |
| crit     | 2      | গুরুতর সমস্যা        |
| err      | 3      | Error                |
| warning  | 4      | সতর্কতা              |
| notice   | 5      | পরিলক্ষণ             |
| info     | 6      | তথ্য                 |
| debug    | 7      | ডিবাগ                |

### Boot Log:

```bash
# বর্তমান boot-এর log
journalctl -b

# আগের boot-এর log
journalctl -b -1

# কয়টি boot recorded আছে
journalctl --list-boots
```

### Real-Life Use Case:

> ```bash
> # সিস্টেমে সমস্যা? Error log দেখুন:
> journalctl -p err --since today
>
> # কোনো service কাজ করছে না? তার log দেখুন:
> journalctl -u NetworkManager -n 50
>
> # Boot-এ কোনো সমস্যা? Boot log দেখুন:
> journalctl -b -p err
> ```

---

## 3️⃣ `timedatectl` — সময় ও Timezone

```bash
# বর্তমান সময়ের তথ্য
timedatectl

# Timezone পরিবর্তন
sudo timedatectl set-timezone Asia/Dhaka

# সব available timezone দেখুন
timedatectl list-timezones

# Timezone-এ "Dhaka" খুঁজুন
timedatectl list-timezones | grep Dhaka

# NTP (Internet time sync) চালু করুন
sudo timedatectl set-ntp true
```

---

## 4️⃣ `hostnamectl` — Hostname পরিবর্তন

```bash
# বর্তমান hostname দেখুন
hostnamectl

# Hostname বদলান
sudo hostnamectl set-hostname my-ubuntu-pc
```

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কমান্ড                                | কাজ               |
| ------------------------------------- | ----------------- |
| `systemctl status <svc>`              | Service-এর অবস্থা |
| `sudo systemctl start <svc>`          | Service শুরু      |
| `sudo systemctl stop <svc>`           | Service বন্ধ      |
| `sudo systemctl restart <svc>`        | Service restart   |
| `sudo systemctl enable <svc>`         | Boot-এ enable     |
| `sudo systemctl disable <svc>`        | Boot-এ disable    |
| `systemctl list-units --type=service` | সব service        |
| `systemctl --failed`                  | Failed services   |
| `journalctl -u <svc>`                 | Service-এর log    |
| `journalctl -f`                       | Live log          |
| `journalctl -p err`                   | শুধু errors       |
| `timedatectl`                         | সময় তথ্য         |
| `hostnamectl`                         | Hostname তথ্য     |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: Service দেখা

```bash
# 1. চলমান services দেখুন
systemctl list-units --type=service --state=running

# 2. কতগুলো service চলছে?
systemctl list-units --type=service --state=running | wc -l

# 3. NetworkManager-এর অবস্থা দেখুন
systemctl status NetworkManager

# 4. SSH-এর অবস্থা দেখুন
systemctl status ssh

# 5. Failed services আছে কি?
systemctl --failed
```

### অনুশীলন ২: Log দেখা

```bash
# 1. আজকের error log দেখুন
journalctl -p err --since today

# 2. বর্তমান boot log দেখুন (প্রথম ২০ লাইন)
journalctl -b | head -20

# 3. NetworkManager-এর শেষ ১০টি log
journalctl -u NetworkManager -n 10
```

### অনুশীলন ৩: সময় সেট করা

```bash
# 1. বর্তমান সময়ের তথ্য দেখুন
timedatectl

# 2. আপনার timezone ঠিক আছে কি?
# না হলে:
sudo timedatectl set-timezone Asia/Dhaka

# 3. NTP চালু আছে কি?
timedatectl | grep NTP
```

### অনুশীলন ৪: প্রশ্নোত্তর

1. `systemctl start` আর `systemctl enable` পার্থক্য কী?
2. `systemctl restart` আর `systemctl reload` পার্থক্য কী?
3. একটি service failed হলে কিভাবে log দেখবেন?
4. PID 1 কী এবং কেন গুরুত্বপূর্ণ?

---

## ➡️ পরবর্তী Section

[Section 12: Disk ও Storage Management →](section-12.md)

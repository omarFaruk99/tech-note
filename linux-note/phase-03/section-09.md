# 📖 Section 09: Process Management

---

## 🎯 এই Section-এ যা শিখবেন

- Process কী এবং কিভাবে কাজ করে
- Foreground ও Background Process
- Process দেখা ও নিয়ন্ত্রণ করা
- Process Kill করা
- Process Priority (Nice value)
- Job Control

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড    |          Ubuntu 24 LTS-এ          | মন্তব্য                                  |
| --------- | :-------------------------------: | ---------------------------------------- |
| `ps`      |         ✅ Pre-installed          | Process দেখা                             |
| `top`     |         ✅ Pre-installed          | Real-time process monitor                |
| `htop`    |        ❌ ইন্সটল করতে হবে         | `sudo apt install htop` (সুন্দর monitor) |
| `kill`    |         ✅ Pre-installed          | Process বন্ধ করা                         |
| `killall` |         ✅ Pre-installed          | নাম দিয়ে process বন্ধ                   |
| `pkill`   |         ✅ Pre-installed          | Pattern দিয়ে process বন্ধ               |
| `bg`      | ✅ Pre-installed (Shell built-in) | Background-এ পাঠানো                      |
| `fg`      | ✅ Pre-installed (Shell built-in) | Foreground-এ আনা                         |
| `jobs`    | ✅ Pre-installed (Shell built-in) | Job তালিকা দেখা                          |
| `nice`    |         ✅ Pre-installed          | Priority দিয়ে চালানো                    |
| `renice`  |         ✅ Pre-installed          | চলমান process-এর priority বদলানো         |
| `nohup`   |         ✅ Pre-installed          | Terminal বন্ধ করলেও চলতে থাকবে           |
| `pgrep`   |         ✅ Pre-installed          | Process ID খুঁজে বের করা                 |
| `pstree`  |        ❌ ইন্সটল করতে হবে         | `sudo apt install psmisc`                |

---

## ⚙️ Process কী?

**Process** হলো একটি **চলমান প্রোগ্রাম**। আপনি যখন কোনো প্রোগ্রাম চালান, তখন সেটি একটি Process হয়ে যায়।

### সহজ উদাহরণ:

```
প্রোগ্রাম (Program) = রান্নার রেসিপি (ডিস্কে সেভ করা)
Process = আসলে রান্না করা (RAM-এ চলছে)

একই রেসিপি থেকে একসাথে ৩টি রান্না হতে পারে = ৩টি Process
```

### প্রতিটি Process-এর যা থাকে:

| বৈশিষ্ট্য | বিবরণ                     | উদাহরণ            |
| --------- | ------------------------- | ----------------- |
| **PID**   | Process ID (অনন্য সংখ্যা) | 1234              |
| **PPID**  | Parent Process ID         | 1 (systemd)       |
| **User**  | কোন user চালাচ্ছে         | the-king          |
| **State** | বর্তমান অবস্থা            | Running, Sleeping |
| **CPU%**  | CPU ব্যবহার               | 5.2%              |
| **MEM%**  | RAM ব্যবহার               | 2.1%              |

### Process-এর অবস্থা (State):

| State    | চিহ্ন | অর্থ                            |
| -------- | ----- | ------------------------------- |
| Running  | `R`   | এখন চলছে                        |
| Sleeping | `S`   | ঘুমাচ্ছে (কিছু হবার অপেক্ষায়)  |
| Stopped  | `T`   | থামানো হয়েছে                   |
| Zombie   | `Z`   | শেষ হয়েছে কিন্তু তথ্য এখনও আছে |
| Dead     | `X`   | মৃত                             |

---

## 1️⃣ `ps` — Process দেখা

**কাজ:** বর্তমানে চলমান Process-এর তালিকা দেখায়।

**মনে রাখুন:** "**P**rocess **S**tatus" = "প্রক্রিয়ার অবস্থা"

### মৌলিক ব্যবহার:

```bash
# আপনার terminal-এর process দেখুন
ps
```

**আউটপুট:**

```
    PID TTY          TIME CMD
   1234 pts/0    00:00:00 bash
   5678 pts/0    00:00:00 ps
```

### গুরুত্বপূর্ণ Options:

```bash
# সব process দেখুন (সবচেয়ে বেশি ব্যবহৃত!)
ps aux
```

**প্রতিটি কলামের অর্থ:**

```
USER       PID  %CPU  %MEM    VSZ   RSS TTY   STAT  START   TIME  COMMAND
the-king  1234  0.2   1.5  45678  12345 pts/0  Ss   01:00   0:00  bash
root         1  0.0   0.3  16789   6543 ?      Ss   00:00   0:05  /sbin/init
```

| কলাম    | অর্থ                                 |
| ------- | ------------------------------------ |
| USER    | কোন user চালাচ্ছে                    |
| PID     | Process ID                           |
| %CPU    | CPU ব্যবহার (শতকরা)                  |
| %MEM    | RAM ব্যবহার (শতকরা)                  |
| VSZ     | Virtual memory size                  |
| RSS     | Resident set size (আসল RAM)          |
| STAT    | অবস্থা (R=Running, S=Sleeping, etc.) |
| START   | কখন শুরু হয়েছে                      |
| TIME    | মোট CPU সময়                         |
| COMMAND | কোন কমান্ড/প্রোগ্রাম                 |

### নির্দিষ্ট Process খোঁজা:

```bash
# "firefox" নামের process খুঁজুন
ps aux | grep firefox

# "python" নামের process
ps aux | grep python
```

> 💡 `|` (pipe) এবং `grep` নিয়ে Phase 4-এ বিস্তারিত শিখব। এখন শুধু জানুন — এটি ফিল্টার করে।

### `pgrep` — Process ID খোঁজা:

```bash
# Firefox-এর PID খুঁজুন
pgrep firefox
# 3456

# নাম সহ দেখুন
pgrep -l firefox
# 3456 firefox
```

---

## 2️⃣ `top` — Real-Time Process Monitor

**কাজ:** Process-গুলো **real-time**-এ দেখায় (প্রতি ৩ সেকেন্ডে আপডেট হয়)।

```bash
top
```

**আউটপুট (উপরের অংশ):**

```
top - 01:35:00 up 2:00,  1 user,  load average: 0.52, 0.34, 0.28
Tasks: 215 total,   1 running, 214 sleeping,   0 stopped,   0 zombie
%Cpu(s):  5.2 us,  2.1 sy,  0.0 ni, 91.8 id,  0.9 wa,  0.0 hi,  0.0 si
MiB Mem:   7850.4 total,   3420.1 free,   2830.5 used,   1599.8 buff/cache
MiB Swap:  2048.0 total,   2048.0 free,      0.0 used.   4765.3 avail Mem
```

**গুরুত্বপূর্ণ তথ্য:**
| ফিল্ড | অর্থ |
|-------|------|
| up 2:00 | কম্পিউটার ২ ঘণ্টা ধরে চালু আছে |
| 1 user | ১ জন logged in |
| load average | সিস্টেমের ভার (1.0 = একটি CPU core-এ ১০০%) |
| Tasks: 215 total | মোট ২১৫টি process চলছে |
| %Cpu: 91.8 id | CPU ৯১.৮% idle (ফাঁকা) = ভালো! |
| MiB Mem: 3420 free | ৩.৪ GB RAM ফাঁকা |

### top-এ Navigation:

| Key | কাজ                                  |
| --- | ------------------------------------ |
| `q` | বের হোন                              |
| `M` | RAM ব্যবহার অনুযায়ী সাজান           |
| `P` | CPU ব্যবহার অনুযায়ী সাজান           |
| `k` | Process kill করুন (PID জিজ্ঞেস করবে) |
| `u` | নির্দিষ্ট user-এর process দেখুন      |
| `1` | প্রতিটি CPU core আলাদাভাবে দেখুন     |
| `h` | সাহায্য                              |

---

## 3️⃣ `htop` — সুন্দর Process Monitor

**htop** হলো `top`-এর উন্নত ও সুন্দর version।

### ইন্সটল করুন:

```bash
sudo apt install -y htop
```

### চালান:

```bash
htop
```

**htop-এর সুবিধা:**

- 🎨 রঙিন interface
- 🖱️ মাউস সাপোর্ট
- স্ক্রল করা যায়
- সহজে process kill করা যায় (F9)
- Tree view দেখা যায় (F5)

### htop-এ Navigation:

| Key          | কাজ                            |
| ------------ | ------------------------------ |
| `q` বা `F10` | বের হোন                        |
| `F5`         | Tree view (কে কাকে তৈরি করেছে) |
| `F6`         | Sort by (সাজানোর ক্রম বদলান)   |
| `F9`         | Kill process                   |
| `F4`         | Filter (নাম দিয়ে ফিল্টার)     |
| `/`          | Search                         |
| `Space`      | Process tag করুন               |

> 💡 **পরামর্শ:** `top` এর বদলে সবসময় `htop` ব্যবহার করুন — আরও সুন্দর ও সহজ!

---

## 4️⃣ Process বন্ধ করা — `kill`, `killall`, `pkill`

### Signal কী?

Process বন্ধ করতে Linux **Signal** পাঠায়:

| Signal    | সংখ্যা | অর্থ      | কাজ                           |
| --------- | ------ | --------- | ----------------------------- |
| `SIGTERM` | 15     | Terminate | ভদ্রভাবে বন্ধ করো (default)   |
| `SIGKILL` | 9      | Kill      | জোর করে বন্ধ করো (শেষ উপায়!) |
| `SIGSTOP` | 19     | Stop      | সাময়িক থামাও                 |
| `SIGCONT` | 18     | Continue  | আবার চালাও                    |
| `SIGHUP`  | 1      | Hangup    | Restart / config পুনরায় পড়ো |

### `kill` — PID দিয়ে বন্ধ করা:

```bash
# ভদ্রভাবে বন্ধ করুন (SIGTERM - default)
kill 1234

# জোর করে বন্ধ করুন (SIGKILL - শেষ উপায়!)
kill -9 1234

# অথবা
kill -SIGKILL 1234
```

> ⚠️ **নিয়ম:** প্রথমে `kill PID` দিন। কাজ না হলে তবেই `kill -9 PID` দিন। কারণ `-9` process-কে cleanup করার সুযোগ দেয় না।

### `killall` — নাম দিয়ে বন্ধ করা:

```bash
# সব firefox process বন্ধ করুন
killall firefox

# জোর করে
killall -9 firefox
```

### `pkill` — Pattern দিয়ে বন্ধ করা:

```bash
# "fire" দিয়ে শুরু সব process বন্ধ
pkill fire

# নির্দিষ্ট user-এর process বন্ধ
pkill -u john
```

### Real-Life Use Case:

> ```bash
> # Firefox hang করেছে? (সাড়া দিচ্ছে না)
> # ধাপ ১: PID খুঁজুন
> pgrep firefox
> # 3456
>
> # ধাপ ২: ভদ্রভাবে বন্ধ করুন
> kill 3456
>
> # ধাপ ৩: কাজ না হলে জোর করুন
> kill -9 3456
>
> # অথবা একবারে নাম দিয়ে:
> killall firefox
> ```

---

## 5️⃣ Foreground ও Background Process

### Foreground Process:

Terminal-এ কমান্ড চালালে সেটি **foreground**-এ চলে — Terminal ব্লক থাকে, অন্য কিছু করা যায় না।

```bash
# এটি foreground-এ চলবে (terminal ব্লক থাকবে)
sleep 30
# 30 সেকেন্ড terminal আটকে থাকবে
```

### Background Process:

কমান্ডের শেষে **`&`** দিলে সেটি **background**-এ চলে — Terminal ফ্রি থাকে!

```bash
# Background-এ চালান
sleep 30 &
# [1] 5678     ← Job number [1], PID 5678
# Terminal ফ্রি! অন্য কাজ করতে পারবেন
```

### Job Control:

| কমান্ড/Key  | কাজ                                         |
| ----------- | ------------------------------------------- |
| `command &` | Background-এ চালান                          |
| `Ctrl + Z`  | চলমান process **সাময়িক থামান** (Suspend)   |
| `bg`        | থামানো process-কে **background**-এ চালান    |
| `fg`        | Background process-কে **foreground**-এ আনুন |
| `jobs`      | সব background job দেখুন                     |

### ধাপে ধাপে উদাহরণ:

```bash
# 1. একটি process চালান (foreground)
sleep 100

# 2. Ctrl + Z দিয়ে থামান
^Z
# [1]+  Stopped     sleep 100

# 3. Background-এ পাঠান
bg
# [1]+ sleep 100 &

# 4. Job তালিকা দেখুন
jobs
# [1]+  Running     sleep 100 &

# 5. Foreground-এ ফিরিয়ে আনুন
fg
# sleep 100
# (এখন আবার terminal ব্লক)

# 6. Ctrl + C দিয়ে বন্ধ করুন
^C
```

### `nohup` — Terminal বন্ধ করলেও চলতে থাকবে:

```bash
nohup long-running-script.sh &
# Terminal বন্ধ করলেও script চলতে থাকবে
# Output nohup.out ফাইলে সেভ হবে
```

**মনে রাখুন:** "**No H**ang**up**" = "হ্যাংআপ হবে না"

---

## 6️⃣ Process Priority — `nice` ও `renice`

প্রতিটি process-এর একটি **priority** (অগ্রাধিকার) থাকে, যাকে **nice value** বলে।

| Nice Value | পরিসর              | অর্থ                           |
| ---------- | ------------------ | ------------------------------ |
| -20        | সর্বোচ্চ priority  | এই process-কে সবার আগে CPU দাও |
| 0          | Default            | সাধারণ                         |
| +19        | সর্বনিম্ন priority | এই process সবার শেষে চলুক      |

> 💡 **মনে রাখুন:** "Nice" = "ভদ্র" — nice value বেশি মানে process **অন্যদের জন্য ভদ্র**, নিজে কম CPU নেয়!

```bash
# কম priority দিয়ে চালান (system-এর উপর চাপ কম)
nice -n 10 ./heavy-script.sh

# চলমান process-এর priority বদলান
renice +10 -p 1234

# নিজের সব process-এর priority বদলান
renice +5 -u the-king
```

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কমান্ড          | কাজ                   | উদাহরণ               |
| --------------- | --------------------- | -------------------- |
| `ps aux`        | সব process দেখা       | `ps aux`             |
| `top`           | Real-time monitor     | `top`                |
| `htop`          | সুন্দর monitor        | `htop` (ইন্সটল করুন) |
| `kill PID`      | Process বন্ধ (ভদ্র)   | `kill 1234`          |
| `kill -9 PID`   | Process বন্ধ (জোর)    | `kill -9 1234`       |
| `killall name`  | নাম দিয়ে বন্ধ        | `killall firefox`    |
| `pkill pattern` | Pattern দিয়ে বন্ধ    | `pkill fire`         |
| `pgrep name`    | PID খোঁজা             | `pgrep firefox`      |
| `command &`     | Background-এ চালানো   | `sleep 30 &`         |
| `Ctrl + Z`      | Suspend করা           | —                    |
| `bg`            | Background-এ পাঠানো   | `bg`                 |
| `fg`            | Foreground-এ আনা      | `fg`                 |
| `jobs`          | Job দেখা              | `jobs`               |
| `nice`          | Priority দিয়ে চালানো | `nice -n 10 cmd`     |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: Process দেখা

```bash
# 1. আপনার terminal-এর process দেখুন
ps

# 2. সব process দেখুন
ps aux

# 3. কতগুলো process চলছে?
ps aux | wc -l

# 4. আপনার process দেখুন
ps aux | grep $USER

# 5. htop ইন্সটল ও চালান
sudo apt install -y htop
htop
# q দিয়ে বেরোন
```

### অনুশীলন ২: Background ও Foreground

```bash
# 1. Background-এ একটি process চালান
sleep 60 &

# 2. Job দেখুন
jobs

# 3. Foreground-এ আনুন
fg

# 4. Ctrl + Z দিয়ে থামান

# 5. আবার background-এ পাঠান
bg

# 6. kill দিয়ে বন্ধ করুন
kill %1
```

### অনুশীলন ৩: Process Kill

```bash
# 1. একটি process background-এ চালান
sleep 300 &

# 2. PID খুঁজুন
pgrep sleep

# 3. Kill করুন
kill $(pgrep sleep)

# 4. confirm করুন
pgrep sleep
# কোনো output না আসলে মানে বন্ধ হয়েছে
```

---

## ➡️ পরবর্তী Section

[Section 10: System Information ও Monitoring →](section-10.md)

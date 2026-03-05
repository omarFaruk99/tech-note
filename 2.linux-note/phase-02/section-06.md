# 📖 Section 06: User ও Group Management

---

## 🎯 এই Section-এ যা শিখবেন

- Linux-এ User কী এবং কিভাবে কাজ করে
- User তৈরি, পরিবর্তন ও মুছে ফেলা
- Group কী এবং কেন দরকার
- Group তৈরি ও ব্যবস্থাপনা
- Password Management
- গুরুত্বপূর্ণ User/Group ফাইল

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড     |  Ubuntu 24 LTS-এ   | মন্তব্য                                       |
| ---------- | :----------------: | --------------------------------------------- |
| `useradd`  |  ✅ Pre-installed  | Low-level user তৈরি                           |
| `adduser`  |  ✅ Pre-installed  | User-friendly user তৈরি (Ubuntu-তে পছন্দনীয়) |
| `usermod`  |  ✅ Pre-installed  | User পরিবর্তন                                 |
| `userdel`  |  ✅ Pre-installed  | User মুছা                                     |
| `passwd`   |  ✅ Pre-installed  | Password বদলানো                               |
| `groupadd` |  ✅ Pre-installed  | Group তৈরি                                    |
| `groupdel` |  ✅ Pre-installed  | Group মুছা                                    |
| `groups`   |  ✅ Pre-installed  | User কোন কোন group-এ আছে                      |
| `id`       |  ✅ Pre-installed  | User/Group ID দেখা                            |
| `whoami`   |  ✅ Pre-installed  | বর্তমান username                              |
| `who`      |  ✅ Pre-installed  | কে কে logged in                               |
| `w`        |  ✅ Pre-installed  | কে কী করছে                                    |
| `last`     |  ✅ Pre-installed  | Login history                                 |
| `su`       |  ✅ Pre-installed  | User switch করা                               |
| `finger`   | ❌ ইন্সটল করতে হবে | `sudo apt install finger`                     |

---

## 👤 Linux-এ User কী?

Linux-এ প্রতিটি ব্যক্তি যে কম্পিউটার ব্যবহার করে তাকে একটি **User Account** দেওয়া হয়। প্রতিটি user-এর:

- একটি **Username** (নাম)
- একটি **UID** (User ID — সংখ্যা)
- একটি **Home Directory** (নিজের ফোল্ডার)
- একটি **Default Shell** (কোন shell ব্যবহার করবে)

### User-এর প্রকারভেদ:

| ধরন              | UID Range | উদাহরণ              | কাজ                             |
| ---------------- | --------- | ------------------- | ------------------------------- |
| **Root**         | 0         | `root`              | সর্বোচ্চ ক্ষমতাধর, সব করতে পারে |
| **System Users** | 1-999     | `www-data`, `mysql` | Services চালায় (মানুষ নয়)     |
| **Normal Users** | 1000+     | `the-king`          | সাধারণ ব্যবহারকারী (আপনি!)      |

```bash
# আপনার UID দেখুন
id
# uid=1000(the-king) ...
# 1000 মানে আপনি প্রথম normal user
```

---

## 📁 গুরুত্বপূর্ণ User/Group ফাইল

### `/etc/passwd` — সব User-এর তালিকা

```bash
cat /etc/passwd | head -3
```

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
the-king:x:1000:1000:The King,,,:/home/the-king:/bin/bash
```

**প্রতিটি ফিল্ডের অর্থ (`:` দিয়ে আলাদা):**

```
the-king : x : 1000 : 1000 : The King,,, : /home/the-king : /bin/bash
    │      │    │       │        │              │               │
    │      │    │       │        │              │               └── Default Shell
    │      │    │       │        │              └── Home Directory
    │      │    │       │        └── Full Name / Comment
    │      │    │       └── Primary Group ID (GID)
    │      │    └── User ID (UID)
    │      └── Password placeholder (আসল password /etc/shadow-এ)
    └── Username
```

### `/etc/shadow` — Password ফাইল (গোপন!)

```bash
sudo cat /etc/shadow | head -2
```

> ⚠️ এই ফাইল শুধু root পড়তে পারে! এখানে encrypted password থাকে।

### `/etc/group` — সব Group-এর তালিকা

```bash
cat /etc/group | head -5
```

```
root:x:0:
sudo:x:27:the-king
the-king:x:1000:
```

**ফিল্ডের অর্থ:**

```
sudo : x : 27 : the-king
  │    │    │      │
  │    │    │      └── এই group-এর সদস্যরা
  │    │    └── Group ID (GID)
  │    └── Password placeholder
  └── Group name
```

---

## 1️⃣ User তৈরি করা

### `adduser` — User-Friendly পদ্ধতি (Ubuntu-তে পছন্দনীয় ✅)

```bash
sudo adduser john
```

**এটি স্বয়ংক্রিয়ভাবে করবে:**

1. User তৈরি করবে
2. Home directory তৈরি করবে (`/home/john`)
3. Default ফাইল কপি করবে (`.bashrc`, `.profile`)
4. Password সেট করতে বলবে
5. পূর্ণ নাম ও অন্যান্য তথ্য জিজ্ঞেস করবে

**আউটপুট:**

```
Adding user 'john' ...
Adding new group 'john' (1001) ...
Adding new user 'john' (1001) with group 'john' ...
Creating home directory '/home/john' ...
Copying files from '/etc/skel' ...
New password: ****
Retype new password: ****
Full Name []: John Doe
Room Number []:
Work Phone []:
Home Phone []:
Other []:
Is the information correct? [Y/n] Y
```

### `useradd` — Low-Level পদ্ধতি

```bash
# শুধু user তৈরি (home directory, password কিছুই তৈরি হবে না)
sudo useradd bob

# Home directory সহ তৈরি
sudo useradd -m bob

# Shell নির্ধারণ করে তৈরি
sudo useradd -m -s /bin/bash bob

# সব option দিয়ে তৈরি
sudo useradd -m -s /bin/bash -c "Bob Smith" -G sudo bob
```

| Flag | অর্থ                    |
| ---- | ----------------------- |
| `-m` | **m**ake home directory |
| `-s` | default **s**hell       |
| `-c` | **c**omment (পূর্ণ নাম) |
| `-G` | অতিরিক্ত **G**roups     |
| `-d` | home **d**irectory path |

### adduser vs useradd:

| বিষয়          | `adduser`                      | `useradd`                    |
| -------------- | ------------------------------ | ---------------------------- |
| Interactive    | ✅ Interactive, সব জিজ্ঞেস করে | ❌ কিছু জিজ্ঞেস করে না       |
| Home directory | ✅ স্বয়ংক্রিয় তৈরি           | ❌ `-m` flag লাগে            |
| Password       | ✅ সাথে সাথে সেট করায়         | ❌ `passwd` আলাদা চালাতে হয় |
| ব্যবহার        | Ubuntu/Debian-এ পছন্দনীয়      | Scripting-এ ভালো             |

> 💡 **পরামর্শ:** Ubuntu-তে সবসময় `adduser` ব্যবহার করুন।

---

## 2️⃣ User পরিবর্তন করা — `usermod`

**কাজ:** বিদ্যমান User-এর তথ্য পরিবর্তন করে।

**মনে রাখুন:** "**User** **Mod**ify" = "User পরিবর্তন"

```bash
# User-কে sudo group-এ যোগ করুন (admin ক্ষমতা দিন)
sudo usermod -aG sudo john

# Username বদলান
sudo usermod -l new-name old-name

# Home directory বদলান
sudo usermod -d /home/new-home -m john

# Shell বদলান
sudo usermod -s /bin/zsh john

# User-কে lock করুন (login করতে পারবে না)
sudo usermod -L john

# User unlock করুন
sudo usermod -U john
```

| Flag  | অর্থ                                             |
| ----- | ------------------------------------------------ |
| `-aG` | **a**ppend to **G**roup (যোগ করো, আগেরগুলো রাখো) |
| `-l`  | **l**ogin name বদলাও                             |
| `-d`  | home **d**irectory বদলাও                         |
| `-m`  | home directory **m**ove করো                      |
| `-s`  | **s**hell বদলাও                                  |
| `-L`  | **L**ock user                                    |
| `-U`  | **U**nlock user                                  |

> ⚠️ **সতর্কতা:** `-aG` তে **`a` ভুলে গেলে** user-এর **সব আগের group মুছে যাবে!** শুধু `-G` দিলে replace হয়, `-aG` দিলে append হয়।

---

## 3️⃣ User মুছে ফেলা — `userdel`

```bash
# শুধু user মুছুন (home directory থাকবে)
sudo userdel john

# User + home directory + mail spool সব মুছুন
sudo userdel -r john
```

**`-r`** = "**r**emove home directory" — ব্যবহারকারীর সব ডেটাসহ মুছে ফেলো

> ⚠️ `-r` দিলে user-এর সব ফাইল **চিরতরে** মুছে যায়!

---

## 4️⃣ Password Management — `passwd`

```bash
# নিজের password বদলান
passwd

# অন্য user-এর password বদলান (sudo লাগবে)
sudo passwd john

# Password expire করান (পরবর্তী login-এ বদলাতে হবে)
sudo passwd -e john

# Password বিস্তারিত দেখুন
sudo passwd -S john
# john P 2026-03-05 0 99999 7 -1 (Password set, ...)
```

| Flag | কাজ                                     |
| ---- | --------------------------------------- |
| `-e` | **e**xpire — পরবর্তী login-এ বদলাতে হবে |
| `-l` | **l**ock — password disable করো         |
| `-u` | **u**nlock — password enable করো        |
| `-S` | **S**tatus — password-এর অবস্থা দেখাও   |

---

## 5️⃣ Group Management

### Group তৈরি:

```bash
# নতুন Group তৈরি
sudo groupadd developers
sudo groupadd designers
```

### User-কে Group-এ যোগ করা:

```bash
# the-king কে developers group-এ যোগ করুন
sudo usermod -aG developers the-king

# পরিবর্তন দেখুন (logout-login করতে হতে পারে)
groups the-king
# the-king : the-king sudo developers
```

### Group মুছে ফেলা:

```bash
sudo groupdel designers
```

### User-কে Group থেকে বাদ দেওয়া:

```bash
sudo gpasswd -d john developers
```

**`-d`** = "**d**elete from group"

---

## 6️⃣ তথ্য দেখার কমান্ড

### `who` — কে কে logged in?

```bash
who
# the-king tty1    2026-03-05 01:00
# the-king pts/0   2026-03-05 01:30
```

### `w` — কে কী করছে? (বিস্তারিত)

```bash
w
```

```
 01:35:00 up 2:00,  2 users,  load average: 0.52, 0.34, 0.28
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
the-king tty1     -                01:00    35:00  0.05s  0.01s bash
the-king pts/0    -                01:30    0.00s  0.03s  0.00s w
```

### `last` — Login History

```bash
# শেষ ১০ বার কে login করেছে
last -10
```

### `groups` — User কোন কোন group-এ?

```bash
groups
# the-king sudo

groups john
# john developers
```

### `su` — User Switch করা

```bash
# john user-এ switch করুন
su john
# john-এর password দিতে হবে

# root-এ switch করুন
su -
# root-এর password দিতে হবে

# বের হোন (আগের user-এ ফিরুন)
exit
```

**`su`** = "**S**witch **U**ser" বা "**S**ubstitute **U**ser"

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কমান্ড     | কাজ                     | উদাহরণ                         |
| ---------- | ----------------------- | ------------------------------ |
| `adduser`  | User তৈরি (interactive) | `sudo adduser john`            |
| `useradd`  | User তৈরি (low-level)   | `sudo useradd -m john`         |
| `usermod`  | User পরিবর্তন           | `sudo usermod -aG sudo john`   |
| `userdel`  | User মুছা               | `sudo userdel -r john`         |
| `passwd`   | Password বদলানো         | `passwd` বা `sudo passwd john` |
| `groupadd` | Group তৈরি              | `sudo groupadd devs`           |
| `groupdel` | Group মুছা              | `sudo groupdel devs`           |
| `groups`   | Group দেখা              | `groups the-king`              |
| `id`       | UID/GID দেখা            | `id john`                      |
| `who`      | কে logged in            | `who`                          |
| `w`        | কে কী করছে              | `w`                            |
| `last`     | Login history           | `last -10`                     |
| `su`       | User switch             | `su john`                      |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: তথ্য দেখা

```bash
# 1. আপনার complete ID দেখুন
id

# 2. আপনার groups দেখুন
groups

# 3. কে কে logged in দেখুন
who

# 4. বিস্তারিত দেখুন
w

# 5. Login history দেখুন
last -5

# 6. /etc/passwd-এ আপনার entry দেখুন
grep $USER /etc/passwd
```

### অনুশীলন ২: User তৈরি ও পরিচালনা

```bash
# 1. একটি test user তৈরি করুন
sudo adduser testuser

# 2. নতুন user-এর তথ্য দেখুন
id testuser

# 3. নতুন user-এ switch করুন
su testuser
whoami    # testuser হওয়া উচিত
exit      # ফিরে আসুন

# 4. User মুছে ফেলুন
sudo userdel -r testuser
```

### অনুশীলন ৩: Group পরীক্ষা

```bash
# 1. একটি Group তৈরি করুন
sudo groupadd test-team

# 2. নিজেকে সেই group-এ যোগ করুন
sudo usermod -aG test-team $USER

# 3. দেখুন যোগ হয়েছে কিনা
groups $USER

# 4. Group মুছে ফেলুন
sudo groupdel test-team
```

### অনুশীলন ৪: প্রশ্নোত্তর

1. `adduser` আর `useradd` এর মধ্যে কোনটি Ubuntu-তে ভালো এবং কেন?
2. `-aG` আর `-G` এর পার্থক্য কী?
3. UID 0 মানে কী?
4. `/etc/passwd` আর `/etc/shadow` এর মধ্যে পার্থক্য কী?

---

## ➡️ পরবর্তী Section

[Section 07: Package Management (apt) →](section-07.md)

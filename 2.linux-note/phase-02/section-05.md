# 📖 Section 05: File Permissions ও Ownership

---

## 🎯 এই Section-এ যা শিখবেন

- Linux-এ Permission কেন দরকার
- Permission কিভাবে কাজ করে (rwx)
- Numeric (Octal) ও Symbolic Permission
- `chmod` — Permission পরিবর্তন
- `chown` — মালিকানা পরিবর্তন
- `chgrp` — Group পরিবর্তন
- Special Permissions (SUID, SGID, Sticky Bit)
- `sudo` — Superuser ক্ষমতা

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড  | Ubuntu 24 LTS-এ  | মন্তব্য                      |
| ------- | :--------------: | ---------------------------- |
| `chmod` | ✅ Pre-installed | coreutils package-এর অংশ     |
| `chown` | ✅ Pre-installed | coreutils package-এর অংশ     |
| `chgrp` | ✅ Pre-installed | coreutils package-এর অংশ     |
| `sudo`  | ✅ Pre-installed | Ubuntu-তে default ভাবে আসে   |
| `ls -l` | ✅ Pre-installed | Permission দেখতে ব্যবহার হয় |
| `stat`  | ✅ Pre-installed | বিস্তারিত permission দেখায়  |
| `id`    | ✅ Pre-installed | User/Group ID দেখায়         |
| `umask` | ✅ Pre-installed | Default permission সেট করে   |

> ✅ এই section-এর **সব কমান্ড** Ubuntu 24 LTS-এ **আগে থেকেই ইন্সটল করা আছে**। কিছু আলাদা করে ইন্সটল করতে হবে না।

---

## 🔐 Permission কেন দরকার?

Linux একটি **Multi-User** Operating System — একই কম্পিউটারে একাধিক ব্যক্তি কাজ করতে পারে। তাই প্রতিটি ফাইল ও ফোল্ডারে **নিয়ন্ত্রণ** দরকার:

- কে পড়তে পারবে? (Read)
- কে লিখতে/পরিবর্তন করতে পারবে? (Write)
- কে চালাতে পারবে? (Execute)

### সহজ উদাহরণ:

কল্পনা করুন একটি অফিস:

- **আপনার ডেস্ক (Your files):** আপনি সব করতে পারেন
- **সহকর্মীর ডেস্ক (Other's files):** আপনি শুধু দেখতে পারেন
- **ম্যানেজারের কক্ষ (/root):** আপনি ঢুকতেই পারেন না
- **Notice Board (/tmp):** সবাই পড়তে ও লিখতে পারে

---

## 👥 তিন ধরনের ব্যবহারকারী (Permission Categories)

প্রতিটি ফাইলের জন্য **তিন ধরনের** ব্যবহারকারী আছে:

| চিহ্ন | ইংরেজি           | বাংলা  | কে?                     |
| ----- | ---------------- | ------ | ----------------------- |
| **u** | **U**ser (Owner) | মালিক  | যে ফাইলটি তৈরি করেছে    |
| **g** | **G**roup        | গোষ্ঠী | মালিকের গোষ্ঠীর সদস্যরা |
| **o** | **O**thers       | অন্যরা | বাকি সবাই               |
| **a** | **A**ll          | সবাই   | উপরের তিনজনই (u+g+o)    |

### Real-Life তুলনা:

```
একটি বাড়ির চাবি:
├── Owner (u) = বাড়ির মালিক → সব ঘরে ঢুকতে পারে
├── Group (g) = পরিবারের সদস্য → বেশিরভাগ ঘরে ঢুকতে পারে
└── Others (o) = বাইরের মানুষ → শুধু বসার ঘরে ঢুকতে পারে
```

---

## 📋 তিন ধরনের Permission (rwx)

| চিহ্ন | ইংরেজি      | বাংলা  | ফাইলে মানে                      | ফোল্ডারে মানে                    |
| ----- | ----------- | ------ | ------------------------------- | -------------------------------- |
| **r** | **R**ead    | পড়া   | ফাইলের content পড়া যাবে        | ফোল্ডারের ভিতরে কী আছে দেখা যাবে |
| **w** | **W**rite   | লেখা   | ফাইল edit/মুছা যাবে             | ফোল্ডারে ফাইল তৈরি/মুছা যাবে     |
| **x** | e**X**ecute | চালানো | ফাইল program হিসেবে চালানো যাবে | ফোল্ডারে `cd` দিয়ে ঢোকা যাবে    |
| **-** | None        | নেই    | অনুমতি নেই                      | অনুমতি নেই                       |

---

## 🔍 Permission পড়া শেখা

`ls -l` দিয়ে permission দেখা যায়:

```bash
ls -l notes.txt
# -rw-r--r-- 1 the-king the-king 89 Mar 5 01:00 notes.txt
```

### Permission String ভেঙে দেখা:

```
- rw- r-- r--
│ │   │   │
│ │   │   └── Others (অন্যরা): r-- = শুধু পড়তে পারে
│ │   └────── Group (গোষ্ঠী): r-- = শুধু পড়তে পারে
│ └────────── User/Owner (মালিক): rw- = পড়তে ও লিখতে পারে
└──────────── File Type: - = সাধারণ ফাইল
```

### File Type চিহ্ন:

| চিহ্ন | অর্থ                    |
| ----- | ----------------------- |
| `-`   | সাধারণ ফাইল             |
| `d`   | Directory (ফোল্ডার)     |
| `l`   | Symbolic Link (শর্টকাট) |
| `c`   | Character Device        |
| `b`   | Block Device            |

### আরও উদাহরণ:

```
drwxr-xr-x → ফোল্ডার: মালিক সব করতে পারে, বাকিরা পড়তে ও ঢুকতে পারে
-rwxr-xr-x → ফাইল: সবাই পড়তে ও চালাতে পারে, শুধু মালিক লিখতে পারে
-rwx------ → ফাইল: শুধু মালিক সব করতে পারে, বাকি কেউ কিছু পারে না
-rw-rw-r-- → ফাইল: মালিক ও group পড়তে-লিখতে পারে, অন্যরা শুধু পড়তে পারে
```

---

## 🔢 Numeric (Octal) Permission System

প্রতিটি permission-এর একটি **সংখ্যামান** আছে:

| Permission  | সংখ্যা |
| ----------- | ------ |
| Read (r)    | **4**  |
| Write (w)   | **2**  |
| Execute (x) | **1**  |
| None (-)    | **0**  |

### যোগ করে Permission বের করা:

| Permission | হিসাব | মান   |
| ---------- | ----- | ----- |
| `---`      | 0+0+0 | **0** |
| `--x`      | 0+0+1 | **1** |
| `-w-`      | 0+2+0 | **2** |
| `-wx`      | 0+2+1 | **3** |
| `r--`      | 4+0+0 | **4** |
| `r-x`      | 4+0+1 | **5** |
| `rw-`      | 4+2+0 | **6** |
| `rwx`      | 4+2+1 | **7** |

### তিন সংখ্যার Permission:

```
chmod 754 file.txt

7   5   4
│   │   │
│   │   └── Others: r-- (4) = শুধু পড়া
│   └────── Group:  r-x (5) = পড়া ও চালানো
└────────── User:   rwx (7) = সব (পড়া, লেখা, চালানো)
```

### সাধারণ Permission সংখ্যা:

| সংখ্যা  | Permission   | কখন ব্যবহার হয়                      |
| ------- | ------------ | ------------------------------------ |
| **755** | `rwxr-xr-x`  | ফোল্ডার, executable scripts          |
| **644** | `rw-r--r--`  | সাধারণ ফাইল (documents, config)      |
| **700** | `rwx------`  | ব্যক্তিগত ফোল্ডার (শুধু মালিক)       |
| **600** | `rw-------`  | গোপন ফাইল (SSH keys, passwords)      |
| **777** | `rwxrwxrwx`  | সবার জন্য সব খোলা (**⚠️ বিপজ্জনক!**) |
| **000** | `----------` | কারও কোনো অনুমতি নেই                 |

> ⚠️ **সতর্কতা:** `777` permission **কখনও** ব্যবহার করবেন না (বিশেষত production/server-এ)! এটি সিকিউরিটি ঝুঁকি তৈরি করে।

---

## 1️⃣ `chmod` — Permission পরিবর্তন করা

**কাজ:** ফাইল/ফোল্ডারের permission পরিবর্তন করে।

**মনে রাখুন:** "**Ch**ange **Mod**e" = "মোড বদলাও"

### Numeric Method (সংখ্যা দিয়ে):

```bash
# ফাইলকে 644 permission দিন
chmod 644 notes.txt
# মালিক: পড়া+লেখা, বাকি সবাই: শুধু পড়া

# Script-কে executable করুন
chmod 755 script.sh
# মালিক: সব, বাকিরা: পড়া+চালানো

# ফাইলকে শুধু মালিকের জন্য রাখুন
chmod 600 secret.txt
# শুধু মালিক পড়তে ও লিখতে পারবে

# ফোল্ডারকে private করুন
chmod 700 private-folder/
```

### Symbolic Method (চিহ্ন দিয়ে):

| Operator | অর্থ                          |
| -------- | ----------------------------- |
| `+`      | Permission **যোগ** করো        |
| `-`      | Permission **বাদ** দাও        |
| `=`      | **ঠিক এই** permission সেট করো |

```bash
# মালিককে execute permission দিন
chmod u+x script.sh

# অন্যদের write permission বাদ দিন
chmod o-w notes.txt

# Group-কে read ও write দিন
chmod g+rw project.txt

# সবাইকে read permission দিন
chmod a+r public.txt

# মালিককে সব, group-কে read+execute, অন্যদের কিছু না
chmod u=rwx,g=rx,o= file.txt
```

### Recursive Permission (ফোল্ডারের সব কিছুতে):

```bash
# ফোল্ডার ও তার সব content-এ permission দিন
chmod -R 755 my-project/
```

**`-R`** = "**R**ecursive" — ভিতরের সব ফাইল ও ফোল্ডারেও প্রযোজ্য

### Real-Life Use Case:

> ```bash
> # Shell script তৈরি করলেন, কিন্তু চালাতে পারছেন না
> bash: ./script.sh: Permission denied
>
> # সমাধান: execute permission দিন
> chmod +x script.sh
> ./script.sh   # এখন চলবে! ✅
> ```

---

## 2️⃣ `chown` — মালিকানা পরিবর্তন

**কাজ:** ফাইলের **মালিক (owner)** এবং/অথবা **group** পরিবর্তন করে।

**মনে রাখুন:** "**Ch**ange **Own**er" = "মালিক বদলাও"

> ⚠️ `chown` চালাতে সাধারণত **sudo** লাগে!

### Format:

```bash
sudo chown <new-owner> <file>
sudo chown <new-owner>:<new-group> <file>
```

### উদাহরণ:

```bash
# মালিক পরিবর্তন
sudo chown john notes.txt
# এখন john notes.txt-এর মালিক

# মালিক ও group দুটোই পরিবর্তন
sudo chown john:developers notes.txt

# শুধু group পরিবর্তন
sudo chown :developers notes.txt

# Recursive (ফোল্ডারের সব কিছুর মালিক বদলান)
sudo chown -R the-king:the-king my-project/
```

### Real-Life Use Case:

> ```bash
> # Web server-এর ফাইলের মালিক www-data করা (nginx/apache)
> sudo chown -R www-data:www-data /var/www/html/
> ```

---

## 3️⃣ `chgrp` — Group পরিবর্তন

**কাজ:** ফাইলের **group** পরিবর্তন করে।

**মনে রাখুন:** "**Ch**ange **Gr**ou**p**" = "গোষ্ঠী বদলাও"

```bash
# Group পরিবর্তন
sudo chgrp developers project.txt

# Recursive
sudo chgrp -R developers project-folder/
```

> 💡 `chgrp` আসলে `chown :group` এর shortcut। দুটোই একই কাজ করে:
>
> ```bash
> sudo chgrp developers file.txt
> # সমান
> sudo chown :developers file.txt
> ```

---

## 4️⃣ `sudo` — Superuser ক্ষমতা

**কাজ:** সাধারণ user হিসেবে **admin/root** কমান্ড চালাতে দেয়।

**মনে রাখুন:** "**S**uper **U**ser **Do**" = "সুপার ইউজার হিসেবে করো"

### কেন দরকার?

Linux-এ কিছু কাজ শুধু **root** (admin) করতে পারে:

- সফটওয়্যার ইন্সটল করা
- সিস্টেম ফাইল পরিবর্তন করা
- অন্যের ফাইলের মালিকানা বদলানো
- Service শুরু/বন্ধ করা

### ব্যবহার:

```bash
# আপনার password দিতে হবে
sudo apt update
# [sudo] password for the-king: ****

# sudo ছাড়া error হবে:
apt update
# E: Could not open lock file - Permission denied
```

### গুরুত্বপূর্ণ sudo কমান্ড:

```bash
# Root user হিসেবে shell খুলুন (সাবধানে!)
sudo -i

# কোন কমান্ড sudo দিয়ে চালানো যাবে দেখুন
sudo -l

# শেষ sudo session-এর সময় বাড়ানো
sudo -v

# sudo cache মুছুন (password আবার চাইবে)
sudo -k
```

> ⚠️ **সতর্কতা:**
>
> - `sudo` দিয়ে ভুল কমান্ড দিলে সিস্টেম নষ্ট হতে পারে!
> - `sudo -i` বা `sudo su` ব্যবহার কমানোর চেষ্টা করুন
> - প্রতিটি কমান্ডের আগে `sudo` দিন, root shell-এ কাজ করবেন না

---

## 5️⃣ `umask` — Default Permission সেট করা

**কাজ:** নতুন ফাইল/ফোল্ডার তৈরি হলে কী permission পাবে তা নির্ধারণ করে।

**মনে রাখুন:** "**U**ser file creation **MASK**" = "ফাইল তৈরির মুখোশ"

### কিভাবে কাজ করে:

```
নতুন ফাইলের default permission = 666
নতুন ফোল্ডারের default permission = 777

umask এই default থেকে বাদ দেয়

যদি umask = 022:
ফাইল: 666 - 022 = 644 (rw-r--r--)
ফোল্ডার: 777 - 022 = 755 (rwxr-xr-x)
```

### ব্যবহার:

```bash
# বর্তমান umask দেখুন
umask
# 0022

# umask পরিবর্তন করুন
umask 077
# এখন নতুন ফাইল: 600 (rw-------)
# এখন নতুন ফোল্ডার: 700 (rwx------)

# পরীক্ষা করুন
touch test-file.txt
ls -l test-file.txt
# -rw------- 1 the-king the-king 0 ... test-file.txt
```

---

## 6️⃣ `id` — User ও Group তথ্য

**কাজ:** বর্তমান user-এর UID, GID ও group তথ্য দেখায়।

```bash
id
# uid=1000(the-king) gid=1000(the-king) groups=1000(the-king),4(adm),27(sudo)
```

**মানে:**

```
uid=1000(the-king)     → User ID 1000, নাম the-king
gid=1000(the-king)     → Primary Group ID 1000
groups=...27(sudo)     → sudo group-এর সদস্য (admin কাজ করতে পারবে)
```

---

## 🌟 Special Permissions (উন্নত বিষয়)

সাধারণ rwx ছাড়াও তিনটি **বিশেষ permission** আছে:

### SUID (Set User ID):

```bash
ls -l /usr/bin/passwd
# -rwsr-xr-x 1 root root 68208 ... /usr/bin/passwd
```

**`s`** চিহ্ন দেখুন user-এর `x` এর জায়গায়! এর মানে: যে-ই এই প্রোগ্রাম চালাক, এটি **মালিকের (root) ক্ষমতায়** চলবে।

> 💡 `passwd` কমান্ড দিয়ে আপনি নিজের password বদলাতে পারেন। কিন্তু password `/etc/shadow` ফাইলে থাকে যা শুধু root পড়তে পারে। SUID থাকায় `passwd` root ক্ষমতায় চলে এবং ফাইল আপডেট করতে পারে।

### Sticky Bit:

```bash
ls -ld /tmp
# drwxrwxrwt 15 root root 4096 ... /tmp
```

**`t`** চিহ্ন দেখুন Others-এর `x` এর জায়গায়! এর মানে: সবাই ফাইল তৈরি করতে পারে, কিন্তু **শুধু মালিক** নিজের ফাইল মুছতে পারবে।

> 💡 `/tmp` ফোল্ডারে সবাই লিখতে পারে। কিন্তু Sticky Bit থাকায় আপনি অন্যের ফাইল মুছতে পারবেন না, শুধু নিজেরটা পারবেন।

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কমান্ড  | কাজ                | উদাহরণ                  | sudo লাগে?     |
| ------- | ------------------ | ----------------------- | -------------- |
| `chmod` | Permission বদলানো  | `chmod 755 file`        | নিজের ফাইলে না |
| `chown` | মালিক বদলানো       | `sudo chown user file`  | ✅ হ্যাঁ       |
| `chgrp` | Group বদলানো       | `sudo chgrp group file` | ✅ হ্যাঁ       |
| `sudo`  | Admin হিসেবে কাজ   | `sudo apt update`       | —              |
| `umask` | Default permission | `umask 022`             | না             |
| `id`    | User/Group তথ্য    | `id`                    | না             |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: Permission পড়া

```bash
# 1. Home-এ কিছু ফাইলের permission দেখুন
ls -la ~

# 2. নিচের permission-গুলো পড়ে বলুন কে কী পারে:
# -rw-r--r--
# drwxr-xr-x
# -rwx------
# -rw-rw-r--
```

### অনুশীলন ২: chmod ব্যবহার

```bash
# 1. Practice ফোল্ডারে যান
cd ~/linux-practice

# 2. একটি ফাইল তৈরি করুন
echo '#!/bin/bash' > myscript.sh
echo 'echo "Hello from my script!"' >> myscript.sh

# 3. Permission দেখুন
ls -l myscript.sh

# 4. চালানোর চেষ্টা করুন (error হবে)
./myscript.sh

# 5. Execute permission দিন
chmod +x myscript.sh

# 6. এখন চালান (কাজ করবে!)
./myscript.sh

# 7. Numeric method-এ permission দিন
chmod 644 myscript.sh

# 8. Permission দেখুন
ls -l myscript.sh
```

### অনুশীলন ৩: Permission পরীক্ষা

```bash
# 1. একটি ফাইল তৈরি করুন
echo "secret data" > secret.txt

# 2. শুধু মালিক পড়তে পারবে
chmod 400 secret.txt

# 3. লিখতে চেষ্টা করুন (error হবে!)
echo "more data" >> secret.txt

# 4. আবার write permission দিন
chmod 600 secret.txt

# 5. এখন লিখুন (কাজ করবে)
echo "more data" >> secret.txt
```

### অনুশীলন ৪: Numeric Permission প্র্যাকটিস

নিচের permission-গুলোর সংখ্যা বের করুন (মুখে/কাগজে):

1. `rwxr-xr-x` = ?
2. `rw-r--r--` = ?
3. `rwx------` = ?
4. `rw-rw-r--` = ?
5. `r--------` = ?

<details>
<summary>💡 উত্তর দেখুন</summary>

1. `rwxr-xr-x` = 755
2. `rw-r--r--` = 644
3. `rwx------` = 700
4. `rw-rw-r--` = 664
5. `r--------` = 400

</details>

---

## ➡️ পরবর্তী Section

[Section 06: User ও Group Management →](section-06.md)

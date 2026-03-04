# 📖 Section 04: File Content দেখা ও Text Processing Basics

---

## 🎯 এই Section-এ যা শিখবেন

- ফাইলের ভিতরে কী আছে দেখা
- বড় ফাইল পড়ার কৌশল
- ফাইলের তথ্য সংগ্রহ করা
- ফাইলে লেখা (Redirect দিয়ে)
- ফাইল খোঁজা
- `cat`, `less`, `more`, `head`, `tail`, `wc`, `file`, `find`, `locate`, `echo` কমান্ড

---

## 1️⃣ `cat` — ফাইলের পুরো Content দেখা

**কাজ:** ফাইলের সম্পূর্ণ বিষয়বস্তু Terminal-এ দেখায়।

**মনে রাখুন:** "**Cat**enate" (= যুক্ত করা) — মূলত একাধিক ফাইল জোড়া লাগানোর জন্য তৈরি, কিন্তু সবচেয়ে বেশি ব্যবহার হয় ফাইল পড়তে।

### মৌলিক ব্যবহার:

```bash
# একটি ফাইল পড়ুন
cat /etc/hostname
```

**আউটপুট:**

```
ubuntu
```

### Line Number সহ দেখা:

```bash
cat -n /etc/passwd
```

**`-n` এর অর্থ:** "**n**umber" — প্রতিটি লাইনে নম্বর দেখায়

**আউটপুট (আংশিক):**

```
     1  root:x:0:0:root:/root:/bin/bash
     2  daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
     3  bin:x:2:2:bin:/bin:/usr/sbin/nologin
     ...
```

### একাধিক ফাইল একসাথে দেখা:

```bash
cat file1.txt file2.txt
```

### ফাইলে লেখা (Output Redirection দিয়ে):

```bash
# নতুন ফাইলে লিখুন (আগেরটা মুছে যাবে)
cat > notes.txt
এটি আমার প্রথম নোট
দ্বিতীয় লাইন
তৃতীয় লাইন
# লেখা শেষ হলে Ctrl + D চাপুন

# ফাইলের শেষে যোগ করুন (আগেরটা থাকবে)
cat >> notes.txt
চতুর্থ লাইন
# Ctrl + D চাপুন
```

| চিহ্ন | কাজ                       | ফাইল থাকলে       |
| ----- | ------------------------- | ---------------- |
| `>`   | নতুন করে লেখো (overwrite) | আগেরটা মুছে যায় |
| `>>`  | শেষে যোগ করো (append)     | আগেরটা থাকে      |

> 💡 **সতর্কতা:** `>` ব্যবহারে সাবধান! এটি ফাইলের আগের সব লেখা মুছে দেবে!

### দুটি ফাইল জোড়া লাগানো:

```bash
cat part1.txt part2.txt > complete.txt
```

> **Real-Life Use Case:** কোনো configuration ফাইল দ্রুত দেখতে `cat` সবচেয়ে সহজ:
>
> ```bash
> cat /etc/os-release    # আপনার OS-এর তথ্য
> cat /etc/shells        # সিস্টেমে কোন কোন shell আছে
> ```

---

## 2️⃣ `less` — পৃষ্ঠায় পৃষ্ঠায় পড়া (সবচেয়ে ভালো উপায়)

**কাজ:** বড় ফাইল আরামে, পৃষ্ঠায় পৃষ্ঠায় পড়া যায়।

**মনে রাখুন:** "**Less** is more" — কম দেখায় (একবারে এক পৃষ্ঠা), কিন্তু বেশি সুবিধা দেয়।

```bash
less /etc/passwd
```

### less-এ Navigation:

| Key       | কাজ                              |
| --------- | -------------------------------- |
| `↑` / `↓` | এক লাইন উপরে/নিচে                |
| `Space`   | এক পৃষ্ঠা নিচে                   |
| `b`       | এক পৃষ্ঠা উপরে (**b**ack)        |
| `g`       | ফাইলের শুরুতে যান                |
| `G`       | ফাইলের শেষে যান                  |
| `/search` | নিচের দিকে সার্চ করুন            |
| `?search` | উপরের দিকে সার্চ করুন            |
| `n`       | পরবর্তী search result (**n**ext) |
| `N`       | আগের search result               |
| `q`       | বের হোন (**q**uit)               |

### cat vs less:

| বিষয়      | `cat`                                | `less`                         |
| ---------- | ------------------------------------ | ------------------------------ |
| ছোট ফাইল   | ✅ ভালো                              | ব্যবহার করা যায়               |
| বড় ফাইল   | ❌ সব একবারে দেখায়, স্ক্রল করতে হয় | ✅ পৃষ্ঠায় পৃষ্ঠায় পড়া যায় |
| সার্চ করা  | ❌ পারে না                           | ✅ `/` দিয়ে সার্চ করা যায়    |
| Navigation | ❌ করা যায় না                       | ✅ উপরে-নিচে যাওয়া যায়       |

> 💡 **পরামর্শ:** বড় ফাইল পড়ার জন্য সবসময় `less` ব্যবহার করুন, `cat` নয়।

---

## 3️⃣ `more` — পুরনো ধাঁচে পড়া

**কাজ:** `less` এর মতো, কিন্তু কম বৈশিষ্ট্যযুক্ত।

```bash
more /etc/passwd
```

| বৈশিষ্ট্য    | `less`   | `more` |
| ------------ | -------- | ------ |
| পিছনে যাওয়া | ✅ হ্যাঁ | ❌ না  |
| সার্চ        | ✅ ভালো  | সীমিত  |
| গতি          | দ্রুত    | ধীর    |

> 💡 `less` ব্যবহার করুন, `more` এর দরকার নেই। "**less is more!**" 😄

---

## 4️⃣ `head` — ফাইলের শুরু দেখা

**কাজ:** ফাইলের **প্রথম কিছু লাইন** দেখায় (default: ১০ লাইন)।

**মনে রাখুন:** "**Head**" = "মাথা" — ফাইলের মাথার দিক দেখায়

```bash
# প্রথম ১০ লাইন দেখুন (default)
head /etc/passwd

# প্রথম ৫ লাইন দেখুন
head -n 5 /etc/passwd

# প্রথম ৩ লাইন দেখুন (সংক্ষিপ্ত)
head -3 /etc/passwd
```

**`-n` এর অর্থ:** "**n**umber of lines" — কতগুলো লাইন দেখাবে

### Real-Life Use Case:

> বড় CSV ফাইলের header (কলামের নাম) দেখতে:
>
> ```bash
> head -1 data.csv
> # name,email,phone,address
> ```

---

## 5️⃣ `tail` — ফাইলের শেষ দেখা

**কাজ:** ফাইলের **শেষ কিছু লাইন** দেখায় (default: ১০ লাইন)।

**মনে রাখুন:** "**Tail**" = "লেজ" — ফাইলের লেজের দিক দেখায়

```bash
# শেষ ১০ লাইন দেখুন
tail /etc/passwd

# শেষ ৫ লাইন দেখুন
tail -n 5 /etc/passwd

# শেষ ৩ লাইন
tail -3 /etc/passwd
```

### ⭐ `-f` Flag — Live Monitoring (সবচেয়ে গুরুত্বপূর্ণ!)

```bash
tail -f /var/log/syslog
```

**`-f` এর অর্থ:** "**f**ollow" — ফাইলে নতুন কিছু যোগ হলে **সাথে সাথে** দেখায়, বন্ধ না করা পর্যন্ত চলতে থাকে।

**বন্ধ করতে:** `Ctrl + C`

### Real-Life Use Case:

> 🔍 Server-এর log file real-time-এ দেখা — সমস্যা খুঁজে বের করা (troubleshooting):
>
> ```bash
> # System log দেখুন
> tail -f /var/log/syslog
>
> # Authentication log দেখুন (কে login করল)
> sudo tail -f /var/log/auth.log
> ```
>
> এটি Cybersecurity এবং System Administration-এ **খুবই গুরুত্বপূর্ণ**!

### head vs tail:

```
ফাইলের গঠন:
┌─────────────────────┐
│ Line 1              │ ← head দেখায়
│ Line 2              │ ← head দেখায়
│ Line 3              │ ← head দেখায়
│ ...                 │
│ ...                 │
│ Line 98             │ ← tail দেখায়
│ Line 99             │ ← tail দেখায়
│ Line 100            │ ← tail দেখায়
└─────────────────────┘
```

---

## 6️⃣ `echo` — টেক্সট প্রিন্ট করা

**কাজ:** Terminal-এ কিছু লেখা/প্রিন্ট করা।

**মনে রাখুন:** "**Echo**" = "প্রতিধ্বনি" — আপনি যা বলেন তাই ফিরিয়ে দেয়

```bash
# সাধারণ লেখা
echo "Hello, Linux!"
# Hello, Linux!

# Variable-এর মান দেখা
echo $HOME
# /home/the-king

echo $USER
# the-king

# গণনা করা
echo $((5 + 3))
# 8
```

### ফাইলে লেখা (Redirect দিয়ে):

```bash
# নতুন ফাইলে লিখুন
echo "আমার প্রথম নোট" > my-note.txt

# ফাইলের শেষে যোগ করুন
echo "দ্বিতীয় লাইন" >> my-note.txt

# দেখুন কী লেখা হয়েছে
cat my-note.txt
# আমার প্রথম নোট
# দ্বিতীয় লাইন
```

### `-e` Flag — Special Characters:

```bash
echo -e "প্রথম লাইন\nদ্বিতীয় লাইন\nতৃতীয় লাইন"
```

**আউটপুট:**

```
প্রথম লাইন
দ্বিতীয় লাইন
তৃতীয় লাইন
```

| Special Character | কাজ                  |
| ----------------- | -------------------- |
| `\n`              | নতুন লাইন (New line) |
| `\t`              | Tab space            |
| `\\`              | Backslash itself     |

---

## 7️⃣ `wc` — ফাইলের পরিসংখ্যান

**কাজ:** ফাইলে কতগুলো লাইন, শব্দ ও অক্ষর আছে গুণে দেখায়।

**মনে রাখুন:** "**W**ord **C**ount" = "শব্দ গণনা"

```bash
wc notes.txt
```

**আউটপুট:**

```
  4  12  89 notes.txt
```

**মানে:**

```
4 = লাইনের সংখ্যা
12 = শব্দের সংখ্যা
89 = অক্ষরের (character/byte) সংখ্যা
notes.txt = ফাইলের নাম
```

### নির্দিষ্ট তথ্য দেখা:

| Flag    | অর্থ                 | কাজ                 |
| ------- | -------------------- | ------------------- |
| `wc -l` | **l**ines            | শুধু লাইনের সংখ্যা  |
| `wc -w` | **w**ords            | শুধু শব্দের সংখ্যা  |
| `wc -c` | **c**haracters/bytes | শুধু অক্ষরের সংখ্যা |

```bash
# কতগুলো লাইন আছে?
wc -l /etc/passwd
# 42 /etc/passwd (আপনার সিস্টেমে ভিন্ন হতে পারে)

# এর মানে সিস্টেমে ৪২ জন user account আছে
```

### Real-Life Use Case:

> ```bash
> # আপনার code file-এ কত লাইন code আছে?
> wc -l script.py
>
> # একটি ফোল্ডারে কতগুলো ফাইল আছে?
> ls | wc -l
> ```

---

## 8️⃣ `file` — ফাইলের ধরন জানা

**কাজ:** ফাইলটি আসলে কী ধরনের তা বলে দেয় (extension নয়, আসল content দেখে বলে)।

```bash
file notes.txt
# notes.txt: UTF-8 Unicode text

file /usr/bin/ls
# /usr/bin/ls: ELF 64-bit LSB pie executable

file photo.jpg
# photo.jpg: JPEG image data
```

> 💡 **গুরুত্বপূর্ণ:** Linux-এ extension গুরুত্বপূর্ণ নয়। `file` কমান্ড ফাইলের **আসল content** পরীক্ষা করে বলে সেটি কী ধরনের।
>
> ```bash
> # একটি image file-এর extension .txt দিলেও...
> mv photo.jpg photo.txt
> file photo.txt
> # photo.txt: JPEG image data  ← এটি আসলে image!
> ```

---

## 9️⃣ `find` — ফাইল খোঁজা (শক্তিশালী সার্চ)

**কাজ:** নির্দিষ্ট শর্ত অনুযায়ী ফাইল ও ফোল্ডার খোঁজে।

**মনে রাখুন:** "**Find**" = "খুঁজে বের করো"

### Format:

```bash
find <কোথায়_খুঁজবে> <কী_শর্তে> <কী_খুঁজবে>
```

### নাম দিয়ে খোঁজা:

```bash
# Home directory-তে notes.txt খুঁজুন
find ~ -name "notes.txt"

# Case-insensitive (বড়/ছোট হাতের পার্থক্য নেই) খোঁজা
find ~ -iname "Notes.TXT"
```

### ধরন দিয়ে খোঁজা:

```bash
# শুধু ফাইল খুঁজুন
find ~ -type f -name "*.txt"

# শুধু ফোল্ডার খুঁজুন
find ~ -type d -name "projects"
```

| `-type` | অর্থ                    |
| ------- | ----------------------- |
| `f`     | **f**ile (ফাইল)         |
| `d`     | **d**irectory (ফোল্ডার) |

### আকার দিয়ে খোঁজা:

```bash
# ১০MB-এর বেশি বড় ফাইল খুঁজুন
find ~ -size +10M

# ১KB-এর কম ছোট ফাইল খুঁজুন
find ~ -size -1k

# ঠিক ৫MB-এর ফাইল
find ~ -size 5M
```

| চিহ্ন | একক       |
| ----- | --------- |
| `c`   | Bytes     |
| `k`   | Kilobytes |
| `M`   | Megabytes |
| `G`   | Gigabytes |

### সময় দিয়ে খোঁজা:

```bash
# গত ৭ দিনে পরিবর্তিত ফাইল
find ~ -mtime -7

# ৩০ দিনের বেশি পুরনো ফাইল
find ~ -mtime +30
```

**`-mtime`** = "**m**odification **time**" (পরিবর্তনের সময়)

### Real-Life Use Case:

> ```bash
> # সিস্টেমে সব .log ফাইল খুঁজুন
> sudo find /var/log -name "*.log"
>
> # ১০০MB-এর বেশি বড় ফাইল খুঁজুন (ডিস্ক space বের করতে)
> find / -size +100M 2>/dev/null
>
> # গত ২৪ ঘণ্টায় পরিবর্তিত ফাইল
> find ~ -mtime -1
> ```

---

## 🔟 `locate` — দ্রুত ফাইল খোঁজা

**কাজ:** ডাটাবেজ থেকে দ্রুত ফাইল খোঁজে (find-এর চেয়ে অনেক দ্রুত)।

### ইন্সটল করুন (প্রথমবার):

```bash
sudo apt install plocate
```

> 💡 `sudo` মানে "**S**uper **U**ser **Do**" — Admin/root হিসেবে কমান্ড চালায়। পরে বিস্তারিত শিখব।

### ডাটাবেজ আপডেট করুন:

```bash
sudo updatedb
```

### ব্যবহার:

```bash
# notes.txt খুঁজুন
locate notes.txt

# bashrc ফাইল খুঁজুন
locate bashrc
```

### find vs locate:

| বিষয়       | `find`                | `locate`                         |
| ----------- | --------------------- | -------------------------------- |
| গতি         | ধীর (real-time সার্চ) | খুব দ্রুত (database থেকে)        |
| নতুন ফাইল   | ✅ পায়               | ❌ database আপডেট না হলে পায় না |
| ফিল্টার     | অনেক option আছে       | সীমিত                            |
| কখন ব্যবহার | নির্দিষ্ট শর্তে খোঁজা | দ্রুত নাম দিয়ে খোঁজা            |

---

## 1️⃣1️⃣ `stat` — ফাইলের বিস্তারিত তথ্য

**কাজ:** ফাইলের সব বিস্তারিত তথ্য দেখায়।

```bash
stat notes.txt
```

**আউটপুট:**

```
  File: notes.txt
  Size: 89              Blocks: 8          IO Block: 4096   regular file
Device: 820h/2080d      Inode: 1234567     Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/the-king)  Gid: ( 1000/the-king)
Access: 2026-03-05 01:30:00.000000000 +0600
Modify: 2026-03-05 01:25:00.000000000 +0600
Change: 2026-03-05 01:25:00.000000000 +0600
 Birth: 2026-03-05 01:20:00.000000000 +0600
```

**গুরুত্বপূর্ণ তথ্য:**
| ফিল্ড | অর্থ |
|-------|------|
| Size | ফাইলের আকার (bytes) |
| Access (permission) | কে কী করতে পারবে |
| Uid | মালিকের নাম (Owner) |
| Access (time) | শেষ কবে পড়া হয়েছে |
| Modify | শেষ কবে content বদলানো হয়েছে |
| Birth | কবে তৈরি হয়েছে |

---

## 1️⃣2️⃣ `diff` — দুটি ফাইলের পার্থক্য দেখা

**কাজ:** দুটি ফাইলের মধ্যে কী কী পার্থক্য আছে দেখায়।

**মনে রাখুন:** "**Diff**erence" = "পার্থক্য"

```bash
# প্রথমে দুটি ফাইল তৈরি করুন
echo -e "Apple\nBanana\nCherry" > fruits1.txt
echo -e "Apple\nBlueberry\nCherry" > fruits2.txt

# পার্থক্য দেখুন
diff fruits1.txt fruits2.txt
```

**আউটপুট:**

```
2c2
< Banana
---
> Blueberry
```

**মানে:** দ্বিতীয় লাইনে `Banana` পরিবর্তিত হয়ে `Blueberry` হয়েছে।

### side-by-side তুলনা:

```bash
diff -y fruits1.txt fruits2.txt
```

**আউটপুট:**

```
Apple                    Apple
Banana                 | Blueberry
Cherry                   Cherry
```

> **Real-Life Use Case:** কোড বা config ফাইলে কী বদলেছে দেখতে `diff` ব্যবহার হয়। Git-ও পেছনে `diff` ব্যবহার করে!

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কমান্ড    | পুরো নাম    | কাজ                    | সবচেয়ে ভালো কখন?     |
| --------- | ----------- | ---------------------- | --------------------- |
| `cat`     | Concatenate | ফাইল পড়া/দেখানো       | ছোট ফাইল              |
| `less`    | Less        | পৃষ্ঠায় পৃষ্ঠায় পড়া | বড় ফাইল ✅           |
| `more`    | More        | পৃষ্ঠায় পৃষ্ঠায় পড়া | less ব্যবহার করুন     |
| `head`    | Head        | ফাইলের শুরু দেখা       | প্রথম কয়েক লাইন      |
| `tail`    | Tail        | ফাইলের শেষ দেখা        | Log file দেখা         |
| `tail -f` | Tail Follow | Live monitoring        | Real-time log ✅      |
| `echo`    | Echo        | টেক্সট প্রিন্ট/লেখা    | ফাইলে লেখা            |
| `wc`      | Word Count  | গণনা (লাইন/শব্দ/অক্ষর) | পরিসংখ্যান            |
| `file`    | File        | ফাইলের ধরন জানা        | অজানা ফাইল            |
| `find`    | Find        | ফাইল খোঁজা (শক্তিশালী) | শর্ত দিয়ে খোঁজা ✅   |
| `locate`  | Locate      | দ্রুত ফাইল খোঁজা       | দ্রুত নাম দিয়ে খোঁজা |
| `stat`    | Status      | বিস্তারিত তথ্য         | ফাইলের metadata       |
| `diff`    | Difference  | দুটি ফাইলের পার্থক্য   | তুলনা করা             |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: ফাইল তৈরি ও পড়া

```bash
# 1. Practice directory-তে যান (আগের section-এ তৈরি করেছিলেন)
cd ~/linux-practice

# 2. echo দিয়ে ফাইলে লিখুন
echo "আমি Linux শিখছি" > learning.txt
echo "এটি দ্বিতীয় লাইন" >> learning.txt
echo "এটি তৃতীয় লাইন" >> learning.txt

# 3. cat দিয়ে পড়ুন
cat learning.txt

# 4. line number সহ দেখুন
cat -n learning.txt

# 5. wc দিয়ে গুণুন
wc learning.txt
wc -l learning.txt
wc -w learning.txt
```

### অনুশীলন ২: System ফাইল পড়া

```bash
# 1. আপনার OS-এর তথ্য দেখুন
cat /etc/os-release

# 2. সিস্টেমের hostname দেখুন
cat /etc/hostname

# 3. passwd ফাইলের প্রথম ৫ লাইন
head -5 /etc/passwd

# 4. passwd ফাইলের শেষ ৫ লাইন
tail -5 /etc/passwd

# 5. passwd ফাইল less দিয়ে পড়ুন (q দিয়ে বেরোন)
less /etc/passwd

# 6. passwd ফাইলে কতগুলো লাইন (= কতগুলো user account)?
wc -l /etc/passwd
```

### অনুশীলন ৩: ফাইল খোঁজা

```bash
# 1. Home directory-তে সব .txt ফাইল খুঁজুন
find ~ -name "*.txt"

# 2. Home-তে সব directory খুঁজুন
find ~ -type d -maxdepth 2

# 3. ১MB-এর বেশি ফাইল খুঁজুন
find ~ -size +1M

# 4. আজকে পরিবর্তিত ফাইল খুঁজুন
find ~ -mtime 0
```

### অনুশীলন ৪: diff ব্যবহার

```bash
# 1. দুটি ফাইল তৈরি করুন
echo -e "Red\nGreen\nBlue" > colors1.txt
echo -e "Red\nYellow\nBlue\nPurple" > colors2.txt

# 2. পার্থক্য দেখুন
diff colors1.txt colors2.txt

# 3. পাশাপাশি দেখুন
diff -y colors1.txt colors2.txt
```

### অনুশীলন ৫: চ্যালেঞ্জ

echo ও output redirection ব্যবহার করে একটি ছোট "poem.txt" ফাইল তৈরি করুন যাতে ৫টি লাইন থাকবে। তারপর:

1. `cat` দিয়ে পড়ুন
2. `head -2` দিয়ে প্রথম ২ লাইন দেখুন
3. `tail -2` দিয়ে শেষ ২ লাইন দেখুন
4. `wc` দিয়ে গুণুন
5. `file` দিয়ে ফাইলের ধরন দেখুন

---

## 🎉 Phase 1 Complete!

অভিনন্দন! 🎊 আপনি **Phase 1: Linux ভিত্তি (Foundation)** সম্পূর্ণ করেছেন!

### এই Phase-এ যা শিখলেন:

- ✅ Linux কী, ইতিহাস, Kernel, Distribution
- ✅ Terminal, Shell, Prompt, File System Structure
- ✅ File ও Directory তৈরি, কপি, মুভ, মুছা
- ✅ ফাইলের content দেখা, খোঁজা, তুলনা করা

### পরবর্তী Phase:

**[Phase 2: Permission, User ও Package Management →](../phase-02/section-05.md)**

Phase 2-তে শিখবেন:

- File Permissions — কে কী করতে পারবে
- User ও Group Management
- Package Management (apt) — সফটওয়্যার ইন্সটল
- Text Editors (nano, vim)

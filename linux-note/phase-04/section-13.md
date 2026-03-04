# 📖 Section 13: I/O Redirection ও Piping

---

## 🎯 এই Section-এ যা শিখবেন

- Standard Input, Output, Error কী
- Output Redirection (`>`, `>>`)
- Input Redirection (`<`)
- Error Redirection (`2>`)
- Pipe (`|`) — কমান্ড জোড়া লাগানো
- `tee` — Output দেখাও + ফাইলে সেভ করো
- `/dev/null` — Output ফেলে দেওয়া
- কমান্ড Chaining (`&&`, `||`, `;`)

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড            | Ubuntu 24 LTS-এ  | মন্তব্য                    |
| ----------------- | :--------------: | -------------------------- | ------------------------- |
| `>`, `>>`, `<`, ` |        `         | ✅ Pre-installed           | Shell-এর built-in feature |
| `tee`             | ✅ Pre-installed | Output দুই জায়গায় পাঠানো |
| `xargs`           | ✅ Pre-installed | Pipe থেকে argument তৈরি    |
| `sort`            | ✅ Pre-installed | Data সাজানো                |
| `uniq`            | ✅ Pre-installed | ডুপ্লিকেট বাদ দেওয়া       |
| `cut`             | ✅ Pre-installed | কলাম কেটে নেওয়া           |
| `tr`              | ✅ Pre-installed | Character বদলানো           |
| `wc`              | ✅ Pre-installed | গণনা করা                   |

> ✅ এই section-এর **সব কমান্ড** Ubuntu 24 LTS-এ **আগে থেকেই ইন্সটল করা আছে**।

---

## 📺 Standard Streams — তিনটি ধারা

Linux-এ প্রতিটি কমান্ডের **তিনটি ধারা** (stream) থাকে:

```
                    ┌──────────────┐
  stdin (0) ──────▶│              │──────▶ stdout (1)
  (কীবোর্ড)        │    কমান্ড     │
                    │              │──────▶ stderr (2)
                    └──────────────┘        (Error)
```

| Stream     | নম্বর | নাম             | কোথা থেকে/কোথায় | উদাহরণ            |
| ---------- | ----- | --------------- | ---------------- | ----------------- |
| **stdin**  | 0     | Standard Input  | কীবোর্ড → কমান্ড | আপনি যা টাইপ করেন |
| **stdout** | 1     | Standard Output | কমান্ড → স্ক্রিন | সফল ফলাফল         |
| **stderr** | 2     | Standard Error  | কমান্ড → স্ক্রিন | Error message     |

### সহজ তুলনা:

```
stdin  = আপনার মুখ (কথা বলেন = input দেন)
stdout = স্পিকার (সঠিক উত্তর শোনায়)
stderr = অ্যালার্ম (সমস্যা হলে বাজে)
```

---

## 1️⃣ Output Redirection — `>` এবং `>>`

### `>` — ফাইলে লিখুন (Overwrite)

```bash
# ls-এর output ফাইলে সেভ করুন (স্ক্রিনে দেখাবে না)
ls -la > file-list.txt

# দেখুন
cat file-list.txt
```

### `>>` — ফাইলের শেষে যোগ করুন (Append)

```bash
# প্রথম লাইন
echo "প্রথম লাইন" > notes.txt

# আরও যোগ করুন (আগেরটা থাকবে)
echo "দ্বিতীয় লাইন" >> notes.txt
echo "তৃতীয় লাইন" >> notes.txt

cat notes.txt
# প্রথম লাইন
# দ্বিতীয় লাইন
# তৃতীয় লাইন
```

### `>` vs `>>` পার্থক্য:

| Operator | কাজ       | ফাইল থাকলে                | ফাইল না থাকলে      |
| -------- | --------- | ------------------------- | ------------------ |
| `>`      | Overwrite | আগেরটা **মুছে** নতুন লেখে | নতুন ফাইল তৈরি করে |
| `>>`     | Append    | শেষে **যোগ** করে          | নতুন ফাইল তৈরি করে |

> ⚠️ **সতর্কতা:** `>` ভুলে ব্যবহার করলে গুরুত্বপূর্ণ ফাইলের ডেটা মুছে যেতে পারে!

---

## 2️⃣ Error Redirection — `2>`

```bash
# Error একটি ফাইলে সেভ করুন
ls /nonexistent 2> errors.txt

# Error দেখুন
cat errors.txt
# ls: cannot access '/nonexistent': No such file or directory
```

### stdout ও stderr আলাদা করা:

```bash
# stdout → output.txt, stderr → error.txt
find / -name "*.conf" > output.txt 2> error.txt

# stdout ও stderr দুটোই একই ফাইলে
find / -name "*.conf" > all.txt 2>&1

# সংক্ষিপ্ত (bash-এ)
find / -name "*.conf" &> all.txt
```

| Redirect  | কাজ                            |
| --------- | ------------------------------ |
| `> file`  | stdout → ফাইলে                 |
| `2> file` | stderr → ফাইলে                 |
| `&> file` | stdout + stderr → ফাইলে        |
| `2>&1`    | stderr কে stdout-এর সাথে মিলাও |

---

## 3️⃣ Input Redirection — `<`

```bash
# ফাইল থেকে input নিন
wc -l < /etc/passwd
# 42 (শুধু সংখ্যা, ফাইলের নাম ছাড়া)

# তুলনা:
wc -l /etc/passwd
# 42 /etc/passwd (ফাইলের নাম সহ)
```

### Here Document — `<<`

```bash
cat << EOF
এটি প্রথম লাইন
এটি দ্বিতীয় লাইন
এটি তৃতীয় লাইন
EOF
```

**`<< EOF ... EOF`** = শুরু ও শেষ চিহ্ন দিয়ে একাধিক লাইন input দেওয়া। `EOF` এর জায়গায় যেকোনো শব্দ ব্যবহার করা যায়।

---

## 4️⃣ `/dev/null` — Output ফেলে দেওয়া

**`/dev/null`** হলো Linux-এর **"ব্ল্যাক হোল"** — যা কিছু এখানে পাঠানো হয়, সব অদৃশ্য হয়ে যায়!

```bash
# Error message দেখতে চান না? /dev/null-এ পাঠান
find / -name "*.conf" 2>/dev/null
# শুধু সফল ফলাফল দেখাবে, error দেখাবে না

# সব output চুপ করান (stdout + stderr)
command &>/dev/null
```

### Real-Life Use Case:

> ```bash
> # Permission denied error লুকান
> find / -name "secret.txt" 2>/dev/null
>
> # Script-এ output না দেখিয়ে শুধু কাজ করান
> apt update &>/dev/null
> ```

---

## 5️⃣ Pipe `|` — Linux-এর সবচেয়ে শক্তিশালী Feature! ⚡

**Pipe (`|`)** একটি কমান্ডের **output** কে অন্য কমান্ডের **input** হিসেবে পাঠায়।

```
কমান্ড ১ ──stdout──▶ | ──stdin──▶ কমান্ড ২
```

### সহজ উদাহরণ:

```bash
# ধাপ ধাপ:
ls -la          # সব ফাইল দেখায়
ls -la | wc -l  # কতগুলো ফাইল আছে গুণে দেখায়
```

**কী ঘটছে:**

```
ls -la → output (ফাইল তালিকা) → pipe → wc -l → input হিসেবে নিয়ে → লাইন গুণে
```

### আরও উদাহরণ:

```bash
# passwd ফাইলে "bash" কতবার আছে?
cat /etc/passwd | grep bash

# চলমান process-এ "firefox" খুঁজুন
ps aux | grep firefox

# সবচেয়ে বড় ১০টি ফাইল
du -sh ~/* 2>/dev/null | sort -rh | head -10

# ইন্সটল করা packages কতগুলো
dpkg --list | wc -l

# সবচেয়ে বেশি RAM ব্যবহারকারী ৫টি process
ps aux --sort=-%mem | head -6
```

### একাধিক Pipe (Chain):

```bash
# /etc/passwd থেকে → শুধু username নিন → সাজান → প্রথম ৫টি দেখান
cat /etc/passwd | cut -d: -f1 | sort | head -5
```

**ব্যাখ্যা:**

```
cat /etc/passwd    → ফাইল পড়ো
    | cut -d: -f1  → ":" দিয়ে ভাগ করে প্রথম ফিল্ড নাও (username)
    | sort          → বর্ণানুক্রমে সাজাও
    | head -5       → প্রথম ৫টি দেখাও
```

---

## 6️⃣ Pipe-এর সাথে ব্যবহৃত গুরুত্বপূর্ণ কমান্ড

### `sort` — সাজানো

```bash
# বর্ণানুক্রমে সাজান
cat names.txt | sort

# উল্টো সাজান
cat names.txt | sort -r

# সংখ্যা অনুযায়ী সাজান
du -sh ~/* | sort -rh
```

| Flag   | অর্থ                        |
| ------ | --------------------------- |
| `-r`   | **r**everse (উল্টো)         |
| `-n`   | **n**umeric (সংখ্যা হিসেবে) |
| `-h`   | **h**uman readable (1K, 2M) |
| `-u`   | **u**nique (ডুপ্লিকেট বাদ)  |
| `-k 2` | ২য় কলাম অনুযায়ী           |

### `uniq` — ডুপ্লিকেট বাদ দেওয়া

```bash
# ডুপ্লিকেট বাদ দিন (আগে sort করতে হবে!)
sort names.txt | uniq

# কতবার আছে দেখান
sort names.txt | uniq -c

# শুধু ডুপ্লিকেট দেখান
sort names.txt | uniq -d
```

> ⚠️ **গুরুত্বপূর্ণ:** `uniq` শুধু পরপর থাকা ডুপ্লিকেট বাদ দেয়। তাই **আগে `sort` করতে হবে!**

### `cut` — কলাম কেটে নেওয়া

```bash
# ":" দিয়ে ভাগ করে প্রথম ফিল্ড নিন (username)
cut -d: -f1 /etc/passwd

# ":" দিয়ে ভাগ করে ১ম ও ৭ম ফিল্ড (username ও shell)
cut -d: -f1,7 /etc/passwd

# CSV ফাইল থেকে ২য় কলাম
cut -d, -f2 data.csv
```

| Flag | অর্থ                         |
| ---- | ---------------------------- |
| `-d` | **d**elimiter (বিভাজক চিহ্ন) |
| `-f` | **f**ield (কোন ফিল্ড/কলাম)   |
| `-c` | **c**haracter position       |

### `tr` — Character বদলানো/মুছা

```bash
# ছোট হাতের অক্ষরকে বড় হাতের করুন
echo "hello world" | tr 'a-z' 'A-Z'
# HELLO WORLD

# বড় হাতের থেকে ছোট
echo "HELLO" | tr 'A-Z' 'a-z'
# hello

# space কে newline দিয়ে বদলান
echo "one two three" | tr ' ' '\n'
# one
# two
# three

# নির্দিষ্ট character মুছে ফেলুন
echo "hello 123 world" | tr -d '0-9'
# hello  world
```

**`tr`** = "**Tr**anslate" = "অনুবাদ/রূপান্তর"

### `tee` — Output দুই জায়গায়

```bash
# Output স্ক্রিনেও দেখান + ফাইলেও সেভ করুন
ls -la | tee file-list.txt

# Append mode
ls -la | tee -a file-list.txt
```

**`tee`** এর কাজ:

```
কমান্ড ──▶ tee ──▶ স্ক্রিনে দেখাও (stdout)
              │
              └──▶ ফাইলে সেভ করো
```

> 💡 "Tee" নামটি T-আকৃতির পাইপ থেকে এসেছে — পানি দুই দিকে যায়!

### `xargs` — Pipe থেকে Argument তৈরি

```bash
# সব .txt ফাইল খুঁজে মুছুন
find . -name "*.txt" | xargs rm

# সব .log ফাইল খুঁজে wordcount দিন
find /var/log -name "*.log" | xargs wc -l
```

**`xargs`** pipe থেকে আসা output-কে **argument** হিসেবে পরবর্তী কমান্ডে পাঠায়।

---

## 7️⃣ কমান্ড Chaining — `&&`, `||`, `;`

| Operator | কাজ        | কখন পরেরটি চলবে                 |
| -------- | ---------- | ------------------------------- |
| `&&`     | AND        | প্রথমটি **সফল হলে** তবেই        |
| `\|\|`   | OR         | প্রথমটি **ব্যর্থ হলে** তবেই     |
| `;`      | Sequential | **সবসময়** (সফল/ব্যর্থ যাই হোক) |

```bash
# AND — দুটোই সফল হতে হবে
sudo apt update && sudo apt upgrade -y
# update সফল হলেই upgrade চলবে

# OR — প্রথমটি ব্যর্থ হলে দ্বিতীয়টি চলবে
cd /tmp/test || mkdir /tmp/test
# folder থাকলে cd করবে, না থাকলে তৈরি করবে

# Sequential — পরপর চলবে
echo "শুরু" ; sleep 2 ; echo "শেষ"
# দুটোই চলবে
```

### Real-Life Use Case:

> ```bash
> # ফোল্ডার তৈরি করো, সেখানে যাও, ফাইল তৈরি করো
> mkdir -p ~/project && cd ~/project && touch README.md
>
> # আপডেট + আপগ্রেড + পরিষ্কার — একলাইনে
> sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
> ```

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| Operator/কমান্ড | কাজ                           | উদাহরণ                 |
| --------------- | ----------------------------- | ---------------------- |
| `>`             | Output → ফাইলে (overwrite)    | `ls > list.txt`        |
| `>>`            | Output → ফাইলের শেষে (append) | `echo "hi" >> log.txt` |
| `<`             | ফাইল → Input                  | `wc -l < file.txt`     |
| `2>`            | Error → ফাইলে                 | `cmd 2> err.txt`       |
| `&>`            | সব → ফাইলে                    | `cmd &> all.txt`       |
| `\|`            | Output → পরের কমান্ডের Input  | `ls \| wc -l`          |
| `tee`           | Output দুই জায়গায়           | `ls \| tee file.txt`   |
| `sort`          | সাজানো                        | `sort names.txt`       |
| `uniq`          | ডুপ্লিকেট বাদ                 | `sort \| uniq`         |
| `cut`           | কলাম নেওয়া                   | `cut -d: -f1`          |
| `tr`            | Character বদলানো              | `tr 'a-z' 'A-Z'`       |
| `xargs`         | Argument তৈরি                 | `find \| xargs rm`     |
| `&&`            | AND chain                     | `cmd1 && cmd2`         |
| `\|\|`          | OR chain                      | `cmd1 \|\| cmd2`       |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: Redirection

```bash
# 1. Home-এর ফাইল তালিকা একটি ফাইলে সেভ করুন
ls -la ~ > ~/linux-practice/home-files.txt

# 2. দেখুন
cat ~/linux-practice/home-files.txt

# 3. আরও তথ্য যোগ করুন
echo "---" >> ~/linux-practice/home-files.txt
date >> ~/linux-practice/home-files.txt

# 4. Error redirect করুন
ls /nonexistent 2> ~/linux-practice/errors.txt
cat ~/linux-practice/errors.txt
```

### অনুশীলন ২: Pipe Practice

```bash
# 1. আপনার system-এ কতগুলো user আছে?
cat /etc/passwd | wc -l

# 2. কোন কোন user bash shell ব্যবহার করে?
cat /etc/passwd | grep bash

# 3. ইন্সটল করা packages-এ "python" সম্পর্কিত কী আছে?
dpkg --list | grep python

# 4. সবচেয়ে বেশি RAM ব্যবহারকারী ৫টি process
ps aux --sort=-%mem | head -6

# 5. /etc ফোল্ডারে কতগুলো .conf ফাইল আছে?
find /etc -name "*.conf" 2>/dev/null | wc -l
```

### অনুশীলন ৩: sort, cut, uniq

```bash
# 1. সব username সাজিয়ে দেখুন
cut -d: -f1 /etc/passwd | sort

# 2. সব shell-এর তালিকা (ডুপ্লিকেট ছাড়া)
cut -d: -f7 /etc/passwd | sort | uniq

# 3. কোন shell কতবার ব্যবহৃত?
cut -d: -f7 /etc/passwd | sort | uniq -c | sort -rn
```

### অনুশীলন ৪: চ্যালেঞ্জ

একটি কমান্ডে নিচের কাজ করুন:

1. `/var/log` এ সব `.log` ফাইল খুঁজুন
2. Error message লুকান
3. ফলাফল সাজান
4. ফাইলে সেভ করুন **এবং** স্ক্রিনেও দেখান

<details>
<summary>💡 উত্তর দেখুন</summary>

```bash
find /var/log -name "*.log" 2>/dev/null | sort | tee ~/linux-practice/log-files.txt
```

</details>

---

## ➡️ পরবর্তী Section

[Section 14: grep, sed, awk — Advanced Text Processing →](section-14.md)

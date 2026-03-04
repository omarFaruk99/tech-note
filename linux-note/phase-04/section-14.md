# 📖 Section 14: grep, sed, awk — Advanced Text Processing

---

## 🎯 এই Section-এ যা শিখবেন

- `grep` — টেক্সটে নির্দিষ্ট pattern খোঁজা
- Regular Expressions (regex) — খোঁজার pattern
- `sed` — Stream Editor — টেক্সট বদলানো
- `awk` — ডেটা প্রক্রিয়াকরণ ও রিপোর্ট তৈরি

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড  | Ubuntu 24 LTS-এ  | মন্তব্য                            |
| ------- | :--------------: | ---------------------------------- |
| `grep`  | ✅ Pre-installed | Pattern দিয়ে খোঁজা                |
| `egrep` | ✅ Pre-installed | Extended regex (`grep -E` এর সমান) |
| `fgrep` | ✅ Pre-installed | Fixed string (`grep -F` এর সমান)   |
| `sed`   | ✅ Pre-installed | Stream editor                      |
| `awk`   | ✅ Pre-installed | Text processing tool (gawk)        |

> ✅ এই section-এর **সব কমান্ড** Ubuntu 24 LTS-এ **আগে থেকেই ইন্সটল করা আছে**।

---

## 1️⃣ `grep` — Pattern খোঁজা

**grep** হলো Linux-এর **সবচেয়ে বেশি ব্যবহৃত** text processing কমান্ড।

**মনে রাখুন:** "**G**lobal **R**egular **E**xpression **P**rint" = "সর্বত্র regex অনুযায়ী খুঁজে দেখাও"

### মৌলিক ব্যবহার:

```bash
# ফাইলে "bash" শব্দটি খুঁজুন
grep "bash" /etc/passwd

# case-insensitive (বড়/ছোট হাতে পার্থক্য নেই)
grep -i "BASH" /etc/passwd

# উল্টো খোঁজা (যেখানে নেই সেগুলো দেখান)
grep -v "nologin" /etc/passwd
```

### গুরুত্বপূর্ণ Flags:

| Flag      | অর্থ               | কাজ                         |
| --------- | ------------------ | --------------------------- |
| `-i`      | **i**gnore case    | বড়/ছোট হাতে পার্থক্য নেই   |
| `-v`      | in**v**ert         | যেখানে **নেই** সেগুলো দেখাও |
| `-n`      | line **n**umber    | লাইন নম্বর সহ দেখাও         |
| `-c`      | **c**ount          | কতবার পাওয়া গেছে গণনা করো  |
| `-l`      | **l**ist files     | কোন কোন ফাইলে পাওয়া গেছে   |
| `-r`      | **r**ecursive      | ফোল্ডারের ভিতরেও খোঁজো      |
| `-w`      | **w**hole word     | পুরো শব্দ মিলতে হবে         |
| `-A 3`    | **A**fter          | পরের ৩ লাইনও দেখাও          |
| `-B 3`    | **B**efore         | আগের ৩ লাইনও দেখাও          |
| `-C 3`    | **C**ontext        | আগে-পরে ৩ লাইন দেখাও        |
| `--color` | রঙিন               | মিলে যাওয়া অংশ রঙিন করো    |
| `-E`      | **E**xtended regex | Extended regex ব্যবহার করো  |

### ব্যবহারিক উদাহরণ:

```bash
# ফাইলে কতবার "error" শব্দটি আছে?
grep -c "error" /var/log/syslog

# কোন কোন ফাইলে "password" আছে?
grep -rl "password" /etc/ 2>/dev/null

# "root" শব্দটি লাইন নম্বর সহ
grep -n "root" /etc/passwd

# "error" এর আগে-পরে ২ লাইন দেখান
grep -C 2 "error" /var/log/syslog

# ফোল্ডারের সব ফাইলে খুঁজুন
grep -r "TODO" ~/projects/
```

### Pipe-এর সাথে grep:

```bash
# চলমান process-এ খুঁজুন
ps aux | grep firefox

# ইন্সটল করা package-এ খুঁজুন
dpkg --list | grep python

# history-তে খুঁজুন
history | grep "apt install"

# কমান্ড output ফিল্টার
dmesg | grep -i "usb"
```

---

## 2️⃣ Regular Expressions (Regex) — Pattern ভাষা

Regex হলো **pattern তৈরির ভাষা** — grep, sed, awk সবাই এটি ব্যবহার করে।

### মৌলিক Regex:

| Pattern | অর্থ                                     | উদাহরণ    | মিলবে                 |
| ------- | ---------------------------------------- | --------- | --------------------- |
| `.`     | যেকোনো **একটি** character                | `h.t`     | hat, hit, hot         |
| `*`     | আগের character **শূন্য বা তার বেশি** বার | `ab*c`    | ac, abc, abbc         |
| `+`     | আগের character **এক বা তার বেশি** বার    | `ab+c`    | abc, abbc (ac নয়)    |
| `?`     | আগের character **শূন্য বা এক** বার       | `colou?r` | color, colour         |
| `^`     | লাইনের **শুরু**                          | `^Hello`  | "Hello..." দিয়ে শুরু |
| `$`     | লাইনের **শেষ**                           | `end$`    | "...end" দিয়ে শেষ    |
| `[]`    | বন্ধনীর যেকোনো **একটি**                  | `[abc]`   | a, b, বা c            |
| `[^]`   | বন্ধনীর **বাইরে**                        | `[^0-9]`  | সংখ্যা ছাড়া সব       |
| `\d`    | যেকোনো সংখ্যা                            | `\d+`     | 123, 45               |
| `\w`    | Letter, digit, underscore                | `\w+`     | hello, abc_123        |
| `\s`    | Whitespace (space, tab)                  | —         | —                     |

### grep-এ Regex ব্যবহার:

```bash
# "root" দিয়ে শুরু হওয়া লাইন
grep "^root" /etc/passwd

# "bash" দিয়ে শেষ হওয়া লাইন
grep "bash$" /etc/passwd

# তিন অক্ষরের শব্দ যা "c" দিয়ে শুরু এবং "t" দিয়ে শেষ
grep "c.t" /etc/passwd

# IP address pattern
grep -E "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" /etc/hosts

# email pattern
grep -E "[a-zA-Z]+@[a-zA-Z]+\.[a-z]+" file.txt
```

> 💡 `-E` flag দিলে Extended Regex ব্যবহার করা যায় (`+`, `?`, `|`, `()` কাজ করে)

---

## 3️⃣ `sed` — Stream Editor

**sed** হলো **non-interactive text editor** — ফাইল না খুলেই কমান্ড দিয়ে Edit করা যায়!

**মনে রাখুন:** "**S**tream **Ed**itor" = "ধারা সম্পাদক"

### Format:

```bash
sed 's/পুরনো/নতুন/' ফাইল
```

`s` = **s**ubstitute (প্রতিস্থাপন)

### মৌলিক Find ও Replace:

```bash
# প্রথম match বদলান (প্রতি লাইনে)
sed 's/hello/hi/' file.txt

# সব match বদলান (g = global)
sed 's/hello/hi/g' file.txt

# case-insensitive replace
sed 's/hello/hi/gi' file.txt

# আসল ফাইলেই পরিবর্তন করুন (-i)
sed -i 's/hello/hi/g' file.txt
```

| Flag             | অর্থ                                    |
| ---------------- | --------------------------------------- |
| `g`              | **g**lobal — সব match বদলাও             |
| `i` (pattern-এ)  | case **i**nsensitive                    |
| `-i` (command-এ) | **i**n-place — ফাইলেই পরিবর্তন          |
| `-n`             | output দেখাও না (p এর সাথে ব্যবহার হয়) |

### নির্দিষ্ট লাইনে কাজ:

```bash
# শুধু ৩য় লাইনে বদলান
sed '3s/old/new/' file.txt

# ২-৫ নম্বর লাইনে বদলান
sed '2,5s/old/new/g' file.txt

# শেষ লাইনে বদলান
sed '$s/old/new/' file.txt
```

### লাইন মুছে ফেলা:

```bash
# ৩য় লাইন মুছুন
sed '3d' file.txt

# ২-৫ নম্বর লাইন মুছুন
sed '2,5d' file.txt

# "comment" আছে এমন লাইন মুছুন
sed '/comment/d' file.txt

# খালি লাইন মুছুন
sed '/^$/d' file.txt
```

### লাইন যোগ করা:

```bash
# ৩য় লাইনের পরে নতুন লাইন যোগ
sed '3a\এটি নতুন লাইন' file.txt

# ৩য় লাইনের আগে নতুন লাইন যোগ
sed '3i\এটি নতুন লাইন' file.txt
```

### নির্দিষ্ট লাইন দেখা:

```bash
# শুধু ৫ম লাইন দেখান
sed -n '5p' file.txt

# ২-৫ নম্বর লাইন দেখান
sed -n '2,5p' file.txt

# "root" আছে এমন লাইন দেখান
sed -n '/root/p' /etc/passwd
```

### Real-Life Use Case:

> ```bash
> # Config ফাইলে port বদলান
> sudo sed -i 's/Port 22/Port 2222/' /etc/ssh/sshd_config
>
> # সব comment (#) লাইন মুছুন
> sed '/^#/d' config.conf
>
> # CSV ফাইলে comma কে tab দিয়ে বদলান
> sed 's/,/\t/g' data.csv
> ```

---

## 4️⃣ `awk` — ডেটা প্রক্রিয়াকরণ

**awk** হলো একটি **programming language** যেটি structured text (কলাম-ভিত্তিক ডেটা) প্রক্রিয়াকরণে অতুলনীয়।

**নাম:** তিন স্রষ্টার নামের আদ্যক্ষর — **A**ho, **W**einberger, **K**ernighan

### মৌলিক Format:

```bash
awk '{action}' file
awk '/pattern/ {action}' file
```

### কলাম নেওয়া (সবচেয়ে বেশি ব্যবহার):

`awk` স্বয়ংক্রিয়ভাবে প্রতিটি লাইনকে **কলামে ভাগ** করে:

- `$0` = পুরো লাইন
- `$1` = প্রথম কলাম
- `$2` = দ্বিতীয় কলাম
- `$NF` = শেষ কলাম
- `NR` = লাইন নম্বর

```bash
# প্রথম কলাম দেখান
awk '{print $1}' file.txt

# প্রথম ও তৃতীয় কলাম
awk '{print $1, $3}' file.txt

# শেষ কলাম
awk '{print $NF}' file.txt
```

### Delimiter (বিভাজক) নির্ধারণ:

```bash
# ":" দিয়ে ভাগ করুন (/etc/passwd এর জন্য)
awk -F: '{print $1}' /etc/passwd

# "," দিয়ে ভাগ করুন (CSV)
awk -F, '{print $2}' data.csv
```

### Pattern Matching:

```bash
# "bash" আছে এমন লাইনের username দেখান
awk -F: '/bash/ {print $1}' /etc/passwd

# UID 1000-এর বেশি user দেখান
awk -F: '$3 >= 1000 {print $1, $3}' /etc/passwd
```

### গণনা ও যোগ:

```bash
# মোট লাইন গণনা
awk 'END {print NR}' /etc/passwd

# ফাইল সাইজের যোগফল
ls -l | awk '{total += $5} END {print "Total:", total, "bytes"}'

# গড় বের করা
awk '{sum += $1; count++} END {print "Average:", sum/count}' numbers.txt
```

### Formatted Output:

```bash
# সুন্দরভাবে সাজিয়ে দেখান
awk -F: '{printf "%-15s %s\n", $1, $7}' /etc/passwd
# root            /bin/bash
# daemon          /usr/sbin/nologin
# the-king        /bin/bash
```

### Real-Life Use Case:

> ```bash
> # সবচেয়ে বেশি RAM ব্যবহারকারী process (%MEM ও command)
> ps aux | awk '{print $4, $11}' | sort -rn | head -10
>
> # Disk usage শতকরা হার ৮০%-এর বেশি হলে warning
> df -h | awk '$5 > 80 {print "WARNING:", $6, "is", $5, "full!"}'
>
> # Log ফাইল থেকে IP address বের করা
> awk '{print $1}' /var/log/apache2/access.log | sort | uniq -c | sort -rn | head
> ```

---

## ⚖️ grep vs sed vs awk — কখন কোনটি?

| কাজ                   | সেরা টুল | উদাহরণ                           |
| --------------------- | -------- | -------------------------------- |
| **কিছু খুঁজতে** চান   | `grep`   | `grep "error" log.txt`           |
| **বদলাতে** চান        | `sed`    | `sed 's/old/new/g' file`         |
| **কলাম** নিয়ে কাজ    | `awk`    | `awk '{print $2}' file`          |
| **গণনা/যোগ** করতে চান | `awk`    | `awk '{sum+=$1} END{print sum}'` |
| **লাইন মুছতে** চান    | `sed`    | `sed '/pattern/d' file`          |
| **ফিল্টার** করতে চান  | `grep`   | `ps aux \| grep python`          |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: grep

```bash
# 1. /etc/passwd-এ আপনার username খুঁজুন
grep $USER /etc/passwd

# 2. কোন কোন user bash ব্যবহার করে?
grep "bash$" /etc/passwd

# 3. /etc/ ফোল্ডারে "network" শব্দটি কোন ফাইলে আছে?
grep -rl "network" /etc/ 2>/dev/null

# 4. syslog-এ আজকের error কতগুলো?
grep -c -i "error" /var/log/syslog 2>/dev/null
```

### অনুশীলন ২: sed

```bash
# 1. একটি ফাইল তৈরি করুন
echo -e "Hello World\nhello linux\nHELLO BASH" > ~/linux-practice/sed-test.txt

# 2. "Hello" কে "Hi" দিয়ে বদলান
sed 's/Hello/Hi/' ~/linux-practice/sed-test.txt

# 3. Case-insensitive বদলান
sed 's/hello/Hi/gi' ~/linux-practice/sed-test.txt

# 4. ২য় লাইন মুছুন
sed '2d' ~/linux-practice/sed-test.txt
```

### অনুশীলন ৩: awk

```bash
# 1. সব username দেখান
awk -F: '{print $1}' /etc/passwd

# 2. Username ও Shell দেখান
awk -F: '{print $1, "→", $7}' /etc/passwd

# 3. UID ১০০০+ user দেখান
awk -F: '$3 >= 1000 {print $1, "(UID:"$3")"}' /etc/passwd

# 4. মোট কতজন user?
awk 'END {print "Total users:", NR}' /etc/passwd
```

---

## ➡️ পরবর্তী Section

[Section 15: Shell Scripting Basics →](section-15.md)

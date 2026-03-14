# 📖 Section 15: Shell Scripting Basics

---

## 🎯 এই Section-এ যা শিখবেন

- Shell Script কী ও কেন দরকার
- প্রথম script লেখা ও চালানো
- Variables (চলক)
- User Input নেওয়া
- Conditional Statements (if/else)
- Loops (for, while)
- Functions (ফাংশন)
- Script-এ Argument পাঠানো

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড       |          Ubuntu 24 LTS-এ          | মন্তব্য                                       |
| ------------ | :-------------------------------: | --------------------------------------------- |
| `bash`       |         ✅ Pre-installed          | Script চালানোর shell                          |
| `chmod`      |         ✅ Pre-installed          | Script-কে executable করা                      |
| `read`       | ✅ Pre-installed (Shell built-in) | User input নেওয়া                             |
| `test` / `[` | ✅ Pre-installed (Shell built-in) | শর্ত পরীক্ষা                                  |
| `shellcheck` |        ❌ ইন্সটল করতে হবে         | `sudo apt install shellcheck` (script linter) |

---

## 📜 Shell Script কী?

**Shell Script** হলো একাধিক কমান্ডের সমষ্টি একটি ফাইলে — একবার চালালে **সব কমান্ড পরপর স্বয়ংক্রিয়ভাবে** চলে।

### সহজ উদাহরণ:

প্রতিদিন আপনি এই কাজগুলো করেন:

```bash
sudo apt update
sudo apt upgrade -y
sudo apt autoremove -y
echo "আপডেট সম্পন্ন!"
```

Script-এ একবার লিখে রাখলে, প্রতিদিন শুধু **একটি কমান্ডে** সব হয়ে যাবে:

```bash
./update.sh
```

---

## 1️⃣ প্রথম Script

### ধাপ ১: ফাইল তৈরি

```bash
nano ~/linux-practice/hello.sh
```

### ধাপ ২: Script লিখুন

```bash
#!/bin/bash
# এটি আমার প্রথম shell script
# Author: the-king
# Date: 2026-03-05

echo "🐧 স্বাগতম! আমি একটি Shell Script!"
echo "আজকের তারিখ: $(date)"
echo "আপনার নাম: $USER"
echo "আপনি আছেন: $(pwd)"
echo "আপনার কম্পিউটারের নাম: $(hostname)"
```

### ধাপ ৩: Executable করুন ও চালান

```bash
chmod +x ~/linux-practice/hello.sh
~/linux-practice/hello.sh
```

### Shebang (#!) কী?

```bash
#!/bin/bash
```

এই প্রথম লাইনকে **"Shebang"** বলে (Hash `#` + Bang `!`)। এটি বলে দেয় কোন **interpreter** দিয়ে script চলবে।

| Shebang               | কিসের script                            |
| --------------------- | --------------------------------------- |
| `#!/bin/bash`         | Bash script (সবচেয়ে বেশি ব্যবহৃত)      |
| `#!/bin/sh`           | POSIX Shell script                      |
| `#!/usr/bin/python3`  | Python script                           |
| `#!/usr/bin/env bash` | System-এ যেখানেই bash থাক (portable ✅) |

### Script চালানোর উপায়:

```bash
# Method 1: Executable করে
chmod +x script.sh
./script.sh

# Method 2: bash দিয়ে সরাসরি (chmod লাগে না)
bash script.sh
```

---

## 2️⃣ Variables (চলক)

### Variable তৈরি ও ব্যবহার:

```bash
#!/bin/bash

# Variable তৈরি (= এর আগে-পরে space দেবেন না!)
name="The King"
age=25
os="Ubuntu 24.04"

# Variable ব্যবহার ($)
echo "নাম: $name"
echo "বয়স: $age"
echo "OS: $os"

# Curly braces (জটিল নামের জন্য)
echo "Hello, ${name}!"
```

> ⚠️ **সতর্কতা:** `name = "value"` ← এটি **ভুল!** `=` এর আগে-পরে space দেওয়া **যাবে না**!
> ✅ **সঠিক:** `name="value"`

### বিশেষ Variables:

| Variable    | অর্থ                             |
| ----------- | -------------------------------- |
| `$USER`     | বর্তমান username                 |
| `$HOME`     | Home directory                   |
| `$PWD`      | বর্তমান directory                |
| `$SHELL`    | বর্তমান shell                    |
| `$RANDOM`   | একটি random সংখ্যা               |
| `$?`        | শেষ কমান্ডের exit status (0=সফল) |
| `$0`        | Script-এর নাম                    |
| `$1, $2...` | Script-এ পাঠানো arguments        |
| `$#`        | মোট argument সংখ্যা              |
| `$@`        | সব arguments                     |

### Command Substitution — কমান্ডের output variable-এ:

```bash
#!/bin/bash

current_date=$(date)
file_count=$(ls | wc -l)
my_ip=$(hostname -I | awk '{print $1}')

echo "তারিখ: $current_date"
echo "ফাইল সংখ্যা: $file_count"
echo "IP: $my_ip"
```

---

## 3️⃣ User Input — `read`

```bash
#!/bin/bash

echo "আপনার নাম কী?"
read name

echo "আপনার বয়স কত?"
read age

echo "হ্যালো $name! আপনার বয়স $age।"
```

### read-এর Options:

```bash
# Prompt সহ (আলাদা echo লাগবে না)
read -p "আপনার নাম: " name

# Password (টাইপ দেখাবে না)
read -sp "Password: " password
echo  # নতুন লাইন

# Timeout (৫ সেকেন্ডে input না দিলে continue)
read -t 5 -p "৫ সেকেন্ডে লিখুন: " answer

# Default value সহ
read -p "শহর [Dhaka]: " city
city=${city:-Dhaka}  # খালি থাকলে Dhaka
```

---

## 4️⃣ Conditional Statements — if/else

### মৌলিক if:

```bash
#!/bin/bash

read -p "একটি সংখ্যা দিন: " num

if [ $num -gt 10 ]; then
    echo "$num ১০-এর চেয়ে বড়"
fi
```

### if-else:

```bash
#!/bin/bash

read -p "একটি সংখ্যা দিন: " num

if [ $num -gt 10 ]; then
    echo "$num ১০-এর চেয়ে বড়"
else
    echo "$num ১০-এর চেয়ে বড় নয়"
fi
```

### if-elif-else:

```bash
#!/bin/bash

read -p "আপনার marks: " marks

if [ $marks -ge 80 ]; then
    echo "Grade: A+ 🌟"
elif [ $marks -ge 60 ]; then
    echo "Grade: A"
elif [ $marks -ge 40 ]; then
    echo "Grade: B"
else
    echo "Grade: F ❌"
fi
```

### Comparison Operators:

#### সংখ্যা তুলনা:

| Operator | অর্থ        | ইংরেজি                   |
| -------- | ----------- | ------------------------ |
| `-eq`    | সমান        | **eq**ual                |
| `-ne`    | সমান নয়    | **n**ot **e**qual        |
| `-gt`    | বড়         | **g**reater **t**han     |
| `-lt`    | ছোট         | **l**ess **t**han        |
| `-ge`    | বড় বা সমান | **g**reater or **e**qual |
| `-le`    | ছোট বা সমান | **l**ess or **e**qual    |

#### String তুলনা:

| Operator    | অর্থ         |
| ----------- | ------------ |
| `=` বা `==` | সমান         |
| `!=`        | সমান নয়     |
| `-z`        | খালি (empty) |
| `-n`        | খালি নয়     |

#### ফাইল পরীক্ষা:

| Operator  | অর্থ                          |
| --------- | ----------------------------- |
| `-f file` | ফাইল আছে কি?                  |
| `-d dir`  | ডিরেক্টরি আছে কি?             |
| `-e path` | কিছু আছে কি? (ফাইল/ডিরেক্টরি) |
| `-r file` | পড়ার অনুমতি আছে?             |
| `-w file` | লেখার অনুমতি আছে?             |
| `-x file` | চালানোর অনুমতি আছে?           |
| `-s file` | ফাইল খালি নয়? (size > 0)     |

### ফাইল পরীক্ষার উদাহরণ:

```bash
#!/bin/bash

read -p "ফাইলের নাম দিন: " filename

if [ -f "$filename" ]; then
    echo "✅ '$filename' ফাইল পাওয়া গেছে!"
    echo "আকার: $(wc -c < "$filename") bytes"
    echo "লাইন: $(wc -l < "$filename")"
elif [ -d "$filename" ]; then
    echo "📁 '$filename' একটি ডিরেক্টরি"
else
    echo "❌ '$filename' পাওয়া যায়নি!"
fi
```

---

## 5️⃣ Loops — পুনরাবৃত্তি

### for Loop:

```bash
#!/bin/bash

# তালিকা থেকে
for fruit in Apple Banana Cherry Mango; do
    echo "ফল: $fruit"
done

# সংখ্যার range
for i in {1..5}; do
    echo "সংখ্যা: $i"
done

# ফাইলের উপর loop
for file in *.txt; do
    echo "ফাইল: $file ($(wc -l < "$file") লাইন)"
done

# C-style for loop
for ((i=1; i<=10; i++)); do
    echo "Count: $i"
done
```

### while Loop:

```bash
#!/bin/bash

count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    count=$((count + 1))
done
```

### ফাইল লাইন-by-লাইন পড়া:

```bash
#!/bin/bash

while IFS= read -r line; do
    echo "Line: $line"
done < /etc/hostname
```

### Infinite Loop (অসীম loop):

```bash
#!/bin/bash

while true; do
    echo "চলছে... (Ctrl+C দিয়ে বন্ধ করুন)"
    sleep 2
done
```

---

## 6️⃣ Functions — পুনঃব্যবহারযোগ্য কোড

```bash
#!/bin/bash

# Function তৈরি
greet() {
    echo "🐧 হ্যালো, $1! স্বাগতম Linux-এ!"
}

# Function call
greet "The King"
greet "John"

# Return value সহ function
is_file_exists() {
    if [ -f "$1" ]; then
        return 0  # সত্য (success)
    else
        return 1  # মিথ্যা (failure)
    fi
}

# ব্যবহার
if is_file_exists "/etc/passwd"; then
    echo "ফাইল আছে!"
fi
```

---

## 7️⃣ Script-এ Arguments

```bash
#!/bin/bash
# ফাইল: greet.sh

echo "Script নাম: $0"
echo "প্রথম argument: $1"
echo "দ্বিতীয় argument: $2"
echo "মোট arguments: $#"
echo "সব arguments: $@"
```

```bash
# চালান
./greet.sh "Hello" "World"
# Script নাম: ./greet.sh
# প্রথম argument: Hello
# দ্বিতীয় argument: World
# মোট arguments: 2
# সব arguments: Hello World
```

---

## 8️⃣ Real-Life Script উদাহরণ

### System Info Script:

```bash
#!/bin/bash
# system-info.sh — সিস্টেমের তথ্য দেখায়

echo "================================"
echo "   🖥️  System Information"
echo "================================"
echo "Hostname : $(hostname)"
echo "OS       : $(lsb_release -d | cut -f2)"
echo "Kernel   : $(uname -r)"
echo "Uptime   : $(uptime -p)"
echo "CPU      : $(lscpu | grep 'Model name' | cut -d: -f2 | xargs)"
echo "RAM      : $(free -h | awk '/^Mem:/ {print $3 "/" $2}')"
echo "Disk     : $(df -h / | awk 'NR==2 {print $3 "/" $2 " (" $5 " used)"}')"
echo "IP       : $(hostname -I | awk '{print $1}')"
echo "Users    : $(who | wc -l) logged in"
echo "================================"
```

### Backup Script:

```bash
#!/bin/bash
# backup.sh — ফোল্ডার backup নেয়

SOURCE="$HOME/Documents"
BACKUP_DIR="$HOME/backups"
DATE=$(date +%Y-%m-%d_%H%M)
BACKUP_NAME="backup_${DATE}.tar.gz"

# Backup ফোল্ডার তৈরি
mkdir -p "$BACKUP_DIR"

# Backup নিন
tar -czf "$BACKUP_DIR/$BACKUP_NAME" "$SOURCE" 2>/dev/null

if [ $? -eq 0 ]; then
    echo "✅ Backup সফল: $BACKUP_DIR/$BACKUP_NAME"
    echo "আকার: $(du -sh "$BACKUP_DIR/$BACKUP_NAME" | cut -f1)"
else
    echo "❌ Backup ব্যর্থ!"
fi
```

---

## 🏋️ Practice Exercise

### অনুশীলন ১: প্রথম Script

```bash
# 1. Script তৈরি করুন
nano ~/linux-practice/my-info.sh

# 2. লিখুন:
#!/bin/bash
echo "Username: $USER"
echo "Home: $HOME"
echo "Shell: $SHELL"
echo "Date: $(date)"
echo "Files in home: $(ls ~ | wc -l)"

# 3. Executable করুন ও চালান
chmod +x ~/linux-practice/my-info.sh
~/linux-practice/my-info.sh
```

### অনুশীলন ২: Calculator Script

```bash
#!/bin/bash
# calculator.sh

read -p "প্রথম সংখ্যা: " a
read -p "দ্বিতীয় সংখ্যা: " b

echo "যোগ: $((a + b))"
echo "বিয়োগ: $((a - b))"
echo "গুণ: $((a * b))"

if [ $b -ne 0 ]; then
    echo "ভাগ: $((a / b))"
else
    echo "ভাগ: শূন্য দিয়ে ভাগ করা যায় না!"
fi
```

### অনুশীলন ৩: File Checker

একটি script লিখুন যেটি user-এর কাছ থেকে একটি path নেবে এবং বলবে:

- এটি ফাইল, ডিরেক্টরি, নাকি কিছু নেই
- যদি ফাইল হয়, তাহলে size ও permission দেখাবে

---

## ➡️ পরবর্তী Section

[Section 16: Cron Jobs ও Automation →](section-16.md)

# 📖 Section 03: File ও Directory Management

---

## 🎯 এই Section-এ যা শিখবেন

- ফাইল ও ডিরেক্টরি তৈরি করা
- ফাইল ও ডিরেক্টরি কপি, মুভ ও রিনেম করা
- ফাইল ও ডিরেক্টরি মুছে ফেলা
- File ও Directory-র পার্থক্য
- Wildcards ব্যবহার
- `touch`, `mkdir`, `cp`, `mv`, `rm`, `rmdir` কমান্ড

---

## 📂 File vs Directory

শুরু করার আগে, File ও Directory-র পার্থক্য বুঝে নেই:

| বিষয়           | File (ফাইল)              | Directory (ডিরেক্টরি/ফোল্ডার) |
| --------------- | ------------------------ | ----------------------------- |
| কী?             | তথ্য ধারণ করে            | ফাইলগুলো গোছানো রাখে          |
| উদাহরণ          | `notes.txt`, `photo.jpg` | `Documents/`, `Downloads/`    |
| Windows তুলনা   | File                     | Folder                        |
| `ls -l` এ চিহ্ন | `-` দিয়ে শুরু           | `d` দিয়ে শুরু                |

```bash
ls -l
# drwxr-xr-x  2 the-king the-king 4096 Mar  5 01:00 Documents   ← d = directory
# -rw-r--r--  1 the-king the-king  220 Mar  4 20:00 .bashrc     ← - = file
```

---

## 1️⃣ `touch` — ফাইল তৈরি করা

**কাজ:** নতুন খালি ফাইল তৈরি করে। ফাইল যদি আগে থেকে থাকে, তাহলে শুধু তারিখ/সময় আপডেট করে।

**মনে রাখুন:** "touch" = "স্পর্শ করা" — ফাইলকে স্পর্শ করে তার timestamp আপডেট করে

### মৌলিক ব্যবহার:

```bash
# একটি ফাইল তৈরি করুন
touch notes.txt
```

### একসাথে একাধিক ফাইল:

```bash
# তিনটি ফাইল একসাথে তৈরি
touch file1.txt file2.txt file3.txt
```

### বিভিন্ন ধরনের ফাইল:

```bash
touch readme.md        # Markdown ফাইল
touch script.sh        # Shell script
touch data.csv         # CSV data ফাইল
touch index.html       # HTML ফাইল
touch config.json      # JSON ফাইল
```

> 💡 **গুরুত্বপূর্ণ:** Linux-এ ফাইলের extension (`.txt`, `.md`) বাধ্যতামূলক নয়, কিন্তু সংগঠনের জন্য ব্যবহার করা ভালো।

### Real-Life Use Case:

> আপনি একটি প্রজেক্ট শুরু করছেন এবং দ্রুত কিছু খালি ফাইল তৈরি করতে চান:
>
> ```bash
> touch README.md LICENSE .gitignore index.html style.css script.js
> ```
>
> একটি কমান্ডে ৬টি ফাইল তৈরি!

---

## 2️⃣ `mkdir` — ডিরেক্টরি (ফোল্ডার) তৈরি করা

**কাজ:** নতুন ডিরেক্টরি/ফোল্ডার তৈরি করে।

**মনে রাখুন:** "**M**a**k**e **Dir**ectory" = "ডিরেক্টরি তৈরি করো"

### মৌলিক ব্যবহার:

```bash
# একটি ফোল্ডার তৈরি
mkdir projects
```

### একসাথে একাধিক ফোল্ডার:

```bash
mkdir folder1 folder2 folder3
```

### `-p` Flag — Nested (ভেতরে ভেতরে) ফোল্ডার তৈরি:

```bash
# এটি error দেবে কারণ parent ফোল্ডার নেই:
mkdir projects/web/html
# Error: No such file or directory

# -p দিলে সব ফোল্ডার একসাথে তৈরি হবে:
mkdir -p projects/web/html
```

**`-p` এর অর্থ:** "**p**arents" — দরকার হলে parent ফোল্ডারও তৈরি করো

```
# -p ছাড়া:
# projects নেই → Error!

# -p দিলে:
projects/           ← তৈরি হলো
└── web/            ← তৈরি হলো
    └── html/       ← তৈরি হলো
```

### Real-Life Use Case:

> প্রজেক্টের পুরো structure একটি কমান্ডে তৈরি:
>
> ```bash
> mkdir -p my-website/{css,js,images,pages}
> ```
>
> **ফলাফল:**
>
> ```
> my-website/
> ├── css/
> ├── js/
> ├── images/
> └── pages/
> ```
>
> `{css,js,images,pages}` — এটি **Brace Expansion** বলে। Bash এটিকে আলাদা আলাদাভাবে প্রসারিত করে।

---

## 3️⃣ `cp` — কপি করা

**কাজ:** ফাইল বা ডিরেক্টরি কপি করে।

**মনে রাখুন:** "**C**o**p**y" = "কপি করো"

### Format:

```bash
cp <source> <destination>
cp <কোথা_থেকে> <কোথায়>
```

### ফাইল কপি:

```bash
# notes.txt কে copied-notes.txt নামে কপি
cp notes.txt copied-notes.txt

# notes.txt কে Documents ফোল্ডারে কপি
cp notes.txt Documents/

# notes.txt কে Documents-এ নতুন নামে কপি
cp notes.txt Documents/my-notes.txt
```

### ডিরেক্টরি কপি (`-r` আবশ্যক):

```bash
# projects ফোল্ডার কপি করুন
cp -r projects projects-backup
```

**`-r` এর অর্থ:** "**r**ecursive" — ফোল্ডারের ভিতরের সব কিছুসহ কপি করো

> ⚠️ **সতর্কতা:** `-r` ছাড়া ফোল্ডার কপি করতে গেলে error দেবে!

### গুরুত্বপূর্ণ Flags:

| Flag | অর্থ            | কাজ                               |
| ---- | --------------- | --------------------------------- |
| `-r` | **r**ecursive   | ফোল্ডার ও তার সব content কপি      |
| `-i` | **i**nteractive | ওভাররাইট করার আগে জিজ্ঞেস করবে    |
| `-v` | **v**erbose     | কী কী কপি হচ্ছে দেখাবে            |
| `-u` | **u**pdate      | শুধু নতুন/পরিবর্তিত ফাইল কপি করবে |

```bash
# নিরাপদে কপি করুন (ওভাররাইটের আগে জিজ্ঞেস করবে)
cp -i notes.txt Documents/

# কপি হচ্ছে দেখুন
cp -rv projects/ backup/
# 'projects/file1.txt' -> 'backup/file1.txt'
# 'projects/file2.txt' -> 'backup/file2.txt'
```

### একাধিক ফাইল একসাথে কপি:

```bash
# তিনটি ফাইল Documents-এ কপি করুন
cp file1.txt file2.txt file3.txt Documents/
```

### Real-Life Use Case:

> কাজ শুরুর আগে backup নেওয়া:
>
> ```bash
> cp -rv my-project/ my-project-backup/
> ```
>
> ভুল হলে backup থেকে ফিরিয়ে আনতে পারবেন!

---

## 4️⃣ `mv` — মুভ ও রিনেম করা

**কাজ:** ফাইল/ডিরেক্টরি সরানো (move) **অথবা** নাম পরিবর্তন (rename) করা।

**মনে রাখুন:** "**M**o**v**e" = "সরাও"

### Format:

```bash
mv <source> <destination>
mv <কোথা_থেকে> <কোথায়>
```

### ফাইল সরানো (Move):

```bash
# notes.txt কে Documents-এ সরান
mv notes.txt Documents/

# file1.txt কে Downloads থেকে Documents-এ সরান
mv Downloads/file1.txt Documents/
```

### নাম পরিবর্তন (Rename):

```bash
# old-name.txt এর নাম বদলে new-name.txt করুন
mv old-name.txt new-name.txt

# ফোল্ডারের নামও বদলানো যায়
mv old-folder new-folder
```

> 💡 **গুরুত্বপূর্ণ:** `mv` একই কমান্ড দিয়ে **move** ও **rename** দুটোই করে:
>
> - যদি destination একটি existing ফোল্ডার হয় → **move** হয়
> - যদি destination একটি নতুন নাম হয় → **rename** হয়

### গুরুত্বপূর্ণ Flags:

| Flag | অর্থ            | কাজ                            |
| ---- | --------------- | ------------------------------ |
| `-i` | **i**nteractive | ওভাররাইটের আগে জিজ্ঞেস করবে    |
| `-v` | **v**erbose     | কী হচ্ছে দেখাবে                |
| `-n` | **n**o clobber  | existing ফাইল ওভাররাইট করবে না |

```bash
# নিরাপদে move (ওভাররাইটের আগে জিজ্ঞেস করবে)
mv -i notes.txt Documents/

# কী হচ্ছে দেখুন
mv -v old.txt new.txt
# renamed 'old.txt' -> 'new.txt'
```

### cp vs mv তুলনা:

| বিষয়          | `cp` (Copy)   | `mv` (Move)                |
| -------------- | ------------- | -------------------------- |
| মূল ফাইল       | **থেকে যায়** | **চলে যায়**               |
| ফলাফল          | দুটি কপি থাকে | একটিই থাকে (নতুন জায়গায়) |
| Rename         | পারে না       | পারে ✅                    |
| ফোল্ডারের জন্য | `-r` লাগে     | লাগে না                    |

### Real-Life Use Case:

> Downloads-এ ডাউনলোড হওয়া ফাইলগুলো সঠিক জায়গায় সরানো:
>
> ```bash
> mv ~/Downloads/report.pdf ~/Documents/
> mv ~/Downloads/photo.jpg ~/Pictures/
> mv ~/Downloads/song.mp3 ~/Music/
> ```

---

## 5️⃣ `rm` — ফাইল মুছে ফেলা

**কাজ:** ফাইল মুছে ফেলে। (**একবার মুছলে ফেরত আনা যায় না!**)

**মনে রাখুন:** "**R**e**m**ove" = "সরিয়ে ফেলো"

> ⚠️ **সতর্কতা:** Linux-এ কোনো Recycle Bin নেই! `rm` দিলে ফাইল **চিরতরে** মুছে যায়!

### ফাইল মুছুন:

```bash
# একটি ফাইল মুছুন
rm notes.txt

# একাধিক ফাইল মুছুন
rm file1.txt file2.txt file3.txt
```

### ডিরেক্টরি মুছুন (`-r` আবশ্যক):

```bash
# ফোল্ডার ও তার সব content মুছুন
rm -r projects/
```

### গুরুত্বপূর্ণ Flags:

| Flag | অর্থ            | কাজ                                 |
| ---- | --------------- | ----------------------------------- |
| `-r` | **r**ecursive   | ফোল্ডার ও ভিতরের সব কিছু মুছুন      |
| `-i` | **i**nteractive | প্রতিটি ফাইল মুছার আগে জিজ্ঞেস করবে |
| `-f` | **f**orce       | জোর করে মুছুন (কোনো প্রশ্ন করবে না) |
| `-v` | **v**erbose     | কী মুছছে দেখাবে                     |

```bash
# নিরাপদে মুছুন (জিজ্ঞেস করবে)
rm -i notes.txt
# rm: remove regular file 'notes.txt'? y

# ফোল্ডার নিরাপদে মুছুন
rm -ri projects/
# প্রতিটি ফাইলের জন্য জিজ্ঞেস করবে

# কী মুছছে দেখুন
rm -rv old-backup/
```

> 🚫 **!! কখনও এই কমান্ড চালাবেন না !!**
>
> ```bash
> # এটি আপনার পুরো সিস্টেম মুছে দেবে!
> sudo rm -rf /
> ```
>
> এই কমান্ড root directory (`/`) থেকে সব কিছু জোর করে (`-f`) এবং recursive (`-r`) ভাবে মুছে ফেলে। **পরিণতি: সিস্টেম ধ্বংস!**

---

## 6️⃣ `rmdir` — খালি ডিরেক্টরি মুছুন

**কাজ:** **শুধুমাত্র খালি ফোল্ডার** মুছে ফেলে।

**মনে রাখুন:** "**R**e**m**ove **Dir**ectory" = "ডিরেক্টরি সরাও"

```bash
# খালি ফোল্ডার মুছুন
rmdir empty-folder

# Error হবে যদি ফোল্ডার খালি না হয়:
rmdir projects/
# rmdir: failed to remove 'projects/': Directory not empty
```

### rmdir vs rm -r:

| কমান্ড         | কাজ                           | নিরাপদ?                 |
| -------------- | ----------------------------- | ----------------------- |
| `rmdir folder` | শুধু **খালি** ফোল্ডার মুছে    | ✅ খুব নিরাপদ           |
| `rm -r folder` | ফোল্ডার ও **সব content** মুছে | ⚠️ সাবধানে ব্যবহার করুন |

---

## 🃏 Wildcards — একসাথে অনেক ফাইল নিয়ে কাজ

**Wildcards** হলো বিশেষ চিহ্ন যেগুলো দিয়ে **প্যাটার্ন ম্যাচ** করা যায়।

### প্রধান Wildcards:

| Wildcard | অর্থ                                      | উদাহরণ          | ম্যাচ করবে                            |
| -------- | ----------------------------------------- | --------------- | ------------------------------------- |
| `*`      | যেকোনো কিছু (শূন্য বা তার বেশি character) | `*.txt`         | সব `.txt` ফাইল                        |
| `?`      | ঠিক একটি character                        | `file?.txt`     | `file1.txt`, `fileA.txt`              |
| `[abc]`  | বন্ধনীর যেকোনো একটি character             | `file[123].txt` | `file1.txt`, `file2.txt`, `file3.txt` |
| `[a-z]`  | range-এর যেকোনো character                 | `file[a-c].txt` | `filea.txt`, `fileb.txt`, `filec.txt` |

### ব্যবহারিক উদাহরণ:

```bash
# সব .txt ফাইল দেখুন
ls *.txt

# সব .txt ফাইল Documents-এ কপি করুন
cp *.txt Documents/

# "report" দিয়ে শুরু হওয়া সব ফাইল দেখুন
ls report*

# সব .jpg এবং .png ফাইল মুছুন
rm *.jpg *.png

# file1, file2, file3 মুছুন
rm file[1-3].txt

# সব ফাইল ও ফোল্ডার দেখুন যার নামে "log" আছে
ls *log*
```

### Real-Life Use Case:

> Downloads থেকে সব PDF ফাইল Documents-এ সরান:
>
> ```bash
> mv ~/Downloads/*.pdf ~/Documents/
> ```

> সব পুরনো backup মুছুন:
>
> ```bash
> rm -i backup-*.tar.gz
> ```

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কমান্ড     | পুরো নাম                 | কাজ                   | উদাহরণ               |
| ---------- | ------------------------ | --------------------- | -------------------- |
| `touch`    | Touch                    | খালি ফাইল তৈরি        | `touch file.txt`     |
| `mkdir`    | Make Directory           | ফোল্ডার তৈরি          | `mkdir projects`     |
| `mkdir -p` | Make Directory (parents) | Nested ফোল্ডার তৈরি   | `mkdir -p a/b/c`     |
| `cp`       | Copy                     | ফাইল কপি              | `cp a.txt b.txt`     |
| `cp -r`    | Copy Recursive           | ফোল্ডার কপি           | `cp -r dir1 dir2`    |
| `mv`       | Move                     | ফাইল সরান / নাম বদলান | `mv old.txt new.txt` |
| `rm`       | Remove                   | ফাইল মুছুন            | `rm file.txt`        |
| `rm -r`    | Remove Recursive         | ফোল্ডার মুছুন         | `rm -r folder/`      |
| `rmdir`    | Remove Directory         | খালি ফোল্ডার মুছুন    | `rmdir empty/`       |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: প্রজেক্ট Structure তৈরি

Terminal-এ এই commands ক্রমানুসারে চালান:

```bash
# 1. Home-এ যান
cd ~

# 2. একটি practice ফোল্ডার তৈরি করুন
mkdir linux-practice

# 3. সেখানে যান
cd linux-practice

# 4. কিছু ফোল্ডার তৈরি করুন
mkdir documents images scripts

# 5. কিছু ফাইল তৈরি করুন
touch readme.txt notes.txt todo.txt

# 6. দেখুন কী কী তৈরি হয়েছে
ls -la

# 7. Nested ফোল্ডার তৈরি করুন
mkdir -p projects/web/html

# 8. tree structure দেখুন (tree ইন্সটল থাকলে)
ls -R
```

### অনুশীলন ২: কপি ও মুভ

```bash
# 1. notes.txt কপি করুন documents ফোল্ডারে
cp notes.txt documents/

# 2. todo.txt মুভ করুন documents ফোল্ডারে
mv todo.txt documents/

# 3. readme.txt এর নাম বদলান
mv readme.txt README.md

# 4. কী হয়েছে দেখুন
ls -la
ls -la documents/
```

### অনুশীলন ৩: মুছে ফেলা

```bash
# 1. scripts ফোল্ডারটি মুছুন (খালি)
rmdir scripts

# 2. notes.txt মুছুন (home directory-র টা)
rm -i notes.txt

# 3. দেখুন কী আছে
ls -la
```

### অনুশীলন ৪: Wildcards

```bash
# 1. বেশ কিছু ফাইল তৈরি করুন
touch file1.txt file2.txt file3.txt image1.jpg image2.jpg data.csv

# 2. শুধু .txt ফাইল দেখুন
ls *.txt

# 3. শুধু .jpg ফাইল দেখুন
ls *.jpg

# 4. "file" দিয়ে শুরু সব ফাইল দেখুন
ls file*

# 5. file1 ও file2 দেখুন
ls file[12].txt

# 6. সব .txt ফাইল documents-এ কপি করুন
cp *.txt documents/

# 7. সব .jpg ফাইল images-এ মুভ করুন
mv *.jpg images/

# 8. চেক করুন
ls documents/
ls images/
```

### অনুশীলন ৫: চ্যালেঞ্জ

নিচের structure তৈরি করুন **একটি মাত্র `mkdir -p` কমান্ডে** (Brace Expansion ব্যবহার করুন):

```
school/
├── bangla/
├── english/
├── math/
└── science/
    ├── physics/
    ├── chemistry/
    └── biology/
```

<details>
<summary>💡 উত্তর দেখুন</summary>

```bash
mkdir -p school/{bangla,english,math,science/{physics,chemistry,biology}}
```

</details>

---

## ➡️ পরবর্তী Section

[Section 04: File Content দেখা ও Text Processing Basics →](section-04.md)

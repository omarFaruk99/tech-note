# 📖 Section 22: Archive ও Compression (tar, gzip, zip)

---

## 🎯 এই Section-এ যা শিখবেন

- Archive (প্যাকেজ করা) এবং Compression (সাইজ কমানো) এর মধ্যে পার্থক্য কী?
- Linux-এর প্রধান Archive টুল `tar` এর ব্যবহার ও অপশনসমূহ
- ফাইল সাইজ কমানোর জন্য `gzip`, `bzip2`, `xz` এর তুলনা ও ব্যবহার
- বহুল ব্যবহৃত `.zip` এবং `.unzip` ফরম্যাট ব্যবহার
- বড় ফোল্ডারকে আর্কাইভ করা এবং এক্সট্রাক্ট (আনজিপ) করা

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড              |  Ubuntu 24 LTS-এ   | মন্তব্য                                            |
| ------------------- | :----------------: | -------------------------------------------------- |
| `tar`               |  ✅ Pre-installed  | Tape Archive - অনেকগুলো ফাইল একসাথে করার মূল টুল   |
| `gzip` / `gunzip`   |  ✅ Pre-installed  | দ্রুত সাইজ কমানোর টুল (`.gz`)                      |
| `bzip2` / `bunzip2` |  ✅ Pre-installed  | আরো ভালো কম্প্রেশন, কিন্তু একটু ধীর (`.bz2`)       |
| `xz` / `unxz`       |  ✅ Pre-installed  | সবচেয়ে ভালো কম্প্রেশন, তবে সময় বেশি লাগে (`.xz`) |
| `zip` / `unzip`     | ❌ ইন্সটল করতে হবে | Windows-এর সাথে ফাইলের আদান-প্রদান করতে            |

---

## 📦 Archive বনাম Compression

অনেকেই মনে করেন "আর্কাইভ করা" এবং "কম্প্রেস করা" একই জিনিস। কিন্তু লিনাক্সে এদের কাজ আলাদা।

- **Archive (প্যাকেজ):** এটি করা হয় যখন আপনি অনেকগুলো ফাইল এবং ফোল্ডারকে **একত্রিত করে একটিমাত্র ফাইলে** রূপান্তর করতে চান (যেমন: ১০টি বই একটি বাক্সে রাখা)। এতে ফাইলের সাইজ কমে না।
- **Compression (সাইজ কমানো):** এটি হলো সেই বাক্সটির ভেতরের ডেটাকে ছোট করে **জায়গা কমানো** (যেমন: বাতাস বের করে ভ্যাকুয়াম ব্যাগে প্যাক করা)।

---

## 1️⃣ `tar` — The Tape Archiver

Linux এবং Unix সিস্টেমে আর্কাইভ করার সবচেয়ে জনপ্রিয় টুল হলো `tar`। ইন্টারনেটে প্রায়ই লক্ষ্য করবেন সফটওয়্যারগুলো `.tar.gz` নামের এক্সটেনশন নিয়ে আসে। একে **"Tarball"** বলা হয়।

### শুধু Archive করা (সাইজ কমবে না)

```bash
# syntax: tar -cvf <নতুন ফাইলের নাম> <যে ফোল্ডারগুলো প্যাক করবেন>
tar -cvf backup.tar /home/the-king/Documents

# এখানে:
# -c : Create (নতুন তৈরি করা)
# -v : Verbose (কী কী প্যাক হচ্ছে তা স্ক্রিনে দেখানো)
# -f : File name (নতুন ফাইলের নাম দেওয়া)
```

### Archive থেকে বের করা (Extract / Unarchive)

```bash
# syntax: tar -xvf <আর্কাইভ ফাইল>
tar -xvf backup.tar

# এখানে:
# -x : Extract (বের করা)
```

### আর্কাইভের ভেতরে কী আছে তা দেখা (না খুলেই)

```bash
tar -tvf backup.tar
# -t : list / Table of content
```

---

## 2️⃣ `tar` এর সাথে Compression যুক্ত করা

খালি আর্কাইভ করলে যেহেতু সাইজ কমে না, তাই `tar` কমান্ডের মধ্যেই কম্প্রেশন টুলগুলো (যেমন `gzip`, `bzip2`) যুক্ত করে দেওয়া যায়।

### পদ্ধতি ১: `gzip` (সবচেয়ে বেশি ব্যবহৃত - `.tar.gz` বা `.tgz`)

এটি দ্রুত কাজ করে এবং মাঝারি সাইজ কমায়।

```bash
# তৈরি করা (-z মানে gzip ব্যবহার করো)
tar -czvf backup.tar.gz /home/the-king/Documents

# বের করা (Extract)
tar -xzvf backup.tar.gz

# নির্দিষ্ট কোনো ফোল্ডারে বের করা (-C)
tar -xzvf backup.tar.gz -C /var/www/backup_folder/
```

### পদ্ধতি ২: `bzip2` (ভালো কম্প্রেশন - `.tar.bz2`)

এটি `gzip` এর চেয়ে ভালো কম্প্রেস করে, তবে একটু বেশি সময় নেয়।

```bash
# তৈরি করা (-j মানে bzip2 ব্যবহার করো)
tar -cjvf backup.tar.bz2 /home/the-king/Documents

# বের করা (Extract)
tar -xjvf backup.tar.bz2
```

### পদ্ধতি ৩: `xz` (সেরা কম্প্রেশন - `.tar.xz`)

বর্তমান সময়ের সবচেয়ে শক্তিশালী কম্প্রেশন টুল। অনেক লিনাক্স ডিসট্রো তাদের মূল ফাইল শেয়ার করার জন্য এটি ব্যবহার করে। সাইজ অনেক কমে যায়, কিন্তু প্রসেসিং পাওয়ার ও সময় বেশি লাগে।

```bash
# তৈরি করা (-J মানে xz ব্যবহার করো)
tar -cJvf backup.tar.xz /home/the-king/Documents

# বের করা (Extract)
tar -xJvf backup.tar.xz
```

---

## 3️⃣ শুধু একটি ফাইল কম্প্রেস করা (Without tar)

যদি ফোল্ডার না হয়ে শুধু একটি বড় ফাইল (যেমন কোনো বড় লগ ফাইল বা ডাটাবেস এক্সপোর্ট) হয়, তবে সরাসরি কম্প্রেস করা যায়।

### Gzip ব্যবহার করে:

```bash
# ফাইলটি কম্প্রেস হওয়া মাত্র মূল ফাইলটি মুছে গিয়ে file.txt.gz তৈরি হবে
gzip file.txt

# আনজিপ করতে
gunzip file.txt.gz
```

### Bzip2 ব্যবহার করে:

```bash
bzip2 database.sql
# আনজিপ করতে
bunzip2 database.sql.bz2
```

---

## 4️⃣ Zip এবং Unzip (Windows-এর সাথে সামঞ্জস্যতা)

Windows বা Mac ইউজারদের সাথে ফাইল আদান প্রদানের জন্য `.zip` ফরম্যাট সবচেয়ে জনপ্রিয়। Ubuntu-তে ডিফল্টভাবে `unzip` থাকলেও `zip` থাকে না।

### ইন্সটল করা:

```bash
sudo apt install zip unzip -y
```

### ব্যবহার:

```bash
# একটি ফাইল জিপ করা
zip file.zip file.txt

# ফোল্ডার জিপ করা (-r মানে Recursive)
zip -r my_folder.zip /home/the-king/Documents

# জিপ ফাইল থেকে কিছু বের করা
unzip my_folder.zip

# নির্দিষ্ট ফোল্ডারে আনজিপ করা (-d মানে Directory)
unzip my_folder.zip -d /tmp/extracted_files/
```

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কাজ                    | কমান্ড                              | এক্সটেনশন  | অপশন                                    |
| ---------------------- | ----------------------------------- | ---------- | --------------------------------------- |
| **Tar (শুধু আর্কাইভ)** | `tar -cvf archive.tar /folder`      | `.tar`     | `c` = create, `v` = verbose, `f` = file |
| **Tar + Gzip**         | `tar -czvf archive.tar.gz /folder`  | `.tar.gz`  | `z` = gzip                              |
| **Tar + Bzip2**        | `tar -cjvf archive.tar.bz2 /folder` | `.tar.bz2` | `j` = bzip2                             |
| **Tar + XZ**           | `tar -cJvf archive.tar.xz /folder`  | `.tar.xz`  | `J` = xz                                |
| **Extract (আনজিপ)**    | `tar -xzvf archive.tar.gz`          | —          | `x` = extract                           |
| **Zip তৈরি**           | `zip -r archive.zip /folder`        | `.zip`     | `-r` = recursive                        |
| **Unzip (বের করা)**    | `unzip archive.zip`                 | —          | —                                       |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: Tarball তৈরি এবং এক্সট্রাক্ট

```bash
# 1. একটি ফোল্ডার এবং কিছু ফাইল তৈরি করুন:
mkdir ~/tar_practice
touch ~/tar_practice/file1.txt ~/tar_practice/file2.log

# 2. পুরো ফোল্ডারটিকে gzip ফরম্যাটে আর্কাইভ করুন:
cd ~
tar -czvf basic_archive.tar.gz tar_practice/

# 3. আর্কাইভের সাইজ এবং ফোল্ডারের অরিজিনাল সাইজ তুলনা করে দেখুন:
ls -lh basic_archive.tar.gz
du -sh tar_practice/

# 4. ফোল্ডারটি মুছে দিন এবং আর্কাইভ থেকে পুনরায় বের করুন:
rm -rf tar_practice/
tar -xzvf basic_archive.tar.gz
```

### অনুশীলন ২: Zip কমান্ড

```bash
# 1. আগে zip/unzip ইন্সটল আছে কিনা নিশ্চিত করুন:
sudo apt install zip unzip -y

# 2. আপনার Home ডিরেক্টরির কনফিগারেশন ফোল্ডারগুলো (যেমন .bashrc) জিপ করুন:
zip -r my_backup.zip ~/.bashrc

# 3. এবার এটি /tmp ফোল্ডরে আনজিপ করে চেক করুন:
unzip my_backup.zip -d /tmp/

ls -la /tmp/
```

---

## ➡️ পরবর্তী Section

[Section 23: Backup ও Restore Strategies →](section-23.md)

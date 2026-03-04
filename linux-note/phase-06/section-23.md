# 📖 Section 23: Backup ও Restore Strategies

---

## 🎯 এই Section-এ যা শিখবেন

- ডেটা ব্যাকআপের গুরুত্ব (3-2-1 Rule)
- `rsync` ഉപയോഗ করে স্মার্ট ব্যাকআপ নেওয়া
- Local (একই পিসিতে) এবং Remote (সার্ভারে) ব্যাকআপ
- Cron Jobs দিয়ে পুরো ব্যাকআপ প্রক্রিয়া অটোমেট (Automate) করা
- `tar` এবং `rsync` মিলিয়ে ফুল ব্যাকআপ সলিউশন তৈরি
- রিস্টোর (Restore) করার সঠিক কৌশল

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড  |  Ubuntu 24 LTS-এ  | মন্তব্য                          |
| ------- | :---------------: | -------------------------------- |
| `rsync` | ✅ Pre-installed  | ফাইল ও ফোল্ডার ব্যাকআপের রাজা    |
| `tar`   | ✅ অ্যাক্সেসযোগ্য | কম্প্রেসড ফুল ব্যাকআপ নিতে       |
| `cron`  | ✅ Pre-installed  | স্বয়ংক্রিয় ব্যাকআপ শিডিউল করতে |
| `ssh`   | ✅ Pre-installed  | রিমোট ব্যাকআপের জন্য             |

---

## 🛡️ ডেটা ব্যাকআপের 3-2-1 Rule

প্রোডাকশন এনভায়রনমেন্টে ব্যাকআপের ক্ষেত্রে সিস্টেম অ্যাডমিনরা বিশ্বখ্যাত **3-2-1 Rule** মেনে চলেন:

1. **3** কপি ডেটা রাখুন (১টি অরিজিনাল, ২টি ব্যাকআপ)।
2. **2** টি ভিন্ন ধরনের স্টোরেজ ব্যবহার করুন (যেমন: একটি লোকাল হার্ডড্রাইভে, আরেকটি NAS বা এক্সটার্নাল ড্রাইভ)।
3. **1** টি ব্যাকআপ ফিজিক্যাল লোকেশনের বাইরে (যেমন Cloud বা দূরবর্তী কোনো সার্ভারে) রাখুন।

---

## 1️⃣ `rsync` দিয়ে স্মার্ট লোকাল ব্যাকআপ 🚀

`rsync` সাধারণ `cp` (copy) কমান্ডের চেয়ে অনেক ভালো। কারণ এটি শুধু **পরিবর্তিত অংশটুকু** কপি করে (Incremental Backup), ফলে সময় ও স্টোরেজ দুই-ই বাঁচে।

### Local Backup (এক ড্রাইভ থেকে অন্য ড্রাইভে):

ধরি, আপনার `/home/the-king/Documents` ফোল্ডারটিকে আপনি এক্সটার্নাল ড্রাইভে (যা `/media/backup_drive` এ মাউন্ট করা) ব্যাকআপ নিতে চান।

```bash
# -a: Archive (পারমিশন, টাইমস্ট্যাম্প সব ঠিক রাখে)
# -v: Verbose (কী হচ্ছে তা দেখায়)
# --delete: সোর্স ফোল্ডার থেকে কিছু মুছলে, ব্যাকআপ থেকেও মুছে দেবে (Mirror)

rsync -av --delete /home/the-king/Documents/ /media/backup_drive/Documents_Backup/
```

> ⚠️ **খুবই গুরুত্বপূর্ণ:** সোর্স ফোল্ডারের শেষে স্ল্যাশ `/` দেওয়া মানে "ফোল্ডারের ভেতরের সব ফাইল"। স্ল্যাশ না দেওয়া মানে "পুরো ফোল্ডারটি"। `rsync`-এ এটি ভুল করলে আউটপুট উলটোপাল্টা হতে পারে।

---

## 2️⃣ Remote (Server) ব্যাকআপ

আপনার লোকাল পিসির ডেটা নিরাপদ রাখতে অন্য একটি লিনাক্স সার্ভারে (যেমন VPS বা Raspberry Pi) ব্যাকআপ নেওয়া। (এর জন্য পাসওয়ার্ডলেস SSH সেট করা থাকলে ভালো - Section 18 দেখুন)।

### Local থেকে Server-এ পাঠানো (Push):

```bash
# -z: Compress (নেটওয়ার্ক ব্যান্ডউইথ বাঁচাতে)
# -e ssh: SSH প্রোটোকল ব্যবহার করতে (ডিফল্ট, তবে স্পষ্টভাবে লেখা ভালো)

rsync -avz -e ssh /home/the-king/Work/ remoteuser@192.168.1.100:/backup/Work_Backup/
```

### Server থেকে Local-এ আনা (Pull):

সার্ভারের কোনো ব্যাকআপ আপনার ল্যাপটপে নামিয়ে আনতে:

```bash
rsync -avz -e ssh remoteuser@192.168.1.100:/var/www/html/ /home/the-king/Website_Backup/
```

---

## 3️⃣ Full System Backup (`tar` + `rsync`)

অনেক সময় শুধু ফাইল নয়, পুরো লিনাক্স সিস্টেমের স্ন্যাপশট (Snapshot) নিতে হয়।

### শুধু কনফিগারেশন এবং ইউজার ডেটা ব্যাকআপ:

সাধারনত `/etc` (সিস্টেম কনফিগ), `/home` (ইউজার ডেটা), এবং `/var/log` (লগ) ব্যাকআপ নিলেই যথেষ্ট।

```bash
# সবকিছু tar.gz এ কম্প্রেস করুন:
sudo tar -czvf /backup/server_full_backup_$(date +%F).tar.gz /etc /home /var/log
```

_`$(date +%F)` কমান্ডটি ফাইলের নামে আজকের তারিখ (যেমন: 2026-03-05) বসিয়ে দেবে।_

---

## 4️⃣ অটোমেশন — Cron দিয়ে ব্যাকআপ শিডিউল করা

রোজ রোজ হাতে কমান্ড লেখা বোরিং এবং ভোলার সম্ভাবনা বেশি। তাই আমরা এটি **Cron** (Section 16) দিয়ে স্বয়ংক্রিয় করব।

### একটি ব্যাকআপ স্ক্রিপ্ট তৈরি:

```bash
nano ~/backup_script.sh
```

ভেতরে লিখুন:

```bash
#!/bin/bash
# રોજિંદા ব্যাকআপ স্ক্রিপ্ট

echo "ব্যাকআপ শুরু হচ্ছে: $(date)" >> /var/log/my_backup.log

# rsync কমান্ড
rsync -av --delete /home/the-king/Documents/ /media/backup_drive/Documents/ >> /var/log/my_backup.log 2>&1

echo "ব্যাকআপ শেষ: $(date)" >> /var/log/my_backup.log
echo "-----------------------------------" >> /var/log/my_backup.log
```

ফাইলটি সেভ করুন এবং Executable করুন:

```bash
chmod +x ~/backup_script.sh
```

### Cron-এ যুক্ত করা (প্রতিদিন রাত ২টায়):

```bash
crontab -e

# ফাইলের শেষে যোগ করুন:
0 2 * * * /home/the-king/backup_script.sh
```

---

## 5️⃣ Restore (ডেটা ফিরিয়ে আনা)

ব্যাকআপ নেওয়া যতটা গুরুত্বপূর্ণ, ডেটা রিস্টোর করার প্র্যাকটিস থাকা তার চেয়ে বেশি জরুরি। (ব্যাকআপ টেস্ট না করলে বিপদের দিনে তা কাজ নাও করতে পারে!)

### `rsync` দিয়ে রিস্টোর:

শুধু সোর্স এবং ডেস্টিনেশন উল্টে দিলেই রিস্টোর হয়ে যাবে!

```bash
# ব্যাকআপ ড্রাইভ থেকে কম্পিউটারে ফেরানো
rsync -av /media/backup_drive/Documents_Backup/ /home/the-king/Documents_Restored/
```

### `tar` দিয়ে রিস্টোর:

```bash
# নির্দিষ্ট ফোল্ডারে আনজিপ করা
sudo tar -xzvf /backup/server_full_backup_2026-03-05.tar.gz -C /restore_point/
```

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কাজ                           | কমান্ড                                        |
| ----------------------------- | --------------------------------------------- |
| **লোকাল সিঙ্ক**               | `rsync -av /source/ /dest/`                   |
| **Mirror ব্যাকআপ (ডিলিট সহ)** | `rsync -av --delete /source/ /dest/`          |
| **রিমোট ব্যাকআপ (Push)**      | `rsync -avz /source/ user@ip:/dest/`          |
| **রিমোট থেকে রিস্টোর (Pull)** | `rsync -avz user@ip:/source/ /dest/`          |
| **Tar ডেট ব্যাকআপ**           | `tar -czvf backup_$(date +%F).tar.gz /folder` |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: Rsync Local Mirror

```bash
# 1. দুটি টেস্ট ফোল্ডার তৈরি করুন
mkdir -p ~/sync_source ~/sync_dest
touch ~/sync_source/file{1..3}.txt

# 2. ফাইলগুলো rsync করুন
rsync -av ~/sync_source/ ~/sync_dest/
ls ~/sync_dest

# 3. Source থেকে একটি ফাইল মুছুন এবং আবার সিঙ্ক করুন
rm ~/sync_source/file2.txt
rsync -av --delete ~/sync_source/ ~/sync_dest/

# 4. Dest ফোল্ডার চেক করুন, ২ নম্বর ফাইলটি সেখান থেকেও মুছে গেছে! (Mirror Effect)
ls ~/sync_dest
```

### অনুশীলন ২: Backup Script Practice

```bash
# 1. একটি ছোট স্ক্রিপ্ট তৈরি করুন যা আপনার ~/.bashrc ব্যাকআপ নেবে
echo '#!/bin/bash' > ~/bashrc_backup.sh
echo 'tar -czf ~/bashrc_backup_$(date +%F).tar.gz ~/.bashrc' >> ~/bashrc_backup.sh

# 2. এক্সিকিউটেবল করুন
chmod +x ~/bashrc_backup.sh

# 3. স্ক্রিপ্টটি একবার রান করান
~/bashrc_backup.sh

# 4. দেখুন ব্যাকআপ ফাইল তৈরি হয়েছে কিনা!
ls -l ~/*tar.gz
```

---

## ➡️ পরবর্তী Section

[Section 24: Linux Troubleshooting Best Practices →](section-24.md)

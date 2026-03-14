# 📖 Section 12: Disk ও Storage Management

---

## 🎯 এই Section-এ যা শিখবেন

- Disk Partition কী ও কিভাবে কাজ করে
- Mount ও Unmount ধারণা
- Disk Format করা
- USB/External Drive ব্যবহার
- Swap Management
- Disk Health Check

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড               |  Ubuntu 24 LTS-এ   | মন্তব্য                                 |
| -------------------- | :----------------: | --------------------------------------- |
| `lsblk`              |  ✅ Pre-installed  | Block device দেখা                       |
| `fdisk`              |  ✅ Pre-installed  | Partition management                    |
| `mount`              |  ✅ Pre-installed  | Device mount করা                        |
| `umount`             |  ✅ Pre-installed  | Device unmount করা                      |
| `mkfs`               |  ✅ Pre-installed  | Filesystem তৈরি (format)                |
| `blkid`              |  ✅ Pre-installed  | Partition ID দেখা                       |
| `df`                 |  ✅ Pre-installed  | Disk space                              |
| `du`                 |  ✅ Pre-installed  | Folder size                             |
| `swapon` / `swapoff` |  ✅ Pre-installed  | Swap নিয়ন্ত্রণ                         |
| `parted`             |  ✅ Pre-installed  | আধুনিক partition tool                   |
| `smartctl`           | ❌ ইন্সটল করতে হবে | `sudo apt install smartmontools`        |
| `gparted`            | ❌ ইন্সটল করতে হবে | `sudo apt install gparted` (GUI)        |
| `ncdu`               | ❌ ইন্সটল করতে হবে | `sudo apt install ncdu` (disk analyzer) |

---

## 💾 Disk ও Partition কী?

### সহজ উদাহরণ:

```
Hard Disk = একটি বড় আলমারি
Partition = আলমারির তাক (shelves)

আলমারিতে যেমন আলাদা তাকে জামা, বই, জুতা রাখেন,
তেমনি Disk-এ আলাদা partition-এ OS, Data, Swap রাখেন।
```

### Partition-এর ধরন:

| ধরন          | বিবরণ                                           |
| ------------ | ----------------------------------------------- |
| **Primary**  | মূল partition (সর্বোচ্চ ৪টি)                    |
| **Extended** | Primary-র মধ্যে container (আরও partition রাখতে) |
| **Logical**  | Extended-এর ভিতরে partition                     |
| **Swap**     | RAM সহায়ক (virtual memory)                     |

### Device নামকরণ:

```
/dev/sda     → প্রথম SATA/SCSI/USB disk
/dev/sda1    → প্রথম disk-এর প্রথম partition
/dev/sda2    → প্রথম disk-এর দ্বিতীয় partition
/dev/sdb     → দ্বিতীয় disk (যেমন USB)
/dev/sdb1    → দ্বিতীয় disk-এর প্রথম partition
/dev/nvme0n1 → NVMe SSD
```

**নামের অর্থ:**

```
sd = SCSI/SATA Disk
 a = প্রথম disk (b = দ্বিতীয়, c = তৃতীয়...)
  1 = প্রথম partition (2 = দ্বিতীয়...)
```

---

## 1️⃣ `lsblk` — Disk ও Partition দেখা

```bash
lsblk
```

```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda      8:0    0   500G  0 disk
├─sda1   8:1    0   512M  0 part /boot/efi
├─sda2   8:2    0   488G  0 part /
└─sda3   8:3    0    12G  0 part [SWAP]
sdb      8:16   1    16G  0 disk
└─sdb1   8:17   1    16G  0 part /media/the-king/USB
```

| কলাম        | অর্থ                                  |
| ----------- | ------------------------------------- |
| NAME        | Device/Partition নাম                  |
| SIZE        | আকার                                  |
| TYPE        | disk (পুরো ডিস্ক) বা part (partition) |
| MOUNTPOINTS | কোথায় সংযুক্ত                        |

```bash
# Filesystem ও UUID সহ দেখুন
lsblk -f
```

### `blkid` — Partition ID দেখা:

```bash
sudo blkid
# /dev/sda1: UUID="1234-ABCD" TYPE="vfat" PARTUUID="..."
# /dev/sda2: UUID="abcd-1234-..." TYPE="ext4" PARTUUID="..."
```

---

## 2️⃣ Mount ও Unmount

### Mount কী?

**Mount** মানে একটি storage device-কে file system-এর নির্দিষ্ট জায়গায় **সংযুক্ত করা**।

### সহজ উদাহরণ:

```
Mount = পেনড্রাইভ/HDD কম্পিউটারে লাগানো ও ব্যবহারযোগ্য করা

Windows-এ আপনি USB লাগালে D:, E: দেখায়
Linux-এ USB লাগালে /media/your-name/USB-name -এ mount হয়
```

### USB/External Drive Mount:

Ubuntu-তে USB লাগালে **স্বয়ংক্রিয়ভাবে** mount হয় `/media/username/` তে। কিন্তু ম্যানুয়ালি করতে চাইলে:

```bash
# 1. Device খুঁজুন
lsblk
# sdb1 দেখুন

# 2. Mount point তৈরি করুন
sudo mkdir -p /mnt/usb

# 3. Mount করুন
sudo mount /dev/sdb1 /mnt/usb

# 4. দেখুন
ls /mnt/usb

# 5. Unmount করুন (ব্যবহার শেষে)
sudo umount /mnt/usb
```

> ⚠️ **সতর্কতা:** USB বের করার আগে **অবশ্যই** `umount` করুন! না হলে ডেটা নষ্ট হতে পারে!

> ⚠️ কমান্ডটি `umount` — **`unmount` নয়!** (u-mount, un নয়)

### Mount Options:

```bash
# Read-only mount
sudo mount -o ro /dev/sdb1 /mnt/usb

# Read-write mount
sudo mount -o rw /dev/sdb1 /mnt/usb
```

### বর্তমানে কী কী mount আছে:

```bash
mount | grep "^/dev"
# অথবা
df -h
```

---

## 3️⃣ `/etc/fstab` — স্থায়ী Mount

**fstab** = **F**ile **S**ystem **Tab**le — বুট-এ কোন partition কোথায় mount হবে তার তালিকা।

```bash
cat /etc/fstab
```

```
# <file system> <mount point> <type> <options>       <dump> <pass>
UUID=abcd-1234  /             ext4   errors=remount-ro 0      1
UUID=5678-EFGH  /boot/efi     vfat   umask=0077        0      1
UUID=9999-0000  none          swap   sw                0      0
```

| ফিল্ড       | অর্থ                               |
| ----------- | ---------------------------------- |
| file system | Partition (UUID বা /dev/sda1)      |
| mount point | কোথায় mount হবে                   |
| type        | Filesystem type (ext4, vfat, ntfs) |
| options     | Mount options                      |
| dump        | Backup (0 = না)                    |
| pass        | Boot-এ check ক্রম                  |

> ⚠️ **সতর্কতা:** `/etc/fstab` ভুল করলে সিস্টেম **বুট নাও হতে পারে!** পরিবর্তন করার আগে backup নিন:
>
> ```bash
> sudo cp /etc/fstab /etc/fstab.backup
> ```

---

## 4️⃣ Filesystem তৈরি (Format)

### `mkfs` — Format করা

```bash
# ext4 filesystem তৈরি (Linux-এর সবচেয়ে বেশি ব্যবহৃত)
sudo mkfs.ext4 /dev/sdb1

# NTFS (Windows compatible)
sudo mkfs.ntfs /dev/sdb1

# FAT32 (USB-র জন্য সবচেয়ে compatible)
sudo mkfs.vfat /dev/sdb1

# exFAT (বড় ফাইলের জন্য, USB compatible)
sudo mkfs.exfat /dev/sdb1
```

> ⚠️ **সতর্কতা:** Format করলে **সমস্ত ডেটা মুছে যাবে!** ভুল partition format করবেন না!

### Filesystem ধরন:

| Filesystem | কখন ব্যবহার                 | সর্বোচ্চ File Size |
| ---------- | --------------------------- | ------------------ |
| **ext4**   | Linux-এ সবচেয়ে ভালো ✅     | ১৬ TB              |
| **NTFS**   | Windows-এর সাথে share       | ১৬ TB              |
| **FAT32**  | USB, সব OS-এ কাজ করে        | ৪ GB ⚠️            |
| **exFAT**  | USB, বড় ফাইল               | ১৬ EB              |
| **XFS**    | বড় ফাইল, server            | ৮ EB               |
| **Btrfs**  | Snapshot, advanced features | ১৬ EB              |

---

## 5️⃣ `fdisk` — Partition Management

```bash
# Disk-এর partition table দেখুন
sudo fdisk -l

# নির্দিষ্ট disk-এর partition table
sudo fdisk -l /dev/sda

# Interactive partition management (সাবধানে!)
sudo fdisk /dev/sdb
```

> ⚠️ **সতর্কতা:** `fdisk` দিয়ে ভুল করলে ডেটা হারাতে পারেন। এই কমান্ড **সাবধানে** ব্যবহার করুন।

### GUI Alternative — GParted (নিরাপদ ✅):

```bash
# GParted ইন্সটল করুন
sudo apt install -y gparted

# চালান (GUI খুলবে)
sudo gparted
```

> 💡 **পরামর্শ:** Beginners-দের জন্য `gparted` (GUI) ব্যবহার করা অনেক নিরাপদ।

---

## 6️⃣ Swap Management

**Swap** = Hard disk-এর একটি অংশ যেটি RAM ভরে গেলে বাড়তি "RAM" হিসেবে কাজ করে।

```bash
# বর্তমান Swap দেখুন
swapon --show
# NAME      TYPE SIZE USED PRIO
# /dev/sda3 partition 12G   0B   -2

free -h | grep Swap
# Swap:     12Gi       0B      12Gi
```

### Swap File তৈরি (যদি Swap বাড়াতে চান):

```bash
# 1. ২GB Swap file তৈরি
sudo fallocate -l 2G /swapfile

# 2. Permission সেট (শুধু root)
sudo chmod 600 /swapfile

# 3. Swap format করুন
sudo mkswap /swapfile

# 4. Swap চালু করুন
sudo swapon /swapfile

# 5. স্থায়ী করুন (fstab-এ যোগ)
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# 6. Verify
swapon --show
```

### সাময়িকভাবে Swap বন্ধ:

```bash
# সব swap বন্ধ
sudo swapoff -a

# আবার চালু
sudo swapon -a
```

---

## 7️⃣ `ncdu` — Interactive Disk Usage Analyzer

```bash
# ইন্সটল করুন
sudo apt install -y ncdu

# Home directory analyze করুন
ncdu ~

# Root analyze করুন
sudo ncdu /
```

**ncdu** = **NC**urses **D**isk **U**sage — visual ভাবে কোন ফোল্ডার কত বড় দেখায়।

**Key:**
| Key | কাজ |
|-----|-----|
| Arrow keys | Navigate |
| `d` | Delete (সাবধান!) |
| `n` | নাম অনুযায়ী sort |
| `s` | আকার অনুযায়ী sort |
| `q` | বের হোন |

---

## 8️⃣ Disk Health — `smartctl`

```bash
# ইন্সটল করুন
sudo apt install -y smartmontools

# Disk health দেখুন
sudo smartctl -a /dev/sda

# সংক্ষিপ্ত health status
sudo smartctl -H /dev/sda
# PASSED = ভালো আছে ✅
# FAILED = সমস্যা আছে! ⚠️
```

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কমান্ড                     | কাজ                       |
| -------------------------- | ------------------------- |
| `lsblk`                    | Disk/partition দেখা       |
| `blkid`                    | Partition UUID দেখা       |
| `sudo fdisk -l`            | Partition table দেখা      |
| `sudo mount /dev/X /mnt/Y` | Mount করা                 |
| `sudo umount /mnt/Y`       | Unmount করা               |
| `sudo mkfs.ext4 /dev/X`    | Format (ext4)             |
| `df -h`                    | Disk space দেখা           |
| `du -sh`                   | ফোল্ডারের আকার            |
| `swapon --show`            | Swap দেখা                 |
| `ncdu`                     | Interactive disk analyzer |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: Disk তথ্য দেখা

```bash
# 1. আপনার disk ও partition দেখুন
lsblk

# 2. Filesystem সহ দেখুন
lsblk -f

# 3. Disk space দেখুন
df -h

# 4. Home-এর ফোল্ডারগুলোর আকার
du -sh ~/* 2>/dev/null | sort -rh | head -10

# 5. Swap দেখুন
swapon --show
free -h | grep Swap
```

### অনুশীলন ২: ncdu ব্যবহার

```bash
# 1. ncdu ইন্সটল করুন
sudo apt install -y ncdu

# 2. Home directory analyze করুন
ncdu ~

# 3. কোন ফোল্ডার সবচেয়ে বড়?
# q দিয়ে বেরোন
```

### অনুশীলন ৩: Mount Point দেখা

```bash
# 1. কী কী mount আছে দেখুন
mount | grep "^/dev"

# 2. fstab দেখুন
cat /etc/fstab

# 3. USB লাগানো থাকলে দেখুন
ls /media/$USER/
```

---

## 🎉 Phase 3 Complete!

অভিনন্দন! 🎊 আপনি **Phase 3: System Management** সম্পূর্ণ করেছেন!

### এই Phase-এ যা শিখলেন:

- ✅ Process Management — ps, top, htop, kill, background/foreground
- ✅ System Information — uname, free, df, du, hardware info
- ✅ Service Management — systemctl, journalctl, timedatectl
- ✅ Disk Management — partition, mount, format, swap

### পরবর্তী Phase:

**[Phase 4: Input/Output ও Scripting →](../phase-04/section-13.md)**

Phase 4-তে শিখবেন:

- I/O Redirection ও Piping (সবচেয়ে শক্তিশালী concept!)
- grep, sed, awk — Advanced Text Processing
- Shell Scripting — নিজের program লেখা
- Cron Jobs — কাজ স্বয়ংক্রিয় করা

# 📖 Section 18: SSH ও Remote Access

---

## 🎯 এই Section-এ যা শিখবেন

- SSH (Secure Shell) কী এবং কেন দরকার?
- SSH Client ও Server-এর পার্থক্য
- Password ছাড়া লগইন — SSH Key Authentication
- SSH Config ফাইল কাস্টমাইজ করা (`~/.ssh/config`)
- SCP (Secure Copy) দিয়ে ফাইল আদান-প্রদান করা
- RSync দিয়ে দ্রুত ফাইল সিঙ্ক করা

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড        |               Ubuntu 24 LTS-এ               | মন্তব্য                              |
| ------------- | :-----------------------------------------: | ------------------------------------ |
| `ssh`         |              ✅ Pre-installed               | SSH Client (অন্য পিসিতে ঢুকতে)       |
| `sshd`        | ✅ Pre-installed (কখনো কখনো start করতে হয়) | SSH Server (আপনার পিসিতে ঢুকতে দিতে) |
| `ssh-keygen`  |              ✅ Pre-installed               | SSH KeyPair তৈরি করতে                |
| `ssh-copy-id` |              ✅ Pre-installed               | Public Key সার্ভারে পাঠাতে           |
| `scp`         |              ✅ Pre-installed               | ফাইল পাঠাতে/আনতে                     |
| `rsync`       |              ✅ Pre-installed               | ফাইল ও ফোল্ডার সিঙ্ক করতে            |

---

## 🔐 SSH (Secure Shell) কী?

**SSH** হলো এমন একটি ক্রিপ্টোগ্রাফিক নেটওয়ার্ক প্রোটোকল, যার মাধ্যমে **ইন্টারনেটের উপর দিয়ে অন্য একটি লিনাক্স কম্পিউটারে সম্পূর্ণ নিরাপদ (Encrypted) ভাবে টার্মিনাল লগইন করা যায়**।

আগে `Telnet` ব্যবহৃত হতো, কিন্তু তা নিরাপদ ছিল না (Text প্লেইন যেত)। SSH সব ডেটা **End-to-End Encrypted** করে পাঠায়।

### Client vs Server:

- **SSH Client:** আপনি যেখান থেকে লগইন করার চেষ্টা করছেন (যেমন আপনার ল্যাপটপ `ssh` কমান্ড)।
- **SSH Server:** যেখানে ঢুকতে চান (যেমন AWS Server বা Raspberry Pi `sshd` সার্ভিস)।

---

## 1️⃣ সাধারণ SSH লগইন (Password দিয়ে)

```bash
# কমান্ড: ssh <username>@<ip_address>
ssh the-king@192.168.1.50
```

1. প্রথমবার ঢুকলে একটি Warning দেখাবে (`The authenticity of host... can't be established`).
2. `yes` টাইপ করে এন্টার দিন।
3. ইউজারের পাসওয়ার্ড চাইবে, টাইপ করুন (স্ক্রিনে কিছু দেখাবে না)।
4. ব্যাস! আপনি এখন অন্য কম্পিউটারের টার্মিনালে!

### কাস্টম পোর্ট দিয়ে ঢোকা:

যদি সার্ভারের SSH পোর্ট 22 না হয়ে 2222 হয় (নিরাপত্তার জন্য):

```bash
ssh -p 2222 the-king@192.168.1.50
```

---

## 2️⃣ Password-less Login — SSH Keys (সবচেয়ে নিরাপদ!)

পাসওয়ার্ড হ্যাক হতে পারে, তাই হ্যাকার এবং ডেভেলপাররা **SSH Keys** ব্যবহার করেন।

**দুটি Key থাকে (KeyPair):**

1. **Private Key (`id_rsa / id_ed25519`):** এটি আপনার কাছেই থাকবে (গোপন)।
2. **Public Key (`id_rsa.pub / id_ed25519.pub`):** এটি সার্ভারে বা যাকে খুশি দিতে পারেন (তালা)।

### ধাপ ১: KeyPair তৈরি করা (আপনার কম্পিউটারে)

```bash
# ED25519 অ্যালগরিদম সবচেয়ে আধুনিক ও নিরাপদ
ssh-keygen -t ed25519 -C "my-laptop"
```

- আপনাকে সেভ করার পথ জিজ্ঞেস করবে (শুধু এন্টার দিন ডিফল্টের জন্য)।
- একটি Passphrase (Key-এর অতিরিক্ত পাসওয়ার্ড) চাইতে পারে, চাইলে দিতে পারেন বা খালি রেখে এন্টার দিন।

### ধাপ ২: সার্ভারে Public Key পাঠানো (`ssh-copy-id`)

যে কম্পিউটারে পাসওয়ার্ড ছাড়া ঢুকতে চান, সেটিতে আপনার Public Key পাঠাতে হবে:

```bash
# ssh-copy-id <user>@<server-ip>
ssh-copy-id the-king@192.168.1.50
```

- শেষবারের মতো পাসওয়ার্ড চাইবে এবং এরপর Public Key সার্ভারের `~/.ssh/authorized_keys` ফাইলে বসিয়ে দেবে।

### ধাপ ৩: পাসওয়ার্ড ছাড়াই লগইন

```bash
ssh the-king@192.168.1.50
# কোনো পাসওয়ার্ড ছাড়াই সরাসরি ঢুকে যাবে! 🎉
```

---

## 3️⃣ SSH Config File (`~/.ssh/config`)

বারবার `ssh User@111.222.333.444 -p 2222` টাইপ করা বিরক্তিকর।
এর একটি শর্টকাট হলো **SSH Config File**।

**ফাইলটি তৈরি/এডিট করুন:**

```bash
nano ~/.ssh/config
```

**নমুনা কনফিগারেশন:**

```config
Host myserver
    HostName 192.168.1.50
    User the-king
    Port 2222
    IdentityFile ~/.ssh/id_ed25519
```

**এখন শুধু এটি টাইপ করলেই হবে:**

```bash
ssh myserver
```

---

## 4️⃣ `scp` (Secure Copy) — ফাইল পাঠানো/আনা

**SCP** হলো `ssh` এর উপর ভিত্তি করে তৈরি ফাইল কপি করার কমান্ড।

### Local (আপনার পিসি) থেকে Remote (সার্ভারে) পাঠানো:

```bash
# scp <কী পাঠাবেন> <কোথায় পাঠাবেন>
scp my-file.txt myserver:/home/the-king/
```

### Remote (সার্ভার) থেকে Local (আপনার পিসিতে) আনা:

```bash
# scp <কোথা থেকে আনবেন> <কোথায় রাখবেন> (ডট মানে বর্তমান ফোল্ডার)
scp myserver:/home/the-king/remote-file.txt .
```

### পুরো ফোল্ডার পাঠাতে (`-r`):

```bash
scp -r my-folder/ myserver:/home/the-king/
```

---

## 5️⃣ `rsync` — আধুনিক ফাইল সিঙ্কিং (SCP এর চেয়ে ভালো!)

SCP সব ফাইল কপি করে, কিন্তু **rsync** শুধু যেগুলো পরিবর্তন হয়েছে অর্থাৎ পরিবর্তিত অংশটুকু কপি করে, ফলে অনেক দ্রুত!

> 💡 **নিয়ম:** Remote Backups বা বড় ফোল্ডারের জন্য সবসময় SCP এর বদলে RSync ব্যবহার করুন।

```bash
# লোকাল ফোল্ডার সার্ভারে পাঠানো (-a=archive, -v=verbose, -z=compress)
rsync -avz local-folder/ myserver:/home/the-king/remote-folder/

# প্রগ্রেস বার দেখতে (-P)
rsync -avzP large-file.iso myserver:/home/the-king/
```

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কাজ                        | কমান্ড                             |
| -------------------------- | ---------------------------------- |
| সাধারণ লগইন                | `ssh user@ip`                      |
| নির্দিষ্ট পোর্টে লগইন      | `ssh -p 2222 user@ip`              |
| KeyPair তৈরি করা           | `ssh-keygen -t ed25519`            |
| Key সার্ভারে কপি করা       | `ssh-copy-id user@ip`              |
| ফাইল সার্ভারে পাঠানো       | `scp file.txt user@ip:/path`       |
| ফাইল সার্ভার থেকে আনা      | `scp user@ip:/path file.txt`       |
| ফোল্ডার সিঙ্ক (Smart Copy) | `rsync -avz folder/ user@ip:/path` |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: SSH KeyPair তৈরি

```bash
# 1. একটি নতুন নিরাপদ ED25519 KeyPair তৈরি করুন
ssh-keygen -t ed25519 -C "practice-key"

# (প্রম্পট আসলে এন্টার দিয়ে এগিয়ে যান)

# 2. Key দুটি তৈরি হয়েছে কিনা দেখুন
ls -la ~/.ssh/id_ed25519*
# (বিনা .pub এক্সটেনশনেরটি Private Key, কাউকে দেবেন না!)
# (.pub এক্সটেনশনেরটি Public Key)

# 3. Public Key-টির ভেতরের ডেটা দেখুন
cat ~/.ssh/id_ed25519.pub
```

### অনুশীলন ২: SSH সার্ভার চেক

```bash
# 1. আপনার পিসিতে SSH Server চলছে কিনা দেখুন
systemctl status ssh

# 2. OpenSSH Server না থাকলে ইন্সটল করতে পারেন:
# sudo apt install -y openssh-server

# 3. নিজেকেই SSH করে দেখুন!
ssh localhost
```

### অনুশীলন ৩: SCP / RSync

```bash
# 1. একটি টেক্সট ফাইল তৈরি করুন
echo "This is a test file for transfer" > test-transfer.txt

# 2. ফাইলটি SCP দিয়ে /tmp ফোল্ডরে পাঠান (এখানে localhost ব্যবহার করা হচ্ছে)
scp test-transfer.txt localhost:/tmp/

# 3. ফাইলটি চেক করুন
cat /tmp/test-transfer.txt

# 4. RSync দিয়ে ফোল্ডার সিঙ্ক করুন (উভয় ফোল্ডার লোকাল হলেও কাজ করবে)
mkdir -p ~/sync-src ~/sync-dest
touch ~/sync-src/file1.txt ~/sync-src/file2.txt

rsync -avz ~/sync-src/ ~/sync-dest/
ls ~/sync-dest/
```

---

## ➡️ পরবর্তী Section

[Section 19: Firewall (ufw) ও Basic Security →](section-19.md)

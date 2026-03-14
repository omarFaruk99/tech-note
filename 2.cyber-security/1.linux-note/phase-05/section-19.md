# 📖 Section 19: Firewall (ufw) ও Basic Security

---

## 🎯 এই Section-এ যা শিখবেন

- Firewall কী এবং এটি কিভাবে কাজ করে
- **UFW (Uncomplicated Firewall)** দিয়ে সিস্টেম সুরক্ষিত করা
- নির্দিষ্ট পোর্ট (Port) খোলা এবং বন্ধ করা
- নির্দিষ্ট IP Address-কে ব্লক (Block) করা বা অনুমতি (Allow) দেওয়া
- **Fail2ban** দিয়ে ব্রুট-ফোর্স (Brute-force) হ্যাকিং ঠেকানো
- সাধারণ Security Best Practices

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড     |  Ubuntu 24 LTS-এ   | মন্তব্য                                            |
| ---------- | :----------------: | -------------------------------------------------- |
| `ufw`      |  ✅ Pre-installed  | Ubuntu-র ডিফল্ট ও সহজ Firewall                     |
| `iptables` |  ✅ Pre-installed  | Linux-এর মূল Firewall (ufw এর পেছনে কাজ করে)       |
| `fail2ban` | ❌ ইন্সটল করতে হবে | `sudo apt install fail2ban` (হ্যাকারদের ব্লক করতে) |

---

## 🛡️ Firewall কী?

**Firewall (ফায়ারওয়াল)** হলো আপনার কম্পিউটার এবং ইন্টারনেটের মাঝখানের এক **নিরাপত্তা রক্ষী** (Security Guard)। কে ঢুকতে পারবে (Inbound) এবং কে বের হতে পারবে (Outbound), তা সে নিয়ন্ত্রণ করে।

### UFW (Uncomplicated Firewall)

Linux-এ মূল ফায়ারওয়াল হলো `iptables` বা `nftables`, যেগুলো ব্যবহার করা বেশ কঠিন। তাই Ubuntu নিয়ে এসেছে **UFW**, যা খুবই সহজ।

**UFW-এর ডিফল্ট নীতি (Default Policy):**

- **Incoming (আসা):** `Deny` (বাইরের কেউ আপনার পিসিতে ঢুকতে পারবে না)।
- **Outgoing (যাওয়া):** `Allow` (আপনি ইন্টারনেট থেকে ব্রাউজ বা ডাউনলোড করতে পারবেন)।

---

## 1️⃣ UFW-এর প্রাথমিক ব্যবহার

### Firewall-এর অবস্থা দেখা:

```bash
sudo ufw status

# বিস্তারিত দেখতে
sudo ufw status verbose
```

_(যদি "Status: inactive" দেখায়, তার মানে Firewall বন্ধ আছে)_

### Firewall চালু (Enable) এবং বন্ধ (Disable) করা:

> ⚠️ **সতর্কতা:** আপনি যদি রিমোট সার্ভারে (SSH দিয়ে) থাকেন, তবে UFW চালু করার **আগে** অবশ্যই SSH পোর্ট (সাধারণত 22) খোলার অনুমতি দেবেন। না হলে আপনি নিজেই সার্ভার থেকে বের হয়ে যাবেন!

```bash
# SSH-কে আগে Allow করুন
sudo ufw allow ssh

# এবার Firewall চালু করুন
sudo ufw enable

# (দরকার হলে) Firewall বন্ধ করতে
sudo ufw disable
```

---

## 2️⃣ পোর্ট (Port) খোলা এবং বন্ধ করা

### পোর্ট Allow (খোলুন):

```bash
# নির্দিষ্ট পোর্ট খোলা (যেমন Web Server এর জন্য 80)
sudo ufw allow 80

# প্রোটোকল নির্দিষ্ট করে (শুধু TCP)
sudo ufw allow 80/tcp

# সেবার নাম দিয়ে (যেমন https বা 443)
sudo ufw allow https

# একটি রেঞ্জ (Range) খোলা (যেমন 3000 থেকে 3010)
sudo ufw allow 3000:3010/tcp
```

### পোর্ট Deny (বন্ধ করুন):

```bash
# নির্দিষ্ট পোর্ট বন্ধ করা
sudo ufw deny 23

# সেবার নাম দিয়ে (Telnet)
sudo ufw deny telnet
```

---

## 3️⃣ নির্দিষ্ট IP Address নিয়ন্ত্রণ করা

گاهی আমরা চাই কেবল নির্দিষ্ট কেউ (যেমন আমাদের অফিস বা বাসা) সার্ভারে ঢুকতে পারুক, অথবা কোনো ক্ষতিকর IP-কে ব্লক করতে।

### নির্দিষ্ট IP-কে Allow করা:

```bash
# শুধু 192.168.1.50-কে সব পোর্টে ঢোকার অনুমতি
sudo ufw allow from 192.168.1.50

# নির্দিষ্ট IP-কে শুধু নির্দিষ্ট পোর্টে (যেমন 22) ঢোকার অনুমতি
sudo ufw allow from 192.168.1.50 to any port 22
```

### নির্দিষ্ট IP-কে Block/Deny করা:

```bash
# একটি হ্যাকার IP ব্লক করুন
sudo ufw deny from 203.0.113.5
```

---

## 4️⃣ UFW Rules মুছে ফেলা (Delete)

ভুল করে কোনো রুল তৈরি করলে তা মুছবেন কীভাবে?

**পদ্ধতি ১: রুল নম্বর দেখে মুছা (সবচেয়ে সহজ)**

```bash
# রুলগুলো নম্বরসহ দেখুন
sudo ufw status numbered

# ধরি, ৩ নম্বর রুলটি মুছতে চান
sudo ufw delete 3
```

**পদ্ধতি ২: রুলের নাম লিখে মুছা**

```bash
# যেমন allow 80 করেছিলেন, এখন মুছবেন
sudo ufw delete allow 80
```

---

## 5️⃣ Fail2ban — হ্যাকারদের স্বয়ংক্রিয় ব্লক করা

কেউ যদি বারবার ভুল পাসওয়ার্ড দিয়ে আপনার সার্ভারে (যেমন SSH-এ) ঢোকার চেষ্টা করে (Brute-force attack), `fail2ban` তাকে স্বয়ংক্রিয়ভাবে ফায়ারওয়ালে ব্লক করে দেয়।

### ইন্সটল ও চালু করা:

```bash
sudo apt install -y fail2ban
sudo systemctl enable --now fail2ban
```

### স্ট্যাটাস চেক করা:

```bash
# fail2ban চলছে কিনা দেখুন
sudo systemctl status fail2ban

# SSH জেল (Jail) এর স্ট্যাটাস দেখুন (কয়জনকে ব্লক করেছে)
sudo fail2ban-client status sshd
```

> 💡 **নিয়ম:** `fail2ban` ইন্সটলের সাথে সাথেই এটি কাজ শুরু করে এবং ডিফল্টভাবে SSH সুরক্ষিত করে ফেলে (সাধারণত ৫ বার ভুল করলে ১০ মিনিটের জন্য ব্লক)।

---

## 6️⃣ Linux Basic Security Best Practices (টিপস)

1. **সর্বদা সিস্টেম আপ-টু-ডেট রাখুন:**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
2. **অপ্রয়োজনীয় পোর্ট বন্ধ রাখুন:**
   UFW দিয়ে শুধু যে পোর্টগুলো দরকার (যেমন 80, 443, 22) সেগুলোই Allow করবেন। বাকি সব Deny.
3. **root ইউজার দিয়ে সরাসরি SSH নিষিদ্ধ করুন:**
   `/etc/ssh/sshd_config` ফাইলে `PermitRootLogin no` করে দিন।
4. **পাসওয়ার্ড লগইন বন্ধ করে SSH Keys ব্যবহার করুন** (Section 18-এ শেখানো হয়েছে)।
5. **Fail2ban অবশ্যই ব্যবহার করুন।**

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কাজ             | UFW কমান্ড                         |
| --------------- | ---------------------------------- |
| Status দেখা     | `sudo ufw status verbose`          |
| Numbered Status | `sudo ufw status numbered`         |
| চালু করা        | `sudo ufw enable`                  |
| বন্ধ করা        | `sudo ufw disable`                 |
| Port Allow      | `sudo ufw allow 80/tcp`            |
| Port Deny       | `sudo ufw deny 23`                 |
| IP Allow        | `sudo ufw allow from 192.168.1.50` |
| IP Deny (Block) | `sudo ufw deny from 203.0.113.5`   |
| রুল ডিলিট       | `sudo ufw delete <rule_number>`    |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: UFW চালু ও رول (Rule) সেট করা

```bash
# 1. আগে SSH-কে Allow করুন (খুব জরুরি!)
sudo ufw allow ssh

# 2. Web Server (HTTP/HTTPS) Allow করুন
sudo ufw allow http
sudo ufw allow https

# 3. UFW চালু (Enable) করুন
sudo ufw enable

# 4. বর্তমান অবস্থা দেখুন
sudo ufw status
```

### অনুশীলন ২: রুল মুছা ও IP ব্লক

```bash
# 1. একটি অস্থায়ী রুল (8080 পোর্ট) তৈরি করুন
sudo ufw allow 8080/tcp

# 2. রুলগুলো নম্বরসহ দেখুন
sudo ufw status numbered

# 3. 8080 পোর্টের রুল নম্বরটি মুছে ফেলুন (আপনার নম্বরটি বসান)
sudo ufw delete 3

# 4. একটি ডামি হ্যাকার আইপি ব্লক করুন
sudo ufw deny from 123.123.123.123
```

---

## ➡️ পরবর্তী Section

[Section 20: Log Management →](section-20.md)

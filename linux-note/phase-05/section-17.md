# 📖 Section 17: Networking Basics

---

## 🎯 এই Section-এ যা শিখবেন

- IP Address, MAC Address, DNS, এবং Port এর সাধারণ ধারণা
- নিজের কম্পিউটারের IP ও Network তথ্য দেখা
- Network-এর সংযোগ পরীক্ষা করা (`ping`, `traceroute`)
- Open Port এবং Network Connections দেখা
- DNS Query করা

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড             |  Ubuntu 24 LTS-এ   | মন্তব্য                                                          |
| ------------------ | :----------------: | ---------------------------------------------------------------- |
| `ip`               |  ✅ Pre-installed  | Networking-এর প্রধান আধুনিক কমান্ড                               |
| `ping`             |  ✅ Pre-installed  | সংযোগ পরীক্ষা                                                    |
| `ss`               |  ✅ Pre-installed  | Socket (Port) তথ্য দেখা                                          |
| `wget` / `curl`    |  ✅ Pre-installed  | ইন্টারনেট থেকে ডেটা আনা                                          |
| `dig` / `nslookup` |  ✅ Pre-installed  | DNS তথ্য দেখা                                                    |
| `net-tools`        | ❌ ইন্সটল করতে হবে | `ifconfig`, `netstat` (এখন obsolete, `ip` এবং `ss` ব্যবহার করুন) |
| `traceroute`       | ❌ ইন্সটল করতে হবে | `sudo apt install traceroute`                                    |

---

## 🌐 Networking-এর ৪টি মূল স্তম্ভ

### ১. IP Address (ইন্টারনেট প্রোটোকল)

আপনার কম্পিউটারের **ভার্চুয়াল ঠিকানা** (যেমন আপনার বাড়ির ঠিকানা)।

- **IPv4:** `192.168.1.100` (৪টি সংখ্যা)
- **IPv6:** `2001:0db8:85a3::...` (নতুন ও বড় ফরম্যাট)

### ২. MAC Address

আপনার Network Card-এর **ফিজিক্যাল ঠিকানা** (যেমন গাড়ির চেসিস নম্বর)। কারখানাতেই এটি দেওয়া থাকে।

- উদাহরণ: `00:1A:2B:3C:4D:5E`

### ৩. Port (পোর্ট)

IP Address যদি বাড়ির ঠিকানা হয়, Port হলো সেই বাড়ির **দরজা**।

- **Web (HTTP):** পোর্ট `80`
- **Secure Web (HTTPS):** পোর্ট `443`
- **SSH (Remote Login):** পোর্ট `22`
- **DNS:** পোর্ট `53`

### ৪. DNS (Domain Name System)

ইন্টারনেটের **ফোনবুক**। এটি `google.com` (নাম) কে `142.250.190.46` (IP Address)-এ রূপান্তর করে, কারণ কম্পিউটার শুধু IP বোঝে।

---

## 1️⃣ Network Interfaces ও IP Address দেখা

আগে সবাই `ifconfig` ব্যবহার করত, কিন্তু এখন Linux-এ **`ip`** কমান্ড ব্যবহৃত হয়।

```bash
# সব Network Interface ও IP Address দেখুন
ip a
# বা
ip addr show
```

**আউটপুট (সাধারণত থাকে):**

- **`lo` (Loopback):** `127.0.0.1` — এটি আপনার নিজের কম্পিউটার।
- **`enp...` বা `eth...`:** Ethernet (ক্যাবল) কানেকশন।
- **`wlp...` বা `wlan...`:** WiFi কানেকশন (এখানেই আপনার লোকাল IP থাকে, যেমন `192.168.x.x`)।

### শুধু IP বের করা (Scripting-এর জন্য):

```bash
hostname -I
# 192.168.1.100
```

### Routing Table ও Gateway দেখা:

Gateway হলো সেই রাউটার, যার মাধ্যমে আপনি ইন্টারনেটে যুক্ত।

```bash
ip r
# বা
ip route show
# default via 192.168.1.1 dev wlp2s0 ...
```

যা `default via` এর পরে থাকে, সেটিই আপনার **Router IP** (`192.168.1.1`)।

---

## 2️⃣ `ping` — Network সংযোগ পরীক্ষা

`ping` (Ping) কমান্ড একটি সার্ভারে ছোট প্যাকেট পাঠায় এবং দেখে প্যাকেটটি ফিরে আসে কিনা।

```bash
# Google-এ ping করুন (Ubuntu-তে এটি চলতেই থাকে, Ctrl+C দিয়ে থামান)
ping google.com

# শুধু ৪ বার ping করুন
ping -c 4 google.com

# নিজের রাউটারে ping করুন (Local network check)
ping 192.168.1.1
```

**আউটপুট বোঝা:**

- `time=45.2 ms`: প্যাকেট যেতে এবং আসতে ৪৫.২ মিলি-সেকেন্ড সময় লেগেছে (যত কম, তত ভালো)।
- `0% packet loss`: কোনো প্যাকেট হারায়নি (সংযোগ স্থিতিশীল ✅)।

---

## 3️⃣ `ss` — Open Ports ও Active Connections দেখা

আগে `netstat` ব্যবহৃত হতো, এখন আধুনিক কমান্ড হলো **`ss` (Socket Statistics)**। এটি Cybersecurity এবং SysAdmin-দের সবচেয়ে বেশি ব্যবহৃত কমান্ড।

```bash
# শুধু Listening port-গুলো (যে দরজাগুলো খোলা আছে) দেখুন
ss -ltn
```

**Flags এর অর্থ - `tulnp` (টুলনপ):**

- **`-t`**: **T**CP পোর্ট
- **`-u`**: **U**DP পোর্ট
- **`-l`**: **L**istening (অপেক্ষমান)
- **`-n`**: **N**umeric (নামের বদলে IP ও পোর্ট সংখ্যায় দেখাবে)
- **`-p`**: **P**rocess Name (কোন প্রোগ্রাম পোর্টটি খুলেছে - sudo প্রয়োজন)

```bash
# সম্পূর্ণ চিত্র: কোন প্রোগ্রাম কোন পোর্ট খুলে রেখেছে
sudo ss -tulnp
```

> 💡 **Cybersecurity Tip:** এই কমান্ড দিয়ে আপনি দেখতে পারবেন আপনার কম্পিউটারে কোনো অজানা/suspicious প্রোগ্রাম কোনো পোর্ট খুলে লুকিয়ে আছে কিনা!

---

## 4️⃣ `traceroute` — প্যাকেটের যাত্রাপথ দেখা

আপনার কম্পিউটার থেকে `google.com` পর্যন্ত পৌঁছাতে প্যাকেটটি কোন কোন রাউটার (hops) পার হলো, তা দেখায়।

```bash
# প্রথমে ইন্সটল করুন
sudo apt install -y traceroute

# যাত্রাপথ দেখুন
traceroute google.com
```

---

## 5️⃣ DNS Query — `dig` ও `nslookup`

ওয়েবসাইটের পেছনের IP Address বা মেইল সার্ভারের তথ্য বের করতে ব্যবহৃত হয়।

```bash
# সাধারণ IP বের করা
nslookup google.com

# বিস্তারিত DNS তথ্য ('A' রেকর্ড, 'MX' মেইল রেকর্ড ইত্যাদি)
dig google.com

# শুধু IP Address (Short answer)
dig +short google.com
```

---

## 6️⃣ ফাইল/ডেটা ডাউনলোড — `wget` ও `curl`

Terminal থেকে ইন্টারনেট থেকে কিছু নামাতে।

### `wget` (Web Get)

সহজে ফাইল ডাউনলোড করতে:

```bash
# ফাইল ডাউনলোড (বর্তমান ফোল্ডারে সেভ হবে)
wget https://example.com/file.zip

# অন্য নামে সেভ করতে (-O = Output)
wget -O newfile.zip https://example.com/file.zip
```

### `curl` (Client URL)

ডেটা দেখতে ও API রিকোয়েস্ট করতে বেশি ব্যবহৃত হয়:

```bash
# ওয়েবসাইটের HTML কোড টার্মিনালে দেখতে
curl https://example.com

# ফাইল ডাউনলোড করে সেভ করতে (-o)
curl -o file.zip https://example.com/file.zip

# Headers দেখতে (-I)
curl -I https://google.com
```

> 💡 **Public IP দেখা:** আপনার রাউটারের বাইরের IP (পাবলিক আইপি) কত?
>
> ```bash
> curl ifconfig.me
> # বা
> curl -s https://api.ipify.org
> ```

---

## 📊 সব কমান্ডের সারসংক্ষেপ

| কমান্ড                | কাজ                              |
| --------------------- | -------------------------------- |
| `ip a`                | IP Address ও interface দেখা      |
| `ip r`                | Routing (Router/Gateway IP) দেখা |
| `hostname -I`         | শুধু নিজের IP Address দেখা       |
| `ping google.com`     | ইন্টারনেট কানেকশন চেক            |
| `sudo ss -tulnp`      | Open Ports এবং Programs দেখা     |
| `traceroute <domain>` | রাউটারের হপ্স (যাত্রাপথ) দেখা    |
| `dig +short <domain>` | ডোমেইনের IP Address বের করা      |
| `wget <url>`          | ফাইল ডাউনলোড                     |
| `curl ifconfig.me`    | পাবলিক (External) IP দেখা        |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: নিজের Network তথ্য

```bash
# 1. আপনার Local IP Address বের করুন
ip a | grep inet

# 2. আপনার Router/Gateway IP বের করুন
ip r

# 3. আপনার Public IP বের করুন
curl ifconfig.me
echo "" # নতুন লাইন
```

### অনুশীলন ২: Connectivity ও DNS

```bash
# 1. google.com-এ ৪টি ping টেস্ট করুন
ping -c 4 google.com

# 2. facebook.com-এর IP Address বের করুন
dig +short facebook.com
```

### অনুশীলন ৩: Security Check (Ports)

```bash
# 1. আপনার কম্পিউটারে কোন কোন পোর্ট খোলা আছে?
sudo ss -ltnp

# (যদি পোর্ট 22 খোলা থাকে, তার মানে SSH চালু আছে,
# পোর্ট 53 মানে DNS Systemd Resolve ইত্যাদি)
```

---

## ➡️ পরবর্তী Section

[Section 18: SSH ও Remote Access →](section-18.md)

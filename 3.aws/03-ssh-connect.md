# ধাপ ৩: SSH দিয়ে EC2 Server-এ প্রবেশ করুন (March 2026 Update)

> **সময়:** প্রায় ১০ মিনিট
> **আগের ধাপ:** [← EC2 Instance তৈরি](./02-ec2-instance-setup.md)
> **পরবর্তী ধাপ:** [Node.js ইনস্টল →](./04-nodejs-install.md)

---

## 🎯 এই ধাপে যা শিখবেন

- SSH কী এবং কেন দরকার
- Terminal থেকে EC2 Server-এ Login করা
- Server-এর প্রাথমিক পরিচয় এবং Update করা

---

## 💡 SSH কী?

**SSH (Secure Shell)** হলো একটি নিরাপদ পদ্ধতি যা দিয়ে আপনি দূরের কম্পিউটারে (Server) Terminal-এর মাধ্যমে কাজ করতে পারেন।

```
আপনার Ubuntu PC          AWS EC2 Server
────────────────          ──────────────
Terminal খুলুন   ──SSH──▶  ubuntu@54.XXX.XXX.XXX
(আপনার হাত)              (দূরের Server)
```

---

## 🔧 প্রয়োজনীয় তথ্য যোগাড় করুন

SSH Connect করতে আপনার দরকার:

1. **Key File:** `~/.ssh/my-react-server-key.pem`
2. **Server IP:** (আগের ধাপে নোট করা, যেমন: `54.XXX.XXX.XXX`)

---

## 🚀 SSH দিয়ে Connect করুন

### ধাপ ৩.১ — Terminal খুলুন

আপনার Ubuntu PC-তে Terminal খুলুন:

- **Keyboard Shortcut:** `Ctrl + Alt + T`
- অথবা Application Menu থেকে "Terminal" খুঁজুন

---

### ধাপ ৩.২ — Key File আছে কিনা Check করুন

```bash
ls -la ~/.ssh/
```

এরকম দেখতে পাবেন:

```
-r-------- 1 user user 1678 Mar  3 12:00 my-react-server-key.pem
```

> ⚠️ যদি permission `-r--------` না থাকে, তাহলে চালান:
>
> ```bash
> chmod 400 ~/.ssh/my-react-server-key.pem
> ```

---

### ধাপ ৩.৩ — Server-এ Connect করুন

```bash
ssh -i ~/.ssh/my-react-server-key.pem ubuntu@YOUR_SERVER_IP
```

**উদাহরণ (আপনার IP দিয়ে বদলান):**

```bash
ssh -i ~/.ssh/my-react-server-key.pem ubuntu@54.169.123.456
```

**প্রথমবার Connect করলে এই প্রশ্ন আসবে:**

```
The authenticity of host '54.169.123.456' can't be established.
ECDSA key fingerprint is SHA256:XXXXXXXXXXXX.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

→ `yes` টাইপ করুন এবং Enter চাপুন।

---

### ধাপ ৩.৪ — সফলভাবে Connect হল!

এরকম দেখলে বুঝবেন সফল হয়েছে:

```
Welcome to Ubuntu 24.04.X LTS (GNU/Linux 6.8.0-XXXX-aws x86_64)

ubuntu@ip-172-31-XX-XX:~$
```

> 💡 **নোট:** ২০২৬ সালের নতুন কনসোলে উপরে ডানে আপনার Account Name দেখে নিশ্চিত হয়ে নিন যে আপনি সঠিক একাউন্টে আছেন।

> 🎉 অভিনন্দন! আপনি এখন AWS-এর Server-এর ভেতরে আছেন!

**`ubuntu@ip-172-31-XX-XX:~$`** মানে:

- `ubuntu` = ব্যবহারকারীর নাম
- `ip-172-31-XX-XX` = Server-এর নাম
- `~` = আপনি Home Directory-তে আছেন
- `$` = command দেওয়ার জন্য প্রস্তুত

---

## 🔄 Server আপডেট করুন

Server-এ ঢোকার পর আপনার প্রথম কাজ হলো সব Software আপডেট করা। এটি আপনি আপনার **Server-এর ভেতরে** ঢোকার পর যেকোনো ডিরেক্টরি (যেমন: Home Directory) থেকে চালাতে পারেন:

```bash
# Package list আপডেট করুন
sudo apt update

# সব package upgrade করুন (কিছুটা সময় লাগবে)
sudo apt upgrade -y
```

এই command চলার সময় অনেক text দেখাবে — এটা স্বাভাবিক। শেষ হলে আবার `$` prompt দেখাবে।

> 💡 **নোট:** ২০২৬ সালের সিকিউরিটি আপডেট পেতে এটি নিয়মিত করা ভালো।
> `sudo` মানে "Super User Do" — এটি Admin permission দিয়ে কাজ করে।

---

## 🧭 Server-এ কিছু প্রাথমিক Command

এখন আপনি Server-এ আছেন। কিছু useful command:

```bash
# আপনি কোথায় আছেন দেখুন
pwd
# Output: /home/ubuntu

# ফোল্ডার তৈরি করুন
mkdir my-projects

# পোল্ডারে ঢুকুন
cd my-projects

# আবার মূল জায়গায় ফিরুন
cd ~

# Server-এর তথ্য দেখুন
uname -a

# কতটুকু Disk আছে দেখুন
df -h

# কতটুকু RAM আছে দেখুন
free -h
```

---

## 🚪 Server থেকে বের হন

```bash
exit
```

অথবা `Ctrl + D` চাপুন।

আবার connect করতে আগের SSH command আবার চালান।

---

## 🛠️ SSH Command সহজ ও ছোট করুন (খুবই কাজের!)

প্রতিবার লম্বা IP আর Key ফাইলের পথ টাইপ করা বিরক্তির। যখন আপনি নিশ্চিত হবেন যে আপনি ম্যানুয়ালি কানেক্ট করতে পারছেন, তখন নিচের যেকোনো একটি পদ্ধতি ব্যবহার করুন:

### পদ্ধতি ১: Alias তৈরি করা (সহজ)

আপনার **Local PC (আপনার নিজের কম্পিউটার)**-র Terminal-এ এই কমান্ডটি একবার চালান:

```bash
echo 'alias aws="ssh -i ~/.ssh/my-react-server-key.pem ubuntu@YOUR_SERVER_IP"' >> ~/.bashrc
source ~/.bashrc
```

এরপর থেকে শুধু `aws` লিখে এন্টার দিলেই আপনি সার্ভারে ঢুকে যাবেন!

### পদ্ধতি ২: SSH Config ফাইল ব্যবহার করা (সেরা পদ্ধতি)

এটি প্রফেশনাল এবং VS Code-এর জন্য সবচেয়ে ভালো। আপনার লোকাল পিসিতে নিচের ফাইলটি খুলুন/তৈরি করুন:

```bash
nano ~/.ssh/config
```

সেখানে নিচের কোডটুকু লিখে Ctrl+O এবং Ctrl+X দিয়ে সেভ করুন:

```text
Host myserver
    HostName YOUR_SERVER_IP
    User ubuntu
    IdentityFile ~/.ssh/my-react-server-key.pem
```

এখন থেকে আপনি শুধু `ssh myserver` লিখলেই কানেক্ট হবে। এমনকি VS Code-ও এই নাম চিনে নিবে!

---

## ✅ এই ধাপ সম্পন্ন! চেকলিস্ট

- [ ] Terminal থেকে SSH connect সফল হয়েছে
- [ ] `sudo apt update && sudo apt upgrade -y` চালানো হয়েছে
- [ ] প্রাথমিক Linux commands চেষ্টা করা হয়েছে
- [ ] Server থেকে বের হওয়া এবং আবার ঢোকা পারা গেছে

---

## ➡️ পরবর্তী ধাপ

[**ধাপ ৪: Node.js ও npm ইনস্টল করুন →**](./04-nodejs-install.md)

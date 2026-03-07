# ধাপ ২: EC2 Instance তৈরি ও কনফিগার করুন (March 2026 Update)

> **সময়:** প্রায় ২০ মিনিট
> **আগের ধাপ:** [← AWS Account তৈরি](./01-aws-account-create.md)
> **পরবর্তী ধাপ:** [SSH Connect →](./03-ssh-connect.md)

---

## 🎯 এই ধাপে যা শিখবেন

- EC2 কী এবং এটি কীভাবে কাজ করে
- একটি Ubuntu Server (EC2 Instance) তৈরি করা
- Security Group (Firewall) সেটআপ করা
- SSH Key তৈরি এবং সংরক্ষণ করা

---

## 💡 EC2 কী?

**EC2 (Elastic Compute Cloud)** হলো AWS-এর Virtual Computer/Server।
মনে করুন এটা একটা **"ভাড়ার কম্পিউটার"** যা internet-এ সার্বক্ষণিক চলে।

```
আপনার Ubuntu PC  ──SSH──▶  AWS EC2 Server (Ubuntu)
                              └── আপনার React App চলবে এখানে
```

---

## 🚀 EC2 Instance তৈরির ধাপগুলো

### ধাপ ২.১ — EC2 Dashboard খুলুন

১. AWS Console-এ Login করুন: **https://console.aws.amazon.com**
২. উপরে Region নিশ্চিত করুন: **Asia Pacific (Singapore) ap-southeast-1**  
৩. উপরে নতুন **Search Bar**-এ লিখুন: `EC2`  
৪. **EC2** সার্ভিসে ক্লিক করুন।  
৫. বাম পাশের মেনু থেকে **"Instances"** ক্লিক করুন অথবা সরাসরি ড্যাশবোর্ড থেকে **"Launch instance"** বাটনে ক্লিক করুন।

> 💡 **নোট:** ২০২৬ সালের UI-তে সার্চ বারটি আরও বেশি ইন্টেলিজেন্ট (Amazon Q চালিত), তাই দ্রুত সার্ভিস খুঁজে পেতে এটি ব্যবহার করুন।

---

### ধাপ ২.২ — Instance-এর নাম দিন

```
Name: my-react-server
```

> 💡 যেকোনো নাম দিতে পারেন, শুধু মনে রাখার মতো।

---

### ধাপ ২.৩ — Operating System বেছে নিন

**"Application and OS Images"** সেকশনে:

1. **"Ubuntu"** ট্যাবে ক্লিক করুন
2. নিচের মতো সিলেক্ট করুন:

```
AMI: Ubuntu Server 24.04 LTS (HVM), SSD Volume Type
     ✅ Free tier eligible  ← এই লেখা থাকতে হবে
Architecture: 64-bit (x86)
```

> ✅ আপনার Local PC-তেও Ubuntu 24 আছে, তাই Server-এও একই OS নেওয়া ভালো।

---

### ধাপ ২.৪ — Instance Type বেছে নিন

**"Instance type"** সেকশনে:

```
Instance type: t2.micro
               ✅ Free tier eligible  ← এই লেখা থাকতে হবে
```

এর Specs:

- **1 vCPU** (1টি Virtual Processor)
- **1 GB RAM**
- React App Practice-এর জন্য যথেষ্ট

> ⚠️ **সতর্কতা:** অন্য কোনো type বেছে নেবেন না — charge হতে পারে!

---

### ধাপ ২.৫ — SSH Key Pair তৈরি করুন 🔑

এটা সবচেয়ে গুরুত্বপূর্ণ ধাপ! Key Pair হলো আপনার Server-এর "চাবি"।

**"Key pair (login)"** সেকশনে:

1. **"Create new key pair"** ক্লিক করুন
2. নিচের মতো পূরণ করুন:

```
Key pair name: my-react-server-key
Key pair type: RSA
Private key file format: .pem  ← Ubuntu-এর জন্য এটা নিন
```

3. **"Create key pair"** ক্লিক করুন
4. একটি **.pem** ফাইল Download হবে (যেমন: `my-react-server-key.pem`)

> ⚠️ **অত্যন্ত জরুরি:** এই `.pem` ফাইলটি হারাবেন না! এটা ছাড়া server-এ ঢুকতে পারবেন না। এবং কাউকে দেবেন না।

**Ubuntu Terminal-এ ফাইলটি সঠিক জায়গায় রাখুন:**

```bash
# Terminal খুলুন এবং এই commands চালান:

# একটি .ssh ফোল্ডার তৈরি করুন (যদি না থাকে)
mkdir -p ~/.ssh

# Downloaded key ফাইলটি সরান
mv ~/Downloads/my-react-server-key.pem ~/.ssh/

# Key ফাইলের permission ঠিক করুন (এটা অবশ্যই করতে হবে!)
chmod 400 ~/.ssh/my-react-server-key.pem

# নিশ্চিত করুন
ls -la ~/.ssh/
```

---

### ধাপ ২.৬ — Network ও Firewall সেটআপ করুন

**"Network settings"** সেকশনে **"Edit"** ক্লিক করুন:

```
**Firewall (Security Groups):**

**"Create security group"** সিলেক্ট করা থাকবে। নিচের Rules গুলো নিশ্চিত করুন (২০২৬ সালের UI-তে এটি "Inbound security group rules" নামে থাকতে পারে):

| Type       | Protocol | Port | Source   | কারণ                  |
| ---------- | -------- | ---- | -------- | --------------------- |
| SSH        | TCP      | 22   | My IP    | Terminal-এ ঢোকার জন্য |
| HTTP       | TCP      | 80   | Anywhere | Website দেখার জন্য    |
| Custom TCP | TCP      | 3000 | Anywhere | React App-এর জন্য     |

**৩ নম্বর Rule (Port 3000) যোগ করতে:**

1. **"Add security group rule"** ক্লিক করুন
2. Type: `Custom TCP`
3. Port range: `3000`
4. Source: `0.0.0.0/0` (Anywhere)

---

### ধাপ ২.৭ — Storage সেটআপ

**"Configure storage"** সেকশনে:

```

8 GiB gp3 Root volume ✅ Free tier eligible

```

> ✅ Default 8 GB রাখুন — Practice-এর জন্য যথেষ্ট।

---

### ধাপ ২.৮ — Instance Launch করুন

1. ডানে **"Summary"** সেকশনে সব ঠিক আছে কিনা দেখুন
2. **"Launch instance"** বাটনে ক্লিক করুন
3. একটি success message আসবে

**Instance চালু হচ্ছে কিনা দেখুন:**

1. **"View all instances"** ক্লিক করুন
2. আপনার `my-react-server` দেখতে পাবেন
3. **Instance State:** `Running` হওয়া পর্যন্ত অপেক্ষা করুন (~১-২ মিনিট)
4. **Status check:** `2/2 checks passed` দেখালে সব ঠিক আছে ✅

---

## 📋 Instance-এর IP Address নোট করুন

Instance Running হওয়ার পর:

1. আপনার Instance-এ ক্লিক করুন (এটি খুললে একটি নতুন সাইড প্যানেল বা ট্যাব আসতে পারে)।
2. **"Details"** ট্যাবে **"Public IPv4 address"** খুঁজুন।
3. এই IP টি নোট করে রাখুন! (যেমন: `54.XXX.XXX.XXX`)

```

আমার Server IP: **\*\*\*\***\_\_\_**\*\*\*\*** ← এখানে লিখে রাখুন

```

> 💡 **মনে রাখুন:** প্রতিবার Server বন্ধ করে চালু করলে IP পরিবর্তন হয়।
> Practice-এর জন্য এটা সমস্যা না, তবে জানা দরকার।

---

## ✅ এই ধাপ সম্পন্ন! চেকলিস্ট

- [ ] EC2 Instance তৈরি হয়েছে (Ubuntu 24.04, t2.micro)
- [ ] `.pem` Key ফাইল Download হয়েছে
- [ ] Key ফাইল `~/.ssh/` ফোল্ডারে রাখা হয়েছে
- [ ] `chmod 400` দিয়ে permission ঠিক করা হয়েছে
- [ ] Security Group-এ Port 22, 80, 3000 খোলা হয়েছে
- [ ] Instance State: `Running` দেখাচ্ছে
- [ ] Public IP Address নোট করা হয়েছে

---

## ➡️ পরবর্তী ধাপ

[**ধাপ ৩: SSH দিয়ে Server-এ প্রবেশ করুন →**](./03-ssh-connect.md)
```

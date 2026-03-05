# ধাপ ৪: EC2 Server-এ Node.js ও npm ইনস্টল করুন (March 2026 Update)

> **সময়:** প্রায় ১০ মিনিট
> **আগের ধাপ:** [← SSH Connect](./03-ssh-connect.md)
> **পরবর্তী ধাপ:** [React Deploy →](./05-react-deploy.md)

---

## 🎯 এই ধাপে যা শিখবেন

- Node.js কী এবং React-এর জন্য কেন দরকার
- Server-এ Node.js (LTS version) ইনস্টল করা
- ইনস্টলেশন যাচাই করা

---

## 💡 Node.js কী?

**Node.js** হলো JavaScript-কে Server-এ চালানোর পরিবেশ।
**npm (Node Package Manager)** হলো JavaScript-এর package/library ইনস্টল করার টুল।

React Project Build ও Run করতে দুটোই দরকার।

```
Node.js  →  React App চালাতে পারে
npm      →  React-এর সব Library ইনস্টল করে
```

---

## 🚀 Node.js ইনস্টলের ধাপগুলো

### ধাপ ৪.১ — Server-এ SSH Connect করুন

```bash
ssh -i ~/.ssh/my-react-server-key.pem ubuntu@YOUR_SERVER_IP
```

---

### ধাপ ৪.২ — NodeSource Repository যোগ করুন

আমরা **Node.js 24 LTS (Krypton)** ভার্সন ইনস্টল করব। ২০২৬ সালের জন্য এটাই সবচেয়ে আধুনিক এবং stable ভার্সন।

```bash
# NodeSource setup script ডাউনলোড ও চালান (Node 24)
curl -fsSL https://deb.nodesource.com/setup_24.x | sudo -E bash -
```

এই command কিছুটা সময় নেবে। শেষে এরকম দেখাবে:

```
## Run `sudo apt-get install -y nodejs` to install Node.js 24.x...
```

---

### ধাপ ৪.৩ — Node.js ইনস্টল করুন

```bash
sudo apt-get install -y nodejs
```

---

### ধাপ ৪.৪ — ইনস্টলেশন যাচাই করুন

```bash
# Node.js version দেখুন
node --version
# Output এরকম হবে: v24.X.X

# npm version দেখুন
npm --version
# Output এরকম হবে: 10.X.X (বা এর চেয়ে বেশি)
```

> ✅ দুটোই Output দেখালে ইনস্টলেশন সফল!

---

### ধাপ ৪.৫ — NVM (Node Version Manager) ব্যবহার করা (আরও ভালো পদ্ধতি)

যদি আপনি ভবিষ্যতে খুব সহজে Node-এর ভার্সন বদলাতে চান, তবে **NVM** ব্যবহার করা ভালো:

```bash
# NVM ইনস্টল করুন
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc

# Node.js 24 ইনস্টল করুন
nvm install 24
nvm use 24
```

> ✅ NVM ব্যবহার করলে `sudo` ছাড়াই প্যাকেজ ম্যানেজ করা যায়।

---

### ধাপ ৪.৬ — npm আপডেট করুন (ঐচ্ছিক)

```bash
sudo npm install -g npm@latest
```

---

## 🧪 একটা Quick Test করুন

Node.js সত্যিই কাজ করছে কিনা দেখুন:

```bash
# Node.js REPL খুলুন
node

# এটা একটা > prompt দেখাবে। তারপর লিখুন:
console.log("Hello from AWS Server!")

# Output: Hello from AWS Server!

# বের হতে:
.exit
```

---

## ✅ এই ধাপ সম্পন্ন! চেকলিস্ট

- [ ] Node.js 24.x ইনস্টল হয়েছে (`node --version` কাজ করছে)
- [ ] npm ইনস্টল হয়েছে (`npm --version` কাজ করছে)
- [ ] Quick test সফল হয়েছে (ধাপ ৪.৭)

---

## ➡️ পরবর্তী ধাপ

[**ধাপ ৫: React Project Deploy ও রান করুন →**](./05-react-deploy.md)

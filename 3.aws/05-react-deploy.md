# ধাপ ৫: React Project Deploy ও রান করুন EC2-তে (March 2026 Update)

> **সময়:** প্রায় ২০ মিনিট
> **আগের ধাপ:** [← Node.js ইনস্টল](./04-nodejs-install.md)

---

## 🎯 এই ধাপে যা শিখবেন

- EC2 Server-এ React Project তৈরি করা
- Browser থেকে React App দেখা
- Project ফাইল Local PC থেকে Server-এ পাঠানো (Bonus)

---

## 🗺️ দুটি পদ্ধতি আছে

| পদ্ধতি                       | কখন ব্যবহার করবেন            |
| ---------------------------- | ---------------------------- |
| **A. সরাসরি Server-এ তৈরি**  | Practice / নতুন project শুরু |
| **B. Local থেকে Upload করা** | আগে থেকে তৈরি project আছে    |

---

## 🅰️ পদ্ধতি A: সরাসরি Server-এ React Project তৈরি

### ধাপ ৫.১ — Server-এ Connect করুন

```bash
ssh -i ~/.ssh/my-react-server-key.pem ubuntu@YOUR_SERVER_IP
```

---

### ধাপ ৫.২ — Projects ফোল্ডারে যান

```bash
cd ~
mkdir projects
cd projects
```

---

### ধাপ ৫.৩ — React Project তৈরি করুন

```bash
# Vite 6+ দিয়ে React Project তৈরি (সবচেয়ে আধুনিক পদ্ধতি)
# ২০২৬ সালে Vite ৬ বা তার বেশি ভার্সন ব্যবহার করা হয়।
npm create vite@latest my-app -- --template react
```

**Vite ব্যবহার করলে কিছু প্রশ্ন করবে:**

```
✔ Project name: my-app
✔ Select a framework: React
✔ Select a variant: JavaScript (বা TypeScript)
```

---

### ধাপ ৫.৪ — Dependencies ইনস্টল করুন

```bash
# project ফোল্ডারে ঢুকুন
cd my-app

# সব package ইনস্টল করুন
npm install
```

কিছুটা সময় লাগবে (ইন্টারনেটের গতি অনুযায়ী)।

---

### ধাপ ৫.৫ — React App রান করুন

```bash
# Development server চালু করুন
npm run dev -- --host 0.0.0.0 --port 3000
```

> 💡 `--host 0.0.0.0` দিলে যেকোনো IP থেকে access করা যায়।
> `--port 3000` দিলে Port 3000-এ চলবে।

এরকম দেখাবে:

```
  VITE v5.X.X  ready in 500 ms

  ➜  Local:   http://localhost:3000/
  ➜  Network: http://172.31.XX.XX:3000/
```

---

### ধাপ ৫.৬ — Browser-এ দেখুন! 🎉

আপনার **Local PC-র Browser** খুলুন এবং যান:

```
http://YOUR_SERVER_IP:3000
```

**উদাহরণ:**

```
http://54.169.123.456:3000
```

> 🎉 React-এর Default Page দেখলেন? অভিনন্দন! আপনার React App এখন AWS-এ চলছে!

---

## 🅱️ পদ্ধতি B: Local PC থেকে Project Upload করা

আপনার Local PC-তে আগে থেকে React Project থাকলে:

### Local PC-তে (নতুন Terminal-এ)

```bash
# আপনার project ফোল্ডারে যান
cd ~/path/to/your/react-project

# Server-এ Upload করুন (scp command)
scp -i ~/.ssh/my-react-server-key.pem -r . ubuntu@YOUR_SERVER_IP:~/projects/my-app
```

এরপর Server-এ SSH করে `npm install` এবং `npm run dev -- --host 0.0.0.0 --port 3000` চালান।

---

## 🔧 সমস্যা হলে কী করবেন

### ❓ Browser-এ দেখা যাচ্ছে না?

**১. Security Group চেক করুন:**

- AWS Console → EC2 → Security Groups
- Port 3000 open আছে কিনা দেখুন। ২০২৬ সালের কনসোলে এটি "Inbound rules" ট্যাবে পাবেন।
- Search বারে Instance ID বা নাম দিয়ে দ্রুত আপনার সার্ভার খুঁজে নিন।

**২. App কি সত্যিই চলছে?**

```bash
# Server-এ এই command দিন:
curl http://localhost:3000
# HTML দেখালে App চলছে, কিন্তু Firewall সমস্যা
```

**৩. Server IP সঠিক?**

```bash
# Server-এ Public IP দেখুন:
curl ifconfig.me
```

---

## 🚀 Background-এ App চালু রাখুন (গুরুত্বপূর্ণ!)

এখন Terminal বন্ধ করলে App-ও বন্ধ হয়ে যাবে। সবসময় চালু রাখতে **PM2** ব্যবহার করুন:

```bash
# PM2 ইনস্টল করুন
sudo npm install -g pm2

# App চালু করুন PM2 দিয়ে (Vite-এর জন্য)
pm2 start npm --name "my-react-app" -- run dev -- --host 0.0.0.0 --port 3000

# অথবা প্রোডাকশন বিল্ড সার্ভ করতে (আরও ভালো):
npm run build
pm2 start "npx serve -s dist -p 3000" --name "my-react-prod"

# Status দেখুন
pm2 status

# Log দেখুন
pm2 logs

# App বন্ধ করুন
pm2 stop my-react-app

# Server restart-এও Auto-start করতে (জরুরি)
pm2 startup
# (উপরে দেওয়া command-টি একটি লম্বা লাইন দেখাবে, সেটি কপি করে পেস্ট করুন)
pm2 save
```

> ✅ PM2 ব্যবহার করলে Terminal বন্ধ করলেও App চলতে থাকবে।

---

## 📁 Project Structure (Vite React)

```
my-app/
├── public/          ← Static files (images, fonts)
├── src/
│   ├── App.jsx      ← Main React Component ← এখানে কাজ করুন
│   ├── App.css      ← Styles
│   └── main.jsx     ← Entry point
├── index.html
├── package.json     ← Project info & dependencies
└── vite.config.js   ← Vite configuration
```

---

## 🎨 কিছু পরিবর্তন করে দেখুন

Server-এ `src/App.jsx` ফাইল edit করুন:

```bash
# nano editor দিয়ে ফাইল খুলুন
nano ~/projects/my-app/src/App.jsx
```

`<h1>Vite + React</h1>` এর জায়গায় লিখুন:

```jsx
<h1>আমার প্রথম AWS React App! 🚀</h1>
```

**Save করুন:** `Ctrl + O` → Enter → `Ctrl + X`

Browser Refresh করুন — পরিবর্তন দেখতে পাবেন!

---

## ✅ এই ধাপ সম্পন্ন! চেকলিস্ট

- [ ] Server-এ React Project তৈরি হয়েছে
- [ ] `npm install` সফলভাবে সম্পন্ন হয়েছে
- [ ] `npm run dev` দিয়ে App চালু হয়েছে
- [ ] Browser থেকে `http://SERVER_IP:3000` দেখা যাচ্ছে
- [ ] (ঐচ্ছিক) PM2 দিয়ে App Background-এ চালু রাখা হয়েছে

---

## 🎉 অভিনন্দন! সম্পূর্ণ Journey শেষ!

```
✅ AWS Account তৈরি
✅ EC2 Instance চালু
✅ SSH দিয়ে Server-এ প্রবেশ
✅ Node.js ইনস্টল
✅ React App Deploy ও রান
```

---

## ➡️ পরবর্তী ধাপ

[**ধাপ ৬: VS Code কানেকশন এবং এক্সেস শেয়ারিং →**](./06-vscode-and-sharing.md)

---

_🙏 এই গাইডটি আপনার কাজে লাগলে ভালো লাগবে। যেকোনো সমস্যায় AI-কে জিজ্ঞেস করুন।_

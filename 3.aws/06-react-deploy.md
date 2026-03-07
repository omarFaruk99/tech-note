# ধাপ ৬: React App Deploy করুন EC2-তে (March 2026)

> **সময়:** প্রায় ৩০-৪৫ মিনিট
> **আগের ধাপ:** [← Project কোড Server-এ আনা](./05-project-to-server.md)

---

## 🎯 এই ধাপে যা শিখবেন

- তিনটি **Production-Ready** পদ্ধতিতে React App deploy করা
- কোন পদ্ধতি কখন ব্যবহার করবেন তা বোঝা
- প্রতিটি পদ্ধতি **একদম শুরু থেকে** ধাপে ধাপে করা

---

## 🗺️ তিনটি Deploy পদ্ধতি

| #     | পদ্ধতি               | কখন ব্যবহার করবেন                                 | কঠিনতা    |
| ----- | -------------------- | ------------------------------------------------- | --------- |
| **১** | Nginx + Static Build | সাধারণ React site (Portfolio, Blog, Landing page) | 🟢 সহজ    |
| **২** | Docker + Nginx       | Team project, multiple environment, CI/CD         | 🟡 মাঝারি |
| **৩** | Nginx Reverse Proxy  | Full-stack app (React + Node.js/Express backend)  | 🟡 মাঝারি |

> 💡 **নতুন হলে পদ্ধতি ১ দিয়ে শুরু করুন।** এটা সবচেয়ে সহজ এবং সবচেয়ে বেশি ব্যবহৃত।

> ⚠️ **আগের ধাপ (ধাপ ৫) সম্পন্ন করেছেন তো?** আপনার project কোড Server-এ থাকতে হবে এবং `npm run build` দিয়ে `dist/` ফোল্ডার তৈরি হতে হবে। না হলে আগে [ধাপ ৫](./05-project-to-server.md) করুন।

---

---

## 🟢 পদ্ধতি ১: Nginx + Static Build (সবচেয়ে জনপ্রিয়)

> **এটা কী?** Nginx হলো একটি খুব দ্রুত ও নির্ভরযোগ্য Web Server। আমরা React-এর build ফাইলগুলো Nginx দিয়ে serve করবো। Website-এর জন্য এটাই সবচেয়ে standard পদ্ধতি।

### ধাপ ১.১ — Nginx ইনস্টল করুন

```bash
sudo apt update
sudo apt install nginx -y
```

**চেক করুন Nginx ঠিকমতো ইনস্টল হয়েছে কিনা:**

```bash
nginx -v
# nginx version: nginx/1.x.x দেখাবে
```

```bash
sudo systemctl status nginx
# active (running) দেখাবে
```

> 💡 ইনস্টল করার সাথে সাথেই Nginx চালু হয়ে যায়। Browser-এ `http://YOUR_SERVER_IP` গেলে Nginx-এর default page দেখতে পাবেন।

---

### ধাপ ১.২ — React Build ফাইল Nginx-এ কপি করুন

Nginx-এর default ফোল্ডার হলো `/var/www/html/`। আমরা সেখানে React-এর build ফাইল রাখবো:

```bash
# আগের default ফাইল মুছুন
sudo rm -rf /var/www/html/*

# React build কপি করুন
sudo cp -r ~/projects/my-app/dist/* /var/www/html/
```

**চেক করুন ফাইল ঠিকমতো কপি হয়েছে:**

```bash
ls /var/www/html/
# index.html এবং assets/ দেখতে পাবেন
```

---

### ধাপ ১.৩ — Nginx Configuration করুন (React Router সাপোর্ট)

React-এ আপনি যদি React Router ব্যবহার করেন (যেমন `/about`, `/contact` পেজ), তাহলে Nginx-কে বলতে হবে যেন সব route-এ `index.html` পাঠায়। না করলে সরাসরি URL-এ গেলে **404 error** পাবেন।

```bash
sudo nano /etc/nginx/sites-available/default
```

**পুরো ফাইলটি মুছে এটি paste করুন:**

```nginx
server {
    listen 80;
    server_name _;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

> 🔍 **কোনটা কী করে:**
>
> | লাইন                               | মানে                                                   |
> | ---------------------------------- | ------------------------------------------------------ |
> | `listen 80`                        | Port 80 (HTTP)-তে শুনবে                                |
> | `server_name _`                    | যেকোনো domain/IP-তে কাজ করবে                           |
> | `root /var/www/html`               | ফাইলগুলো এই ফোল্ডার থেকে serve করবে                    |
> | `try_files $uri $uri/ /index.html` | Route না পেলে index.html দেখাবে (React Router-এর জন্য) |

**Save করুন:** `Ctrl + O` → Enter → `Ctrl + X`

---

### ধাপ ১.৪ — Nginx রিস্টার্ট করুন

```bash
# প্রথমে config-এ কোনো ভুল আছে কিনা চেক করুন
sudo nginx -t
# "syntax is ok" এবং "test is successful" দেখালে ঠিক আছে

# Nginx রিস্টার্ট করুন
sudo systemctl restart nginx
```

---

### ধাপ ১.৫ — Security Group-এ Port 80 খুলুন

AWS Console-এ যান:

1. **EC2** → আপনার Instance select করুন
2. **Security** tab → Security Group-এ ক্লিক করুন
3. **Edit inbound rules** → **Add rule** →
   - Type: **HTTP**
   - Port: **80**
   - Source: **0.0.0.0/0** (Anywhere IPv4)
4. **Save rules**

---

### ধাপ ১.৬ — Browser-এ দেখুন! 🎉

```
http://YOUR_SERVER_IP
```

> 🎉 **React App দেখতে পাচ্ছেন?** অভিনন্দন! Production-Ready ভাবে deploy হয়ে গেছে!

---

### 🔄 পরে কোড আপডেট করলে কী করবেন?

যখনই React-এ কোনো পরিবর্তন করবেন, শুধু এই ৩টি command দিন:

```bash
cd ~/projects/my-app

# নতুন build তৈরি করুন
npm run build

# নতুন ফাইল কপি করুন
sudo rm -rf /var/www/html/*
sudo cp -r dist/* /var/www/html/
```

> ✅ Nginx রিস্টার্ট করারও দরকার নেই! Browser refresh করলেই নতুন version দেখবেন।

---

---

## 🟡 পদ্ধতি ২: Docker + Nginx (Team Project / CI-CD)

> **এটা কী?** Docker হলো একটি container tool — এটা আপনার App-কে একটি "বাক্সে" ভরে দেয়, যেন যেকোনো server-এ একইভাবে চলে। ভেতরে Nginx-ও থাকে।
>
> **কেন ব্যবহার করবেন?**
>
> - Team-এ সবাই একই environment পায়
> - সহজে update ও rollback করা যায়
> - CI/CD pipeline-এ ব্যবহার করা যায়

### ধাপ ২.১ — Docker ইনস্টল করুন

```bash
# Docker ইনস্টল করুন (Official পদ্ধতি)
sudo apt update
sudo apt install -y ca-certificates curl gnupg

# Docker-এর official GPG key যোগ করুন
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Docker repository যোগ করুন
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Docker ইনস্টল করুন
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io

# Docker চলছে কিনা চেক করুন
sudo docker --version
# Docker version 2X.X.X দেখাবে
```

**Docker command `sudo` ছাড়া ব্যবহার করতে:**

```bash
sudo usermod -aG docker $USER
# ⚠️ এটার পর Log out করে আবার SSH করুন
```

---

### ধাপ ২.২ — Dockerfile তৈরি করুন

আপনার React project ফোল্ডারে (`~/projects/my-app/`) যান:

```bash
cd ~/projects/my-app
nano Dockerfile
```

**নিচের সবকিছু paste করুন:**

```dockerfile
# ----- ধাপ ১: React Build করুন -----
FROM node:24-alpine AS build

WORKDIR /app

# Package ফাইল কপি ও install
COPY package*.json ./
RUN npm install

# বাকি সব কোড কপি ও build
COPY . .
RUN npm run build

# ----- ধাপ ২: Nginx দিয়ে Serve করুন -----
FROM nginx:alpine

# Build ফাইল Nginx-এ কপি করুন
COPY --from=build /app/dist /usr/share/nginx/html

# React Router সাপোর্ট-এর জন্য custom Nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

**Save করুন:** `Ctrl + O` → Enter → `Ctrl + X`

> 🔍 **এটা কী করে:**
>
> | অংশ                            | মানে                             |
> | ------------------------------ | -------------------------------- |
> | `FROM node:22-alpine AS build` | Node.js দিয়ে React build করে    |
> | `FROM nginx:alpine`            | Nginx দিয়ে build ফাইল serve করে |
> | `COPY --from=build`            | Build ফাইল Nginx-এ কপি করে       |
> | `EXPOSE 80`                    | Port 80-তে চলবে                  |

---

### ধাপ ২.৩ — Nginx Config ফাইল তৈরি করুন

```bash
nano nginx.conf
```

**paste করুন:**

```nginx
server {
    listen 80;
    server_name _;

    root /usr/share/nginx/html;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

**Save করুন:** `Ctrl + O` → Enter → `Ctrl + X`

---

### ধাপ ২.৪ — .dockerignore ফাইল তৈরি করুন

এটা Docker-কে বলে কোন ফাইলগুলো ignore করবে (build দ্রুত হয়):

```bash
nano .dockerignore
```

```
node_modules
dist
.git
```

**Save করুন:** `Ctrl + O` → Enter → `Ctrl + X`

---

### ধাপ ২.৫ — Docker Image Build করুন

```bash
cd ~/projects/my-app

docker build -t my-react-app .
```

> ⏳ প্রথমবার কিছুটা সময় লাগবে (৩-৫ মিনিট)। পরেরবার অনেক দ্রুত হবে।

**চেক করুন Image তৈরি হয়েছে:**

```bash
docker images
# my-react-app image দেখতে পাবেন
```

---

### ধাপ ২.৬ — Docker Container চালু করুন

```bash
docker run -d -p 80:80 --name react-app my-react-app
```

> 🔍 **কোনটা কী:**
>
> | Flag               | মানে                                     |
> | ------------------ | ---------------------------------------- |
> | `-d`               | Background-এ চলবে                        |
> | `-p 80:80`         | Server-এর Port 80 → Container-এর Port 80 |
> | `--name react-app` | Container-এর নাম                         |

**চেক করুন চলছে কিনা:**

```bash
docker ps
# react-app container "Up" দেখাবে
```

---

### ধাপ ২.৭ — Security Group-এ Port 80 খুলুন

(পদ্ধতি ১-এর ধাপ ১.৫ দেখুন — একই পদ্ধতি)

---

### ধাপ ২.৮ — Browser-এ দেখুন! 🎉

```
http://YOUR_SERVER_IP
```

---

### 🔄 পরে কোড আপডেট করলে কী করবেন?

```bash
cd ~/projects/my-app

# পুরানো container বন্ধ ও মুছুন
docker stop react-app
docker rm react-app

# নতুন image build করুন
docker build -t my-react-app .

# নতুন container চালু করুন
docker run -d -p 80:80 --name react-app my-react-app
```

---

### 🧹 দরকারি Docker Commands

```bash
# চলমান containers দেখুন
docker ps

# সব containers দেখুন (বন্ধ সহ)
docker ps -a

# Container-এর logs দেখুন
docker logs react-app

# Container বন্ধ করুন
docker stop react-app

# Container মুছুন
docker rm react-app

# Image মুছুন
docker rmi my-react-app
```

---

---

## 🟡 পদ্ধতি ৩: Nginx Reverse Proxy (Full-Stack App)

> **এটা কী?** আপনার যদি React frontend + Node.js/Express backend দুটোই থাকে, তাহলে Nginx-কে "traffic controller" হিসেবে ব্যবহার করা হয়। Nginx সিদ্ধান্ত নেয় কোন request কোথায় যাবে।
>
> **কেন ব্যবহার করবেন?**
>
> - একটি domain দিয়ে frontend ও API দুটোই access করা যায়
> - যেমন: `yoursite.com` → React, `yoursite.com/api` → Express

```
ব্রাউজার → Nginx (Port 80)
                ├── / → React Static Files (HTML, CSS, JS)
                └── /api → Node.js Backend (Port 5000)
```

---

### ধাপ ৩.১ — React Build প্রস্তুত করুন

```bash
cd ~/projects/my-app
npm run build
sudo mkdir -p /var/www/html
sudo rm -rf /var/www/html/*
sudo cp -r dist/* /var/www/html/
```

---

### ধাপ ৩.২ — Backend (Node.js/Express) তৈরি করুন

একটি সহজ Express backend তৈরি করি:

```bash
cd ~/projects
mkdir my-backend
cd my-backend
npm init -y
npm install express
```

```bash
nano index.js
```

**paste করুন:**

```javascript
const express = require('express')
const app = express()

app.get('/api/hello', (req, res) => {
  res.json({ message: 'Backend থেকে সালাম! 🎉' })
})

app.get('/api/time', (req, res) => {
  res.json({ time: new Date().toLocaleString('bn-BD') })
})

app.listen(5000, () => {
  console.log('Backend চলছে Port 5000-এ')
})
```

**Save করুন:** `Ctrl + O` → Enter → `Ctrl + X`

---

### ধাপ ৩.৩ — PM2 দিয়ে Backend চালু করুন

```bash
# PM2 ইনস্টল করুন (আগে না করলে)
sudo npm install -g pm2

# Backend চালু করুন
cd ~/projects/my-backend
pm2 start index.js --name "my-backend"

# চলছে কিনা চেক করুন
pm2 status
```

**Backend সরাসরি কাজ করছে কিনা চেক করুন:**

```bash
curl http://localhost:5000/api/hello
# {"message":"Backend থেকে সালাম! 🎉"} দেখাবে
```

---

### ধাপ ৩.৪ — Nginx ইনস্টল ও Configure করুন

```bash
# Nginx ইনস্টল করুন (আগে না করলে)
sudo apt update
sudo apt install nginx -y
```

```bash
sudo nano /etc/nginx/sites-available/default
```

**পুরো ফাইলটি মুছে এটি paste করুন:**

```nginx
server {
    listen 80;
    server_name _;

    # React Frontend (Static Files)
    location / {
        root /var/www/html;
        index index.html;
        try_files $uri $uri/ /index.html;
    }

    # API Requests → Node.js Backend
    location /api/ {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_cache_bypass $http_upgrade;
    }
}
```

**Save করুন:** `Ctrl + O` → Enter → `Ctrl + X`

> 🔍 **কোনটা কী করে:**
>
> | অংশ                                | মানে                                              |
> | ---------------------------------- | ------------------------------------------------- |
> | `location /`                       | Root URL-এ React-এর static ফাইল দেখায়            |
> | `location /api/`                   | `/api/` দিয়ে শুরু হওয়া request Backend-এ পাঠায় |
> | `proxy_pass http://localhost:5000` | Port 5000-এ চলমান Express-এ redirect করে          |
> | `proxy_set_header` লাইনগুলো        | সঠিক header তথ্য Backend-এ পাঠায়                 |

---

### ধাপ ৩.৫ — Nginx রিস্টার্ট করুন

```bash
sudo nginx -t
# "syntax is ok" এবং "test is successful" দেখাবে

sudo systemctl restart nginx
```

---

### ধাপ ৩.৬ — Security Group-এ Port 80 খুলুন

(পদ্ধতি ১-এর ধাপ ১.৫ দেখুন — একই পদ্ধতি)

---

### ধাপ ৩.৭ — Browser-এ দেখুন! 🎉

**React Frontend:**

```
http://YOUR_SERVER_IP
```

**API Backend:**

```
http://YOUR_SERVER_IP/api/hello
# {"message":"Backend থেকে সালাম! 🎉"} দেখাবে
```

> 🎉 একটি URL দিয়ে Frontend ও Backend দুটোই কাজ করছে!

---

### 🔄 পরে কোড আপডেট করলে কী করবেন?

**Frontend আপডেট করলে:**

```bash
cd ~/projects/my-app
npm run build
sudo rm -rf /var/www/html/*
sudo cp -r dist/* /var/www/html/
```

**Backend আপডেট করলে:**

```bash
cd ~/projects/my-backend
pm2 restart my-backend
```

---

### 🛡️ PM2 Auto-Start সেটআপ (Server Restart-এও চলবে)

```bash
pm2 startup
# একটি command দেখাবে → সেটি কপি করে Run করুন

pm2 save
```

> ✅ এখন Server restart হলেও Backend আবার নিজে চালু হয়ে যাবে।

---

---

## 🔧 সবার জন্য: সমস্যা হলে কী করবেন

### ❓ Browser-এ কিছু দেখা যাচ্ছে না?

**১. Security Group চেক করুন:**

- AWS Console → EC2 → Security Groups
- Port **80** (HTTP) open আছে কিনা দেখুন

**২. Nginx চলছে কিনা চেক করুন:**

```bash
sudo systemctl status nginx
# active (running) দেখাবে
```

**৩. Config-এ ভুল আছে কিনা:**

```bash
sudo nginx -t
# ভুল থাকলে কোন লাইনে তা দেখাবে
```

**৪. Nginx-এর Error Log দেখুন:**

```bash
sudo tail -20 /var/log/nginx/error.log
```

**৫. Server-এর IP সঠিক কিনা:**

```bash
curl ifconfig.me
```

---

## ✅ এই ধাপ সম্পন্ন! চেকলিস্ট

- [ ] তিনটি পদ্ধতির মধ্যে একটি বেছে নিয়ে deploy করেছি
- [ ] Browser-এ `http://SERVER_IP` দিয়ে React App দেখা যাচ্ছে
- [ ] (পদ্ধতি ৩ হলে) API endpoint-ও কাজ করছে

---

## ➡️ পরবর্তী ধাপ

[**ধাপ ৭: VS Code কানেকশন এবং এক্সেস শেয়ারিং →**](./07-vscode-and-sharing.md)

---

_🙏 এই গাইডটি আপনার কাজে লাগলে ভালো লাগবে। যেকোনো সমস্যায় AI-কে জিজ্ঞেস করুন।_

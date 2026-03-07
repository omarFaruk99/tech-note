# 🚀 AWS EC2 — বাংলা গাইড (Free Tier)

### React Project Deploy করার সম্পূর্ণ গাইড

> **লক্ষ্য:** AWS Free Tier একাউন্ট তৈরি থেকে শুরু করে EC2-তে React Project চালানো পর্যন্ত সব কিছু।
> **পরিবেশ:** Ubuntu 24 LTS (Local) + Ubuntu 24 LTS (EC2 Server)

---

## 📚 গাইডের সূচিপত্র

| ধাপ | ফাইল                                                   | বিষয়                           | সময়      |
| --- | ------------------------------------------------------ | ------------------------------- | --------- |
| ১   | [01-aws-account-create.md](./01-aws-account-create.md) | AWS একাউন্ট তৈরি (Free Tier)    | ~১৫ মিনিট |
| ২   | [02-ec2-instance-setup.md](./02-ec2-instance-setup.md) | EC2 Instance তৈরি ও কনফিগার     | ~২০ মিনিট |
| ৩   | [03-ssh-connect.md](./03-ssh-connect.md)               | SSH দিয়ে Server-এ প্রবেশ       | ~১০ মিনিট |
| ৪   | [04-nodejs-install.md](./04-nodejs-install.md)         | Node.js ও npm ইনস্টল            | ~১০ মিনিট |
| ৫   | [05-project-to-server.md](./05-project-to-server.md)   | Project কোড Server-এ আনা        | ~২০ মিনিট |
| ৬   | [06-react-deploy.md](./06-react-deploy.md)             | React App Deploy (Nginx/Docker) | ~৩০ মিনিট |
| ৭   | [07-vscode-and-sharing.md](./07-vscode-and-sharing.md) | VS Code কানেকশন ও এক্সেস শেয়ার | ~১৫ মিনিট |

---

## ⚠️ শুরু করার আগে মনে রাখুন

- AWS Free Tier **১২ মাস** ফ্রি থাকে
- **t2.micro** instance ব্যবহার করবেন (Free Tier eligible)
- Credit card লাগবে (charge হবে না, শুধু verify-এর জন্য)
- সব ধাপ **ক্রমানুসারে** অনুসরণ করুন

---

## 🛠️ প্রয়োজনীয় জিনিস

- [ ] একটি Email Address
- [ ] একটি Credit/Debit Card (Visa/Mastercard)
- [ ] Mobile Number
- [ ] Ubuntu 24 Terminal খোলা থাকতে হবে

---

_গাইডটি ধাপে ধাপে তৈরি করা হয়েছে। প্রতিটি ফাইল একটি নির্দিষ্ট ধাপ কভার করে।_

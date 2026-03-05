# ধাপ ১: AWS Account তৈরি করুন (Free Tier - March 2026 Update)

> **সময়:** প্রায় ১৫ মিনিট
> **পরবর্তী ধাপ:** [EC2 Instance তৈরি →](./02-ec2-instance-setup.md)

---

## 🎯 এই ধাপে যা শিখবেন

- AWS Free Tier কী এবং এটি কীভাবে কাজ করে
- AWS একাউন্ট তৈরির সম্পূর্ণ প্রক্রিয়া
- AWS Console-এ প্রথমবার লগইন করা

---

## 📋 AWS Free Tier কী?

AWS (Amazon Web Services) নতুন ব্যবহারকারীদের **১২ মাস ফ্রি** সার্ভিস দেয়। এর মধ্যে আছে:

| সার্ভিস              | ফ্রি পরিমাণ                   |
| -------------------- | ----------------------------- |
| EC2 (Virtual Server) | মাসে **৭৫০ ঘন্টা** (t2.micro) |
| Storage (EBS)        | **৩০ GB**                     |
| Data Transfer        | **১৫ GB/মাস**                 |

> ✅ **React Project Practice-এর জন্য এটাই যথেষ্ট!**

---

## 🚀 একাউন্ট তৈরির ধাপগুলো

### ধাপ ১.১ — AWS Website-এ যান

১. আপনার Browser খুলুন
২. এই লিংকে যান: **https://aws.amazon.com/free**  
৩. **"Create an AWS Account"** বাটনে ক্লিক করুন (এটি সাধারণত উপরের ডানে থাকে)।

---

### ধাপ ১.২ — Root User তথ্য দিন (নতুন UI)

একটি ফর্ম আসবে। নিচের মতো পূরণ করুন:

```
Root user email address: আপনার@email.com
AWS account name:        MyPracticeAccount (এটি এখন লগইন করার পর উপরে দেখাবে)
```

> ⚠️ **সতর্কতা:** এই email এবং password সুরক্ষিত রাখুন। এটাই আপনার "Root" একাউন্ট।

**"Verify email address"** ক্লিক করুন → আপনার email-এ একটি **৬ সংখ্যার OTP** আসবে → সেটি দিন।

---

### ধাপ ১.৩ — Password তৈরি করুন

```
Root user password:         একটি শক্তিশালী password দিন
Confirm root user password: আবার একই password দিন
```

> 💡 **টিপস:** Password-এ বড় হাতের অক্ষর, সংখ্যা এবং special character (@#$) ব্যবহার করুন।
> উদাহরণ: `MyAWS@2024Practice`

**"Continue"** ক্লিক করুন।

---

### ধাপ ১.৪ — Personal তথ্য দিন

এখন Contact Information ফর্ম আসবে:

```
Account type:  Personal  ← এটা সিলেক্ট করুন
Full name:     আপনার নাম
Phone number:  +880XXXXXXXXXX  (বাংলাদেশি নম্বর)
Country:       Bangladesh
Address:       আপনার ঠিকানা
City:          আপনার শহর
Postal code:   আপনার পোস্টাল কোড
```

**"Continue"** ক্লিক করুন।

---

### ধাপ ১.৫ — Payment তথ্য দিন

> ⚠️ **জরুরি:** এখানে Card তথ্য দিতে হবে, কিন্তু **$1 পর্যন্ত charge হতে পারে verification-এর জন্য**, যা পরে ফেরত দেওয়া হয়।

```
Credit/Debit card number:  আপনার card number
Expiration date:           Card-এর মেয়াদ শেষের তারিখ
Cardholder's name:         Card-এ থাকা নাম
```

**Billing address:** "Use my contact address" সিলেক্ট করুন।

**"Verify and Continue"** ক্লিক করুন।

> 💡 **টিপস:** Dutch-Bangla Bank, BRAC Bank, বা যেকোনো Visa/Mastercard কাজ করে। Nagad বা bKash এখানে কাজ করে না।

---

### ধাপ ১.৬ — Phone Verification

আপনার Mobile Number verify করতে হবে:

```
Country code:   +880 (Bangladesh)
Phone number:   আপনার নম্বর
```

**"Send SMS"** বা **"Call me"** সিলেক্ট করুন → OTP পাবেন → দিন → **"Continue"**।

---

### ধাপ ১.৭ — Support Plan বেছে নিন

এখন ৩টি Plan দেখাবে:

| Plan              | মূল্য     | আমাদের জন্য? |
| ----------------- | --------- | ------------ |
| **Basic Support** | ফ্রি      | ✅ এটা নিন   |
| Developer Support | $29/মাস   | ❌ দরকার নেই |
| Business Support  | $100+/মাস | ❌ দরকার নেই |

**"Basic Support - Free"** সিলেক্ট করুন → **"Complete sign up"** ক্লিক করুন।

---

## ✅ সফলভাবে একাউন্ট তৈরি হলো!

AWS একটি confirmation email পাঠাবে। একাউন্ট **সম্পূর্ণ activate হতে ৫-১৫ মিনিট** লাগতে পারে।

---

## 🔑 প্রথমবার Login করুন

১. যান: **https://console.aws.amazon.com**
২. **"Root user"** সিলেক্ট করুন
৩. আপনার email ও password দিন
৪. AWS Console Dashboard দেখতে পাবেন — অভিনন্দন! 🎉

---

## 🔒 নিরাপত্তার জন্য গুরুত্বপূর্ণ পদক্ষেপ (MFA Mandatory)

> 🚨 **গুরুত্বপূর্ণ (২০২৬ আপডেট):** AWS এখন Root User-এর জন্য MFA বাধ্যতামূলক করেছে। একাউন্ট খোলার পরপরই এটি চালু করুন।

Login করার পর **MFA (Multi-Factor Authentication)** চালু করুন:

1. উপরে ডানে আপনার **Account Name** (নতুন ভাবে এখানে নাম দেখায়) এর পাশে ক্লিক করুন।
2. **"Security credentials"** অথবা **"My Security Credentials"** সিলেক্ট করুন।
3. **"Multi-factor authentication (MFA)"** সেকশনে যান।
4. **"Assign MFA device"** ক্লিক করুন।
5. একটি নাম দিন (যেমন: `MyPhone`) এবং **"Authenticator app"** সিলেক্ট করুন।
6. Google Authenticator বা Microsoft Authenticator অ্যাপ দিয়ে QR Code স্ক্যান করুন।
7. পরপর দুটি MFA Code দিন এবং সফলভাবে যুক্ত করুন।

> ✅ এটা করলে আপনার একাউন্ট অনেক বেশি সুরক্ষিত থাকবে এবং AWS-এর নতুন নিয়ম মেনে চলা হবে।

---

## 🗺️ AWS Console-এর সাথে পরিচয় (Modern Cloudscape UI)

Login করার পর যা দেখবেন:

```
┌───────────────────────────────────────────────┐
│  AWS Management Console [Toolbar ▾] [Account] │
│                                               │
│  [Search Bar: Type service name...]           │
│                                               │
│  ┌─────────┐  ┌─────────┐  ┌────────┐         │
│  │   EC2   │  │   S3    │  │  RDS   │         │
│  └─────────┘  └─────────┘  └────────┘         │
└───────────────────────────────────────────────┘
```

> 💡 **নতুন কি?** এখন উপরে ডানে সরাসরি আপনার **Account Name** দেখতে পাবেন (ফেব্রুয়ারি ২০২৬ আপডেট)। আর বামে "Toolbar" দিয়ে দ্রুত বিভিন্ন ফিচার নেভিগেট করা যায়।

> 🌏 **Region মানে কী?** আপনার server কোন দেশে থাকবে তা। Practice-এর জন্য **"Asia Pacific (Singapore) ap-southeast-1"** বেছে নিন — এটা বাংলাদেশের সবচেয়ে কাছের।

**Region পরিবর্তন করুন:**

- উপরে ডানে Region-এর নাম (যেমন: **"N. Virginia"**) এ ক্লিক করুন।
- **"Asia Pacific (Singapore)"** সিলেক্ট করুন।

---

## ✅ এই ধাপ সম্পন্ন! চেকলিস্ট

- [ ] AWS একাউন্ট তৈরি হয়েছে
- [ ] Email confirm করা হয়েছে
- [ ] AWS Console-এ Login করা হয়েছে
- [ ] Region → Singapore সেট করা হয়েছে
- [ ] (ঐচ্ছিক) MFA চালু করা হয়েছে

---

## ➡️ পরবর্তী ধাপ

[**ধাপ ২: EC2 Instance তৈরি ও কনফিগার করুন →**](./02-ec2-instance-setup.md)

---

_সমস্যা হলে নিচে কমেন্ট করুন অথবা AI-কে জিজ্ঞেস করুন।_

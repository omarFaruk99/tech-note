# 📖 Section 08: Text Editor (nano ও vim)

---

## 🎯 এই Section-এ যা শিখবেন

- Terminal-based Text Editor কেন দরকার
- **nano** — সহজ ও beginner-friendly editor
- **vim** — শক্তিশালী ও professional editor
- vim-এর Mode system
- ফাইল তৈরি, edit, save করা
- গুরুত্বপূর্ণ shortcuts ও কমান্ড

## 🔧 এই Section-এর কমান্ড/টুল

| কমান্ড     |  Ubuntu 24 LTS-এ   | মন্তব্য                                 |
| ---------- | :----------------: | --------------------------------------- |
| `nano`     |  ✅ Pre-installed  | সহজ text editor, beginners-এর জন্য      |
| `vi`       |  ✅ Pre-installed  | vim-এর basic version (vim-tiny)         |
| `vim`      | ❌ ইন্সটল করতে হবে | `sudo apt install vim` (full version)   |
| `vimtutor` | ❌ vim-এর সাথে আসে | `sudo apt install vim` করলে পাবেন       |
| `gedit`    | ❌ ইন্সটল করতে হবে | `sudo apt install gedit` (GUI editor)   |
| `code`     | ❌ ইন্সটল করতে হবে | VS Code — `snap install code --classic` |

> 💡 **Ubuntu 24-এ** `nano` আগে থেকেই আছে। `vim` পেতে `sudo apt install vim` চালাতে হবে। `vi` (vim-tiny) আগে থেকে আছে, কিন্তু limited features সহ।

---

## ❓ Terminal-based Text Editor কেন?

আপনি হয়তো ভাবছেন — GUI editor (VS Code, Notepad) থাকতে Terminal editor কেন শিখব?

### কারণগুলো:

1. **Server-এ GUI থাকে না** — SSH দিয়ে remote server-এ ঢুকলে শুধু Terminal পাবেন
2. **দ্রুত সম্পাদনা** — ছোট config ফাইল দ্রুত Edit করতে Terminal editor সেরা
3. **সর্বত্র পাওয়া যায়** — nano/vi প্রায় সব Linux সিস্টেমে থাকে
4. **যেকোনো file edit** — system ফাইল edit করতে `sudo nano` প্রয়োজন
5. **Professional দক্ষতা** — Cybersecurity, DevOps, SysAdmin-এ অত্যাবশ্যক

---

## 📝 nano — সহজ Editor

**nano** হলো সবচেয়ে সহজ terminal text editor। Beginners-এর জন্য এটি সেরা।

### nano খোলা:

```bash
# নতুন ফাইল তৈরি করুন
nano myfile.txt

# বিদ্যমান ফাইল খুলুন
nano /etc/hostname

# sudo দিয়ে system ফাইল edit করুন
sudo nano /etc/hosts
```

### nano-র Interface:

```
  GNU nano 7.2             myfile.txt

এখানে আপনার লেখা দেখাবে
আপনি সরাসরি টাইপ করতে পারেন...



^G Help    ^O Write Out  ^W Where Is  ^K Cut       ^T Execute
^X Exit    ^R Read File  ^\ Replace   ^U Paste     ^J Justify
```

**নিচের বারে যা দেখাচ্ছে:**

- `^` = **Ctrl** key
- `^O` = **Ctrl + O** (Save করা)
- `^X` = **Ctrl + X** (বের হওয়া)

### nano-র গুরুত্বপূর্ণ Shortcuts:

| Shortcut   | কাজ                       | মনে রাখুন         |
| ---------- | ------------------------- | ----------------- |
| `Ctrl + O` | Save (Write **O**ut)      | **O** = Output    |
| `Ctrl + X` | বের হওয়া (E**x**it)      | **X** = eXit      |
| `Ctrl + K` | পুরো লাইন কাটুন (**K**ut) | **K** = Kut (Cut) |
| `Ctrl + U` | Paste করুন (**U**ncut)    | **U** = Uncut     |
| `Ctrl + W` | সার্চ করুন (**W**here is) | **W** = Where     |
| `Ctrl + \` | খুঁজুন ও বদলান (Replace)  | —                 |
| `Ctrl + G` | সাহায্য দেখুন             | **G** = Get help  |
| `Ctrl + _` | নির্দিষ্ট লাইনে যান       | —                 |
| `Alt + U`  | Undo (বাতিল)              | —                 |
| `Alt + E`  | Redo (পুনরায়)            | —                 |
| `Ctrl + C` | বর্তমান লাইন নম্বর দেখুন  | —                 |

### nano-তে ধাপে ধাপে কাজ:

#### ফাইল তৈরি ও সেভ:

```bash
# 1. nano খুলুন
nano hello.txt

# 2. কিছু লিখুন (সরাসরি টাইপ করুন):
Hello! This is my first nano file.
I am learning Linux.

# 3. Save করুন: Ctrl + O
# ফাইলের নাম confirm করতে Enter চাপুন

# 4. বের হোন: Ctrl + X
```

#### ফাইল edit করা:

```bash
# 1. ফাইল খুলুন
nano hello.txt

# 2. Arrow keys দিয়ে cursor সরান
# 3. যেখানে চান সেখানে টাইপ করুন বা মুছুন (Backspace/Delete)
# 4. Save (Ctrl + O) → Exit (Ctrl + X)
```

#### সার্চ ও Replace:

```bash
# nano-তে ফাইল খোলা থাকলে:

# সার্চ: Ctrl + W → search term লিখুন → Enter
# পরবর্তী result: Ctrl + W → Enter (আবার)

# Replace: Ctrl + \ → পুরনো শব্দ → Enter → নতুন শব্দ → Enter
# Y = এটি বদলাও, N = এটি বদলাও না, A = সব বদলাও
```

### Real-Life Use Case:

> ```bash
> # SSH config edit করা
> sudo nano /etc/ssh/sshd_config
>
> # Hosts file edit করা
> sudo nano /etc/hosts
>
> # Bash configuration edit করা
> nano ~/.bashrc
> ```

---

## 🚀 vim — শক্তিশালী Editor

**vim** (Vi IMproved) হলো সবচেয়ে **শক্তিশালী** terminal text editor। এটি শিখতে সময় লাগে, কিন্তু একবার শিখলে এটি সবচেয়ে দ্রুত editor।

### vim ইন্সটল করুন:

```bash
sudo apt install vim
```

> ✅ **ইন্সটলের পর check করুন:**
>
> ```bash
> vim --version | head -1
> ```

### ⚡ vim-এর সবচেয়ে গুরুত্বপূর্ণ বিষয় — MODE SYSTEM

vim-এ কাজ করতে হলে এটি বুঝতেই হবে। vim-এর **৩টি প্রধান Mode** আছে:

```
┌─────────────────────────────────────────────────┐
│                                                  │
│              ┌──────────────┐                    │
│              │ NORMAL MODE  │ ← vim খুললেই      │
│              │   (দেখা ও    │   এই mode-এ থাকে  │
│              │  নেভিগেশন)   │                    │
│              └──────┬───────┘                    │
│                     │                            │
│          i,a,o      │        Esc                  │
│          ┌──────────▼──────────┐                 │
│          │   INSERT MODE       │                 │
│          │   (লেখালেখি)        │                 │
│          └──────────┬──────────┘                 │
│                     │                            │
│                    Esc                            │
│                     │                            │
│          :          ▼                             │
│          ┌──────────────────────┐                │
│          │   COMMAND MODE       │                │
│          │  (save, quit, etc.)  │                │
│          └──────────────────────┘                │
│                                                  │
└─────────────────────────────────────────────────┘
```

| Mode        | কিভাবে যাবেন            | কাজ                       | কখন ব্যবহার             |
| ----------- | ----------------------- | ------------------------- | ----------------------- |
| **Normal**  | `Esc` চাপুন             | দেখা, নেভিগেশন, কপি, মুছা | cursor সরানো, শব্দ মুছা |
| **Insert**  | `i` চাপুন               | টাইপ করা (লেখালেখি)       | নতুন কিছু লিখতে         |
| **Command** | `:` চাপুন (Normal থেকে) | Save, quit, search        | ফাইল সংরক্ষণ ও বন্ধ     |

> 🧠 **মনে রাখুন:** কোন Mode-এ আছেন তা বুঝতে সমস্যা হলে **Esc চাপুন!** এটি সবসময় Normal Mode-এ ফিরিয়ে আনবে।

### vim খোলা:

```bash
# নতুন ফাইল
vim myfile.txt

# বিদ্যমান ফাইল
vim hello.txt

# sudo দিয়ে
sudo vim /etc/hosts
```

### vim-এ প্রথম কাজ — ফাইল তৈরি, edit, save:

```
ধাপ 1: vim খুলুন
$ vim test.txt

ধাপ 2: Insert Mode-এ যান
i চাপুন (নিচে -- INSERT -- দেখাবে)

ধাপ 3: কিছু লিখুন
Hello vim!
This is my first vim file.

ধাপ 4: Normal Mode-এ ফিরুন
Esc চাপুন

ধাপ 5: Save ও Exit
:wq লিখুন → Enter চাপুন
```

### ⚠️ vim থেকে বের হওয়া (সবচেয়ে জরুরি!)

> 🤣 ইন্টারনেটে সবচেয়ে বেশি সার্চ করা প্রশ্নগুলোর একটি: **"How to exit vim?"**

| কমান্ড | কাজ                                    | মনে রাখুন             |
| ------ | -------------------------------------- | --------------------- |
| `:q`   | বের হোন (কোনো পরিবর্তন না থাকলে)       | **q**uit              |
| `:q!`  | পরিবর্তন না সেভ করেই বের হোন (জোর করে) | **q**uit + force**!** |
| `:w`   | Save করুন (বের হবেন না)                | **w**rite             |
| `:wq`  | Save করে বের হোন                       | **w**rite + **q**uit  |
| `:wq!` | জোর করে save করে বের হোন               | —                     |
| `ZZ`   | সেভ ও exit (shortcut)                  | Normal mode-এ         |

> 💡 **সবচেয়ে সহজ:** `:wq` Enter — Save ও Exit!  
> **Save না করে বের হতে:** `:q!` Enter

---

### vim Normal Mode — Navigation:

| Key   | কাজ                | মনে রাখুন       |
| ----- | ------------------ | --------------- |
| `h`   | বাঁয়ে (←)         | —               |
| `j`   | নিচে (↓)           | **j**ump down   |
| `k`   | উপরে (↑)           | **k**ick up     |
| `l`   | ডানে (→)           | —               |
| `0`   | লাইনের শুরুতে      | —               |
| `$`   | লাইনের শেষে        | —               |
| `gg`  | ফাইলের শুরুতে      | **g**o to start |
| `G`   | ফাইলের শেষে        | **G**o to end   |
| `w`   | পরের শব্দে         | **w**ord        |
| `b`   | আগের শব্দে         | **b**ack        |
| `:10` | ১০ নম্বর লাইনে যান | —               |

> 💡 Arrow keys-ও কাজ করে, কিন্তু `hjkl` ব্যবহার করা professional style এবং দ্রুত।

### vim Normal Mode — Edit:

| Key        | কাজ                   | মনে রাখুন           |
| ---------- | --------------------- | ------------------- |
| `x`        | একটি character মুছুন  | —                   |
| `dd`       | পুরো লাইন মুছুন (cut) | **d**elete          |
| `5dd`      | ৫ লাইন মুছুন          | —                   |
| `yy`       | পুরো লাইন কপি করুন    | **y**ank            |
| `5yy`      | ৫ লাইন কপি করুন       | —                   |
| `p`        | নিচে paste করুন       | **p**aste           |
| `P`        | উপরে paste করুন       | —                   |
| `u`        | Undo (বাতিল)          | **u**ndo            |
| `Ctrl + r` | Redo (পুনরায়)        | **r**edo            |
| `dw`       | একটি শব্দ মুছুন       | **d**elete **w**ord |

### vim Insert Mode-এ যাওয়ার বিভিন্ন উপায়:

| Key | কোথায় Insert Mode শুরু হবে | মনে রাখুন           |
| --- | --------------------------- | ------------------- |
| `i` | cursor-এর **আগে**           | **i**nsert          |
| `I` | লাইনের **শুরুতে**           | —                   |
| `a` | cursor-এর **পরে**           | **a**ppend          |
| `A` | লাইনের **শেষে**             | —                   |
| `o` | নিচে **নতুন লাইন** তৈরি করে | **o**pen line below |
| `O` | উপরে **নতুন লাইন** তৈরি করে | —                   |

### vim Command Mode — Search:

```
Normal mode-এ:

/search-term    → নিচের দিকে সার্চ করুন → Enter
?search-term    → উপরের দিকে সার্চ করুন → Enter
n               → পরবর্তী result
N               → আগের result

# Find ও Replace (সব):
:%s/old/new/g   → সব "old" কে "new" দিয়ে বদলান
:%s/old/new/gc  → প্রতিটিতে জিজ্ঞেস করবে (c = confirm)
```

---

## ⚖️ nano vs vim তুলনা

| বিষয়             | nano             | vim                |
| ----------------- | ---------------- | ------------------ |
| শেখার সময়        | ✅ ৫ মিনিট       | ❌ কয়েক সপ্তাহ    |
| গতি (শেখার পর)    | সাধারণ           | ✅ অত্যন্ত দ্রুত   |
| Features          | সীমিত            | ✅ অসীম            |
| Pre-installed     | ✅ Ubuntu-তে আছে | ❌ ইন্সটল করতে হবে |
| Server-এ          | থাকতে পারে       | ✅ vi সবসময় থাকে  |
| Beginner-friendly | ✅ হ্যাঁ         | ❌ না              |
| Professional use  | সাধারণ edit      | ✅ ভারী কাজ        |

> 💡 **পরামর্শ:**
>
> - **এখন → nano ব্যবহার করুন** (সহজ, কাজ হয়ে যায়)
> - **এরই মধ্যে vim শিখতে শুরু করুন** (ভবিষ্যতের জন্য)
> - **vim শিখতে →** Terminal-এ `vimtutor` চালান (interactive tutorial!)

---

## 📊 সব কমান্ডের সারসংক্ষেপ

### nano Quick Reference:

| Shortcut   | কাজ      |
| ---------- | -------- |
| `Ctrl + O` | Save     |
| `Ctrl + X` | Exit     |
| `Ctrl + K` | Cut line |
| `Ctrl + U` | Paste    |
| `Ctrl + W` | Search   |
| `Ctrl + \` | Replace  |
| `Alt + U`  | Undo     |

### vim Quick Reference:

| কমান্ড/Key | Mode            | কাজ               |
| ---------- | --------------- | ----------------- |
| `i`        | Normal → Insert | লিখতে শুরু        |
| `Esc`      | Any → Normal    | Normal-এ ফিরুন    |
| `:w`       | Command         | Save              |
| `:q`       | Command         | Quit              |
| `:wq`      | Command         | Save & Quit       |
| `:q!`      | Command         | Quit without save |
| `dd`       | Normal          | লাইন মুছুন        |
| `yy`       | Normal          | লাইন কপি          |
| `p`        | Normal          | Paste             |
| `u`        | Normal          | Undo              |
| `/text`    | Normal          | Search            |

---

## 🏋️ Practice Exercise

### অনুশীলন ১: nano ব্যবহার

```bash
# 1. nano-তে একটি ফাইল তৈরি করুন
nano ~/linux-practice/my-notes.txt

# 2. নিচের লাইনগুলো লিখুন:
# আজ আমি Linux শিখছি
# nano editor ব্যবহার করছি
# এটি খুবই সহজ!

# 3. Save করুন (Ctrl + O → Enter)

# 4. আরও কিছু লিখুন:
# এটি চতুর্থ লাইন
# পঞ্চম লাইন

# 5. Save ও Exit (Ctrl + O → Enter → Ctrl + X)

# 6. cat দিয়ে পড়ে দেখুন
cat ~/linux-practice/my-notes.txt
```

### অনুশীলন ২: vim ইন্সটল ও প্রথম ব্যবহার

```bash
# 1. vim ইন্সটল করুন
sudo apt install -y vim

# 2. vim-এ একটি ফাইল খুলুন
vim ~/linux-practice/vim-test.txt

# 3. i চাপুন (Insert Mode)
# 4. লিখুন: "Hello from vim!"
# 5. Esc চাপুন (Normal Mode)
# 6. :wq Enter (Save ও Exit)

# 7. cat দিয়ে পড়ুন
cat ~/linux-practice/vim-test.txt
```

### অনুশীলন ৩: vim Navigation

```bash
# 1. /etc/passwd ফাইল vim-এ খুলুন (read-only)
vim /etc/passwd

# 2. Navigate করুন:
#    gg → ফাইলের শুরুতে
#    G  → ফাইলের শেষে
#    /root → "root" সার্চ
#    :10 → ১০ নম্বর লাইনে
#    :q → বের হোন

# 3. vimtutor চালান (২০-৩০ মিনিটের tutorial)
vimtutor
```

### অনুশীলন ৪: Real Config File Edit

```bash
# 1. nano দিয়ে .bashrc edit করুন
nano ~/.bashrc

# 2. ফাইলের শেষে এই লাইন যোগ করুন:
# # My custom alias
# alias ll='ls -la'
# alias update='sudo apt update && sudo apt upgrade -y'

# 3. Save (Ctrl + O) ও Exit (Ctrl + X)

# 4. Reload করুন
source ~/.bashrc

# 5. এখন চেষ্টা করুন
ll       # ls -la চলবে
update   # full update চলবে
```

---

## 🎉 Phase 2 Complete!

অভিনন্দন! 🎊 আপনি **Phase 2: Permission, User ও Package Management** সম্পূর্ণ করেছেন!

### এই Phase-এ যা শিখলেন:

- ✅ File Permissions (rwx) ও chmod, chown, sudo
- ✅ User তৈরি, পরিবর্তন, মুছা ও Group Management
- ✅ Package Management (apt, dpkg, snap)
- ✅ Text Editors (nano ও vim)

### পরবর্তী Phase:

**[Phase 3: System Management →](../phase-03/section-09.md)**

Phase 3-তে শিখবেন:

- Process Management — চলমান প্রোগ্রাম নিয়ন্ত্রণ
- System Information ও Monitoring
- Service Management (systemd)
- Disk ও Storage Management

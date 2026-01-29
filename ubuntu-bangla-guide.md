# Ubuntu 24.04 - সম্পূর্ণ বাংলা গাইড
## দৈনন্দিন ব্যবহার এবং আত্মবিশ্বাস বৃদ্ধির জন্য

---

## 📑 সূচিপত্র
1. [Ubuntu পরিচিতি](#ubuntu-পরিচিতি)
2. [Desktop Environment বুঝুন](#desktop-environment-বুঝুন)
3. [File System এবং File Management](#file-system-এবং-file-management)
4. [Software Installation এবং Management](#software-installation-এবং-management)
5. [Terminal/Command Line বেসিক](#terminalcommand-line-বেসিক)
6. [System Settings এবং Customization](#system-settings-এবং-customization)
7. [Networking এবং Internet](#networking-এবং-internet)
8. [দৈনন্দিন কাজের Software](#দৈনন্দিন-কাজের-software)
9. [System Maintenance](#system-maintenance)
10. [Troubleshooting এবং সমস্যা সমাধান](#troubleshooting-এবং-সমস্যা-সমাধান)

---

## Ubuntu পরিচিতি

### Ubuntu কি?
Ubuntu হলো একটি **free** এবং **open-source** Linux-based operating system। এটি Debian Linux এর উপর ভিত্তি করে তৈরি এবং Canonical Ltd. দ্বারা পরিচালিত।

### Ubuntu 24.04 LTS বিশেষত্ব
- **LTS (Long Term Support)**: ৫ বছরের সাপোর্ট (২০২৯ পর্যন্ত)
- **GNOME 46 Desktop Environment**
- আরও দ্রুত এবং স্থিতিশীল
- উন্নত security features

### Windows থেকে পার্থক্য

| বিষয় | Windows | Ubuntu |
|------|---------|--------|
| **মূল্য** | টাকা দিয়ে কিনতে হয় | সম্পূর্ণ বিনামূল্যে |
| **ভাইরাস** | বেশি ঝুঁকি | খুবই কম ঝুঁকি |
| **Updates** | জোরপূর্বক update | আপনার নিয়ন্ত্রণে |
| **Customization** | সীমিত | সম্পূর্ণ স্বাধীনতা |
| **File System** | C:, D: drive | / (root) থেকে শুরু |

---

## Desktop Environment বুঝুন

### GNOME Desktop পরিচিতি

Ubuntu 24.04 এ **GNOME** desktop environment ব্যবহৃত হয়।

#### মূল উপাদান:

**১. Top Bar (উপরের বার)**
- বাম পাশে: Activities বাটন
- মাঝখানে: বর্তমান সময় ও তারিখ
- ডান পাশে: System tray (volume, network, battery, power)

**২. Activities Overview**
- উপরে বাম কোণে "Activities" ক্লিক করুন অথবা **Super Key** (Windows key) চাপুন
- এখানে পাবেন:
  - খোলা সব window
  - Search bar (যেকোনো কিছু খুঁজতে)
  - Workspaces (ডান পাশে)

**৩. Dash/Dock (বাম পাশের বার)**
- পছন্দের application এর shortcut
- চলমান application দেখায়
- যেকোনো app pin করতে: right-click → "Add to Favorites"

**৪. Application Grid**
- Activities → নিচে ৯ বিন্দু আইকন ক্লিক করুন
- সব installed application এখানে পাবেন
- Windows এর Start Menu এর মতো

### কিবোর্ড শর্টকাট (দ্রুত কাজের জন্য অবশ্যই শিখুন)

#### অতি প্রয়োজনীয়:
- **Super (Windows key)**: Activities খুলুন
- **Super + L**: Lock screen
- **Super + D**: Desktop দেখান
- **Alt + Tab**: Applications এর মধ্যে switch
- **Alt + F4**: বর্তমান window বন্ধ করুন
- **Ctrl + Alt + T**: Terminal খুলুন
- **Super + A**: Application grid খুলুন
- **Ctrl + C**: Copy (terminal এ Ctrl+Shift+C)
- **Ctrl + V**: Paste (terminal এ Ctrl+Shift+V)
- **Ctrl + Z**: Undo
- **Ctrl + S**: Save

#### Screenshot:
- **PrtScn**: পুরো screen
- **Shift + PrtScn**: নির্দিষ্ট area
- **Alt + PrtScn**: বর্তমান window

#### Workspace Management:
- **Super + Page Up/Down**: Workspace পরিবর্তন
- **Shift + Super + Page Up/Down**: বর্তমান window অন্য workspace এ নিয়ে যান

---

## File System এবং File Management

### Linux File System Structure

Windows এ আপনি দেখতেন C:, D: drive। Linux এ সব কিছু **/** (root) থেকে শুরু হয়।

#### গুরুত্বপূর্ণ Directories:

```
/
├── home/          → আপনার ব্যক্তিগত files (Windows এর C:\Users এর মতো)
│   └── [username]/
│       ├── Desktop/
│       ├── Documents/
│       ├── Downloads/
│       ├── Music/
│       ├── Pictures/
│       ├── Videos/
│       └── Public/
│
├── etc/           → System configuration files
├── usr/           → User programs এবং applications
├── var/           → Variable data (logs, cache)
├── tmp/           → Temporary files
├── opt/           → Optional software
├── bin/           → Essential user commands
└── boot/          → Boot loader files
```

#### আপনার Home Directory:
- Location: `/home/আপনার-username/`
- Shortcut: `~` (tilde চিহ্ন দিয়ে লেখা যায়)
- এটাই আপনার প্রধান কাজের জায়গা

### Files Application (File Manager)

**খোলার উপায়:**
- Activities → "Files" লিখুন
- Dash থেকে folder আইকন ক্লিক করুন

#### মূল Features:

**১. বাম Sidebar:**
- Starred: গুরুত্বপূর্ণ folder
- Home: আপনার home directory
- Desktop, Documents, Downloads, etc.
- Other Locations: অন্য partition/drive

**২. File Operations:**
- **কপি করা**: Ctrl+C অথবা right-click → Copy
- **কাট করা**: Ctrl+X অথবা right-click → Cut
- **পেস্ট করা**: Ctrl+V অথবা right-click → Paste
- **মুছে ফেলা**: Delete key অথবা right-click → Move to Trash
- **স্থায়ীভাবে মুছে ফেলা**: Shift+Delete
- **নাম পরিবর্তন**: F2 অথবা right-click → Rename

**৩. Hidden Files:**
- **দেখার উপায়**: Ctrl+H
- Linux এ যেসব file/folder নাম `.` দিয়ে শুরু, সেগুলো hidden
- উদাহরণ: `.bashrc`, `.config/`

**৪. File Properties:**
- Right-click → Properties
- এখানে দেখতে পাবেন:
  - Size, Type, Modified date
  - Permissions (কে file টি দেখতে/edit করতে পারবে)
  - Open With (কোন program দিয়ে খুলবেন)

### File Permissions (গুরুত্বপূর্ণ concept)

Linux এ প্রতিটি file এর ৩ ধরনের permission আছে:
- **r (read)**: পড়তে পারবে
- **w (write)**: লিখতে/edit করতে পারবে
- **x (execute)**: চালাতে পারবে (program হলে)

৩ ধরনের user এর জন্য:
- **Owner**: file এর মালিক
- **Group**: নির্দিষ্ট group
- **Others**: বাকি সবাই

**Permission পরিবর্তন করা:**
Right-click → Properties → Permissions tab

---

## Software Installation এবং Management

Ubuntu তে software install করার ৪টি প্রধান উপায়:

### ১. Ubuntu Software (GUI - সবচেয়ে সহজ)

**খোলার উপায়:**
- Activities → "Software" টাইপ করুন
- অথবা Dash থেকে shopping bag আইকন

**কিভাবে ব্যবহার করবেন:**
1. Software Center খুলুন
2. Search করুন অথবা categories ব্রাউজ করুন
3. Install বাটন ক্লিক করুন
4. Password দিন

**জনপ্রিয় Software:**
- **VLC**: Video player
- **GIMP**: Image editing (Photoshop এর মতো)
- **LibreOffice**: Office suite (MS Office এর মতো)
- **Chrome/Firefox**: Web browsers
- **Spotify**: Music streaming

### ২. APT (Terminal থেকে - দ্রুত এবং powerful)

**APT কি?**
Advanced Package Tool - Ubuntu এর package manager।

**মূল Commands:**

```bash
# Software list update করুন (সবসময় প্রথমে এটা করুন)
sudo apt update

# System upgrade করুন
sudo apt upgrade

# নতুন software install
sudo apt install [package-name]
# উদাহরণ:
sudo apt install vlc
sudo apt install gimp

# একসাথে অনেক software install
sudo apt install vlc gimp htop

# Software remove করুন
sudo apt remove [package-name]

# Software এবং তার configuration file মুছুন
sudo apt purge [package-name]

# অব্যবহৃত packages মুছুন
sudo apt autoremove

# Software খুঁজুন
apt search [keyword]
# উদাহরণ:
apt search "video player"

# Software এর details দেখুন
apt show [package-name]
```

**ব্যবহারিক উদাহরণ:**
```bash
# প্রথমে update করুন
sudo apt update

# এরপর software install করুন
sudo apt install vlc firefox

# Install করার সময় "Y" চাপুন confirm করতে
```

### ৩. Snap Packages

**Snap কি?**
Canonical এর নতুন universal package format। সব dependency সাথে আসে।

**মূল Commands:**
```bash
# Snap install
sudo snap install [package-name]

# উদাহরণ:
sudo snap install vlc
sudo snap install code  # VS Code
sudo snap install spotify

# Installed snaps দেখুন
snap list

# Snap remove করুন
sudo snap remove [package-name]

# Snap খুঁজুন
snap find [keyword]
```

### ৪. .deb Files (Windows এর .exe এর মতো)

কিছু software তাদের website থেকে .deb file দেয়।

**Install করার উপায়:**

**Method 1: GUI দিয়ে**
1. .deb file download করুন
2. File এ double-click করুন
3. Software Center খুলবে
4. Install বাটন ক্লিক করুন

**Method 2: Terminal দিয়ে**
```bash
cd Downloads/
sudo dpkg -i package-name.deb

# যদি error আসে dependency এর জন্য:
sudo apt install -f
```

**জনপ্রিয় .deb Software:**
- Google Chrome
- Microsoft Edge
- TeamViewer
- Zoom

### Software Update করা

**GUI থেকে:**
- Software Updater automatically খুলবে
- অথবা Activities → "Software Updater"

**Terminal থেকে:**
```bash
sudo apt update && sudo apt upgrade -y
```

**Snap software update:**
```bash
sudo snap refresh
```

---

## Terminal/Command Line বেসিক

Terminal হলো Ubuntu এর সবচেয়ে powerful tool। ভয় পাবেন না, ধীরে ধীরে শিখবেন!

### Terminal খোলার উপায়
- **Ctrl + Alt + T** (সবচেয়ে দ্রুত)
- Activities → "Terminal" টাইপ করুন

### Terminal বুঝুন

যখন Terminal খুলবেন, দেখবেন:
```
username@computername:~$
```

- **username**: আপনার user name
- **computername**: আপনার computer এর নাম
- **~**: বর্তমান location (~ মানে home directory)
- **$**: সাধারণ user (# হলে root user)

### মৌলিক Commands (অবশ্যই শিখতে হবে)

#### ১. Navigation (চলাচল)

```bash
# বর্তমান directory দেখুন
pwd
# Output: /home/username

# Directory এর contents দেখুন
ls

# Details সহ দেখুন
ls -l

# Hidden files সহ দেখুন
ls -a

# সবকিছু একসাথে
ls -lah

# Directory পরিবর্তন করুন
cd [directory-name]

# উদাহরণ:
cd Documents/
cd Downloads/

# এক level উপরে যান
cd ..

# Home directory তে যান
cd ~
# অথবা শুধু
cd

# আগের directory তে ফিরে যান
cd -

# Root directory তে যান
cd /
```

#### ২. File এবং Directory Operations

```bash
# নতুন directory তৈরি করুন
mkdir [folder-name]
# উদাহরণ:
mkdir MyProjects

# একসাথে nested directories তৈরি
mkdir -p Projects/Web/HTML

# নতুন file তৈরি করুন
touch [filename]
# উদাহরণ:
touch myfile.txt

# File copy করুন
cp [source] [destination]
# উদাহরণ:
cp file.txt backup.txt

# Directory copy করুন
cp -r [source-folder] [destination-folder]

# File/Folder move করুন (বা rename করুন)
mv [source] [destination]
# উদাহরণ:
mv oldname.txt newname.txt
mv file.txt Documents/

# File/Folder মুছুন
rm [filename]

# Directory মুছুন
rm -r [foldername]

# জোরপূর্বক মুছুন (সাবধান!)
rm -rf [foldername]
```

#### ৩. File দেখা এবং Edit করা

```bash
# File এর content দেখুন
cat [filename]

# বড় file page by page দেখুন
less [filename]
# (Space: next page, q: quit)

# File এর প্রথম 10 line দেখুন
head [filename]

# File এর শেষ 10 line দেখুন
tail [filename]

# File edit করুন (nano editor - সহজ)
nano [filename]
# Save: Ctrl+O, Exit: Ctrl+X

# File edit করুন (gedit - GUI)
gedit [filename]
```

#### ৪. System Information

```bash
# Current user দেখুন
whoami

# Computer এর hostname
hostname

# System information
uname -a

# Ubuntu version দেখুন
lsb_release -a

# Disk space দেখুন
df -h

# Directory size দেখুন
du -sh [directory]

# Memory usage দেখুন
free -h

# চলমান processes দেখুন
top
# (q চাপলে বন্ধ হবে)

# আরও ভালো process viewer
htop
# (install করতে হবে: sudo apt install htop)
```

#### ৫. Search এবং Find

```bash
# File খুঁজুন
find [path] -name [filename]
# উদাহরণ:
find ~ -name "*.txt"
find /home -name "myfile.pdf"

# File এর ভিতরে text খুঁজুন
grep [text] [filename]
# উদাহরণ:
grep "hello" file.txt

# Recursively সব file এ খুঁজুন
grep -r "search-term" [directory]
```

#### ৬. Permissions এবং Ownership

```bash
# File permissions দেখুন
ls -l [filename]

# Permission পরিবর্তন করুন
chmod [permissions] [filename]
# উদাহরণ:
chmod +x script.sh  # Executable করুন
chmod 755 file.txt
chmod 644 file.txt

# File এর owner পরিবর্তন করুন
sudo chown [user]:[group] [filename]
```

#### ৭. Network Commands

```bash
# Internet connection test করুন
ping google.com
# (Ctrl+C চাপলে বন্ধ হবে)

# Network configuration দেখুন
ip addr
# অথবা
ifconfig

# Download করুন
wget [URL]

# আরও advanced download
curl -O [URL]

# Speed test (install করতে হবে)
speedtest-cli
```

### Command Line Tips

**১. Tab Completion:**
- File/folder name টাইপ করা শুরু করে Tab চাপুন
- Automatically complete হবে

**২. Command History:**
- উপর/নিচ arrow key দিয়ে আগের commands দেখুন
- `history` লিখে সব command দেখুন

**৩. Clear Screen:**
- `clear` অথবা Ctrl+L

**৪. Cancel Command:**
- Ctrl+C

**৫. Multiple Commands:**
```bash
# একসাথে চালান (একটা fail হলেও পরেরটা চলবে)
command1 ; command2

# একটা success হলে পরেরটা চলবে
command1 && command2

# একটা fail হলে পরেরটা চলবে
command1 || command2
```

**৬. Output Redirect করা:**
```bash
# Output file এ save করুন
command > output.txt

# Output add করুন (overwrite না করে)
command >> output.txt

# Error redirect করুন
command 2> error.txt
```

---

## System Settings এবং Customization

### Settings খুলুন
- Activities → "Settings" টাইপ করুন
- অথবা top bar → Power icon → Settings

### গুরুত্বপূর্ণ Settings

#### ১. Wi-Fi (Internet Connection)

**Path:** Settings → Wi-Fi

- Available networks দেখুন
- Network select করে password দিন
- "Connect automatically" চেক করুন

**Terminal থেকে:**
```bash
# Wi-Fi on/off করুন
nmcli radio wifi on
nmcli radio wifi off

# Available networks দেখুন
nmcli device wifi list

# Connect করুন
nmcli device wifi connect [SSID] password [password]
```

#### ২. Bluetooth

**Path:** Settings → Bluetooth

- Bluetooth on করুন
- Device scan করুন
- Pair করুন

#### ৩. Display Settings

**Path:** Settings → Displays

- **Resolution**: Screen resolution পরিবর্তন করুন
- **Scale**: Text size পরিবর্তন করুন (100%, 125%, 150%, 200%)
- **Night Light**: রাতে screen লাল করুন (চোখের জন্য ভালো)
- **Multiple Monitors**: একাধিক monitor setup

#### ৪. Appearance (Look পরিবর্তন করুন)

**Path:** Settings → Appearance

- **Style**: Light/Dark mode
- **Background**: Wallpaper পরিবর্তন করুন
- **Desktop Icons**: Show/hide করুন

**Custom Wallpaper:**
1. Pictures folder এ image রাখুন
2. Settings → Appearance → Background
3. Add Picture

#### ৫. Sound

**Path:** Settings → Sound

- **Output**: Speaker/Headphone select করুন
- **Input**: Microphone select করুন
- **Volume**: System volume নিয়ন্ত্রণ
- **Alert Sound**: System notification sound

#### ৬. Power Management

**Path:** Settings → Power

- **Power Mode**: Performance/Balanced/Power Saver
- **Screen Blank**: কত সময় পরে screen off হবে
- **Automatic Suspend**: Auto sleep
- **Battery Percentage**: Show করুন (laptop এ)

**Laptop ব্যবহারকারীদের জন্য:**
- "Power Saver" mode চালু করুন battery save করতে
- Screen Blank time কমান

#### ৭. Mouse & Touchpad

**Path:** Settings → Mouse & Touchpad

**Mouse:**
- Mouse speed
- Natural scrolling (যেভাবে scroll করবেন)

**Touchpad:**
- Tap to Click চালু করুন
- Two-finger scrolling
- Touchpad speed

#### ৮. Keyboard Shortcuts

**Path:** Settings → Keyboard → View and Customize Shortcuts

এখানে সব shortcuts দেখতে পাবেন এবং customize করতে পারবেন।

**নিজের shortcut বানান:**
1. Scroll down → Custom Shortcuts
2. + বাটন ক্লিক করুন
3. Name এবং Command দিন
4. Set Shortcut দিয়ে key combination চাপুন

#### ৯. Users (নতুন user যোগ করা)

**Path:** Settings → Users

- **Add User**: নতুন user account
- **Automatic Login**: Enable/disable করুন
- **Password**: পরিবর্তন করুন
- **User Type**: Administrator/Standard

#### ১০. Date & Time

**Path:** Settings → Date & Time

- **Automatic Date & Time**: চালু রাখুন
- **Time Zone**: সঠিক time zone select করুন
- **Time Format**: 12-hour/24-hour

#### ১১. Region & Language

**Path:** Settings → Region & Language

- **Language**: System language পরিবর্তন
- **Input Sources**: Keyboard layout যোগ করুন

**বাংলা Keyboard যোগ করা:**
1. Input Sources → + বাটন
2. "Bangla" খুঁজুন
3. Select করুন

**Switch করা:**
- Super + Space

#### ১২. Privacy & Security

**Path:** Settings → Privacy & Security

**Screen Lock:**
- Automatic Screen Lock চালু করুন
- Lock delay set করুন

**File History:**
- Recently Used clear করুন

**Location Services:**
- Apps কে location access দিন/না দিন

---

## Networking এবং Internet

### Browser ব্যবহার

**Pre-installed:**
- **Firefox**: Default browser

**অন্যান্য জনপ্রিয় Browsers:**
```bash
# Google Chrome install
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb

# Brave Browser
sudo snap install brave

# Microsoft Edge
sudo apt install microsoft-edge-stable
```

### Network Troubleshooting

**১. Internet connection check:**
```bash
# Google ping করুন
ping -c 4 google.com

# DNS check করুন
nslookup google.com

# Network interfaces দেখুন
ip addr show
```

**২. Wi-Fi restart করুন:**
```bash
# Network Manager restart
sudo systemctl restart NetworkManager

# অথবা
nmcli networking off
nmcli networking on
```

**৩. Speed test:**
```bash
# Install করুন
sudo apt install speedtest-cli

# Test করুন
speedtest-cli
```

### File Sharing

**Network এর মাধ্যমে file share করা:**

**১. Local Network Sharing (Same Wi-Fi):**

Files app → right-click folder → Local Network Share → Share this folder

**২. USB Transfer:**
- USB plug করুন
- Automatically mount হবে
- Files app এর বাম sidebar এ দেখা যাবে

**৩. Cloud Storage:**
- Google Drive: Web browser দিয়ে
- OneDrive: rclone ব্যবহার করে
- Dropbox: Official app আছে

---

## দৈনন্দিন কাজের Software

### ১. Office Suite

**LibreOffice (Pre-installed)**
- **Writer**: Word processing (MS Word এর মতো)
- **Calc**: Spreadsheet (MS Excel এর মতো)
- **Impress**: Presentations (MS PowerPoint এর মতো)

**OnlyOffice (Alternative):**
```bash
sudo snap install onlyoffice-desktopeditors
```

**WPS Office (MS Office এর কাছাকাছি):**
Download from wps.com

### ২. Web Browsers

আগেই আলোচনা করা হয়েছে। Firefox, Chrome, Brave, Edge সব আছে।

### ৩. Email Clients

**Thunderbird:**
```bash
sudo apt install thunderbird
```

**Evolution (Pre-installed):**
- GNOME এর default email client

### ৪. Media Players

**Video:**
- **VLC**: সর্বোত্তম
```bash
sudo apt install vlc
```

- **MPV**: lightweight
```bash
sudo apt install mpv
```

**Music:**
- **Rhythmbox**: Pre-installed
- **Spotify**:
```bash
sudo snap install spotify
```

### ৫. Image Viewers & Editors

**Viewer:**
- **Eye of GNOME**: Pre-installed

**Editors:**
- **GIMP** (Photoshop alternative):
```bash
sudo apt install gimp
```

- **Krita** (Digital painting):
```bash
sudo apt install krita
```

- **Inkscape** (Vector graphics):
```bash
sudo apt install inkscape
```

### ৬. PDF Reader

**Evince**: Pre-installed

**Alternatives:**
```bash
# Okular
sudo apt install okular

# Master PDF Editor
sudo snap install master-pdf-editor
```

### ৭. Video Conferencing

```bash
# Zoom
# Download .deb from zoom.us

# Skype
sudo snap install skype

# Microsoft Teams
# Download .deb from microsoft.com
```

### ৮. Download Managers

```bash
# uGet
sudo apt install uget

# Transmission (Torrent)
sudo apt install transmission
```

### ৯. Text Editors

**Simple:**
- **gedit**: Pre-installed
- **nano**: Terminal based

**Advanced (Programming জন্য):**
```bash
# VS Code
sudo snap install code --classic

# Sublime Text
sudo snap install sublime-text --classic

# Vim
sudo apt install vim
```

### ১০. Screenshot Tools

**Built-in:**
- PrtScn key ব্যবহার করুন

**Advanced:**
```bash
# Flameshot
sudo apt install flameshot
```

### ১১. Screen Recording

```bash
# SimpleScreenRecorder
sudo apt install simplescreenrecorder

# OBS Studio
sudo apt install obs-studio
```

### ১২. Archive Managers

**File-Roller**: Pre-installed (.zip, .tar.gz, .rar support)

**Additional formats:**
```bash
sudo apt install unrar p7zip-full p7zip-rar
```

---

## System Maintenance

### Daily/Weekly Tasks

#### ১. System Update (সবচেয়ে গুরুত্বপূর্ণ)

**প্রতি সপ্তাহে করুন:**
```bash
# Package list update করুন
sudo apt update

# সব software upgrade করুন
sudo apt upgrade -y

# System packages upgrade করুন
sudo apt full-upgrade -y

# Snap update
sudo snap refresh
```

**একসাথে সব:**
```bash
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```

#### ২. Disk Cleanup

**অপ্রয়োজনীয় packages মুছুন:**
```bash
# Unused packages
sudo apt autoremove -y

# Package cache clean করুন
sudo apt clean

# Old kernels মুছুন (সাবধানে!)
sudo apt autoremove --purge
```

**Disk space check করুন:**
```bash
# Overall disk usage
df -h

# Folder size দেখুন
du -sh /*
du -sh ~/Downloads

# বড় files খুঁজুন (1GB+)
find ~ -type f -size +1G
```

**GUI থেকে:**
- **Disk Usage Analyzer** (Baobab):
```bash
sudo apt install baobab
```

#### ৩. Trash Empty করা

**GUI:**
- Files app → Trash → Empty Trash

**Terminal:**
```bash
rm -rf ~/.local/share/Trash/*
```

#### ৪. Log Files Cleanup

```bash
# System logs check করুন
journalctl --disk-usage

# Logs clean করুন (older than 7 days)
sudo journalctl --vacuum-time=7d

# Or size limit (keep only 500MB)
sudo journalctl --vacuum-size=500M
```

### System Monitoring

#### ১. System Monitor (GUI)

Activities → "System Monitor" টাইপ করুন

দেখতে পাবেন:
- **Processes**: চলমান programs
- **Resources**: CPU, Memory, Network usage
- **File Systems**: Disk usage

#### ২. Terminal Monitoring

```bash
# Real-time processes
top

# Better version (install করতে হবে)
sudo apt install htop
htop

# Memory usage
free -h

# Disk I/O
iostat

# Network usage
sudo apt install nethogs
sudo nethogs
```

### Backup Strategy

#### ১. Important Files Backup

**Manual Backup:**
- External hard drive বা USB তে copy করুন
- Cloud storage (Google Drive, Dropbox) ব্যবহার করুন

**GUI Tool:**
```bash
# Deja Dup (Backup tool)
sudo apt install deja-dup
```

#### ২. System Backup (Timeshift)

**Timeshift install করুন:**
```bash
sudo apt install timeshift
```

**Setup:**
1. Timeshift খুলুন
2. RSYNC select করুন
3. Backup location select করুন
4. Snapshot schedule set করুন (Weekly recommended)
5. Filters set করুন (Home directory include/exclude)

**Snapshot create করুন:**
```bash
sudo timeshift --create --comments "Before major update"
```

**Restore করুন:**
```bash
sudo timeshift --restore
```

### Performance Optimization

#### ১. Startup Applications

অপ্রয়োজনীয় startup programs disable করুন:

```bash
# Startup Applications খুলুন
gnome-session-properties
```

অথবা install করুন:
```bash
sudo apt install gnome-startup-applications
```

#### ২. GNOME Extensions

Extensions install করে customize করুন:

```bash
# Extension manager install
sudo apt install gnome-shell-extension-manager
```

**Recommended Extensions:**
- Dash to Dock: Dock customize করুন
- User Themes: Theme পরিবর্তন করুন
- Clipboard Indicator: Clipboard history
- CPU Power Manager: CPU control করুন

#### ৩. Disable Unnecessary Services

```bash
# চলমান services দেখুন
systemctl list-unit-files --state=enabled

# Service disable করুন (example)
sudo systemctl disable bluetooth.service
```

#### ৪. Swap Management

```bash
# Swap usage দেখুন
swapon --show

# Swappiness check করুন (default 60)
cat /proc/sys/vm/swappiness

# Swappiness কমান (recommended 10 for SSD)
sudo sysctl vm.swappiness=10

# Permanent করুন
echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
```

---

## Troubleshooting এবং সমস্যা সমাধান

### সাধারণ সমস্যা ও সমাধান

#### ১. System Slow বা Freeze হচ্ছে

**Diagnosis:**
```bash
# CPU usage দেখুন
top
# (P চাপলে CPU sort করবে)

# Memory usage দেখুন
free -h

# Disk usage দেখুন
df -h
```

**Solutions:**
- Heavy programs বন্ধ করুন
- Startup applications কমান
- Swap space বাড়ান
- RAM upgrade করুন (hardware)

**Emergency: Unresponsive system**
- Ctrl + Alt + F2 (TTY2 তে যাবেন)
- Login করুন
- `top` চালিয়ে problematic process kill করুন:
```bash
kill -9 [PID]
```
- Ctrl + Alt + F1 দিয়ে GUI তে ফিরে আসুন

#### ২. Wi-Fi Connect হচ্ছে না

**Solutions:**
```bash
# Network Manager restart
sudo systemctl restart NetworkManager

# Wi-Fi driver reinstall
sudo apt install --reinstall [your-wifi-driver]

# Check if blocked
rfkill list
# If blocked:
sudo rfkill unblock wifi
```

#### ৩. Sound কাজ করছে না

**Solutions:**
```bash
# PulseAudio restart
pulseaudio -k
pulseaudio --start

# ALSA check
alsamixer
# (M চাপলে unmute করুন)

# Sound packages reinstall
sudo apt install --reinstall alsa-base pulseaudio
```

#### ৪. Screen Brightness Control করতে পারছি না

**Solutions:**
```bash
# Manual brightness control
sudo nano /etc/default/grub

# এই line খুঁজুন:
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"

# পরিবর্তন করুন:
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi_backlight=vendor"

# Save করে update করুন:
sudo update-grub
sudo reboot
```

#### ৫. Printer Setup করতে পারছি না

**Solutions:**
```bash
# CUPS (Printing system) install
sudo apt install cups

# CUPS service চালু করুন
sudo systemctl start cups
sudo systemctl enable cups

# Printer setup করুন
system-config-printer
```

#### ৬. External Drive Mount হচ্ছে না

**Solutions:**
```bash
# Available drives দেখুন
lsblk

# Manually mount করুন
sudo mkdir /mnt/mydrive
sudo mount /dev/sdb1 /mnt/mydrive

# NTFS support install করুন
sudo apt install ntfs-3g

# exFAT support
sudo apt install exfat-fuse exfat-utils
```

#### ৭. Software Install হচ্ছে না

**Solutions:**
```bash
# Broken packages fix করুন
sudo apt --fix-broken install

# Package cache clean করুন
sudo apt clean
sudo apt autoclean

# Sources list reset করুন
sudo rm /var/lib/apt/lists/* -vf
sudo apt update
```

#### ৮. Grub/Boot Problems

**If system boot হচ্ছে না:**

1. Live USB boot করুন
2. Terminal খুলুন:

```bash
# Disk identify করুন
sudo fdisk -l

# Root partition mount করুন
sudo mount /dev/sda1 /mnt

# Grub repair
sudo grub-install --root-directory=/mnt /dev/sda
sudo update-grub
```

#### ৯. Forgot Password

**Recovery mode থেকে:**
1. Restart করুন
2. GRUB menu তে "Advanced options"
3. "Recovery mode" select করুন
4. "root" shell select করুন
5. Password reset করুন:

```bash
# File system remount করুন
mount -o remount,rw /

# Password পরিবর্তন করুন
passwd username

# Reboot
reboot
```

### Log Files Check করা

যেকোনো সমস্যা হলে logs দেখুন:

```bash
# System logs
sudo journalctl -xe

# Last boot logs
journalctl -b

# Specific service logs
journalctl -u NetworkManager

# Kernel messages
dmesg

# Xorg logs (Display issues)
cat /var/log/Xorg.0.log
```

### Package Dependency Issues

```bash
# Broken dependencies fix
sudo apt --fix-broken install

# Force install/remove
sudo dpkg --configure -a

# Clean all
sudo apt clean && sudo apt autoclean && sudo apt autoremove
```

### System Not Booting (Black Screen)

**Try:**
1. Boot করার সময় "e" চাপুন (GRUB এ)
2. "quiet splash" এর পরিবর্তে "nomodeset" লিখুন
3. F10 চাপুন boot করতে

**Permanent fix:**
```bash
sudo nano /etc/default/grub
# GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset"
sudo update-grub
```

---

## বোনাস টিপস এবং ট্রিক্স

### ১. System Information দ্রুত দেখা

```bash
# Hardware info
sudo apt install neofetch
neofetch

# Detailed hardware
sudo apt install hardinfo
hardinfo

# CPU info
lscpu

# GPU info
lspci | grep VGA

# USB devices
lsusb
```

### ২. Terminal Productivity

**Aliases তৈরি করুন (shortcuts):**
```bash
# .bashrc edit করুন
nano ~/.bashrc

# নিচের lines যোগ করুন:
alias update='sudo apt update && sudo apt upgrade -y'
alias install='sudo apt install'
alias remove='sudo apt remove'
alias clean='sudo apt autoremove -y && sudo apt clean'

# Save করে reload করুন:
source ~/.bashrc
```

এখন শুধু `update` লিখলেই system update হবে!

### ৩. Mouse সঙ্গে Text Copy-Paste

Terminal এ:
- **Select করলেই copy হয়ে যায়**
- **Middle click করলে paste হয়**

### ৪. Quick File Preview

```bash
# File preview without opening
cat filename
head filename
tail filename

# Code syntax highlighting সহ preview
sudo apt install bat
bat filename
```

### ৫. System Theme পরিবর্তন

```bash
# GNOME Tweaks install
sudo apt install gnome-tweaks

# Popular themes:
# Yaru (default Ubuntu theme)
# Adwaita
# Nordic
# Dracula

# Theme install করতে:
# 1. gnome-look.org থেকে download
# 2. Extract করে ~/.themes/ তে রাখুন
# 3. GNOME Tweaks দিয়ে apply করুন
```

### ৬. Keyboard Shortcuts Cheat Sheet

একটা file তৈরি করুন সব shortcuts এর:
```bash
nano ~/shortcuts.txt
```

এবং সব গুরুত্বপূর্ণ shortcuts লিখে রাখুন।

### ৭. Auto-mounting Partitions

অন্য partition automatically mount করার জন্য:

```bash
# UUID খুঁজুন
sudo blkid

# fstab edit করুন
sudo nano /etc/fstab

# এই format এ যোগ করুন:
# UUID=xxx /mnt/mydrive ntfs defaults 0 0
```

### ৮. Dual Boot (Windows এর সাথে)

**Time sync issue fix:**
```bash
timedatectl set-local-rtc 1 --adjust-system-clock
```

**Grub order পরিবর্তন:**
```bash
sudo nano /etc/default/grub
# GRUB_DEFAULT=0 পরিবর্তন করুন
sudo update-grub
```

---

## নিরাপত্তা (Security)

### ১. Firewall Enable করুন

```bash
# UFW (Uncomplicated Firewall) install
sudo apt install ufw

# Enable করুন
sudo ufw enable

# Status check
sudo ufw status

# Rules যোগ করুন
sudo ufw allow 22/tcp    # SSH
sudo ufw allow 80/tcp    # HTTP
sudo ufw allow 443/tcp   # HTTPS
```

### ২. Antivirus (Optional)

Linux এ virus খুবই কম, তবুও চাইলে install করতে পারেন:

```bash
# ClamAV
sudo apt install clamav clamav-daemon

# Update করুন
sudo freshclam

# Scan করুন
clamscan -r /home
```

### ৩. Password Management

```bash
# KeePassXC (Password manager)
sudo apt install keepassxc
```

### ৪. System Updates

সবসময় system updated রাখুন - এটাই সবচেয়ে বড় security measure।

### ৫. Secure Browsing

- HTTPS Everywhere extension ব্যবহার করুন
- uBlock Origin (Ad blocker)
- Privacy Badger

---

## শিখতে থাকুন

### ১. Documentation পড়ুন

```bash
# কোনো command এর manual
man [command]
# Example:
man ls
man apt

# Quick help
[command] --help
# Example:
ls --help
```

### ২. Online Resources

**বাংলায়:**
- Ubuntu বাংলা community forums
- Facebook groups: "Ubuntu Bangladesh", "Linux Bangladesh"
- YouTube channels (Bangla Linux tutorials)

**English:**
- Ubuntu Official Documentation: help.ubuntu.com
- Ask Ubuntu: askubuntu.com
- Ubuntu Forums: ubuntuforums.org
- Reddit: r/Ubuntu, r/linux4noobs

### ৩. Practice করুন

- প্রতিদিন কিছু নতুন command শিখুন
- নিজে নিজে explore করুন
- ভুল করতে ভয় পাবেন না (backup থাকলে)

### ৪. Community তে যুক্ত হন

- Local Linux User Groups (LUG)
- Online forums
- IRC channels

---

## দ্রুত Reference

### সবচেয়ে ব্যবহৃত Commands

```bash
# Navigation
cd, ls, pwd

# Files
cp, mv, rm, mkdir, touch

# System
sudo apt update, sudo apt upgrade
sudo apt install [package]
sudo systemctl restart [service]

# Information
df -h, free -h, top, htop

# Network
ping, ip addr, nmcli

# Search
find, grep, locate

# Help
man [command]
[command] --help
```

### Emergency Commands

```bash
# System hanging: Kill process
killall [process-name]
pkill [process-name]

# Network issues
sudo systemctl restart NetworkManager

# Sound issues
pulseaudio -k && pulseaudio --start

# Full system restart
sudo reboot

# Shutdown
sudo shutdown now
```

---

## সমাপনী কথা

এই গাইড দিয়ে আপনি Ubuntu 24.04 এর সব মূল features এবং দৈনন্দিন কাজ শিখে ফেলেছেন। মনে রাখবেন:

1. **ধৈর্য ধরুন**: Linux শিখতে সময় লাগে
2. **Practice করুন**: যত বেশি ব্যবহার করবেন, তত expert হবেন
3. **Community এর সাহায্য নিন**: আটকে গেলে প্রশ্ন করুন
4. **Backup রাখুন**: গুরুত্বপূর্ণ data সবসময় backup করুন
5. **Update রাখুন**: System নিয়মিত update করুন

**আপনি যদি Windows থেকে আসেন**, তাহলে প্রথম কয়েক সপ্তাহ কঠিন লাগতে পারে। কিন্তু ধৈর্য ধরুন। একবার익্ষিড় দন্ত্ব অন্তরহলে, Ubuntu ব্যবহার করা আপনার জন্য অনেক সহজ এবং enjoyable হবে।

**শুভকামনা এবং Happy Linux Journey! 🐧🎉**

---

## প্রশ্ন বা সাহায্য দরকার?

এই গাইড সম্পর্কে কোনো প্রশ্ন থাকলে বা কোনো specific বিষয়ে আরও details জানতে চাইলে, নির্দ্বিধায় জিজ্ঞাসা করুন। আমি সাহায্য করতে প্রস্তুত!

**Common scenarios:**
- "Terminal এ কোনো command কাজ করছে না"
- "Specific software install করতে চাই"
- "Hardware সমস্যা সমাধান করতে হবে"
- "আরও advanced features শিখতে চাই"

যেকোনো সমস্যায় online communities তেও সাহায্য চাইতে পারেন। Linux community খুবই helpful এবং supportive!

---

**Version:** 1.0  
**Last Updated:** January 2026  
**For:** Ubuntu 24.04 LTS (Noble Numbat)

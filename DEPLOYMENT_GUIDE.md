# 🚀 Complete Deployment Guide — ITT B2B Documentation Site

> **Author:** Auto-generated from project analysis  
> **Project:** B2B Panel User Documentation (Docusaurus)  
> **Server:** `109.123.232.6` (`tutorial.innotraveltech.com`)  
> **GitHub Repo:** `https://github.com/ittrepo/b2b-panel-user-document.git`

---

## 📋 Table of Contents

1. [The Big Picture — What Happens When You Deploy?](#1-the-big-picture)
2. [Your Scenario Explained](#2-your-scenario-explained)
3. [Tools You Need on Your PC](#3-tools-you-need-on-your-pc)
4. [Step 1 — Push Your Code to GitHub](#step-1--push-your-code-to-github)
5. [Step 2 — Connect to the Server via SSH](#step-2--connect-to-the-server-via-ssh)
6. [Step 3 — Pull Code on the Server](#step-3--pull-code-on-the-server)
7. [Step 4 — Build & Deploy with Docker](#step-4--build--deploy-with-docker)
8. [Quick Deploy (After First Setup)](#quick-deploy-after-first-setup)
9. [Understanding Every Command](#understanding-every-command)
10. [Project Architecture Diagram](#project-architecture-diagram)
11. [Troubleshooting Common Problems](#troubleshooting-common-problems)
12. [VS Code SSH Remote Setup](#vs-code-ssh-remote-setup)
13. [Useful Day-to-Day Commands](#useful-day-to-day-commands)

---

## 1. The Big Picture

Here's what happens from start to finish when you deploy:

```
Your PC (Windows)                    GitHub                        AWS Server
┌──────────────┐    git push     ┌──────────┐    git pull     ┌──────────────────┐
│  Write Code  │ ──────────────► │  GitHub  │ ◄──────────────│  Server pulls    │
│  in VS Code  │                 │   Repo   │                │  latest code     │
└──────────────┘                 └──────────┘                │                  │
                                                              │  Docker builds   │
                                                              │  the site        │
                                                              │                  │
                                                              │  Nginx serves    │
                                                              │  it to users     │
                                                              └──────────────────┘
                                                                     │
                                                                     ▼
                                                              Users visit:
                                                              tutorial.innotraveltech.com
```

**In simple words:**

1. You write/edit documentation on **your PC**
2. You **push** changes to **GitHub** (cloud storage for code)
3. You **SSH** into the **server** (remote computer on AWS)
4. You **pull** the latest code from GitHub onto the server
5. You **build** and **restart** the Docker containers
6. Users can now see your changes on the live website!

---

## 2. Your Scenario Explained

### ✅ Yes, your understanding is correct!

| Step | Who Does It                    | What Happens                                    |
| ---- | ------------------------------ | ----------------------------------------------- |
| 1    | You (on your PC)               | Write code, test locally                        |
| 2    | You (on your PC)               | `git add` → `git commit` → `git push` to GitHub |
| 3    | Previously Senior, **Now You** | SSH into the AWS server                         |
| 4    | Previously Senior, **Now You** | `git pull` to get latest code on server         |
| 5    | Previously Senior, **Now You** | Run Docker commands to build & deploy           |

> **Before:** You push → Tell senior → Senior deploys  
> **Now:** You push → You deploy it yourself! 💪

---

## 3. Tools You Need on Your PC

### Must Have

| Tool                       | Purpose                   | How to Get                      |
| -------------------------- | ------------------------- | ------------------------------- |
| **VS Code**                | Code editor               | You already have it             |
| **Git**                    | Version control           | You already have it             |
| **Remote - SSH Extension** | Connect VS Code to server | Install from VS Code Extensions |

### Optional but Helpful

| Tool                 | Purpose                                                 |
| -------------------- | ------------------------------------------------------- |
| **Windows Terminal** | A better terminal than default CMD                      |
| **Git Bash**         | Comes with Git, provides Linux-like commands on Windows |

---

## Step 1 — Push Your Code to GitHub

After you finish editing files on your PC, run these commands in the VS Code terminal:

### 1.1 Check what files changed

```bash
git status
```

> **Meaning:** Shows you which files you modified, added, or deleted.  
> **You'll see:** Red filenames = not staged, Green = staged (ready to commit)

### 1.2 Stage your changes

```bash
git add .
```

> **Meaning:** The `.` means "add ALL changed files" to the staging area.  
> **Purpose:** Tells Git "I want to include these files in my next commit."

Or to add a specific file only:

```bash
git add docs/my-new-page.md
```

### 1.3 Commit your changes

```bash
git commit -m "your message describing what you changed"
```

> **Meaning:** Creates a "save point" (snapshot) of your code with a message.  
> **Example:** `git commit -m "added new booking guide page"`  
> **Rule:** Always write clear, short messages. Your senior will read these!

### 1.4 Push to GitHub

```bash
git push origin main
```

> **Meaning:** Uploads your committed code to GitHub.
>
> - `origin` = the GitHub remote server (the repo URL)
> - `main` = the branch name (your repo uses `main`)  
>   **After this:** Your code is on GitHub! ✅

### ⚠️ If `git push` asks for credentials

GitHub no longer accepts passwords. You need a **Personal Access Token (PAT)**:

1. Go to GitHub → Settings → Developer Settings → Personal Access Tokens → Tokens (classic)
2. Generate a new token with `repo` access
3. Use the token as your password when prompted

---

## Step 2 — Connect to the Server via SSH

### What is SSH?

**SSH (Secure Shell)** = A secure way to remotely control another computer using a terminal. Think of it as "remote desktop" but with only a command line (no visual interface).

### Your Server Details

| Field          | Value                         |
| -------------- | ----------------------------- |
| **IP Address** | `109.123.232.6`               |
| **Username**   | `root`                        |
| **Password**   | `hUmba789*****.`              |
| **Domain**     | `tutorial.innotraveltech.com` |

### 2.1 SSH from Terminal (Simple Method)

Open **Git Bash**, **Windows Terminal**, or **VS Code Terminal** and run:

```bash
ssh root@109.123.232.6
```

> **Meaning:**
>
> - `ssh` = the command to start a secure connection
> - `root` = the username on the server (root = admin/superuser)
> - `@` = separator between username and address
> - `109.123.232.6` = the server's IP address

It will then ask:

```
root@109.123.232.6's password:
```

Type your password: `hUmba789*****.` (it won't show anything as you type — this is normal!)

Press **Enter** → You're now inside the server! 🎉

### 2.2 SSH Config File (Easier Method — No Need to Remember IP Every Time)

Create/edit the SSH config file on your PC:

**File location:** `C:\Users\<YourUsername>\.ssh\config`

Add this content:

```
Host itt-server
    HostName 109.123.232.6
    User root
```

> **What this does:** Creates a shortcut so instead of typing `ssh root@109.123.232.6`, you just type:

```bash
ssh itt-server
```

> **Meaning of each line:**
>
> - `Host itt-server` → A friendly name/alias you choose (can be anything)
> - `HostName 109.123.232.6` → The actual IP address of the server
> - `User root` → The username to log in with

### 2.3 How Do You Know You're on the Server?

Your terminal prompt will change from something like:

```
saaqe@YOUR-PC   →   root@server-name:~#
```

The `root@...:#` means you're now controlling the **remote server**, not your local PC.

---

## Step 3 — Pull Code on the Server

### 3.1 Navigate to the project folder

```bash
cd /root/b2b-panel-user-document
```

> **Meaning:**
>
> - `cd` = "change directory" (like opening a folder)
> - `/root/b2b-panel-user-document` = the path where the project lives on the server

> **⚠️ Note:** The exact path might be slightly different. If this path doesn't work, use this command to find it:
>
> ```bash
> find / -name "docker-compose.yml" -path "*/b2b-panel*" 2>/dev/null
> ```
>
> This searches the entire server for the project's `docker-compose.yml` file.

### 3.2 Pull the latest code from GitHub

```bash
git pull origin main
```

> **Meaning:**
>
> - `git pull` = Download + merge the latest code from GitHub
> - `origin` = GitHub remote
> - `main` = the branch name  
>   **Purpose:** Gets the code you just pushed from your PC onto the server.

### If you see "Already up to date"

This means the server already has the latest code. No action needed.

### If you see merge conflicts

Contact your senior. This happens when someone else edited the same lines.

---

## Step 4 — Build & Deploy with Docker

### What is Docker?

Think of Docker as a **"virtual box"** that packages your app with everything it needs to run (Node.js, dependencies, settings). This means the app runs the same way on every computer.

### Your Project's Docker Setup

Your project uses **2 Docker containers**:

```
┌─────────────────────────────────────────────────┐
│               Docker Compose                     │
│                                                  │
│  ┌──────────────────┐    ┌──────────────────┐   │
│  │   docusaurus      │    │     nginx         │   │
│  │   (Node.js app)   │    │   (Web server)    │   │
│  │                   │    │                   │   │
│  │  Runs the docs    │◄───│  Receives user    │   │
│  │  site on port     │    │  requests on      │   │
│  │  3000 (internal)  │    │  port 80 and      │   │
│  │                   │    │  forwards to      │   │
│  │                   │    │  docusaurus        │   │
│  └──────────────────┘    └──────────────────┘   │
│                                   │              │
│                              Port 8080           │
│                          (exposed to internet)    │
└─────────────────────────────────────────────────┘
```

> - **docusaurus container**: Runs your documentation site
> - **nginx container**: Acts as a "traffic controller" — receives user requests and sends them to docusaurus

### 4.1 Build the Docusaurus Site Inside Docker

```bash
docker exec -it b2b-panel-user-document-docusaurus-1 npm run build
```

> **Breaking down every part:**
> | Part | Meaning |
> |------|---------|
> | `docker exec` | Execute/run a command inside a running Docker container |
> | `-it` | `-i` = interactive mode, `-t` = allocate a terminal (so you see output) |
> | `b2b-panel-user-document-docusaurus-1` | The name of the container to run the command in |
> | `npm run build` | The actual command: build the Docusaurus site (creates the `/build` folder) |

> **Purpose:** Compiles your markdown documentation into a fast, static HTML website.

### 4.2 If Build Fails or You Need a Fresh Rebuild

If the above command doesn't work (maybe the container isn't running), do a **full rebuild**:

```bash
docker-compose down
```

> **Meaning:** Stop and remove all containers.  
> Think of it as "turning off the server."

```bash
docker-compose build --no-cache
```

> **Meaning:** Rebuild all container images from scratch.
>
> - `build` = create the Docker images
> - `--no-cache` = don't use any old cached layers, start fresh  
>   **When to use:** When you change `package.json`, `Dockerfile`, or when things are broken.

```bash
docker-compose up -d
```

> **Meaning:** Start all containers in the background.
>
> - `up` = create and start containers
> - `-d` = "detached" mode (runs in background, gives you terminal back)  
>   **After this:** Your site is live! 🎉

---

## Quick Deploy (After First Setup)

Once everything is set up, your daily deployment is just these commands:

```bash
# === On Your PC (VS Code Terminal) ===

git add .
git commit -m "describe your changes"
git push origin main

# === SSH into Server ===

ssh root@109.123.232.6
# (enter password)

# === On the Server ===

cd /root/b2b-panel-user-document
git pull origin main
docker exec -it b2b-panel-user-document-docusaurus-1 npm run build
```

**That's it! 4 commands on PC + 3 commands on server.** ✅

> **⚠️ If build fails**, do the full rebuild:
>
> ```bash
> docker-compose down
> docker-compose build --no-cache
> docker-compose up -d
> ```

---

## Understanding Every Command

### Git Commands Cheat Sheet

| Command                | What It Does                    | When to Use                                 |
| ---------------------- | ------------------------------- | ------------------------------------------- |
| `git status`           | Shows changed files             | Before adding/committing                    |
| `git add .`            | Stages all changes              | After editing files                         |
| `git add <file>`       | Stages one file                 | When you only want to commit specific files |
| `git commit -m "msg"`  | Saves a snapshot with message   | After staging                               |
| `git push origin main` | Uploads to GitHub               | After committing                            |
| `git pull origin main` | Downloads from GitHub           | On the server, to get latest code           |
| `git log --oneline -5` | Shows last 5 commits            | To check history                            |
| `git diff`             | Shows what changed line-by-line | Before committing, to review changes        |

### Docker Commands Cheat Sheet

| Command                           | What It Does                             | When to Use                        |
| --------------------------------- | ---------------------------------------- | ---------------------------------- |
| `docker ps`                       | Lists running containers                 | To check if containers are running |
| `docker ps -a`                    | Lists ALL containers (including stopped) | To check all containers            |
| `docker-compose up -d`            | Starts all services in background        | To start the site                  |
| `docker-compose down`             | Stops and removes all services           | Before rebuilding                  |
| `docker-compose build`            | Builds container images                  | After changing Dockerfile          |
| `docker-compose build --no-cache` | Builds from scratch                      | When cache causes issues           |
| `docker-compose logs -f`          | Shows live logs (like console.log)       | To debug errors                    |
| `docker-compose logs docusaurus`  | Shows logs for one service               | To debug one container             |
| `docker exec -it <name> <cmd>`    | Runs command inside container            | To build, check files, etc.        |
| `docker exec -it <name> sh`       | Opens a shell inside container           | To explore inside a container      |
| `docker-compose restart`          | Restarts all services                    | Quick restart without rebuild      |

### Linux/Server Commands Cheat Sheet

| Command       | What It Does                    | Example                 |
| ------------- | ------------------------------- | ----------------------- |
| `cd <path>`   | Change directory (go to folder) | `cd /root/project`      |
| `ls`          | List files in current folder    | `ls`                    |
| `ls -la`      | List ALL files with details     | `ls -la`                |
| `pwd`         | Print current directory path    | `pwd` → `/root/project` |
| `cat <file>`  | Display file contents           | `cat .env.local`        |
| `nano <file>` | Edit a file (simple editor)     | `nano .env.local`       |
| `clear`       | Clear the terminal screen       | `clear`                 |
| `exit`        | Disconnect from SSH             | `exit`                  |
| `df -h`       | Check disk space                | `df -h`                 |
| `free -m`     | Check memory usage              | `free -m`               |

---

## Project Architecture Diagram

```
Your Project Structure on the Server:
.
├── docker/
│   └── Dockerfile          ← Builds the Docusaurus app (Node.js 20)
├── nginx/
│   ├── Dockerfile          ← Builds the Nginx web server
│   ├── nginx.conf          ← Nginx configuration (routing rules)
│   ├── .htpasswd           ← Password file (for basic auth, currently disabled)
│   └── html/
│       └── custom_401.html ← Custom "access denied" page
├── docs/                   ← Your documentation files (Markdown)
├── src/                    ← Custom React components & pages
├── static/                 ← Static assets (images, etc.)
├── docker-compose.yml      ← Defines how Docker containers work together
├── docusaurus.config.js    ← Main Docusaurus configuration
├── package.json            ← Node.js dependencies & scripts
├── .env.local              ← Secret keys (Clerk auth) — NOT in git!
└── sidebars.js             ← Sidebar navigation structure
```

### How Requests Flow:

```
User Browser
    │
    ▼ (visits tutorial.innotraveltech.com)
┌──────────┐
│  Nginx   │ ← Listens on port 80 (inside Docker)
│  :8080   │ ← Mapped to port 8080 on server
└────┬─────┘
     │ proxy_pass (forwards request)
     ▼
┌──────────────┐
│  Docusaurus  │ ← Runs on port 3000 (internal only)
│  (Node.js)   │ ← Serves the built documentation
└──────────────┘
```

---

## Troubleshooting Common Problems

### ❌ Problem: `ssh: connect to host ... Connection refused`

**Cause:** Server might be down or SSH service not running.  
**Fix:** Wait and try again. If persists, contact your senior.

### ❌ Problem: `Permission denied (publickey,password)`

**Cause:** Wrong password.  
**Fix:** Make sure you're typing the password correctly. Remember, it won't show as you type.

### ❌ Problem: `docker-compose: command not found`

**Cause:** Docker Compose might be installed differently.  
**Fix:** Try `docker compose` (without hyphen — newer syntax):

```bash
docker compose up -d
```

### ❌ Problem: `Container not found` when running docker exec

**Cause:** Container name might be different.  
**Fix:** First check the actual container name:

```bash
docker ps
```

Then use the correct name from the `NAMES` column.

### ❌ Problem: Build takes too long or runs out of memory

**Cause:** Server might have low resources.  
**Fix:**

```bash
# Check memory
free -m

# If needed, stop, rebuild from scratch:
docker-compose down
docker system prune -f       # Clean up unused Docker data
docker-compose build --no-cache
docker-compose up -d
```

### ❌ Problem: Changes not showing on website after deploy

**Fix:**

1. Clear browser cache (Ctrl+Shift+R)
2. Make sure the build was successful (check logs):

```bash
docker-compose logs docusaurus
```

### ❌ Problem: `git pull` shows merge conflicts

**Cause:** Someone else edited the same files.  
**Fix:** For now, ask your senior. Later, you can learn to resolve conflicts with:

```bash
git stash          # Save local changes temporarily
git pull origin main
git stash pop      # Restore local changes
```

---

## VS Code SSH Remote Setup

This lets you edit files on the server directly from VS Code (like your senior does).

### Step 1: Install the Extension

1. Open VS Code
2. Press `Ctrl+Shift+X` (Extensions)
3. Search "Remote - SSH"
4. Install **"Remote - SSH"** by Microsoft

### Step 2: Add SSH Host

1. Press `Ctrl+Shift+P` (Command Palette)
2. Type "Remote-SSH: Add New SSH Host"
3. Enter: `ssh root@109.123.232.6`
4. Select the config file (usually `C:\Users\<YourName>\.ssh\config`)

### Step 3: Connect

1. Press `Ctrl+Shift+P`
2. Type "Remote-SSH: Connect to Host"
3. Select `109.123.232.6`
4. Enter your password when prompted
5. Click "Open Folder" → navigate to your project folder

### Step 4: Open Terminal on Server

- Press `` Ctrl+` `` to open terminal
- This terminal is running ON THE SERVER, not your PC!
- You can run `git pull`, `docker-compose` commands directly here

---

## Useful Day-to-Day Commands

### Check if the site is running

```bash
docker ps
```

> You should see 2 containers: `docusaurus` and `nginx` with status "Up"

### View live logs (useful for debugging)

```bash
docker-compose logs -f
```

> Press `Ctrl+C` to stop watching logs

### Restart without rebuilding (for quick fixes)

```bash
docker-compose restart
```

### Check server disk space

```bash
df -h
```

### Check who's logged into the server

```bash
who
```

### Disconnect from server

```bash
exit
```

---

## 📝 Summary — Your Daily Workflow

```
┌─────────────────────────────────────────────────────────┐
│                    YOUR DAILY WORKFLOW                    │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  1. 📝 Edit your docs/code in VS Code (on your PC)     │
│                                                          │
│  2. 💾 Save and push to GitHub:                          │
│     git add .                                            │
│     git commit -m "what I changed"                       │
│     git push origin main                                 │
│                                                          │
│  3. 🔌 Connect to server:                                │
│     ssh root@109.123.232.6                               │
│                                                          │
│  4. 📥 Pull latest code:                                 │
│     cd /root/b2b-panel-user-document                     │
│     git pull origin main                                 │
│                                                          │
│  5. 🔨 Build the site:                                   │
│     docker exec -it b2b-panel-user-document-docusaurus-1 npm run build  │
│                                                          │
│  6. ✅ Done! Check the site:                             │
│     tutorial.innotraveltech.com                          │
│                                                          │
│  7. 🔌 Disconnect:                                       │
│     exit                                                 │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

> **💡 Tip:** If the build fails, use the full rebuild:
>
> ```bash
> docker-compose down && docker-compose build --no-cache && docker-compose up -d
> ```

---

_Last Updated: 2026-02-16_

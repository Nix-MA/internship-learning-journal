## 🛠 Hands-on
### Chapter 01
### Installing & Setting Up WSL (Windows Subsystem for Linux)

These are the exact steps demonstrated in the session.

---

### Prerequisites

- OS: Windows 10 or Windows 11  
- Goal: Install Ubuntu to run Linux commands natively inside Windows  

---

### Step 1: Enable Windows Features

1. Press the Windows Key and search:

   **Turn Windows features on or off**

2. Enable these three options:

   - Virtual Machine Platform  
   - Windows Hypervisor Platform  
   - Windows Subsystem for Linux  

3. Click OK  
4. Restart your computer

---

### Step 2: Install Ubuntu via PowerShell

1. Open PowerShell as Administrator  

2. Update WSL kernel (recommended):

```bash
wsl --update
```

3.Install Ubuntu:

```
wsl --install
```

Optional: Install a specific version

```bash
wsl --list --online
wsl --install -d Ubuntu-24.04
```

---

### Step 3: First-time Linux Configuration
After installation, Ubuntu opens automatically.

Create a UNIX username:

  - Use something like jdoe
  
  - Avoid spaces (not John Doe)

Set a password:

  - Type it normally

  - Linux will not show * while typing (this is normal)

---

### Step 4: Update Linux Packages

Run these commands after logging in:

Check for updates:
```
sudo apt update
```

Upgrade packages:

```
sudo apt upgrade
```

---

### Chapter 02
Part 1: Managing & Resetting WSL
1. If your WSL installation is corrupted or you forgot your UNIX password, use these steps to reset it completely.

Check Installed Distributions: Open PowerShell and run:
```
wsl --list --verbose
# Lists all distros and their status (Running/Stopped)
```

2. Unregister (Delete) a Distribution:

Warning: This deletes all files inside the Linux system (but not your Windows C: drive).
```
wsl --unregister Ubuntu
# Or 'Ubuntu-24.04' depending on the name from the list command above
```

3. Reinstall Ubuntu:
```
wsl --install Ubuntu-24.04
```

Part 2: Basic Git Workflow (Local)
How to initialize a project and save your first "checkpoint."

1. Install Git (if not installed): Inside your Ubuntu terminal:
```
sudo apt update
sudo apt install git
```

2. Initialize a Repository: Navigate to your project folder and start Git tracking:
```
mkdir my-project
cd my-project
git init
# Creates a hidden .git folder to track changes
```

3. The "Save" Cycle (Add & Commit):
  - Create/Edit a file:
```
echo "Hello World" > file.txt
```

  - Stage the file (Prepare for saving):
```
git add file.txt
# Or 'git add .' to add all changes
```

  - Commit the file (Save the checkpoint):
```
git commit -m "Initial commit"
```

4. View History & Rollback:

  - See the log of changes:
```
git log --oneline
```

  - Demonstration: If you delete the file content and want to go back:
```
git checkout <commit-hash>
# Reverts the files to the state of that specific commit
```
---

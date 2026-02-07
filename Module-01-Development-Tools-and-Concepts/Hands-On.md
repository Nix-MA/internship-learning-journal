## 🛠 Hands-on

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

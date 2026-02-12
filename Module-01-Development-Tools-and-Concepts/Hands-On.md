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

### Chapter 03
Step 1: Install uv (Python Tool Manager)
Run the following command in your WSL (Ubuntu) terminal to install uv.

  - Note: Do not run this in Windows PowerShell. Run it inside the Ubuntu terminal.
  ```
curl -LsSf https://astral.sh/uv/install.sh | sh
```
After installation, you may need to close and reopen the terminal for the uv command to be recognized.

Step 2: Install the llm Tool
Use uv to install the llm command-line interface.
```
uv tool install llm
```

Step 3: Setup Google Gemini (Personal Account)
1. Install the Gemini Plugin:
```
llm install llm-gemini
```
2. Get API Key: Visit Google AI Studio (use your personal Gmail, not student ID) and create a new API key.

3. Set the Key:
```
llm keys set gemini
# Paste your API key when prompted and press Enter
```
4. Test Gemini:
```
llm -m gemini-2.5-flash "Who are you?"
```

Step 4: Setup OpenAI via AI Pipe (Student Account)
1. Get Token: Go to the Course Portal -> "Tools" or "Week 4" section -> Find AI Pipe. Login with your student ID and copy your Access Token.

2. Set the Key:
```
llm keys set openai
# Paste your AI Pipe Access Token when prompted
```
3. Configure the Proxy URL (.bashrc Setup):

  - Get the Base URL from the AI Pipe instructions (usually found on the AI Pipe GitHub or Portal).

  - Open your shell configuration file:
  ```
nano ~/.bashrc
# OR if you are on Mac using Zsh:
# nano ~/.zshrc
```
  - Scroll to the bottom of the file and add the following line:
  ```
export OPENAI_API_BASE="https://aipipe.rory.wo/v1" 
# Note: Verify the exact URL from the course portal/GitHub as it may change.
```
  - Save and exit (Ctrl+O, Enter, Ctrl+X in nano).

4. Apply Changes:
```
source ~/.bashrc
# OR close and reopen the terminal
```
5. Test OpenAI:
```
llm -m gpt-4o-mini "Hello"
```

# Chapter 04
Step 1: Install Homebrew (Mac/Linux)
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
After installation, follow the on-screen instructions to run the echo commands that add Homebrew to your PATH.

Step 2: Python Setup with pyenv
1. Install pyenv:
```
brew install pyenv
```
2. Install Python Build Dependencies (Mac):
```
brew install openssl readline sqlite3 xz zlib
```
3. Install a specific Python version:
```
pyenv install 3.12.11
```
4. Set Global Version:
```
pyenv global 3.12.11
```

Step 3: fast Project Setup with uv
1. Install uv:
```
curl -LsSf https://astral.sh/uv/install.sh | sh
```
2. Initialize a Project:
```
mkdir my-project
cd my-project
uv init
```
3. Add a Dependency (e.g., Flask):
```
uv add flask
```
This automatically creates the virtual environment and installs Flask.

Step 4: GitHub Automation with gh CLI
1. Install GitHub CLI:
```
brew install gh
```
2. Login:
```
gh auth login
# Select GitHub.com -> HTTPS -> Login with Browser
```
3. Create & Push a Repo (One Step): Inside your project folder:
```
git add .
git commit -m "Initial commit"
gh repo create my-new-repo --public --source=. --push
```

Step 5: LLM CLI Configuration
1. Install LLM:
```
brew install llm
```
2. Install Gemini Plugin:
```
llm install llm-gemini
```
3. Set API Key:
```
llm keys set gemini
# Paste key from aistudio.google.com
```
4. Run a Prompt:
```
llm -m gemini-2.0-flash "Explain quantum computing in one sentence"
```
---


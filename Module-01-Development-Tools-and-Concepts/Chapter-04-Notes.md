### Week 01, Session 04: Development Tools Setup (Mac/Linux Focus)

---

# 1: VS Code and Copilot Setup
The session begins with setting up the primary code editor, VS Code. For Mac users, a crucial tip is shared: drag the application to the "Applications" folder rather than running it from "Downloads" to ensure permissions and updates work correctly. The instructor then highlights GitHub Copilot, accessible for free via the GitHub Student Developer Pack. To enable it in VS Code:

1. Obtain the Student Developer Pack.

2. Activate "Copilot Pro" in your GitHub account settings.

3. Sign in to GitHub within VS Code to sync the license.

# 2: Package Management with Homebrew
For efficient software installation, Homebrew is introduced as the standard package manager for macOS (and can be used on Linux). It handles dependencies automatically, preventing "missing library" errors common with manual downloads.

  - Installation: A single command line script installs Homebrew.

  - Post-Install: It's vital to add Homebrew to the system PATH so commands like brew can be run from any folder.

# 3: Python Version Management (pyenv)
Managing Python versions is critical for stability. The system default Python (often v3.9 on Mac) should not be used for development to avoid breaking system tools.

- pyenv: A tool to install and manage multiple isolated Python versions.

- Workflow:

  - Install build dependencies (xcode tools, openssl, etc.).

  - Install a specific Python version (e.g., pyenv install 3.12.11).

  - Set a version locally per folder (pyenv local 3.12.11) or globally (pyenv global 3.12.11).

# 4: The uv Tool Manager & Project Initialization
uv is introduced as a modern, high-speed Python package and project manager that replaces standard pip and virtualenv workflows.

- Why uv? It unifies creating virtual environments, installing packages, and managing dependencies into single commands. It creates a central cache, saving disk space compared to pip.

- Project Init: uv init <project_name> automatically creates a project folder, a .venv (virtual environment), a .gitignore, and a hello.py file.

- Adding Packages: uv add flask installs the package and updates dependencies instantly, managing the environment automatically.

# 5: GitHub CLI (gh) & Automation
To streamline Git operations, the GitHub CLI is installed. This tool brings GitHub features (like creating repos, checking actions) directly to the terminal.

- Authentication: gh auth login links the terminal to your GitHub account via browser authorization.

- Creating Repos: You can create a remote repository and push local code in one command: gh repo create <name> --public --source=. --push. This replaces the manual "create repo on website -> copy URL -> git remote add -> git push" cycle.

# 6: LLM CLI Tool
The session concludes with the llm command-line tool, essential for building intelligent agents later in the course.

- Setup: Installed via brew or uv.

- Plugins: To use Google's models, the llm-gemini plugin is installed.

- Keys: API keys are set securely using llm keys set <provider>.

- Usage: Simple prompts like llm -m gemini-2.0-flash "translate this" can process text or even audio files directly from the command line, facilitating automation scripts.

---

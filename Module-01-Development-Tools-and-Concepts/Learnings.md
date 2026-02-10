### Key Learnings

---

### Chapter 01
1. System Over Syntax: The course prioritizes "System-Level Thinking" (connecting APIs, databases, and deployment) over just writing Python syntax.

2. The "Save" Trap: In the custom portal, the "Check" button only validates the answer. You must click the Save button to submit the grade to the server.

3. WSL Architecture: WSL allows you to run Linux binaries natively on Windows. It is more efficient than VirtualBox because it shares the kernel/hardware resources more directly (Type-1 Hypervisor integration).

4. Deployment is Key: The two biggest hurdles for students are typically APIs (how systems talk) and Deployment (making code accessible to the world).

5. Linux Naming Convention: Always avoid spaces in file names and directory names in Linux to prevent scripting errors later.

---

### Chapter 02
- Type-1 vs. Type-2 Hypervisors: WSL is faster because it runs directly on the hardware (Type-1), whereas VirtualBox runs on top of the OS (Type-2), adding overhead.

- The "Undo" Limit: Standard editors cannot undo changes after the application is closed. Git solves this by permanently recording file states.

- Destructive Reset: You can fix a broken WSL instance by "unregistering" it. This wipes the Linux container clean but leaves your Windows files (Downloads, Documents) untouched.

- GitHub Policy: Never maintain multiple free GitHub accounts. GitHub uses algorithms to detect this, and they may ban all your accounts, jeopardizing your ability to submit course projects.

---

### chaapter 03
 - Linux File Paths: The mnt directory is the bridge between Linux and Windows drives. /mnt/c/ corresponds to the Windows C: drive.

 - Tool Isolation: uv is used instead of global pip installs to keep tools isolated and prevent dependency conflicts.

 - Plugins: The llm CLI is modular; you must install specific plugins (like llm-gemini) to use models other than the defaults.

 - Environment Variables: Permanent configurations (like pointing to a proxy server URL) should be written to ~/.bashrc (Linux/WSL) or ~/.zshrc (Mac) so they persist across sessions.

 - Proxy Usage: When using the student quota for OpenAI, you must change the OPENAI_API_BASE URL; otherwise, the tool will try to contact OpenAI directly and reject your student token.



- File Systems: In WSL, you should ideally work within the Linux file system (e.g., /home/username/) for better performance, though you can access Windows files from /mnt/c/


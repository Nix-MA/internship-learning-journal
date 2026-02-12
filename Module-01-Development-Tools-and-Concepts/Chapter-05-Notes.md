### Week 01, Session 05: GitHub Setup & Fast API

---

# 1: The Role of Git & GitHub
The instructor explains that Git is essential for version control, allowing developers to track code changes, collaborate, and manage different features via branches. GitHub acts as the remote hosting service for these Git repositories.

  - Why SSH? The instructor strongly recommends using SSH (Secure Shell) for authentication over HTTPS. SSH keys provide a more secure and persistent connection without requiring users to enter their username and personal access token for every single push or pull operation.

# 2: Generating SSH Keys
To link a local machine (specifically WSL in this context) to GitHub securely:

1. Generate a Key Pair: The user generates a public and private SSH key pair using the ssh-keygen command.

2. Add Key to Agent: The private key is added to the local SSH agent to manage the identity.

3. Upload to GitHub: The public key (files ending in .pub) is copied and pasted into the user's GitHub settings under "SSH and GPG keys". This establishes trust between the GitHub server and the user's computer.

# 3: Cloning & Pushing Code
Once the secure connection is established:

- Cloning: Users can copy a remote repository to their local machine using git clone <ssh-url>.

- The Push Workflow:

  1. Add: Stage modified files (git add .).

  2. Commit: Save a snapshot of the changes locally with a descriptive message (git commit -m "message").

  3. Push: Upload the commits to the remote GitHub repository (git push).

- Troubleshooting: Common issues like "Permission Denied" usually stem from the SSH agent not having the correct key loaded or a mismatch between the key used locally and the one uploaded to GitHub.

# 4: Creating a Basic Web Server (FastAPI)
The session shifts to practical application development using FastAPI, a modern Python web framework.

- Setup: The instructor uses uv (a fast Python package manager introduced in previous sessions) to install FastAPI.

- Boilerplate: A simple "Hello World" server is created to demonstrate how backend code works.

- Running the Server: The server is started locally, and it listens on a specific port (e.g., 8000), allowing the user to visit localhost:8000 in their browser to see the API response.

# 5: AI Coding Assistants (GitHub Copilot)
The instructor briefly demonstrates GitHub Copilot's capabilities within VS Code.

- Code Generation: Copilot can generate entire code blocks (like the FastAPI boilerplate) from simple natural language comments.

- Refactoring: It can also help refactor existing code or suggest fixes for errors.

- Content Creation: The instructor shows an advanced use case where an AI agent helps generate markdown documentation for a new course module by analyzing external resources (like YouTube videos) and formatting the output to match existing course materials.

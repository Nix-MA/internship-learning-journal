Week 02, Session 03: GitHub Code Spaces, Hugging Face, & CI/CD
---
# 1: GitHub Code Spaces
The session begins with an introduction to GitHub Code Spaces, a cloud-hosted development environment. Unlike local setups (VS Code on your laptop), Code Spaces runs on GitHub's servers, offering a consistent environment pre-configured with necessary tools.

- Why use it? It solves the "works on my machine" problem. New team members can onboard instantly without manual installations. It's ideal for teams or when local hardware is insufficient.

- Configuration: It uses a .devcontainer folder containing a devcontainer.json file (configuration) and a Dockerfile (dependencies). This defines the OS, tools (like Python, UV), and extensions (VS Code plugins) installed automatically when the environment spins up.

- Cost/Usage: GitHub provides a free tier (e.g., 120 core-hours/month for free users, 180 for students). Usage is calculated based on machine power (2-core vs. 4-core) and active time.

# 2: Deployment on Hugging Face Spaces
The instructor shifts to deploying applications using Hugging Face Spaces, a platform popular for hosting ML models and demos.

- Setup: Similar to GitHub, you create a "Space" (repository). It supports various SDKs, but the session focuses on using Docker for maximum flexibility.

- Deployment Workflow:

  1. Create a Space on Hugging Face.

  2. Clone the Space locally (using Git).

  3. Add application code (e.g., app.py with FastAPI) and a Dockerfile defining the runtime.

  4. Push changes to Hugging Face. The platform automatically builds the Docker image and deploys the app.

- Git LFS: Mention is made of Git Large File Storage (LFS), essential for handling large model files (often GBs in size) that standard Git cannot manage efficiently.

# 3: GitHub Actions (CI/CD)
The final major topic is GitHub Actions, an automation tool for Continuous Integration/Continuous Deployment (CI/CD).

- Workflows: Actions are defined in YAML files located in .github/workflows/.

- Triggers: Workflows can be triggered by events (push, pull request) or schedules (cron jobs).

- Use Cases:

  - Automated Testing: Running tests whenever code is pushed to ensure no regressions.

  - Deployment: Automatically deploying to platforms like Hugging Face or Vercel upon a successful merge to the main branch.

  - Scheduled Tasks: The instructor demonstrates a workflow that runs daily to fetch data (ISS coordinates) and commit it back to the repository.

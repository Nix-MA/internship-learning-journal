# Week 01, Chapter 02: WSL Troubleshooting & Introduction to Git

---

# 1: Course Logistics & Infrastructure

This session begins with a quick walkthrough of the **TDS Portal**, which is separate from the standard Seek portal. The portal hosts dynamic content that is updated frequently to stay aligned with current industry tools and trends.

Key logistical points discussed include:

- **Assessments**
  - Clicking **Check** only validates your answer.
  - You must click **Save** to officially submit your response.

- **Support System**
  - **Discourse** is the main platform for questions and discussions, replacing email.
  - This helps build a shared knowledge base for all learners.

- **AI Access**
  - Students are provided **AI Pipe**, which gives free access to OpenAI models for coursework and projects.

- **Projects**
  - Projects are graded using an **LLM-based rubric**.
  - Evaluation focuses on:
    - Code quality  
    - Error handling  
    - Robustness  
  - Functional testing is done by running test cases against the student’s deployed server.

---

# 2: Deep Dive into WSL (Windows Subsystem for Linux)

A major part of the session focuses on troubleshooting WSL installations.

The instructors reinforce that **WSL 2 is strongly preferred over VirtualBox**, mainly because of architecture:

- **WSL 2 uses a Type-1 Hypervisor**
  - Linux communicates directly with hardware (CPU/RAM)
  - Faster and more resource-efficient

- **VirtualBox uses a Type-2 Hypervisor**
  - Runs Linux through an extra translation layer
  - Slower and heavier on system resources

Key points covered:

- **Standard Installation Logic**
  - Enable required Windows features:
    - Virtual Machine Platform  
    - Windows Subsystem for Linux  
  - Install a Linux distribution such as **Ubuntu 24.04**

- **Recovery & Reset**
  - If installation fails or a password is forgotten, you can completely wipe and restart by **unregistering** the Linux distribution.
  - This removes the Linux instance without affecting Windows files.

---

# 3: The Need for Version Control (Git)

The instructor introduces **Git** by pointing out a limitation of normal code editors: once you close a file (like in VS Code), you lose the ability to "Undo" (Ctrl+Z) previous changes.

- What is Git? Git acts as a time machine for code, allowing developers to create "checkpoints" (commits). Even if the editor is closed or the computer is restarted, one can roll back to any previous state.

- Git vs. GitHub:

  - Git: Local software that tracks version history on your machine.

  - GitHub: A cloud-based hosting service (like Google Drive for code) where Git repositories are stored for backup and collaboration.

- Policy Warning: A strict warning is issued regarding GitHub accounts. Students must have only one free GitHub account. Creating multiple free accounts violates GitHub's policy and has led to students losing access to their accounts (and coursework) in the middle of the term.

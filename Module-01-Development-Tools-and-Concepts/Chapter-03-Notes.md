### Week 01, Chapter 03: Linux File System, UV, and LLM Setup

---

# 1: Linux File System Fundamentals
The session begins with a review of the Linux file system structure within WSL (Ubuntu). Unlike Windows, which uses drive letters (C:, D:), Linux uses a unified directory tree starting from the Root (/).

  - Home Directory (~): The personal workspace for the user (e.g., /home/username). The tilde symbol (~) is a shortcut for this path.

  - Mount Points (/mnt): Windows drives are accessible in Linux via the /mnt directory. For example, the C: drive is located at /mnt/c/.

  - Absolute vs. Relative Paths:

     - Absolute: Starts with / (e.g., /home/user/project).

    - Relative: Starts from the current location (e.g., ./folder for current directory, ../folder for parent directory).

  - Hidden Files: Configuration files often start with a dot (e.g., .bashrc) and are hidden from standard directory listings.

# 2: The uv Tool Manager
The instructor introduces uv, a fast Python package and tool manager. It is preferred over standard pip for this course because of its speed and ability to manage isolated environments for tools.

  - Installation: uv is installed via a curl script directly into the Linux environment (WSL).

  - Usage: It is used to install Python-based command-line tools (like llm) without polluting the global Python environment.

# 3: Setting up the LLM CLI
The core of the session focuses on setting up llm, a command-line utility that allows users to interact with Large Language Models (like GPT-4 and Gemini) directly from the terminal.

  - Installation: Installed using uv tool install llm.

  - Plugins: The llm tool is extensible. The instructor demonstrates installing the Gemini plugin to access Google's models.

# 4: API Key Configuration
To use LLMs, authentication is required.

  - Gemini Setup: Students use their personal Google accounts (not the IITM ID) to generate a free API key from Google AI Studio. This key is set using llm keys set gemini.

  - OpenAI Setup (AI Pipe): For OpenAI models, students use the course-provided AI Pipe proxy. This requires a specific token from the course portal.

    - Token: The AI Pipe token is set as the OpenAI key (llm keys set openai).

    - Base URL: Crucially, simply setting the key isn't enough for the proxy. Students must configure the API Base URL so the tool knows to send requests to the course proxy instead of OpenAI directly. This is done by exporting an environment variable in the .bashrc file.

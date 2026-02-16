### Week 02, Session 01: Containerization with Podman

# 1: The Concept of Containerization
The session begins by addressing the problem of dependency management. Typically, running code requires installing specific versions of Python, libraries (like Flask/FastAPI), and other OS-dependent tools. This "it works on my machine" problem is solved by Containerization.

Image: A single, static file (often 500MB+) that contains the entire operating system (e.g., Alpine Linux), runtime (Python), and libraries needed to run an application. It is a snapshot.

Container (Pod): A running instance of an image. It creates an isolated environment (like a lightweight virtual machine) where the code executes. It runs on the host's RAM but uses the host kernel.

Podman vs. Docker: Both are tools to manage containers. Podman is open-source, daemonless, and rootless (doesn't require admin privileges to run containers), making it safer and often preferred in educational/secure environments. Docker is the industry standard but requires a background daemon. Commands are largely interchangeable (podman run ≈ docker run).

# 2: Managing Images and Containers
The instructor demonstrates the lifecycle of a container using Podman:

Pulling: Downloading an image from a registry like Docker Hub or Quay.io (e.g., podman pull docker.io/library/alpine).

Running: Starting a container from an image (e.g., podman run).

Listing: Checking running containers (podman ps) and all containers including stopped ones (podman ps -a).

Stopping/Removing: podman stop <id> halts execution, while podman rm <id> deletes the container instance. podman rmi <id> deletes the image file itself to save space.

# 3: Port Forwarding and Volume Mounting
Two critical concepts for interacting with containers are introduced:

Port Forwarding (-p): Containers are isolated networks. To access a web server running inside a container (e.g., Jupyter on port 8888) from the host machine (your browser), you must map the container port to a host port (e.g., -p 8888:8888).

Volume Mounting (-v): Containers are ephemeral; if you delete a container, all files created inside it are lost. Volumes map a folder on your host machine to a folder inside the container. This persists data (like code files or datasets) even after the container is destroyed.

# 4: Advanced Networking (Ollama & Jupyter)
The session scales up to running multiple interacting containers.

Ollama: A tool to run LLMs locally. The instructor pulls a lightweight image (alpine-ollama) and the Gemma 2:2b model to avoid high resource usage.

Networking: To allow a Jupyter Lab container (running Python code) to talk to the Ollama container (running the LLM), they must share a network. The instructor creates a custom network (podman network create ai) and attaches both containers to it. This allows them to communicate using their container names as hostnames instead of IP addresses.

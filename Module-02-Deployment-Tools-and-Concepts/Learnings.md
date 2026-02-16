### Key Learnings
---
# Chapter 01
- Isolation vs. Persistence: Containers provide a clean slate every time (Isolation). To save work, you must use Volumes to map data to your physical hard drive (Persistence).

- Ephemeral Nature: Treat containers as disposable ("cattle, not pets"). Do not store important configurations or data inside the container layer itself; define them in the run command or Dockerfile.

- Networking Magic: Containers on the same user-defined network (like ai-net) can resolve each other by name (DNS). This is crucial for microservices (e.g., App container talking to DB container).

- Port Mapping: 127.0.0.1 (localhost) inside a container refers to the container itself, not your computer. You must explicitly map ports (-p host:container) to bridge the gap.

- Resource Awareness: Running LLMs locally is heavy. Use quantized or smaller models (like Gemma 2B or Phi-2) and lightweight base images (Alpine) to reduce RAM/disk usage.

---

# Chapter 02
- Kernel Sharing: Containers are lightweight because they share the host OS kernel, unlike VMs which boot a full OS.

- Stateless Functions: Vercel/Serverless is ideal for stateless, short-lived tasks (API requests). It is not suitable for long-running processes (like training ML models or WebSockets) due to timeout limits.

- FastAPI & Async: FastAPI natively supports asynchronous request handling, making it highly performant for I/O-bound operations compared to older synchronous frameworks like Flask.

- Security Hygiene: Never push .env files or API keys to GitHub. Use .gitignore to exclude them and configure environment variables directly in your deployment platform (Vercel).

- Docs Automation: FastAPI's auto-generated /docs (Swagger UI) is a powerful tool for testing and debugging APIs without writing any extra frontend code.

---

# Chapter 03
- Cloud Development: Code Spaces decouple the development environment from local hardware, ensuring consistency across teams and simplifying onboarding.

- Containerized Deployment: Hugging Face Spaces (via Docker) provides a robust platform for deploying ML apps. Using Dockerfiles gives you full control over the runtime environment compared to pre-set SDKs.

- Automation is Key: GitHub Actions automate repetitive tasks (testing, deployment, data fetching), reducing human error and ensuring that the "main" branch is always tested and deployable.

- Secrets Management: Never hardcode secrets (API keys). Use Environment Variables (in Vercel/Hugging Face settings) or GitHub Secrets (for Actions) to manage sensitive data securely.

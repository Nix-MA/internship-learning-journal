### Key Learnings
---
# Chapter 01
- Isolation vs. Persistence: Containers provide a clean slate every time (Isolation). To save work, you must use Volumes to map data to your physical hard drive (Persistence).

- Ephemeral Nature: Treat containers as disposable ("cattle, not pets"). Do not store important configurations or data inside the container layer itself; define them in the run command or Dockerfile.

- Networking Magic: Containers on the same user-defined network (like ai-net) can resolve each other by name (DNS). This is crucial for microservices (e.g., App container talking to DB container).

- Port Mapping: 127.0.0.1 (localhost) inside a container refers to the container itself, not your computer. You must explicitly map ports (-p host:container) to bridge the gap.

- Resource Awareness: Running LLMs locally is heavy. Use quantized or smaller models (like Gemma 2B or Phi-2) and lightweight base images (Alpine) to reduce RAM/disk usage.

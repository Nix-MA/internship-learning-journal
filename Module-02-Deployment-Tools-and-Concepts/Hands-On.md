## 🛠 Hands-on
### Chapter 01

Step 1: Install Podman (WSL/Linux)
```
sudo apt update
sudo apt install podman
# For WSL users, install QEMU dependency if needed
sudo apt install qemu-user-static
```

Step 2: Pull and Run a Basic Image
1. Pull an image:
```
podman pull docker.io/library/nginx
```
2. Run in detached mode (-d) with a specific name:
```
podman run -d --name my-web-server nginx
```
3. Check status:
```
podman ps
```
4. Stop and remove:
```
podman stop my-web-server
podman rm my-web-server
```

Step 3: Run Jupyter Lab with Persistence
Run a Jupyter Lab container that saves files to your local ~/work directory.

1. Create local directory:
```
mkdir -p ~/work
chmod 777 ~/work  # Ensure write permissions
```
2. Run with Volume (-v) and Port (-p):
```
podman run -d \
  --name jup-lab \
  -p 8888:8888 \
  -v ~/work:/home/jovyan/work \
  quay.io/jupyter/base-notebook
```
3. Access: Check logs for the token (podman logs jup-lab) and visit localhost:8888 in your browser.

Step 4: Run Local LLM (Ollama)
1. Run Ollama container:
```
podman run -d \
  --name ollama \
  -p 11434:11434 \
  -v ollama:/root/.ollama \
  docker.io/ollama/ollama
```
2. Enter container to pull a model:
```
podman exec -it ollama bash
# Inside container:
ollama pull gemma2:2b
# Exit container
exit
```

Step 5: Networking Containers
Connect the Jupyter container to Ollama to build an AI app.

1. Create Network:
```
podman network create ai-net
```
2. Run Ollama on Network:
```
podman run -d --name ollama --network ai-net ollama/ollama
```
3. Run Jupyter on Same Network:
```
podman run -d --name jup-lab --network ai-net -p 8888:8888 quay.io/jupyter/base-notebook
```
Now, inside Jupyter, you can reach Ollama at http://ollama:11434 instead of localhost.

---

## Chapter 02

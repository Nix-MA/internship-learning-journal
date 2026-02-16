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

Step 1: Create a Fast API App
1. Initialize project with uv:
```
mkdir my-fastapi-app
cd my-fastapi-app
uv init
uv add fastapi
```
2. Create app.py:
```
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}

@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id}
```
3. Run locally:
```
uv run fastapi dev app.py
```
- Access at http://localhost:8000.

- Test APIs at http://localhost:8000/docs.

Step 2: Deploy to Vercel (CLI Method)
1. Install Vercel CLI:
```
npm install -g vercel
```
2. Login:
```
vercel login
```
3. Create vercel.json:
```
{
  "builds": [
    {
      "src": "app.py",
      "use": "@vercel/python"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "app.py"
    }
  ]
}
```
4. Deploy:
```
vercel
# Follow prompts: Set scope (username), link to existing project (N), project name (my-app), directory (./).
```

Step 3: Managing Environment Variables
1. Local: Create a .env file.
```
MY_SECRET_KEY=12345
```
2. Code Access:
```
import os
from dotenv import load_dotenv
load_dotenv()
secret = os.getenv("MY_SECRET_KEY")
```
3. Vercel: Go to Vercel Dashboard -> Project Settings -> Environment Variables -> Add MY_SECRET_KEY and value 12345.

Step 4: Expose Localhost with Ngrok
1. Install & Auth: Download Ngrok, sign up, and run the auth command provided on your dashboard.

2. Tunnel:
```
ngrok http 8000
```
3. Share: Copy the Forwarding URL (https) and share it.
---

## Chapter 03

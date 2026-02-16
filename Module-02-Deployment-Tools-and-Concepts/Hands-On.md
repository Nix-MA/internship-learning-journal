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
Step 1: Setting up GitHub Code Spaces
1. Create/Open a Repo: Go to a GitHub repository.

2. Launch Code Space: Click the green "Code" button -> "Codespaces" tab -> "Create codespace on main".

3. Configure Environment (Optional):

- Add a .devcontainer/devcontainer.json file.

- Define extensions (e.g., ms-python.python) and post-create commands (e.g., pip install -r requirements.txt).

- Rebuild the container to apply changes.

Step 2: Deploying to Hugging Face Spaces (Docker Method)
1. Create Space:

- Go to Hugging Face -> New Space.

- Enter a name, select license, and choose Docker as the SDK.

2. Clone Locally:
```
git clone https://huggingface.co/spaces/your-username/your-space-name
cd your-space-name
```
3. Create Application Files:

- app.py:
```
from fastapi import FastAPI
app = FastAPI()
@app.get("/")
def read_root():
    return {"message": "Hello from Hugging Face!"}
```
- Dockerfile:
```
FROM python:3.9
WORKDIR /code
COPY ./requirements.txt /code/requirements.txt
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt
COPY . .
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]
```
- requirements.txt:
```
fastapi
uvicorn
```
4. Push to Deploy:
```
git add .
git commit -m "Initial deploy"
git push
```
Note: If prompted for password, use a Hugging Face Access Token with write permissions.

Step 3: Creating a GitHub Action
1. Create Workflow File:

- Inside your repo, create .github/workflows/daily-task.yml.

2. Define Workflow (Example):
```
name: Daily Data Fetch
on:
  schedule:
    - cron: '0 12 * * *' # Runs daily at 12:00 UTC
  workflow_dispatch: # Allows manual trigger

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'
      - name: Run script
        run: |
          pip install requests
          python fetch_data.py
      - name: Commit results
        run: |
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          git add data.json
          git commit -m "Update data" || exit 0
          git push
```
3. Commit: Push this file to the repository. The action will run according to the schedule or can be triggered manually under the "Actions" tab.

---

# Chapter 04
Step 1: Basic FastAPI Server Setup
1. Create a directory and virtual environment:
```
mkdir fast-api-demo
cd fast-api-demo
python -m venv venv
# Activate: source venv/bin/activate (Mac/Linux) or venv\Scripts\activate (Windows)
```
2.  Install dependencies:
```
pip install fastapi uvicorn python-multipart
```
3. Create app.py:
```
from fastapi import FastAPI
import uvicorn

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello from FastAPI"}

if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
```
4. Run the server:
```
python app.py
# Access at http://localhost:8000
# Docs at http://localhost:8000/docs
```

Step 2: Implementing Pydantic Models
Add data validation for a POST request.
```
from pydantic import BaseModel, EmailStr

class User(BaseModel):
    username: str
    email: EmailStr
    age: int

@app.post("/users/")
def create_user(user: User):
    return {"message": "User created", "data": user}
```
Note: Requires pip install pydantic[email].

Step 3: Dockerizing for Hugging Face
Create a Dockerfile in the same directory.
```
# Use official Python image
FROM python:3.9

# Set working directory
WORKDIR /code

# Copy requirements and install
COPY ./requirements.txt /code/requirements.txt
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

# Copy app code
COPY . .

# Run the application on port 7860 (Hugging Face default)
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]
```

Step 4: Deploying to Hugging Face
1. Go to Hugging Face Spaces -> Create new Space.

2. Name it, select Docker as the SDK, and choose Public.

3. Upload app.py, requirements.txt, and Dockerfile via the "Files" tab.

4. Add Secrets: Go to Settings -> Variables and secrets. Add your SECRET_KEY (e.g., value: 92).

5. Update Code to Use Secret:
```
import os
secret_key = os.getenv("SECRET_KEY")
```
---



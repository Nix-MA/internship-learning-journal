### Week 02, Session 02: Podman vs. VMs, GitHub Pages, & Fast API Deployment
---
# 1: Podman/Containers vs. Virtual Machines (VMs)
The session opens with a conceptual comparison between Containers (Podman/Docker) and Virtual Machines.

- Virtual Machines: Heavyweight. Each VM runs its own full Operating System (OS) and Kernel on top of the host hardware. This consumes significant resources (RAM, CPU), limiting how many can run simultaneously (e.g., 1-2 on an 8GB laptop).

- Containers (Podman): Lightweight. Containers share the host machine's kernel but maintain isolation at the process level. They don't need a full OS, only the application and its specific libraries. This allows running many more instances (e.g., 10+) on the same hardware. They are also highly portable—you can push an image to a hub and pull it anywhere.

- Podman vs. Docker: Both are functionally similar with compatible CLI commands. The key difference is architecture: Podman is daemonless and supports rootless mode by default (runs as a non-admin user), enhancing security. Docker historically required a central daemon running as root, though it now also supports rootless mode.

# 2: Static Hosting with GitHub Pages
The instructor demonstrates how to host static websites using GitHub Pages.

- Use Case: Ideal for hosting Markdown, HTML, CSS, and JavaScript files (static content). It cannot execute backend logic (like Python/Database code).

- Setup: Go to repository Settings -> Pages -> Select the branch (e.g., main) and folder (usually /root or /docs).

- Jekyll: GitHub Pages uses Jekyll (a static site generator) by default. If your project isn't a Jekyll site (e.g., plain HTML or a specific documentation framework), you might need to add a .nojekyll file to bypass Jekyll processing, ensuring files are served exactly as they are.

# 3: Building a Fast API Backend
The focus shifts to creating a dynamic backend application using FastAPI.

- Setup: Use uv (a fast Python package manager) to initialize the project and install dependencies (fastapi).

- The Application: A basic app.py is created.

  - Instance: app = FastAPI() initializes the app.

  - Endpoints: Decorators like @app.get("/items") define routes. When a user visits /items, the function below the decorator executes.

- Async: FastAPI is preferred over Flask in this course because it natively supports asynchronous operations (async def), making it much faster and better at handling concurrent requests (e.g., 1000 users hitting an endpoint simultaneously).

- Documentation: FastAPI automatically generates interactive API documentation (using Swagger UI) at the /docs endpoint, allowing developers to test GET/POST methods directly in the browser without writing frontend code.

# 4: Serverless Deployment on Vercel
The session covers deploying the Fast API app to Vercel, a serverless platform.

- Serverless Concept: Unlike a traditional server that runs 24/7, Vercel runs functions. It spins up resources only when a request comes in and shuts them down immediately after the response.

- Configuration: A vercel.json file is required to tell Vercel how to build and route requests to the Python app.

- Limitations:

  - Execution Time: Functions must complete within 10 seconds (default) or up to 300 seconds (pro/configured). Longer tasks will timeout (Error 504).

  - Read-Only Filesystem: You cannot write files to the disk (except /tmp).

  - No Subprocesses: You cannot spawn new system processes.

- Environment Variables: Sensitive data (like API Keys) should never be hardcoded. They are stored in a .env file locally (added to .gitignore) and configured in the Vercel project settings for deployment.

# 5: Local Tunneling with Ngrok
For testing code that is running locally but needs to be accessed by others (or external webhooks), Ngrok is introduced.

- Function: It creates a secure tunnel from the public internet to a port on your local machine (e.g., localhost:8000).

- Usage: Running ngrok http 8000 generates a public URL (e.g., https://random-name.ngrok-free.app). Anyone with this URL can access the app running on your laptop as if it were hosted on a server.

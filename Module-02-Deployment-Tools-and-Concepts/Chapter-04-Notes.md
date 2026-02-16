Week 02, Session 04: Project 1 Workflow & FastAPI Fundamentals
---
# 1: Project 1 Workflow Overview
The session begins with a comprehensive walkthrough of the Project 1 Workflow, which is the core assignment for this module. The workflow is designed to simulate a real-world scenario where an automated system interacts with your application.

1. Google Form Submission: Students must submit a Google Form before the deadline (approx. Oct 17th). This form collects:

- API Endpoint: The URL of the student's deployed FastAPI application (e.g., hosted on Hugging Face Spaces).

- GitHub Repo Link: The public repository containing the code for the API server.

- Secret Key: A custom string (e.g., "92") chosen by the student. This acts as a password.

2. The "Handshake" (Round 1): After the deadline, the IITM evaluation server will send a POST request to the student's API endpoint. This request will include the student's Secret Key in the payload.

3. Authentication & Immediate Response: The student's server must verify the secret key to ensure the request is from the official evaluator. It must then immediately return a 200 OK status code to acknowledge receipt. This starts a 10-minute timer on the evaluation server.

4. The Task (Asynchronous Processing): The request includes a "brief" (a task description, e.g., "Create a Snake & Ladder game"). The student's application must then:

- Use an LLM (via API) to generate the code for the requested application.

- Create a new public GitHub repository.

- Push the generated code to this new repo.

- Deploy the application using GitHub Pages.

5. Completion Notification: Within the 10-minute window, the student's server must send a POST request back to the evaluation server containing the URLs of the new repo and the deployed GitHub Page.

6. Round 2 (Modification): A second request may be sent to modify the existing application (e.g., "Add multi-player support"), following a similar workflow of update -> push -> notify.

# 2: FastAPI Fundamentals
The instructor transitions to a hands-on coding session to build the API server required for the project using FastAPI.

- Setup: A virtual environment is created, and dependencies like fastapi, uvicorn, and python-multipart are installed.

- Creating an App: A basic app.py is initialized. Endpoints are defined using decorators like @app.get("/").

- HTTP Methods: The difference between GET (retrieving data) and POST (sending data) is explained. The project requires handling POST requests to receive tasks.

- Path & Query Parameters:

  - Path Parameters: Variables in the URL path (e.g., /items/{item_id}).

  - Query Parameters: Key-value pairs after the ? in a URL (e.g., /search?q=apple).

- Data Validation with Pydantic: Pydantic models (classes inheriting from BaseModel) are introduced to define the structure of request and response bodies. This ensures data integrity (e.g., validating that an email string is actually an email) and provides automatic error messages.

# 3: File Uploads & Automation
Handling file uploads is crucial for more advanced API interactions.

- Single & Multiple Files: The instructor demonstrates how to create endpoints that accept file uploads (UploadFile).

- Form Data: Using Postman (or curl), files like JSON or CSV are sent to the API, and the server reads and returns their content.

- Automation with AI: A key productivity tip is shown where GitHub Copilot is used to generate curl commands or test scripts. Instead of manually clicking through Postman for every test, a script can run all test cases in seconds, significantly speeding up development.

# 4: Deployment to Hugging Face Spaces
The session concludes with deploying the FastAPI application to Hugging Face Spaces.

- Docker Containerization: A Dockerfile is created to package the Python application. It installs dependencies from requirements.txt and runs the server using uvicorn.

- Deployment Steps:

1. Create a new Space on Hugging Face (select Docker SDK).

2. Upload app.py, Dockerfile, and requirements.txt via the web interface or Git.

3. Secrets Management: Sensitive information (like API keys or the Project Secret) is stored in the Space's Settings -> Repository Secrets, not in the code. These are accessed in Python via os.getenv().


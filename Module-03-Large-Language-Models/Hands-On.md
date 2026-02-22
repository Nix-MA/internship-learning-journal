### Hands-On
---
## Chapter 01
(Note: This session was primarily conceptual, laying the groundwork for coding in the next class. However, the instructor outlined the architecture and setups required for the upcoming assignments.)

Step 1: Configuring API Keys for the Course Proxy
When using the course's AI proxy (AI Pipe), you must override the default OpenAI base URL.

1. Get the Token: Go to aipipe.org, log in with your student ID, and generate your token.
2. Set the Key Locally:
```
llm keys set openai
# Paste your AI Pipe token when prompted
```
3. Override the Base URL:
Add the proxy URL to your shell environment (e.g., ~/.bashrc or ~/.zshrc).
```
export OPENAI_API_BASE="https://api.aipipe.org/v1" # Example URL, check course docs for the exact one
```

Step 2: Structuring Output with JSON Schemas (Text Extraction)
To force an LLM to extract unstructured text into a predictable format, define a JSON schema.

Example Schema Structure for API Calls:
```
{
  "type": "object",
  "properties": {
    "state": {
      "type": "object",
      "properties": {
        "name": { "type": "string" },
        "code": { "type": "string" }
      }
    },
    "zip_code": { "type": "string" }
  },
  "required": ["state", "zip_code"]
}
```
You pass this schema in the API request payload so the LLM responds strictly with this JSON structure instead of conversational text.

Step 3: LLM Evaluation Setup (Promptfoo Concept)
To test LLM performance programmatically:

1. Create a promptfooconfig.yaml file:
```
prompts:
  - "Write a short summary of {{topic}}"
providers:
  - openai:gpt-4o-mini
  - openai:gpt-3.5-turbo
tests:
  - vars:
      topic: "Machine Learning"
    assert:
      - type: "icontains"
        value: "algorithm"
```
2. Run the evaluation (requires installing Promptfoo CLI) to generate a matrix comparing the models' speed, cost, and pass/fail rate for the assertions.

---

# Chapter 02
Step 1: Generating Text Embeddings and Calculating Similarity
To calculate the similarity between text strings using an API like AI Pipe / OpenAI.

1. Set the API Key:
```
export OPENAI_API_KEY="your_api_key_here"
```
2. Python Code to Fetch Embeddings and Calculate Similarity:
```
import os
import httpx
import numpy as np

# Define the API URL and Key
api_key = os.getenv("OPENAI_API_KEY")
url = "https://aipipe.rory.wo/v1/embeddings" # Replace with valid proxy or OpenAI URL

def get_embedding(text):
    headers = {"Authorization": f"Bearer {api_key}"}
    payload = {
        "model": "text-embedding-3-small",
        "input": text
    }
    response = httpx.post(url, headers=headers, json=payload, timeout=30.0)
    return response.json()["data"][0]["embedding"]

def get_similarity(emb1, emb2):
    # Dot product normalized by the magnitudes of the vectors
    dot_product = np.dot(emb1, emb2)
    norm1 = np.linalg.norm(emb1)
    norm2 = np.linalg.norm(emb2)
    return dot_product / (norm1 * norm2)

# Test the similarity
emb_apple = get_embedding("apple")
emb_orange = get_embedding("orange")
emb_lightning = get_embedding("lightning")

print("Apple vs Orange:", get_similarity(emb_apple, emb_orange))
print("Apple vs Lightning:", get_similarity(emb_apple, emb_lightning))
```
Step 2: Generating Multimodal Embeddings (Nomic AI)
Using Nomic to get image and text embeddings in the same vector space.

1. Bash Script to get Image Embedding:
```
curl -X POST "https://api-atlas.nomic.ai/v1/embedding/text" \
  -H "Authorization: Bearer YOUR_NOMIC_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "nomic-embed-vision-v1.5",
    "images": [
      "base64_encoded_string_of_cat_image",
      "base64_encoded_string_of_box_image"
    ]
  }' > image_response.json
```
Step 3: Building a Simple RAG Application
1. Create the Vector Collection (JSON Database):
```
import json

# Assume `chunks` is a list of strings from your Markdown files
collection = []
for chunk in chunks:
    embedding = get_embedding(chunk)
    collection.append({
        "source": "filename.md",
        "text": chunk,
        "embedding": embedding
    })

with open("vector_db.json", "w") as f:
    json.dump(collection, f)
```
2. Query the Vector Database:
```
# Load collection
with open("vector_db.json", "r") as f:
    db = json.load(f)

question = "Which operator converts a value to a boolean?"
q_emb = get_embedding(question)

results = []
for item in db:
    sim = get_similarity(q_emb, item["embedding"])
    results.append({
        "similarity": sim,
        "text": item["text"],
        "source": item["source"]
    })

# Sort by highest similarity
results.sort(key=lambda x: x["similarity"], reverse=True)

# Print the top match
print("Top Match Source:", results[0]["source"])
print("Content:", results[0]["text"])
```

---

# Chapter 03
Note: As this was a Q&A and troubleshooting session, there was no live coding or step-by-step technical demonstration. The following steps summarize the solutions provided verbally for common student issues.

Troubleshooting Step: Configuring AI Pipe/Proxy for LLMs
If you are receiving "API Key Expired" or quota errors when trying to use OpenAI models for your assignments, you must route your requests through the course proxy.

1. Get your AI Pipe Token: Log in to the AI Pipe portal using your student credentials to retrieve your specific access token.

2. Set Environment Variables: Do not put the token directly in your code. Set it in your .env file or system environment.
```
# Set the token as your API key
export OPENAI_API_KEY="your_ai_pipe_token_here"
```
3. Change the Base URL: You must redirect the API calls from OpenAI's default servers to the course proxy.
```
# Update the base URL in your environment or code configuration
export OPENAI_BASE_URL="https://aipipe.your-course-url.com/v1"
```
Troubleshooting Step: Enabling Missing Checkboxes in GA
If you encounter a Graded Assignment question (like Week 3, Question 3) where the submission checkbox is hidden or disabled:

1. Open Chrome Developer Tools (Right-click -> Inspect, or F12).

2. Use the Element Selector tool to click on the area where the checkbox should be.

3. In the HTML DOM tree, locate the <input type="checkbox"> element.

4. Remove the disabled or hidden attribute from the HTML tag to make the checkbox interactive. (This tests the web scraping and DevTools concepts taught in the course).

---

# Chapter 04
Step 1: Environment Setup (API Key & Proxy)
Set up your API key in your terminal profile so you don't hardcode it into scripts.

1. Open your bash configuration:
```
nano ~/.bashrc
```
2. Add your AI Pipe (or OpenAI) key at the bottom:
```
export OPENAI_API_KEY="your_ai_pipe_token_here"
```
3. Save, exit, and reload the terminal (or run source ~/.bashrc).

Step 2: Build a Chatbot with Memory (httpx)
Create a simple CLI chatbot that remembers context.
```
import os
import httpx

# Configuration
API_KEY = os.getenv("OPENAI_API_KEY")
# Using the course proxy URL instead of api.openai.com
URL = "https://aipipe.rory.wo/v1/chat/completions" 

headers = {
    "Authorization": f"Bearer {API_KEY}",
    "Content-Type": "application/json"
}

# Initialize message history with a System Prompt
messages = [
    {"role": "developer", "content": "Answer concisely in less than 10 words."}
]

def get_ai_response(msg_list):
    payload = {
        "model": "gpt-4o-mini", # Cost-effective model
        "messages": msg_list
    }
    # Using timeout=15 as LLMs can take time to respond
    response = httpx.post(URL, headers=headers, json=payload, timeout=15.0)
    data = response.json()
    # Parse the response dictionary
    return data["choices"][0]["message"]["content"]

# Chat Loop
while True:
    user_input = input("You: ")
    if user_input.lower() == "exit":
        break
    
    # Add user query to history
    messages.append({"role": "user", "content": user_input})
    
    # Get and print AI response
    ai_reply = get_ai_response(messages)
    print(f"AI: {ai_reply}\n")
    
    # Add AI reply to history for the next turn
    messages.append({"role": "assistant", "content": ai_reply})
```
Step 3: Base64 Image Encoding
Convert an image to Base64 to send it to the API.
```
import base64

def encode_image(image_path):
    with open(image_path, "rb") as image_file:
        binary_data = image_file.read()
        # Encode to base64 string
        base64_encoded = base64.b64encode(binary_data).decode('utf-8')
    return base64_encoded

base64_image = encode_image("product.png")
image_uri = f"data:image/png;base64,{base64_image}"

# Adding image to the API message payload:
messages = [{
    "role": "user",
    "content": [
        {"type": "text", "text": "Extract details from this image."},
        {"type": "image_url", "image_url": {"url": image_uri}}
    ]
}]
```
Step 4: Forcing Structured Output (Function Calling)
Pass a tools parameter to the API request to force JSON output based on an image.
```
# Define the expected JSON structure
tools = [{
    "type": "function",
    "function": {
        "name": "extract_product_details",
        "description": "Extract manufacturing and expiry dates from the product image.",
        "parameters": {
            "type": "object",
            "properties": {
                "name": {"type": "string", "description": "Name of the product"},
                "mfd_year": {"type": "number", "description": "Manufacturing year"},
                "exp_year": {"type": "number", "description": "Expiry year"}
            },
            "required": ["name", "mfd_year", "exp_year"]
        }
    }
}]

payload = {
    "model": "gpt-4o-mini",
    "messages": messages, # Messages array from Step 3 containing the image
    "tools": tools,
    "tool_choice": "required" # Forces the model to use the tool
}

response = httpx.post(URL, headers=headers, json=payload, timeout=20.0)
data = response.json()

# The structured output is found deep in the response JSON:
tool_call_args = data["choices"][0]["message"]["tool_calls"][0]["function"]["arguments"]
print(tool_call_args) 
# Output: {"name": "Medicine", "mfd_year": 2021, "exp_year": 2024}
```

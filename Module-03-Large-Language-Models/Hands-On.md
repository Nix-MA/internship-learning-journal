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




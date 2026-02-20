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

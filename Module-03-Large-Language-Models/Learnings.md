### Key Learnings 
---
## Chapter 01
- Context is the Bottleneck: LLM hallucinations are primarily a result of limited context windows. Treating them as reasoning engines rather than encyclopedias yields better results.

- Embeddings Bridge the Gap: Converting data into vectors (embeddings) allows for semantic searching. This is the foundation of RAG, which grounds the LLM in factual, custom data.

- Function Calling Drives Automation: The true power of LLMs in applications isn't just generating text; it's translating natural language into structured API calls (JSON) that trigger backend system functions.

- Structured Output is Mandatory: For text extraction (e.g., parsing invoices), always use JSON schemas in your prompts to guarantee the output can be parsed by your code.

- Evaluate Before Production: Never assume a prompt that works once will work always or that a more expensive model is necessary. Use tools like promptfoo to rigorously test prompts against multiple models for cost, speed, and accuracy regression.

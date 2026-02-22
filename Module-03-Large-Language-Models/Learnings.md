### Key Learnings 
---
## Chapter 01
- Context is the Bottleneck: LLM hallucinations are primarily a result of limited context windows. Treating them as reasoning engines rather than encyclopedias yields better results.

- Embeddings Bridge the Gap: Converting data into vectors (embeddings) allows for semantic searching. This is the foundation of RAG, which grounds the LLM in factual, custom data.

- Function Calling Drives Automation: The true power of LLMs in applications isn't just generating text; it's translating natural language into structured API calls (JSON) that trigger backend system functions.

- Structured Output is Mandatory: For text extraction (e.g., parsing invoices), always use JSON schemas in your prompts to guarantee the output can be parsed by your code.

- Evaluate Before Production: Never assume a prompt that works once will work always or that a more expensive model is necessary. Use tools like promptfoo to rigorously test prompts against multiple models for cost, speed, and accuracy regression.

---

## Chapter 02
- Embeddings: Text and images can be converted into arrays of numbers (vectors). The semantic meaning is captured by the position of the vector in a high-dimensional space.

- Cosine Similarity: The standard mathematical method to compare embeddings. It involves taking the dot product of two vectors and normalizing it, resulting in a score between 0 and 1 (where 1 is highly similar).

- Multimodal Spaces: Advanced models map different data types (like an image of a cat and the word "cat") to the exact same area in a vector space, enabling cross-media search.

- RAG Limitations & Chunking: You cannot feed an entire code repository or book into an LLM prompt due to strict token limits. You must "chunk" the data, convert the chunks to embeddings, and use similarity search to retrieve only the 3 or 4 most relevant chunks to send to the LLM.

- Cost Efficiency: Storing calculated embeddings in a local file (like a JSON vector database) prevents you from having to repeatedly call the API for the same text, heavily reducing API costs and latency.

---

## Chapter 03
- AI Pipe over OpenAI: To avoid billing issues and API limits, always use the provided AI Pipe or AI Proxy tokens and update the Base URL accordingly when completing assignments requiring LLMs.

- Project Prerequisite vs. Final Score: In automated evaluations, an initial "perfect" score (like 2/2) often just indicates that your server passed the health check (it is alive and responding). It does not mean your application logic is correct.

- Course Philosophy: The goal of the course is not to memorize every CLI command, but to learn how to quickly read documentation, use AI assistants, and integrate multiple tools to deploy a working data science application.

- Resume Building: Building and deploying an end-to-end application (like an LLM chatbot hosted on Hugging Face or Vercel with a public GitHub repo) is one of the most effective ways to demonstrate practical software engineering and data science skills to employers.

---

# Chapter 04
- Statelessness of LLMs: The API itself has no memory. To create conversational bots, you must manually manage an array of messages and send the entire chat history with every single request.

- Vector Math for Similarity: To find how similar two text strings or images are, you use embedding models to convert them to vectors. You then compare them using Cosine Similarity (higher is better) or Euclidean Distance (lower is better).

- Multimodal Compatibility: For cross-modal comparisons (e.g., comparing an image to a text string), you must use a specific multimodal embedding model (like Jina AI) so that both outputs share the exact same dimensional space.

- Function Calling for Extraction: When you need reliable data extraction (like pulling dates from an invoice to put in a database), do not rely on standard text prompting. Define a strict JSON schema using the tools and tool_choice parameters to guarantee structured, parseable output.

- Base64 Necessity: When dealing with standard REST APIs that accept JSON, you cannot send raw binary image files. You must encode them into Base64 strings first.

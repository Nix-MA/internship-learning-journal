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

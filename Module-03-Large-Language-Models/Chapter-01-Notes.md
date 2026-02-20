### Week 03, Session 01: LLM Fundamentals, Embeddings, and Applications
---
# 1: How LLMs Actually Work
The session starts by demystifying Large Language Models (LLMs). The instructor emphasizes that LLMs are not sentient beings but are grounded in the mathematical concept of transformers.

- Tokens & Vectors: When a user inputs a prompt, the text is broken down into "tokens" (parts of words). Each token is represented internally by a multi-dimensional vector (e.g., a 1600-feature vector).

- Self-Attention: A core mechanism in transformers is "self-attention." This allows the model to look at the context of a word (e.g., does "it" refer to the "animal" or the "road" in a sentence?) and assign probabilities to understand the precise meaning within that specific context.

- Context Windows: The biggest limitation of LLMs is their context window (how much memory/text they can hold at once). While older models were limited (e.g., 128k tokens), newer ones can hold up to 1 million tokens. However, once the conversation exceeds this window, the model starts "hallucinating" or forgetting earlier instructions.

# 2: Embeddings & Vector Databases
To overcome the limitations of the context window and general training data, the concept of Embeddings is introduced.

- What are Embeddings? Embeddings convert text, images, or audio into numerical vectors. If two pieces of data have similar meanings or contexts, their vectors will be mathematically close to each other in the vector space.

- Multimodal Embeddings: This allows different data types (like an image of a cat and the word "cat") to map to the same vector space, enabling features like searching for photos using natural language.

- Vector Databases: Once data is embedded into vectors, it must be stored efficiently. Vector databases like DuckDB, SQLite (with vector extensions), ChromaDB, or LanceDB are used to store and quickly query these massive mathematical representations.

# 3: RAG (Retrieval-Augmented Generation) & Hybrid Search
RAG is presented as the primary solution to LLM hallucinations and context limitations in enterprise applications.

- How it works: Instead of relying on the LLM's internal memory, you convert your company's specific documents into embeddings and store them in a vector database. When a user asks a question, the system first retrieves the most relevant document chunks from the database and then feeds that specific context to the LLM to generate an accurate answer.

- Hybrid RAG: Standard vector search relies purely on contextual similarity, which can sometimes miss exact keyword matches. TypeSense is introduced as a tool for Hybrid RAG, combining the precision of traditional keyword search with the contextual understanding of vector embeddings to yield the best results.

# 4: Vision Models and Base64 Encoding
LLMs primarily process text. To analyze non-text data like images or videos, the data must be encoded.

- Base64 Encoding: This technique takes binary data (like an image) and converts it into a string of standard text characters. This text string is then sent to the LLM's API. The LLM decodes it back into an image internally to process it.

- Analyzing Video: Videos are just a sequence of images (frames). By extracting frames at intervals (e.g., every 10 seconds) and sending them to a vision-capable LLM via Base64, you can build applications for automated proctoring (catching cheating behavior in online exams) or workplace safety monitoring (identifying safety violations on a factory floor).

# 5: Prompt Engineering & Function Calling
The session concludes with advanced ways to structure LLM interactions.

- Prompt Engineering: Writing detailed, structured prompts is critical for consistent, scalable applications. Techniques include using XML tags <instruction>, <example> or Markdown/JSON structures to guide the LLM's output.

- Function Calling (Tools): This is how you make LLMs take action. You provide the LLM with a JSON schema defining the functions your backend system can perform (e.g., book_flight(origin, destination)). The LLM processes the user's natural language, extracts the required arguments, and returns a structured JSON object telling your application exactly which function to execute.

- LLM Evaluation (Promptfoo): For commercial applications, testing prompts is mandatory. Tools like Promptfoo use YAML files to run automated tests, comparing different models (e.g., GPT-3.5 vs GPT-4) against specific prompts to measure cost, speed, and accuracy, ensuring updates don't break the application.

# 📁 Data Sourcing & Web Engineering: The Fundamentals

This guide covers the journey from identifying a data source to automating the extraction process using modern libraries, AI vision, and cloud automation.

---

## 🏗️ 1. Core Concepts (The Basics)

### **Data Sourcing**
The process of identifying and gathering raw information from various locations (databases, sensors, or websites) to solve a specific problem. Think of it as a chef selecting high-quality ingredients before cooking.



### **Web Crawling vs. Scraping**
* **Crawling:** An automated "Spider" that browses the web to map out links (e.g., how Google Search works).
* **Scraping:** The surgical extraction of specific data (prices, titles, dates) from a webpage's HTML code.

---

## 🛠️ 2. The Scraping Toolkit

Depending on the complexity of the source, we use different tools:

| Tool | Role | Best For |
| :--- | :--- | :--- |
| **Excel Power Query** | No-Code Extraction | Quick, live-connected tables (e.g., Weather forecasts). |
| **BeautifulSoup4** | HTML Parsing | Static pages where data is held in clear tags (e.g., IMDB). |
| **Wikipedia Lib** | API Wrapper | Structured knowledge extraction without manual parsing. |
| **Playwright** | Browser Automation | Dynamic sites that require clicking, scrolling, or logins. |
| **Tabula-py** | PDF Extraction | Converting tables inside PDFs (like Sports Handbooks) to CSV. |



### **Advanced Performance Tools**
* **HTTPX:** Faster, modern version of `requests` supporting asynchronous tasks.
* **LXML:** An industrial-strength parser for high-speed processing of thousands of lines of code.

---

## 🤖 3. Modern & AI-Driven Extraction

### **Vision-Based Scraping (Gemini Flash)**
Instead of parsing messy HTML DOM trees, we record the screen (1 FPS) and use Multimodal LLMs to extract data.
* **Pros:** Bypasses complex JS/CSS; handles dynamic apps easily.
* **Cost:** Highly efficient (~$0.04 for 20 frames).

### **Document Standardization (MarkItDown)**
Microsoft’s tool to convert PDFs, Excel, and PPTs into clean **Markdown**. This is a foundational step for **RAG (Retrieval-Augmented Generation)** pipelines, ensuring LLMs receive high-quality, structured text.

### **LLM Extraction**
Using AI to find "needles in haystacks." You provide the raw HTML/Text to an LLM, and it identifies entities (Product Name, Price, Date) even if the website layout changes frequently.

---

## ⏰ 4. Automation & Workflows (GitHub Actions)

We use **GitHub Actions** to move from manual scripts to scheduled "live" data pipelines.

* **The Trigger:** A "Cron" schedule (e.g., `0 8 * * *` for daily at 8 AM UTC).
* **The Environment:** A virtual Ubuntu runner that installs dependencies (`pip install`).
* **The Storage:** Automatically committing the updated `.json` or `.csv` back to the repository.



---

## 💡 Technical Takeaways & Best Practices

1.  **Caching is Critical:** Use the `cached_get()` pattern during development to avoid hitting servers repeatedly and speed up debugging.
2.  **Incremental Saving:** Always write your output to a file *inside* the loop. If the script crashes after 4 hours, you won't lose your data.
3.  **XPath > Guesswork:** Use stable container IDs and `contains()` functions in XPath for more resilient scrapers.
4.  **Semantic Search:** Scraped data isn't just for tables; it can be used to build **Semantic Search Engines** using embeddings to find meaning rather than just keyword matches.
5.  **Vibe Coding:** Focus on the "idea-first" development. Use AI to handle the syntax while you focus on the logic, modularity, and product design.

---


## 🏗️ 1. Understanding APIs (The Foundation)
An **API (Application Programming Interface)** acts as a structured "waiter" between a client and a server.

### Key Concepts
* **Request-Response Cycle:** Sending a message to an **Endpoint** with specific **Parameters** (e.g., `city=Mumbai`) and receiving a **JSON** response.
* **Geocoding (Nominatim):** Using OpenStreetMap’s API via `geopy` to convert text addresses into coordinates ($Latitude, Longitude$).
* **Library Wrappers:** Tools like the `wikipedia` Python library simplify complex API calls into simple functions like `wikipedia.summary()`.

---

## 🕷️ 2. Web Scraping Methodologies
When a structured API isn't available, we use scraping to "read" the visual interface of the web.

### A. Static Scraping (BeautifulSoup & LXML)
Best for HTML that doesn't change after the page loads.
* **Tools:** `requests`, `httpx`, `BeautifulSoup`, `lxml`.
* **IMDb Extraction:** Scraping top-rated movies, release years, and ratings.
* **DocSearch Project:** A robust crawler using `hashlib` for caching and `tqdm` for progress tracking of ~7,000 articles.

### B. Dynamic & Browser Automation (Playwright)
Used for websites that require JavaScript execution or user interaction (clicking, scrolling).
* **Key Feature:** Headless browser control via `sync_playwright` to scrape JS-heavy sites like `quotes.toscrape.com`.

### C. PDF Data Extraction (Tabula)
Extracting structured tables from documents like Premier League Handbooks.
* **Workflow:** Parsing web links with `BeautifulSoup`, downloading binary PDF content, and using `tabula-py` to convert specific page areas into `.csv`.

---

## 🤖 3. Next-Gen & No-Code Extraction

### Vision-Based Scraping (Gemini Flash)
* **Concept:** Record the screen (1 FPS) and let AI extract structured JSON from the video frames.
* **Benefit:** No HTML parsing required; works on any visual interface (e.g., social media feeds).

### Microsoft MarkItDown
* **Purpose:** Converting "messy" files (PDF, Excel, Word, PPT) into clean **Markdown**.
* **Use Case:** Preparing unstructured enterprise documents for **RAG (Retrieval-Augmented Generation)** pipelines.

### No-Code Tools
* **Excel Power Query:** `Data > From Web` to create live, refreshable data connections.
* **Google Sheets:** Using `=IMPORTHTML("URL", "table", index)` for instant data pulls.

---

## ⏰ 4. Automation & Workflows

### GitHub Actions
Automate scripts to run on a schedule (Cron) without keeping your computer on.
* **Path:** `.github/workflows/main.yml`
* **Cron Format:** `* * * * *` (Minute, Hour, Day, Month, Day of Week).
* **Example:** `0 8 * * *` runs daily at 8:00 AM UTC.

---

## 🛠️ Tech Stack Summary

| Category | Tools & Libraries |
| :--- | :--- |
| **Languages** | Python, JavaScript (Console) |
| **APIs** | Nominatim (Geocoding), OpenAI, BBC Weather |
| **HTML Parsing** | BeautifulSoup, LXML, XPath |
| **Automation** | Playwright, GitHub Actions |
| **Data Handling** | Pandas, JSON, CSV |
| **PDF/Docs** | Tabula, MarkItDown |

---

## 🚀 How to Use
1.  **Clone the Repo:** `git clone <repo-url>`
2.  **Install Dependencies:** `pip install -r requirements.txt`
3.  **Environment Variables:** Store API keys in a `.env` file to keep them secure.
4.  **Run Scripts:** Use Jupyter Notebooks or `python script_name.py` to execute.

---
*Developed as part of the "Tools in Data Science" curriculum.*

# 🧹 The Data Cleaning & Preparation Master Guide

Data cleaning is the process of fixing "messy" data so it can be used for reliable analysis. This guide covers techniques ranging from Excel basics to advanced Shell scripting and Python-based automation.

---

## 📊 1. Data Cleaning in Microsoft Excel
Excel is the primary tool for "point-and-click" cleaning of smaller datasets (<100k rows).

### **Core Workflows**
* **Find and Replace (Ctrl + H):** Removing unwanted artifacts like `[more]` from scraped Wikipedia text.
* **Text to Columns:** Splitting combined strings (e.g., `Senator (Party-State)`) into separate structured columns using delimiters like `(`, `-`, and `)`.
* **Data Formatting:** Converting "General" text to "Number" to enable mathematical calculations.
* **TRIM() Function:** Removing hidden leading/trailing spaces that break search formulas.
* **Pivot Tables:** Used for **Data Profiling**—identifying outliers, counting frequencies, and detecting duplicate records by country or category.

---

## 🐚 2. Data Preparation in the Shell (Linux/Colab)
The Shell is a power tool for processing massive files (like web server logs) that would crash standard spreadsheet software.

### **The Log Processing Pipeline**
To identify the top 25 high-traffic IP addresses from a `.log` file:
```
!cut -d " " -f 1 access.log | sort | uniq -c | sort -nr | head -n 25
```
1. cut: Extracts the IP column.

2. sort: Alphabetizes data (required for uniq).

3. uniq -c: Collapses duplicates and counts occurrences.

4. sort -nr: Sorts numerically in reverse (highest traffic first).

## Pattern Matching with grep & sed
- grep "bot": Instantly filters thousands of rows to find automated crawler activity.

- sed: Globally replaces characters (e.g., turning brackets into quotes) to convert raw logs into CSV-ready formats.

---

## 🛠️ 3. Specialized Cleaning Tools
# OpenRefine (The "Power Washer")
Best for inconsistent text (e.g., "Google Inc" vs "google").

- Text Faceting: Visualizes the distribution of unique values.

- Clustering: Uses algorithms (Fingerprint, N-gram) to find similar-looking entries and merge them into a single standard value.

#  VS Code (JSON & Code Cleaning)
- Prettify: Ctrl + Shift + P > "Format Document" to turn a single-line JSON into a readable tree.

- Multi-Cursor Editing: Alt + Enter after a search to edit hundreds of lines simultaneously.

---

##  🐍 4. Programmatic Preparation (Python)
# Pandas Profiling
Instead of manual inspection, use pandas_profiling.ProfileReport to generate an HTML dashboard showing:

- Correlations between variables.

- Missing value percentages.

- Statistical outliers.

# Pillow (Image Processing)
Automating the "cleaning" of image datasets for Machine Learning:

- Batch resizing (generating 300x300 thumbnails).

- Format conversion (JPEG → PNG).

- Applying filters (Grayscale, Gaussian Blur).

# JSON API Analysis
Fetching and cleaning data from live APIs (like Homebrew):

1. requests.get(): Fetching the raw JSON.

2. json.dumps(indent=2): Inspecting the nested structure.

3. Sorting: Writing custom Python functions to rank data by specific metrics (e.g., 30-day installation counts).

---

## 🎞️ 5. Multimedia Engineering (FFMPEG)
For non-text data, FFMPEG is the industry standard for command-line media cleaning.

- Conversion: ffmpeg -i input.avi output.mp4

- Optimization: Adjusting bitrates (-b:v) and Constant Rate Factors (-crf) to balance quality and file size.

- Filtering: Rotating, scaling, and adjusting audio volume via the command line.

---

### 📈 Summary Comparison: Data Cleaning Environments

| Environment | Best For | Key Advantage |
| :--- | :--- | :--- |
| **Excel** | Small datasets (<100k rows) & Pivot Tables | Visual, intuitive, and point-and-click. |
| **Shell (Terminal)** | Massive log files (GBs) & rapid filtering | Extreme speed and powerful command "pipelining." |
| **OpenRefine** | Messy or inconsistent text/naming | Advanced clustering and merging algorithms. |
| **Python** | Automated, repeatable workflows | Highly scalable, customizable, and integration-ready. |

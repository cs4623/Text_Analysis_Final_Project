# White House Framing of the Middle Class and Tax Fairness

Final project for **Intro to Text Analysis in Python**.  
Notebook: `final_project_kellysun.ipynb`

This project analyzes how the Biden White House talks about the **“middle class / working families”** compared with **“tax fairness / the wealthy”** in official economic statements. Using basic text-analysis tools in Python, it compares vocabulary, tone, and named actors across the two frames.

---

## 1. Research Question

> How does the White House frame the “middle class / working families” versus “tax fairness and the wealthy” in its economic messaging?

The analysis focuses on:
- What kinds of **issues and policies** co-occur with each frame (TF–IDF / bigrams).
- Whether the overall **tone** differs between the two frames (sentiment).
- Which **people, organizations, and groups** are most associated with each frame (NER).

---

## 2. Data

- Source: [Biden White House – Briefing Room: Statements & Releases](https://bidenwhitehouse.archives.gov/briefing-room/statements-releases/)
- Initial scrape: 200 statements (titles, dates, URLs, full text).
- Analysis subset: 46 statements with at least one of two keyword-based frames:
  - “middle class”, “working families”, “family budget”, “cost of living”, etc.
  - “tax”, “fair share”, “billionaires”, “wealthiest”, “loopholes”, etc.
- Only English-language text is used.

All scraping and cleaning are done in code so the corpus can be reproduced.

---

## 3. Methods (Notebook Outline)

The main steps in `final_project_kellysun.ipynb` are:

1. **Scraping & Raw Data Snapshot**
   - Use `requests` + `BeautifulSoup` to collect statement metadata and full text.
   - Store results in a pandas DataFrame `df`.

2. **Framing & Filtering**
   - Tag statements with two Boolean columns:
     - `middle_class_frame`
     - `tax_fairness_frame`
   - Extract only sentences that contain framing keywords into `filtered_text`.
   - Build an analysis subset `econ_df` with non-empty framed text.

3. **TF–IDF & Framing Comparison**
   - Clean text (lower-case, remove non-alphabetic chars, stopwords, White House boilerplate).
   - Use `TfidfVectorizer` on unigrams + bigrams (`ngram_range=(1, 2)`).
   - Compare TF–IDF scores between the two corpora and plot:
     - Most distinctive bigrams for **Middle Class / Working Families**.
     - Most distinctive bigrams for **Tax Fairness / Wealthy**.

4. **Sentiment Analysis**
   - Apply VADER `SentimentIntensityAnalyzer` on `filtered_text`.
   - Compute average compound sentiment for each frame.
   - Summarize differences in tone between middle-class and tax-fairness messages.

5. **Named Entity Recognition (NER)**
   - Use spaCy to extract named entities from `filtered_text`.
   - Keep human, organization, geopolitical, and group labels.
   - Build frequency tables and bar charts for entities that are:
     - More frequent in middle-class framing.
     - More frequent in tax-fairness framing.

6. **Discussion**
   - Interpret how the two frames differ in:
     - Level of language (household vs. system).
     - Overall tone.
     - Key actors and targets.

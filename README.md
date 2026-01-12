# Advanced-Portfolio-Intelligence-Through-Semantic-Analysis-
A production-grade AI system that identifies, classifies, and backtests investment opportunities across emerging technology themes using LLM summarization, semantic embeddings, hybrid search, and quantitative portfolio analytics.

This project was developed as part of Low Risk Capital Management’s (LRCM) initiative to modernize thematic investing beyond traditional GICS/BICS sector classifications.

## **Project Overview**

Modern technology companies no longer fit cleanly into legacy sectors.
This system builds an end-to-end pipeline that:

- Extracts company intelligence from multiple data sources

- Generates high-signal LLM summaries from long corporate text

- Produces and evaluates advanced text embeddings

- Enables hybrid semantic search (sparse + dense)

- Uses LLMs to classify companies into specific thematic mandates

- Constructs and backtests 10 thematic portfolios over 5 years

The final deliverable replicates the process used by institutional quantitative research teams to evaluate thematic investment strategies.

---

## **Part 1 — Data Warehouse Construction**
Built a modular, self-healing ETL pipeline using:

- Wikipedia API (primary source)

- Bing Search + Selenium (fallback)

- yfinance summaries (final fallback)

Each document is validated, cleaned, and tagged with a resolver method, achieving 98%+ coverage.
Data is stored in MongoDB with composite indexes for fast retrieval and iterative processing.

----

##  **Part 2 — LLM Summarization Pipeline**

Long-form company articles (~15k words) are distilled using a two-stage MapReduce design:

- Chunk articles into ~1500-word segments

- Extract material investment information

- Synthesize a structured company summary with Pydantic-enforced JSON

- Store all summaries directly in MongoDB
This creates a high-signal text representation suitable for embeddings and search.
---

## **Part 3 — Embedding Evaluation & Model Selection**

Conducted a comprehensive embedding bake-off across:

- BAAI BGE Small & Large

- MPNet

- Nomic Embed (with task prefixes: classification, clustering, query, document)

Two input modes were tested:

- Full wiki_content

- Structured SUMMARY_only

Evaluated using:

- Silhouette Score (cosine)

- Chunk-and-aggregate embedding strategies

- Market correlation precision@k (optional)

Final model selection:
- SUMMARY_only + nomic classification: (highest semantic separability).

---

## **Part 4 — Semantic Search Engine**

Implemented three search architectures:

### **1. Sparse Search (BM25)**

MongoDB Atlas Search with English analyzer, stemming, and stop-word removal.

### **2. Dense Search**

Cosine similarity using the selected Nomic embedding.

### **3. Hybrid Search (RRF Fusion)**

Reciprocal Rank Fusion combining sparse and dense results to improve recall and precision.

The search engine effectively returns high-quality companies for themes such as AI infrastructure, cloud hyperscalers, robotics, and cybersecurity.

---

## **Part 5 — Thematic Portfolio Construction & Backtesting**
### **LLM-as-a-Filter Classification**

Hybrid search provides a candidate list of companies per theme.
An LLM classifier then labels each company as:

- core (direct exposure)

- secondary

- not_relevant

Human-in-the-loop corrections ensure accurate thematic baskets.

### **Portfolio Backtesting (5 Years)**

For each of the 10 themes:

- Download daily data via yfinance

- Construct equal-weighted, daily-rebalanced portfolios

- Generate synthetic OHLC series

- Compare performance against benchmarks (QQQ, ARKK)
---

### **Final Deliverables**

- Multi-theme cumulative return comparison

- Cross-theme correlation heatmap

- Detailed candlestick analysis for best-performing theme

- 1-page Investment Committee Memo summarizing results

---

 ## **Technologies Used**
### **Data Engineering:**
Python, Pandas, NumPy, Selenium, yfinance, MongoDB Atlas, pymongo

### **LLMs & Embeddings:**
Ollama (gemma models), Pydantic, Nomic, BGE, SentenceTransformers

### **Search & Retrieval:**
MongoDB Atlas Vector Search, BM25, Reciprocal Rank Fusion

### **Backtesting & Visualization:**
plotly, pandas, yfinance, seaborn/matplotlib

---

### **Project Outcomes**
This system produces:

- Accurate company-level intelligence for emerging tech themes

- High-performing semantic embeddings suitable for production search

- Clean thematic baskets validated by LLMs + human SME review

- Quantitative performance analysis for institutional use

- The result is a scalable research pipeline that bridges NLP, vector search, and quantitative finance.

---


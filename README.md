# Google Merchandise Store — User Behavior Analysis

A solo practice project exploring behavioral patterns in the GA4 Google Merchandise Store dataset via BigQuery. The goal is to identify distinct user segments through EDA, k-means clustering, and data visualization.

---

## Business Question

**What distinguishes users who convert from those who abandon the funnel?**

Secondary questions:
- Which behavioral patterns cluster into meaningful user segments?
- What product categories and traffic sources correlate with conversion?
- Can data-driven personas be derived from session-level behavior alone?

---

## Dataset

**Source:** GA4 Obfuscated Sample Ecommerce Dataset  
**Access:** BigQuery Public Data (`bigquery-public-data.ga4_obfuscated_sample_ecommerce`)  
**Grain:** Event-level (one row per user interaction)  
**Coverage:** Real GA4 data from the Google Merchandise Store, obfuscated for privacy

> Note: Demographic inference from browsing data is intentionally excluded from this analysis. Device type, product category, and traffic source do not reliably proxy for demographic attributes (shared devices, gift purchasing, diverse use cases).

---

## Approach

### Phase 1 — Data Extraction
- SQL queries in BigQuery to export session-level and event-level data
- Export to CSV, load into local environment

### Phase 2 — EDA
- Data quality check (nulls, duplicates, event distribution)
- Funnel analysis: session start → product view → add to cart → purchase
- Traffic source breakdown
- Device and category distribution
- Conversion rate by segment

### Phase 3 — Clustering
- Feature engineering: session depth, items viewed, conversion flag, category spread
- k-means clustering with Elbow Method to determine optimal k
- Cluster interpretation and persona naming

### Phase 4 — Visualization
- Persona dashboard (React)
- Tableau story with one chapter per persona

---

## Tech Stack

| Layer | Tool |
|---|---|
| Data extraction | BigQuery (SQL) |
| EDA + Clustering | Python, Pandas, scikit-learn |
| Visualization | Matplotlib, Seaborn |
| Dashboard | Tableau Desktop, React |
| Environment | Jupyter Notebook |
| Version control | Git / GitHub |

---

## Repo Structure

```
/data
  /raw          # BigQuery exports — not committed to Git
  /processed    # Cleaned and feature-engineered data
/notebooks
  01_eda.ipynb
  02_clustering.ipynb
/sql
  capstone_bigquery.sql
/dashboard
  /tableau
  /react
/docs
README.md
.gitignore
requirements.txt
```

---

## Setup

```bash
git clone <repo-url>
cd <repo-name>
pip install -r requirements.txt
jupyter notebook
```

BigQuery access requires a Google account with BigQuery Sandbox enabled (free tier, no billing required).

---

## Status

- [x] Repo initialized
- [ ] BigQuery access verified
- [ ] SQL extraction complete
- [ ] EDA notebook complete
- [ ] Clustering notebook complete
- [ ] Dashboard complete

---

## Author

Sebastian Weber — UX/UI Designer & Data Analytics Student  
[sebastian-weber.github.io](https://sebastian-weber.github.io) · Cologne, Germany
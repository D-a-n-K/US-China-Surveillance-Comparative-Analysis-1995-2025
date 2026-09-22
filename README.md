# NYT Surveillance Coverage: A Text Mining Analysis

**SIS/ITEC 724 — Spring 2026 — Professor Cogburn**
Author: Daniel Chavez

## Project Overview

A longitudinal text mining analysis of *New York Times* coverage of government
surveillance from 1995–2025, comparing how U.S. and PRC surveillance are
framed across roughly 13,000 articles (~7,621 U.S. / ~5,391 PRC). Articles
were exported from ProQuest TDM Studio as two CSV files and analyzed using
both R (tidytext, tm, quanteda) and Python (VADER, gensim) via `reticulate`,
following the CRISP-DM process.

## Research Questions

- **RQ1 — Longitudinal sentiment trends**
  - RQ1.1: Overall trajectory of sentiment toward government surveillance, 1995–2025 (Bing lexicon, loess trend)
  - RQ1.2: Does VADER converge with dictionary-based sentiment? (triangulation)
- **RQ2 — Dominant frames and themes**
  - RQ2.1: Most frequent terms and bigrams characterizing coverage (word frequency, n-grams, TF-IDF)
  - RQ2.2: Latent topics via LDA, and how topic proportions shift across eras
  - RQ2.3: Which emotional frames (NRC emotions) dominate coverage?
- **RQ3 — U.S. vs. PRC framing differences**
  - RQ3.1: Words that statistically distinguish U.S. from PRC coverage (quanteda keyness/chi-squared)
  - RQ3.2: How sentiment trajectories differ between the two corpora
  - RQ3.3: Does the semantic neighborhood of "surveillance" differ across corpora? (GloVe + Word2Vec)
- **RQ4 — Event-driven shifts**
  - RQ4.1: Publication volume and sentiment shifts around 9/11 (2001) and the Snowden revelations (2013)
  - RQ4.2: How AI-enabled surveillance (~2017) corresponds with vocabulary and tone changes

## Repository Contents

```
.
├── Midterm Daniel Chavez.qmd          # Full analysis (Quarto, R + Python)
├── Midterm-Daniel-Chavez.pdf          # Rendered report
├── Daniel_Chavez_Assignment_8_Code Report.pdf
└── Data/
    ├── NYT US Sentiment.csv           # U.S. surveillance coverage corpus
    └── NYT China Sentiment extended.csv  # PRC surveillance coverage corpus
```

Each CSV row is one article with full metadata (title, date, authors,
publication, subject terms) exported from ProQuest TDM Studio.

## Methods

Following CRISP-DM (Business Understanding → Data Understanding → Data
Preparation → Modeling → Evaluation → Deployment):

1. **Preprocessing** — tokenization, stopword removal (standard + custom
   surveillance-domain stopwords), alphabetic token filtering
2. **Inductive analysis** — word frequency, bigrams, TF-IDF (RQ2.1)
3. **Deductive analysis** — Bing lexicon sentiment scoring, longitudinal
   trend (loess), sentiment by era, VADER cross-validation (RQ1, RQ3.2)
4. **Extensions** — quanteda keyness/chi-squared (RQ3.1), GloVe embeddings
   in R and Word2Vec in Python for semantic neighborhood comparison (RQ3.3),
   article volume over time with event markers (RQ4.1), NRC emotion
   profiling (RQ2.3)

## Requirements

**R** (≥ 4.x) with:
```r
install.packages(c("tidytext", "tm", "quanteda", "quanteda.textplots",
                    "quanteda.textstats", "tidyverse", "scales",
                    "textdata", "topicmodels", "text2vec", "reticulate"))
```

**Python** (via `reticulate`), with `nltk` (VADER) and `gensim` (Word2Vec)
available in the configured conda environment.

Quarto is required to render the `.qmd` report to PDF.

## Reproducing the Analysis

1. Clone this repository.
2. Open `Midterm Daniel Chavez.qmd` in RStudio or another Quarto-aware editor.
3. Update the `use_condaenv()` path in the setup chunk to point at your
   Python environment.
4. Render with Quarto (`quarto render "Midterm Daniel Chavez.qmd"`) or run
   chunks interactively — the report reads both CSVs directly from `Data/`.

## Status / Next Steps

**Completed (MVP core):** word frequency, bigrams, TF-IDF, Bing sentiment
(article-level, longitudinal trend, by-era comparison).

**In progress (extensions):** VADER triangulation, quanteda keyness, GloVe
and Word2Vec embeddings, NRC emotion profiling.

**Remaining for the final report:**
1. LDA topic modeling for RQ2.2 (test *k* = 5, 10, 15, 20)
2. Event-window analysis for RQ4.1 (12 months before/after 9/11 and Snowden)
3. Multiple AI-era cutoff tests (2015, 2017, 2019) for RQ4.2
4. Normalize comparative analyses for corpus size imbalance (7,621 vs. 5,391)

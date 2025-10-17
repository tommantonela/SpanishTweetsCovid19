# SpanishTweetsCovid19
Companion repository for the data collection ["SpanishTweetsCOVID-19: A Social Media Enriched Covid-19 Twitter Spanish Dataset"](https://data.mendeley.com/datasets/nv8k69y59d/1).

[![Dataset DOI](https://img.shields.io/badge/Mendeley-10.17632/nv8k69y59d.4-blue)](https://data.mendeley.com/datasets/nv8k69y59d/4)
[![License: CC BY 4.0](https://img.shields.io/badge/license-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

This repository contains **code and figures** to process and visualize the **SpanishTweetsCOVID-19** collection — a large-scale dataset of Spanish-language Twitter posts about COVID-19. It complements the dataset hosted on Mendeley Data.

> 📦 **Dataset (IDs & enriched tables):** https://data.mendeley.com/datasets/nv8k69y59d/4  

---

## What’s in this repo?

```bash
├── code/
│ ├── 01-db-extraction/ # from MongoDB (rehydrated tweets) → dataset tables
│ ├── 02-stats-computation/ # compute aggregates & indicators
│ ├── 03-text-processing/ # Empath & SentiSense features
│ └── 04-chart-creation/ # heatmaps & boxplots
├── heatmaps/ # daily prevalence per category (multiple time spans)
├── boxplots/ # monthly distributions per category/emotion
└── Covid_Dataset__supplementary_material.pdf
```

### Dataset at a glance
- **Time span:** March 2020– June 2021 (v5)  
- **Language:** Spanish (tweets collected via COVID-19 keywords + official Argentine government accounts)  
- **Tables included (joinable):** tweet IDs, users, mentions, retweets, media, URLs, hashtags, replies, and content-based user relations.  
- **Intended uses:** policy impact, risk perception, misinformation/rumors, community dynamics, mental-health signals (e.g., anxiety, stress), etc.

> ⚖️ **Ethics & Terms:** The dataset shares **tweet IDs** and derived tables to comply with Twitter’s policies. Always rehydrate before content analysis, respect user privacy, and follow the dataset license (CC BY 4.0).


---

## Getting started

#### 0) Environment

- Python 3.9+  
- Recommended packages:
  - `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `pymongo`, `tqdm`, `jupyter`
  - For rehydration (optional): [`twarc`](https://github.com/docnow/twarc) or use **Faking it!** (below)

Create an environment and install dependencies:
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt  # if you add one, otherwise pip install packages above
```

#### 1) Rehydrate tweet IDs
The dataset provides tweet IDs. Rehydrate them using either:

Faking it! (used to build this dataset): https://github.com/knife982000/FakingIt

Supports collection & rehydration (uses Twitter4J).

twarc (Python):

```bash
pip install twarc
twarc2 hydrate ids.txt hydrated.jsonl
```

Store hydrated tweets in MongoDB (as assumed by the notebooks in 01-db-extraction/).

#### 2) Build the dataset tables
Run the notebooks in code/01-db-extraction/ to export normalized tables from MongoDB into CSV/Parquet files (tweets, users, mentions, hashtags, URLs, media, retweets, replies, content relations).

#### 3) Compute statistics & features

* ``code/02-stats-computation/``: aggregates (daily/monthly) and indicators used in the paper/figures.
* ``code/03-text-processing/``: extract Empath categories and SentiSense emotions from tweet text.

> Tip: Empath’s original English categories can be mapped/translated. Check the notebook for preprocessing and dictionary usage.

#### 4) Reproduce the figures

* ``code/04-chart-creation/`` produces:
	* **Heatmaps**. Heatmaps showing the daily prevalence of each included category. Darker colors indicate higher prevalence of the category. Heatmaps are organized by mental health (anxiety, depression, stress), emotions and crisis (all, preparedness, response, recovery, mitigation). Heatmaps are presented for different time spans: march-june (june was a breakpoing in Argentina's lockdown), march-october, monthly, and bi/tri-monthly.
	* **Boxplots**. Boxplots show the distribution of prevalence across months per involved category/emotion. Boxplots are organized by mental health (anxiety, depression, stress), emotions and crisis (all, preparedness, response, recovery, mitigation).

Outputs are saved into heatmaps/ and boxplots/.

#### Folder structure (details)
* ``code/01-db-extraction/``
	* Expects rehydrated tweets in MongoDB.
	* Exports normalized CSV/Parquet tables.

* ``code/02-stats-computation/``
	* Computes per-day and per-month stats used across visualizations.

* ``code/03-text-processing/``
	* Cleans text, applies Empath & SentiSense, aggregates category prevalence.

* ``code/04-chart-creation/``
	* Generates publication-ready heatmaps and boxplots.

### Citing
If you use the dataset or this companion code, please cite the dataset:

**SpanishTweetsCOVID-19: A Social Media Enriched Covid-19 Twitter Spanish Dataset**
Antonela Tommasel, Juan M. Rodriguez, Daniela Godoy.
Mendeley Data, Version 5, 2025. DOI: https://doi.org/10.17632/nv8k69y59d.5

```bibtex
@dataset{spanishtweetscovid19_v4_2025,
  title        = {SpanishTweetsCOVID-19: A Social Media Enriched Covid-19 Twitter Spanish Dataset},
  author       = {Tommasel, Antonela and Rodriguez, Juan M. and Godoy, Daniela},
  year         = {2025},
  version      = {5},
  publisher    = {Mendeley Data},
  doi          = {10.17632/nv8k69y59d.4},
  url          = {https://data.mendeley.com/datasets/nv8k69y59d/4}
}
```

If applicable, also cite any related publications using or describing this dataset and methods.

### License
* Dataset: CC BY 4.0 (see Mendeley page)
* Code in this repo: MIT (or specify your preferred license here)

---

### FAQ
**Q: Can I get full tweet text here?** *A: No. We share tweet IDs. Rehydrate via the Twitter API (see “Rehydrate tweet IDs”).*

**Q: Do I need MongoDB?** *A: Only if you want to follow the provided extraction workflow. You can adapt the notebooks to your preferred storage.*

**Q: Where do the Empath/SentiSense labels come from?** *A: From code/03-text-processing/ notebooks. They load dictionaries and compute per-tweet/category features, then aggregate by time windows.*

### Contact
* Maintainer: Antonela Tommasel
* Project page: https://tommantonela.github.io/datasets/spanishtweetscovid/
* Dataset (latest): https://data.mendeley.com/datasets/nv8k69y59d/4

Contributions (issues/PRs) that improve the notebooks, documentation, or reproducibility are welcome!

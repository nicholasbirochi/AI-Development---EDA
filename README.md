# Netflix Daily Top 10 — Exploratory Data Analysis (EDA)

This repository contains a **Jupyter Notebook** (`visualizando.ipynb`) that performs a quick **Exploratory Data Analysis (EDA)** on a **Netflix Daily Top 10** dataset. The goal is to validate data quality, understand the time range covered by the dataset, and generate initial descriptive insights and visualizations.

## What’s inside

### Notebook: `visualizando.ipynb`

The notebook covers:

- Importing core libraries (`pandas`, `datetime`)
- Loading the dataset from `./data/netflix_daily_top_10.csv`
- Quick data validation and structure checks:
  - data types (`dtypes`)
  - dataset size (`shape`)
  - dataset overview (`info()`)
  - missing values (`isna().sum()`)
- Time coverage:
  - min/max dates from the **`As of`** column
- Descriptive statistics and outlier exploration:
  - `describe()`
  - boxplots for numeric columns
- High-level business-style slices:
  - counts for **`Netflix Exclusive`**
  - titles with **`Days In Top 10` >= 100**
  - distribution of **`Type`** (bar chart)
  - distribution of **`Viewership Score`** (histogram)
  - the record(s) with the maximum **`Viewership Score`**

## Dataset requirements

Place the CSV file in the following path:

```text
.
├── visualizando.ipynb
└── data/
    └── netflix_daily_top_10.csv
```

The notebook expects, at minimum, these columns to exist in the CSV:

- `As of` (date)
- `Netflix Exclusive`
- `Days In Top 10`
- `Type`
- `Viewership Score`

## Setup

### Prerequisites

- Python 3.9+ (recommended)
- Jupyter Notebook (or VS Code with Jupyter extension)

### Install dependencies

Using a virtual environment is recommended:

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# Linux/macOS
source .venv/bin/activate
```

Install the required packages:

```bash
pip install pandas matplotlib notebook
```

## How to run

1. Ensure `./data/netflix_daily_top_10.csv` exists.
2. Start Jupyter:

```bash
jupyter notebook
```

3. Open `visualizando.ipynb` and run the cells in order (Run All).

## Suggested next steps

If you want to evolve this EDA into a more production-ready analysis:

- Standardize date parsing and enrich time dimensions:
  - convert `As of` to `datetime`
  - derive `year`, `month`, `week`
- Build title-level aggregations:
  - top titles by total/average `Viewership Score`
  - average time in Top 10 by `Type`
- Define explicit missing-value handling rules (drop vs. impute vs. “unknown”)
- Export curated aggregates for Power BI/Tableau dashboards

Example snippet:

```python
import pandas as pd

df = df_netflix.copy()
df["As of"] = pd.to_datetime(df["As of"], errors="coerce")

top_titles = (
    df.groupby("Title", as_index=False)["Viewership Score"]
      .sum()
      .sort_values("Viewership Score", ascending=False)
      .head(10)
)
top_titles
```

## Author

Nicholas Birochi

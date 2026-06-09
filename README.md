# Netflix Movies & TV Shows — Data Cleaning
https://roadmap.sh/projects/cleaning-netflix-dataset


A Pandas data-cleaning project on the **Netflix Titles** dataset. The focus isn't
just dropping nulls — it's *understanding why* data is missing or wrong and making a
**deliberate decision for each column**, the way you have to with real, messy data.

## The dataset

[Netflix Movies and TV Shows (Kaggle)](https://www.kaggle.com/datasets/shivamb/netflix-shows)
— 8,807 titles with 12 columns (type, title, director, cast, country, date added,
release year, rating, duration, genre, description).

> The raw `netflix_titles.csv` is **not committed** (download it from Kaggle and place
> it in this folder). The cleaned output `netflix_titles_cleaned.csv` is produced by the notebook.

## What the notebook does

1. **Inspects** the data with `.info()`, `.describe(include="all")`, and `.head()` *before* changing anything
2. **Audits** missing values (count + percentage per column)
3. **Handles missing values column by column** with reasoning:
   - `director` (~30%), `cast` (~9%), `country` (~9%) → filled with `"Unknown"` instead of dropping rows
4. **Fixes a real data-entry error** — some `rating` cells actually contain durations
   (`"74 min"`), with the matching `duration` left blank. The notebook detects these,
   moves the value into `duration`, and clears the bad `rating`.
5. **Splits the mixed-type `duration`** (`"90 min"` vs `"2 Seasons"`) into:
   - `duration_int` — the number
   - `duration_unit` — `"Minutes"` or `"Seasons"`
6. **Parses `date_added`** into a real `datetime`, then derives `year_added` and `month_added`
   (the 10 genuinely-missing dates are kept as `NaT`, not invented)
7. **Exports** the result to `netflix_titles_cleaned.csv`

## Tech stack

- **Python**
- **Pandas**
- **Jupyter Notebook**

## How to run

```bash
pip install -r requirements.txt
jupyter notebook netflix_data_cleaning.ipynb
```

Run all cells. It reads `netflix_titles.csv` and writes `netflix_titles_cleaned.csv`.

## Key takeaway

Cleaning is about **decisions, not reflexes**. Dropping every null would have thrown
away ~2,600 rows over a missing director alone. Reading the data first revealed a
hidden data-entry error that a blind `dropna()` would never have caught.

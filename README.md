# Video game sales analysis

**UCI Math 10 — Fall 2022** | Course project

Exploratory analysis of 16,000+ video game titles spanning multiple platforms, publishers, and genres. Investigated regional sales trends, publisher dominance by market, and built machine learning models to predict platform and understand what drives Japanese sales.

---

## Tools
| Layer | Tool |
|-------|------|
| Data wrangling & analysis | Python (Pandas, NumPy) |
| Visualization | Altair |
| Machine learning | scikit-learn |

---

## Data

**Source:** [Video Game Sales — Kaggle (GregorySmith)](https://www.kaggle.com/datasets/gregorut/videogamesales)

The dataset contains global video game sales records with the following key columns: `Name`, `Platform`, `Year`, `Genre`, `Publisher`, `NA_Sales`, `EU_Sales`, `JP_Sales`, `Other_Sales`, `Global_Sales`.

---

## Project structure

```
├── video_game_sales.ipynb    # Main analysis notebook
├── vgsales.csv               # Raw dataset
└── README.md
```

---

## Analysis

### Data cleaning
- Removed rows with null values and unknown publishers
- Dropped the redundant `Rank` column
- Renamed the `Platform` genre to `Platformer` to avoid conflict with the `Platform` column
- Converted `Year` to datetime format
- Trimmed to the top 5,000 titles by global sales rank, as remaining entries had negligible sales

### Exploratory data analysis
Built an interactive Altair chart linking global sales over time (by genre) to a bar chart of total sales by publisher — clicking a genre in the legend filters the publisher view.

### Regression — what drives Japanese sales?
Used `LinearRegression` with one-hot encoded publisher and genre features to model `JP_Sales`. Features included release year, top 5 publishers, and all 12 genres.

Key findings from regression coefficients:
- **Nintendo** had the highest publisher coefficient, reflecting its dominance in Japan
- **Role-Playing** had the highest genre coefficient, consistent with the popularity of franchises like Pokémon
- **Year** had a negative coefficient — Japanese sales declined over the period covered

### Classification — predicting release platform
Used `KNeighborsClassifier` (k=30) to predict which platform a game was released on, given publisher, genre, regional sales, and year.

| Split | Accuracy |
|-------|----------|
| Training | ~48.8% |
| Test | ~44.6% |

Training and test scores are close, indicating no overfitting. The modest accuracy suggests platform cannot be reliably predicted from these features alone — a reasonable finding given how many platforms overlap in genre and publisher.

---

## Key findings

- Nintendo dominates the Japanese market; American publishers (EA, Activision) have comparatively low JP sales
- Role-playing games are disproportionately popular in Japan relative to North America and Europe
- Japanese sales have declined over the years covered in the dataset
- Platform is difficult to predict from sales, publisher, and genre alone

---

## References
- Dataset: [Video Game Sales — Kaggle](https://www.kaggle.com/datasets/gregorut/videogamesales)
- Altair sorted bar chart: https://altair-viz.github.io/gallery/bar_chart_sorted.html

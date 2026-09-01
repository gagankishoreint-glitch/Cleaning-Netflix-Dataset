# 🎬 Netflix Movies & TV Shows: Data Cleaning & Exploratory Data Analysis (EDA)

![Python](https://img.shields.io/badge/Python-3.14-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Cleaning-150458?style=flat&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557c?style=flat)

An end-to-end data analysis project focusing on **data hygiene, anomaly resolution, feature engineering, and visual exploration** of the Netflix titles dataset (~8,800 entries) using strictly **Pandas** and **Matplotlib**.

---

## 📌 Project Overview

Raw real-world datasets are rarely analysis-ready. This project demonstrates the step-by-step transformation of raw, un-sanitized Netflix meta-data into clean, structured data, followed by exploratory analysis to uncover content trends, top producing nations, and runtime patterns over time.

---

## 🛠️ Key Data Cleaning & Hygiene Steps

1. **Column Anomaly & Data Shift Fix:**
   * Identified anomalous rows (e.g., Louis C.K. comedy specials) where runtime durations (`"74 min"`, `"84 min"`, `"66 min"`) were incorrectly positioned in the `rating` column.
   * Shifted values back to the `duration` column and assigned appropriate maturity ratings (`TV-MA`).

2. **Categorical Missing Value Handling:**
   * Analyzed missing entries across key columns (`director`: ~2,634 missing, `cast`: ~825 missing, `country`: ~831 missing).
   * Imputed explicit, clean placeholders (`"Unknown Director"`, `"Unknown Cast"`, `"Unknown Country"`, `"Unknown"`) to preserve title metadata without skewing analytical aggregations.

3. **Data Type Conversion & Extraction:**
   * **`date_added`**: Converted raw date strings into native Pandas `datetime64` objects using `pd.to_datetime(..., errors='coerce')` to safely parse formatting errors into `NaT`.
   * **`duration`**: Leveraged regular expressions (`.str.extract(r'(\d+)')`) to isolate numeric values into an integer format for quantitative runtime calculations.

---

## 📊 Exploratory Data Analysis & Visualizations

### 1. Content Distribution (Movies vs. TV Shows)
* **Movies** account for **69.6%** of Netflix's catalog, while **TV Shows** make up **30.4%**.

### 2. Top Content Producing Nations
* The **United States** leads overall volume (2,818+ titles), followed by **India** (972 titles) and the **United Kingdom** (419 titles).

### 3. Maturity Rating Distribution
* **`TV-MA`** (Mature Audiences) is the single most dominant rating category with over 3,200 titles, followed by **`TV-14`** and **`TV-PG`**, highlighting Netflix's heavy focus on adult and young-adult demographics.

### 4. Movie Runtime Trends Over Time
* Categorized movie runtimes into *Short (<60 min)*, *Standard (60-120 min)*, and *Long (>120 min)* to visualize length distributions relative to release years using `matplotlib` scatter plotting.

---

## 💡 Key Business Insights

* **Film-Heavy Strategy:** Netflix's library historically leans heavily toward feature films, though TV show additions have accelerated in recent release years.
* **Regional Hubs:** India represents the second-largest content producer on Netflix, with a overwhelming concentration in feature films compared to episodic TV content.
* **Core Audience Target:** Over 60% of total platform content falls under mature or teen-restricted categories (`TV-MA` and `TV-14`).

---

## 🛠️ Tech Stack & Dependencies

* **Language:** Python 3.x
* **Data Processing:** `pandas`
* **Visualization:** `matplotlib`

*(Strictly built without external machine learning dependencies like Scikit-Learn to showcase native Pandas and Matplotlib data manipulation capabilities).*

---

## 📁 Repository Structure

```text
├── netflix_titles.csv       # Raw Kaggle Netflix dataset (~8,807 rows)
├── Notebook.ipynb           # Complete Jupyter Notebook (Cleaning + EDA Code)
├── top10_countries.png      # Generated Matplotlib charts
└── README.md                # Project documentation

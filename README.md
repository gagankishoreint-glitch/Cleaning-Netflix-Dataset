# Netflix Dataset: Data Cleaning and Exploratory Data Analysis

This project focuses on cleaning and exploring the Netflix Movies and TV Shows dataset containing approximately 8,807 titles.

The main goal was to work through common real-world data quality issues such as missing values, incorrect data placement, inconsistent data types, and unstructured duration values. After cleaning the dataset, exploratory analysis was performed using Pandas and Matplotlib to identify patterns in Netflix's content catalog.

## Dataset

**Source:** [Kaggle - Netflix Movies and Series Dataset](https://www.kaggle.com/datasets/debayank2024/netflix-movies-and-series?resource=download)

The dataset contains information about Netflix movies and TV shows, including:

- Title
- Type
- Director
- Cast
- Country
- Date Added
- Release Year
- Rating
- Duration
- Listed In
- Description

## Data Cleaning

### 1. Initial Missing Value Audit

The first step was to check the dataset for missing values using:

```python
df.isnull().sum()
```

The audit showed missing values in several columns:

| Column | Missing Values |
|---|---:|
| director | 2,634 |
| cast | 825 |
| country | 831 |
| date_added | 10 |
| rating | 4 |
| duration | 3 |

Instead of immediately removing these rows, the missing values were investigated to determine whether they represented actual missing information or possible data quality issues.

### 2. Fixing Misplaced Duration Values

During the investigation of the missing `duration` values, an issue was found in three rows.

These rows corresponded to Louis C.K. comedy specials. Their runtime values (`74 min`, `84 min`, and `66 min`) had been incorrectly placed in the `rating` column, while the `duration` column was empty.

The affected records were corrected by:

1. Identifying runtime values incorrectly stored in the `rating` column.
2. Moving those values into the `duration` column.
3. Replacing the missing rating values with `Unknown`.

This helped preserve the original records instead of dropping them from the dataset.

### 3. Handling Missing Values

For categorical columns with missing values, explicit placeholder values were used instead of removing the affected rows.

```python
fill_values = {
    'director': 'Unknown Director',
    'cast': 'Unknown Cast',
    'country': 'Unknown Country',
    'rating': 'Unknown'
}

df = df.fillna(fill_values)
```

This approach keeps the titles in the dataset while making missing information explicit.

### 4. Data Type Corrections

The `date_added` column was originally stored as text. It was converted into a proper datetime format:

```python
df['date_added'] = pd.to_datetime(
    df['date_added'],
    errors='coerce'
)
```

This makes it easier to perform time-based analysis, such as grouping titles by year or month.

The `duration` column contained values such as:

```text
90 min
45 min
120 min
```

The numeric portion was extracted using a regular expression:

```python
df['duration_numeric'] = (
    df['duration']
    .str.extract(r'(\d+)')[0]
    .astype('Int64')
)
```

### 5. Runtime Categorization

A runtime category was also created to make duration analysis easier.

The categories used were:

| Category | Runtime |
|---|---|
| Short | Less than 60 minutes |
| Standard | 60–120 minutes |
| Long | More than 120 minutes |

This provides a simpler way to compare movie runtimes rather than working only with individual numeric values.

## Exploratory Data Analysis

After cleaning the dataset, exploratory analysis was performed using Pandas and Matplotlib.

### Top Content-Producing Countries

The analysis of title origins showed the following countries among the highest contributors:

| Country | Titles |
|---|---:|
| United States | 2,818 |
| India | 972 |
| Unknown Country | 831 |
| United Kingdom | 419 |
| Japan | 245 |

The United States has the largest number of titles in the dataset, followed by India and the United Kingdom.

### Rating Distribution

The most common ratings in the dataset were:

| Rating | Titles |
|---|---:|
| TV-MA | 3,210 |
| TV-14 | 2,160 |

`TV-MA` and `TV-14` account for a large portion of the catalog, indicating a strong presence of content targeted toward mature and older teenage audiences.

## Visualizations

The notebook includes visualizations created using Matplotlib to explore patterns in the dataset.

Some of the analysis includes:

- Distribution of content by type
- Most common ratings
- Top content-producing countries
- Release year trends
- Movie runtime distribution
- Runtime categories
- Content added to Netflix over time

## Repository Structure

```text
Cleaning-Netflix/
│
├── netflix_titles.csv       # Raw Netflix dataset
├── Notebook.ipynb           # Data cleaning and EDA notebook
└── README.md                # Project documentation
```

## Technologies Used

- Python
- Pandas
- Matplotlib
- Jupyter Notebook

## How to Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/gagankishoreint-glitch/Cleaning-Netflix.git
cd Cleaning-Netflix
```

### 2. Install dependencies

```bash
pip install pandas matplotlib jupyter
```

### 3. Launch the notebook

```bash
jupyter notebook Notebook.ipynb
```

Open `Notebook.ipynb` and run the cells to reproduce the data cleaning process and exploratory analysis.

## Key Takeaways

This project provided practical experience with:

- Identifying and handling missing data
- Investigating data quality issues instead of blindly dropping rows
- Correcting misplaced values
- Converting columns to appropriate data types
- Extracting numerical information from text
- Creating derived features for analysis
- Performing exploratory data analysis
- Creating visualizations with Matplotlib
- Documenting a data-cleaning workflow

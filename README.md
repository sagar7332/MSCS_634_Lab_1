# MSCS_634_Lab_1 – Data Visualization, Preprocessing & Statistical Analysis

## Purpose

This lab applies core data science techniques to the Titanic passenger dataset using Python and Jupyter Notebook. The goal is to practice data exploration, cleaning, transformation, and statistical analysis in a structured, reproducible workflow.

---

## Dataset

**Source:** [Titanic Dataset – Kaggle](https://www.kaggle.com/datasets/yasserh/titanic-dataset)  
**File:** `titanic.csv`  
**Records:** 891 passengers | **Features:** 12 columns  

| Column | Description |
|---|---|
| PassengerId | Unique passenger ID |
| Survived | Survival status (0 = No, 1 = Yes) |
| Pclass | Ticket class (1 = 1st, 2 = 2nd, 3 = 3rd) |
| Name | Passenger name |
| Sex | Gender |
| Age | Age in years |
| SibSp | # of siblings/spouses aboard |
| Parch | # of parents/children aboard |
| Ticket | Ticket number |
| Fare | Passenger fare |
| Cabin | Cabin number |
| Embarked | Port of embarkation (C, Q, S) |

---

## Repository Structure
```
MSCS_634_Lab_1/
├── MSCS_634_Lab_1.ipynb     # Main Jupyter Notebook
├── titanic.csv              # Dataset used in the lab
├── screenshots/             # Required screenshots from each step
│   ├── step1_head.png
│   ├── step2_scatter.png
│   ├── step2_barchart.png
│   ├── step3_missing_before.png
│   ├── step3_missing_after.png
│   ├── step3_iqr_outliers.png
│   ├── step3_reduction.png
│   ├── step3_scaling.png
│   ├── step4_info.png
│   ├── step4_describe.png
│   ├── step4_central_tendency.png
│   ├── step4_dispersion.png
│   └── step4_correlation.png
└── README.md
```

---

## Lab Steps Overview

### Step 1 – Data Collection
Loaded `titanic.csv` into a Pandas DataFrame and displayed the first 5 rows using `.head()`.

### Step 2 – Data Visualization
Created 6 visualizations to explore the dataset:

| Chart | Variables | Key Insight |
|---|---|---|
| Scatter Plot | Age vs. Fare (by survival) | Higher-fare passengers had better survival rates |
| Bar Chart | Survival by Pclass | 1st class survivors outnumbered 3rd class survivors |
| Histogram | Age distribution | Right-skewed; most passengers aged 20–40 |
| Box Plot | Fare by Pclass | 1st class fares had extreme outliers; 3rd class fares were tightly clustered |
| Pie Chart | Gender split | ~65% male, ~35% female |
| Line Plot | Cumulative survivors | ~38.4% overall survival rate across the manifest |

### Step 3 – Data Preprocessing

| Technique | Action Taken |
|---|---|
| Missing Values | Age → median fill; Embarked → mode fill; Cabin → dropped (77% missing) |
| Outlier Removal | IQR method on Fare; 116 outliers identified and removed |
| Data Reduction | Dropped PassengerId, Name, Ticket; sampled 70% of rows |
| Scaling | Min-Max scaling on Fare; Z-score standardization on Age |
| Discretization | Age binned into: Child, Teen, Young Adult, Middle-Aged, Senior |

### Step 4 – Statistical Analysis

| Analysis | Result |
|---|---|
| `.info()` | 891 rows, 12 columns, mixed dtypes |
| `.describe()` | Mean age ≈ 29.7, mean fare ≈ $32.20 |
| Central Tendency | Fare is heavily right-skewed (mean >> median) |
| Dispersion | Fare has very high variance (std ≈ 49.7) indicating wide pricing spread |
| Correlation | Pclass vs. Survival: –0.34 | Pclass vs. Fare: –0.55 (strongest relationships) |

---

## Key Insights

- **Socioeconomic status was the strongest predictor of survival.** First-class passengers paid more, were older on average, and survived at much higher rates than third-class passengers.
- **Missing data required careful handling.** The Cabin column was too sparse (77% missing) to impute reliably and was dropped entirely. Age was safely imputed with the median.
- **Fare contained significant outliers.** The IQR method identified 116 extreme fare values, likely ultra-premium first-class tickets, which were removed before further analysis.
- **The age distribution is right-skewed**, with most passengers in the 20–40 range and a small but meaningful presence of young children.
- **Gender was a major survival factor** — despite females making up only 35% of passengers, the "women and children first" policy led to dramatically higher female survival rates.

---

## Challenges & Decisions

- **Cabin column:** With over 77% of values missing, imputation would have introduced too much noise. Dropping was the correct choice over forward-fill or mode replacement.
- **Outlier strategy:** Rather than capping fare outliers (winsorization), full removal was chosen since the goal was clean statistical analysis, not predictive modeling where preserving distribution matters.
- **Sampling seed:** `random_state=42` was set for reproducibility so the 70% sample is consistent across runs.
- **Age discretization bins** were chosen to reflect meaningful life stages rather than equal-width intervals, providing more interpretable categories for analysis.

---

## How to Run

1. Clone the repository:
```bash
   git clone https://github.com/your-username/MSCS_634_Lab_1.git
   cd MSCS_634_Lab_1
```

2. Install dependencies:
```bash
   pip install pandas numpy matplotlib seaborn scipy jupyter
```

3. Launch Jupyter Notebook:
```bash
   jupyter notebook MSCS_634_Lab_1.ipynb
```

4. Run all cells top to bottom (`Kernel → Restart & Run All`).

---

## Requirements

- Python 3.8+
- pandas
- numpy
- matplotlib
- seaborn
- scipy
- jupyter

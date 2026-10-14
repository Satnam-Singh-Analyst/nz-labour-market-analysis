# New Zealand Macroeconomic & Regional Labour Market Analysis (HLFS)

## Executive Summary & Academic Context
This repository houses a professional-grade economic data analysis project examining structural shifts and regional dynamics within the New Zealand labour market. Utilizing official micro-aggregated data from the Statistics New Zealand **Household Labour Force Survey (HLFS)** spanning from 1986 to 2026, this research models longitudinal trends, regional divergences, and macroeconomic indicators. 

Developed as a cornerstone portfolio piece for Master of Arts in Economics studies at Massey University, this project bridges raw econometric data extraction with rigorous policy interpretation.

---

## Project Structure
```text
├── hlfs-jun26qtr-csv.csv                 # Raw Stats NZ HLFS Dataset (1.27M+ records)
├── Labour Market Statistics.py           # Consolidated Master Python Econometric Script
├── nz_regional_labour_macro_analysis.png # High-resolution multi-panel output chart
└── README.md                             # Project documentation and economic brief
```

---

## Methodology & Data Pipeline
The analysis pipeline is structured into reproducible, modular phases:
1. **Ingestion & Integrity Check:** Loads 1.27 million rows safely using `low_memory=False`, resolving data-type inconsistencies across 58 variables.
2. **Data Cleaning & Sanitisation:** Normalizes categorical text strings via `.str.strip()` and imputes missing numeric values in `Data_value` to maintain mathematical continuity.
3. **Econometric Transformations:** 
   * Aggregates longitudinal time-series data across quarterly periods (`Period`).
   * Isolates sub-national regional council datasets (`Regional Council`).
   * Computes **descriptive statistical distributions** (mean, median, standard deviation, and interquartile dispersion).
   * Calculates **Quarter-on-Quarter (QoQ) Growth Rates** using percentage change transformations to normalize absolute scale disparities between major urban centers.

---

## Key Metrics & Economic Calculations Explained

| Metric / Function | Mathematical / Python Implementation | Economic Significance & Purpose |
| :--- | :--- | :--- |
| **`Data_value` Imputation** | `df['Data_value'].fillna(0)` | Replaces null entries with zero to prevent aggregation runtime exceptions while preserving dataset matrix dimensions. |
| **Groupby Aggregation** | `df.groupby(['Period', 'Regional Council'])` | Clusters observations by time and geographical boundaries to uncover localized macroeconomic shocks. |
| **Statistical Distribution** | `regional_df['Data_value'].describe()` | Computes central tendency (mean, median) and dispersion to assess structural stability and outlier volatility. |
| **QoQ Growth Rate (%)** | `pct_change() * 100` | Normalizes absolute headcount differences between large hubs (Auckland) and smaller regions, revealing relative economic momentum. |

---

## Visualisation Outputs

The script generates a publication-ready multi-panel figure (nz_regional_labour_macro_analysis.png) featuring:

Panel 1: Absolute quarterly labour force trends across Auckland, Wellington, and Canterbury, illustrating massive macroeconomic weighting toward Auckland's scale.

Panel 2: Quarter-on-Quarter percentage growth trajectories, capturing regional business cycle fluctuations and public/private sector sensitivity.

## Tech Stack
Language: Python 3.14+

Data Manipulation & Analysis: Pandas, NumPy

Data Visualization: Matplotlib, Seaborn

IDE: Visual Studio Code (VS Code)

Dataset Download & Local Setup Guide
Due to GitHub's 100MB file size limit, the raw multi-gigabyte Stats NZ dataset is excluded from this repository via .gitignore. Follow these steps to replicate the environment:

## 1. Download the Raw Dataset
Source: Statistics New Zealand (Stats NZ)

Direct Download Link: Stats NZ HLFS Quarterly Datasets

Required File: hlfs-jun26qtr-csv.csv

## 2. Execution Steps
Clone this repository and navigate into the folder:

Bash
git clone [https://github.com/Satnam-Singh-Analyst/nz-labour-market-analysis.git](https://github.com/Satnam-Singh-Analyst/nz-labour-market-analysis.git)
cd nz-labour-market-analysis
Place your downloaded hlfs-jun26qtr-csv.csv file directly into the root project directory.

## Install required Python packages:

Bash
pip install pandas numpy matplotlib seaborn


## Execute the master economic analysis script:

Bash
python "Labour Market Statistics.py"

## Author:Satnam Singh
## Master of Arts (Economics) Candidate — Massey University
## GitHub: @Satnam-Singh-Analyst
## LinkedIn: Satnam Singh
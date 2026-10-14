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
The script generates a publication-ready **multi-panel figure** (`nz_regional_labour_macro_analysis.png`) featuring:
* **Panel 1:** Absolute quarterly labour force trends across Auckland, Wellington, and Canterbury, illustrating massive macroeconomic weighting toward Auckland's scale.
* **Panel 2:** Quarter-on-Quarter percentage growth trajectories, capturing regional business cycle fluctuations and public/private sector sensitivity.

---

## Tech Stack
* **Language:** Python 3.14+
* **Data Manipulation & Analysis:** Pandas, NumPy
* **Data Visualization:** Matplotlib, Seaborn
* **IDE:** Visual Studio Code (VS Code)

---

## How to Execute the Analysis
1. Ensure Python 3.x is installed along with required numerical packages:
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
2. Place `hlfs-jun26qtr-csv.csv` in the root directory.
3. Execute the master script:
   ```bash
   python "Labour Market Statistics.py"
   ```
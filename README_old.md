# 🔬 Data-Driven Optimization of Sperm Selection Efficiency

A comprehensive end-to-end data analytics project on **ICSI (Intracytoplasmic Sperm Injection)** procedures — covering data preprocessing, exploratory data analysis, statistical analysis, business insights, and SQL-based querying using Python, Pandas, NumPy, Matplotlib, Seaborn, and MySQL.

![Python](https://img.shields.io/badge/Python-3.9+-blue) ![Pandas](https://img.shields.io/badge/Pandas-2.0+-green) ![MySQL](https://img.shields.io/badge/MySQL-8.0+-orange) ![Domain](https://img.shields.io/badge/Domain-Reproductive%20Medicine-purple) ![Records](https://img.shields.io/badge/Records-1215-teal)

---

## 🎯 Project Overview

This project applies real-world data analytics to **1,215 ICSI procedure records** collected from a fertility clinic, spanning **May 2024 to December 2025** across **1,108 unique patients** and **10 embryologists**. The goal is to identify key factors that drive sperm selection efficiency and fertilization success, and to produce actionable business and clinical recommendations.

**Overall Fertilization Rate:** 59.75% &nbsp;|&nbsp; **Usable Embryo Rate:** 23.87% &nbsp;|&nbsp; **Avg Selection Time:** 152.6 seconds

---

## 📁 Repository Structure

```
sperm-selection-optimization/
│
├── Sperm_Selection- ICIS procdure .py     # Main EDA script (11 sections)
├── data preprocessing.py                  # Data cleaning & preprocessing pipeline
├── Sperm_Selection- ICIS procdure .sql    # Full MySQL EDA queries
│
├── eda_output/
│   ├── data_quality_report.csv
│   ├── descriptive_statistics.csv
│   ├── correlation_matrix.csv
│   ├── embryologist_performance.csv
│   ├── monthly_trends.csv
│   ├── key_insights_summary.csv
│   └── plots/
│       ├── 01_distributions_numerical.png
│       ├── 02_boxplots_outliers.png
│       ├── 03_categorical_distributions.png
│       ├── 04_outcome_analysis.png
│       ├── 05_correlation_heatmap.png
│       ├── 06_quality_vs_success.png
│       ├── 07_embryologist_performance.png
│       ├── 08_temporal_analysis.png
│       ├── 09_morphological_analysis.png
│       ├── 10_lab_conditions.png
│       └── 11_cycle_analysis.png
│
├── datasets/
│   ├── Sperm_Selection_ICSI.xlsx           # Main dataset (4 sheets)
│   ├── Data_Dictionary.xlsx                # Variable definitions & quality scores
│   ├── Business_and_statistical_insight.docx
│   └── business_insight_and_statistical.xlsx
│
├── templates/
│   └── Data_Analytics_Checklist_Template.xlsx
│
├── presentation/
│   └── sperm_selection_Presentation.pptx
│
├── interview_prep/
│   ├── INTERVIEW QUESTION OF PYTHON.docx
│   └── SQL Question of answer.docx
│
└── README.md
```

---

## 🧬 Dataset Overview

| Attribute | Value |
|---|---|
| Total Records | 1,215 ICSI procedures |
| Date Range | May 2024 – December 2025 |
| Unique Patients | 1,108 |
| Unique Embryologists | 10 (EMB_A to EMB_I) |
| Total Variables | 26 |
| Target Variables | `Fertilization_Success`, `Usable_Embryo` |

### 📋 Key Variables

| Column | Type | Range | Missing |
|---|---|---|---|
| `Sperm_Concentration_M_per_ml` | Float | 10–100 M/ml | 0% |
| `Total_Motility_Percent` | Float | 30–80% | 0% |
| `Progressive_Motility_Percent` | Float | 20–50% | 0% |
| `Normal_Morphology_Percent` | Float | 4–15% | 0% |
| `Selection_Time_Seconds` | Integer | 180–600 sec | 0% |
| `Embryologist_Experience_Years` | Integer | 1–20 years | 0% |
| `Head_Shape_Score` | Categorical | Excellent/Good/Fair/Poor | 0% |
| `Acrosome_Status` | Categorical | Normal/Abnormal | 0% |
| `Midpiece_Assessment` | Categorical | Normal/Defect | 2.6% |
| `Tail_Assessment` | Categorical | Normal/Coiled/Bent | 5.0% |
| `Vacuoles_Present` | Categorical | None/Small/Large | 24.5% |
| `Lab_Temperature_C` | Float | 36.4–37.6°C | 0% |
| `Lab_Humidity_Percent` | Integer | 34–70% | 0% |
| `Fertilization_Success` | Binary | 0 / 1 | 0% ✅ |
| `Usable_Embryo` | Binary | 0 / 1 | 0% ✅ |

---

## 🚀 What This Project Covers

### 📌 1. Data Preprocessing (`data preprocessing.py`)
- Loaded dataset using `pd.read_csv()` with 26 columns
- Detected 0 duplicate records using `duplicated().sum()`
- Handled missing values:
  - `Midpiece_Assessment` → filled with `'Not_Assessed'`
  - `Tail_Assessment` → filled with `'Unknown'`
  - `Magnification_Used` → filled with `'Not_Documented'`
- Fixed formatting: standardized `Patient_ID` prefix (`PT-`), `Head_Shape_Score` to title case, corrected `'Progresive'` typo to `'Progressive'`
- Range validation: flagged `Normal_Morphology_Percent > 30` and `Selection_Time_Seconds < 45` as invalid, set to `NaN`
- Logical integrity: nullified `Day3_Grade` for all records where `Fertilization_Success == 0`
- Date validation: converted `Selection_Date` to datetime; nullified future dates
- Applied `MinMaxScaler` and `StandardScaler` from scikit-learn

### 📌 2. Data Quality Report (Real Findings)

| Issue | Count |
|---|---|
| Duplicate Records | 0 ✅ |
| Future Dates | 0 ✅ |
| Temperature Outliers (outside 36.5–37.5°C) | 83 ⚠️ |
| Humidity Outliers (outside 40–60%) | 44 ⚠️ |
| Missing Midpiece Assessment | 31 (2.55%) |
| Missing Tail Assessment | 61 (5.02%) |
| Missing Vacuoles | 298 (24.53%) |
| Missing Day 3 Grade | 477 (39.26%) |
| Missing Day 5 Grade | 830 (68.31%) |

### 📌 3. EDA — 11 Analytical Sections (`Sperm_Selection- ICIS procdure .py`)

**Section 3 — Univariate Numerical Analysis**
- Distribution plots + KDE for: concentration, motility, morphology, selection time, lab conditions, embryologist experience
- Boxplots with IQR-based outlier counts annotated on each chart
- Descriptive statistics exported to CSV

**Section 4 — Univariate Categorical Analysis**
- Frequency tables and bar charts for 8 categorical variables
- `value_counts(dropna=False)` with both count and percentage
- Bar charts with value labels plotted directly on bars

**Section 5 — Target Variable Analysis**
- Fertilization success: **726 success (59.75%)** vs **489 failure (40.25%)**
- Usable embryo rate: **290 usable (23.87%)**
- Day 3 and Day 5 blastocyst grade distributions visualized as pie + histogram

**Section 6 — Bivariate & Correlation Analysis**
- Full 11×11 correlation matrix with masked upper triangle heatmap
- Box plots: each sperm quality metric split by `Fertilization_Success`
- Independent t-tests (`scipy.stats.ttest_ind`) with significance annotations (*** / ** / * / ns)

**Section 7 — Embryologist Performance Analysis**
```
Embryologist | Procedures | Fert Rate | Usable Rate | Avg Time  | Experience
EMB_B        |    123     |   68.3%   |    21.1%    |  131.7s   |  12 years  ← Top Performer
EMB_C        |    140     |   67.1%   |    30.7%    |  147.8s   |   8 years
EMB_I        |    137     |   63.5%   |    21.2%    |  153.8s   |   7 years
EMB_H        |    134     |   59.7%   |    24.6%    |  146.5s   |  10 years
EMB_F        |    157     |   54.1%   |    29.3%    |  178.9s   |   4 years
EMB_G        |    153     |   51.6%   |    20.9%    |  176.5s   |   3 years  ← Bottom
```
- `groupby('Embryologist_ID').agg()` with multiple metrics
- Scatter: Experience years vs success rate with `np.polyfit()` trend line

**Section 8 — Temporal Analysis**
- Extracted: `Year`, `Month`, `Quarter`, `DayOfWeek`, `WeekOfYear`
- Monthly procedure counts and success rates over time
- Day-of-week and quarterly performance comparisons

**Section 9 — Morphological Assessment Analysis**
- Success rates grouped by: `Head_Shape_Score`, `Acrosome_Status`, `Midpiece_Assessment`, `Tail_Assessment`, `Motility_Pattern`
- Groups with `n < 5` filtered out for reliability
- Sample size `n=` annotations displayed on each bar

**Section 10 — Lab Conditions Analysis**
- Defined optimal: Temp 36.5–37.5°C AND Humidity 40–60%
- **89.88% of procedures** performed under optimal conditions
- Success rate comparison: Optimal vs Suboptimal (bar chart)
- Microscope type performance comparison

**Section 11 — Patient Cycle Analysis**
- Procedures, fertilization rate, and usable embryo rate aggregated by `Cycle_Number` (1–5)
- Finding: Success rate declines progressively with each IVF cycle attempt

### 📌 4. SQL Analysis (`Sperm_Selection- ICIS procdure .sql`)
- Created MySQL database `EDA` and table with 26 VARCHAR columns
- Loaded data via `LOAD DATA LOCAL INFILE` with `SET GLOBAL local_infile = 1`
- Queries cover:
  - Missing value detection per column (`SUM(col IS NULL)`)
  - Duplicate record identification (`GROUP BY HAVING COUNT(*) > 1`)
  - Descriptive stats (`ROUND(AVG())`, `MIN`, `MAX`)
  - Categorical distributions (Motility Pattern, Microscope Type)
  - Fertilization and usable embryo rates
  - Sperm quality comparison: Success vs Failure (`GROUP BY Fertilization_Success`)
  - Embryologist ranking by success rate
  - Lab condition groups (`CASE WHEN ... BETWEEN ... THEN 'Optimal'`)
  - Monthly temporal trends (`YEAR()`, `MONTH()`, `GROUP BY year, month`)

---

## 📊 Key Statistical Findings

| Metric | Value |
|---|---|
| Strongest predictor of fertilization | Normal Morphology % (r = +0.092) |
| Embryologist experience vs success | r = +0.047 |
| Total motility vs success | r = +0.001 |
| Fertilization ↔ Usable embryo | r = +0.460 (strong link) |
| Top embryologist success rate | 68.3% (EMB_B, 12 yrs exp.) |
| Bottom embryologist success rate | 51.6% (EMB_G, 3 yrs exp.) |
| Optimal lab conditions achieved | 89.88% of procedures |
| Temperature outliers | 83 records |

## 💼 Key Business Insights

**1. Sperm Quality → Fertilization Success** — Higher morphology, motility, and concentration consistently predict success. Implement minimum quality thresholds before proceeding to ICSI.

**2. Experience Gap** — A 16.7 percentage point gap exists between the best and worst performing embryologist. Assign complex cases to senior staff and use top performers as training benchmarks.

**3. Optimal Selection Time Window** — Both very fast and very slow selections reduce success (inverted U-shaped pattern). A standard operating time range with deviation alerts is recommended.

**4. Lab Environment** — 83 temperature and 44 humidity outlier records indicate real-time environmental monitoring dashboards should be implemented.

**5. Equipment Investment** — Advanced microscopes yield better embryo usability. Outcome data justifies capital expenditure on higher-magnification imaging equipment.

---

## 🛠️ Technologies Used

| Tool | Purpose |
|---|---|
| Python 3.9+ | Core language |
| Pandas | DataFrame operations, groupby, date handling |
| NumPy | Statistical math, log transforms, polyfit |
| Matplotlib | Subplots, custom chart layouts |
| Seaborn | Heatmaps, violin plots, statistical visuals |
| SciPy (`stats`) | t-tests for group comparison |
| Scikit-learn | MinMaxScaler, StandardScaler |
| MySQL 8.0+ | Database + SQL EDA queries |
| OpenPyXL | Multi-sheet Excel reading |

---

## 📦 Installation & Setup

```bash
# Clone the repository
git clone https://github.com/himanshumaliarya/sperm-selection-optimization.git
cd sperm-selection-optimization

# Install Python dependencies
pip install pandas numpy matplotlib seaborn scipy scikit-learn openpyxl

# Update the file path in the main script (line 31)
# file_path = r"your_local_path/Sperm_Selection_Dataset_DA.xlsx"

# Run preprocessing
python "data preprocessing.py"

# Run full EDA — generates 11 plots + 6 CSV outputs in eda_output/
python "Sperm_Selection- ICIS procdure .py"
```

For SQL: Import your dataset into MySQL and execute `Sperm_Selection- ICIS procdure .sql`.

---

## 📈 Project Statistics

| Metric | Count |
|---|---|
| Total Records Analyzed | 1,215 |
| Variables Studied | 26 |
| EDA Sections Completed | 11 |
| Pandas Functions Used | 50+ |
| Visualizations Generated | 11 PNG plots |
| Statistical Tests Applied | t-test, Pearson r, IQR |
| SQL Queries Written | 15+ |
| Output CSV Files | 6 |

---

## 🤝 Contact

**GitHub:** [@himanshumaliarya1-hub](https://github.com/himanshumaliarya1-hub)  
**LinkedIn:** [Himanshu Maliarya](https://www.linkedin.com/in/himanshu-maliarya-9559aa1b6)  
**Email:** himanshumaliarya1@gmail.com

---

## 📄 License

MIT License — open source and free to use for educational purposes.

> All records used are anonymized. This project is for portfolio and learning purposes only and does not constitute medical advice.

---

⭐ Star this repo if it helped you!

*Made with ❤️, Python, and 1,215 real ICSI procedure records*

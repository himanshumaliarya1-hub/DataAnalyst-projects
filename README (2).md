# ⚡ Power Trading Forecasting

### Predicting Market Clearing Price (MCP) | Indian Energy Exchange (IEX)

A comprehensive end-to-end data analytics project on **Power Trading on IEX (Indian Energy Exchange)** — covering data collection, exploratory data analysis, statistical analysis, business insights, data preprocessing, and data visualization using Python, Pandas, NumPy, Matplotlib, Seaborn, SciPy, Scikit-learn, SQL (DuckDB), and Excel (OpenPyXL).

[![Python](https://img.shields.io/badge/Python-3.9+-blue)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0+-green)](https://pandas.pydata.org/)
[![SQL](https://img.shields.io/badge/SQL-DuckDB-orange)](https://duckdb.org/)
[![Domain](https://img.shields.io/badge/Domain-Energy%20%26%20Power%20Trading-purple)](https://www.iexindia.com/)
[![Records](https://img.shields.io/badge/Records-112128-teal)](https://github.com/himanshumaliarya1-hub/data-projects)

---

## 🎯 Project Overview

This project applies real-world data analytics to **1,12,128 trading records** collected from the Indian Energy Exchange (IEX), spanning **January 2023 to March 2026** across **96 daily 15-minute time blocks** and **14 weather stations** across India. The goal is to identify key factors that drive Market Clearing Price (MCP) and to produce actionable business and trading recommendations.

**Average MCP:** ₹4,648/MWh | **Price Range:** ₹50 – ₹12,000/MWh | **Avg Cleared Volume:** 6,718 MW

---

## 📁 Repository Structure

```
power-trading-forecasting/
│
├── Power_Trading_EDA.py                  # Main EDA script (11 sections, 81 plots)
├── Power_Trading_Preprocessing.py        # Data preprocessing pipeline (10 steps)
├── Power_Trading_EDA.sql                 # SQL EDA script (10 steps, DuckDB)
├── Power_Trading_Preprocessing.sql       # SQL Preprocessing pipeline (9 steps)
│
├── data/
│   └── IEX_Weather_final.csv             # Raw dataset (112,128 rows × 79 cols)
│
├── outputs/
│   ├── business_moments_summary.csv      # 4 moments for all 79 columns
│   ├── Power_Trading_EDA_Full79.xlsx     # Excel EDA with business insights
│   └── plots/
│       ├── step1_blocks_per_day.png
│       ├── step3_distributions.png
│       ├── step4a_mcp_by_hour.png
│       ├── step4b_monthly_mcp.png
│       ├── step5_outliers.png
│       ├── step6_demand_supply.png
│       ├── step7_correlation_mcp.png
│       ├── step8_yoy_trends.png
│       ├── step9_mcp_buckets.png
│       ├── step10_rolling_avg.png
│       └── step11_corr_heatmap.png
│
├── presentation/
│   └── Power_Trading_Analysis.pptx       # Project presentation
│
├── requirements.txt                       # Python libraries needed
└── README.md                              # You are here
```

---

## 🧾 Dataset Overview

| Attribute | Value |
|-----------|-------|
| 📁 Source | Indian Energy Exchange (IEX) + Open-Meteo Weather API |
| 📅 Period | January 2023 – March 2026 |
| 🔢 Total Records | 1,12,128 rows |
| 📐 Total Features | 79 columns |
| ⏱️ Granularity | 15-minute blocks (96 per day) |
| 🌤️ Weather Stations | 14 locations across India |
| 🎯 Target Variable | MCP (Market Clearing Price) in Rs/MWh |
| ❌ Null Values | Zero |
| ❌ Duplicate Rows | Zero |

### 📋 Key Variables

| Column | Type | Unit | Range | Missing |
|--------|------|------|-------|---------|
| `Date` | VARCHAR | YYYY-MM-DD | 2023–2026 | 0% |
| `Hour` | INT | 1–24 | 1 to 24 | 0% |
| `Time Block` | VARCHAR | HH:MM | 96 blocks/day | 0% |
| `Purchase Bid (MW)` | FLOAT | MW | 2,590 – 43,860 | 0% |
| `Sell Bid (MW)` | FLOAT | MW | 762 – 63,406 | 0% |
| `MCV (MW)` | FLOAT | MW | 762 – 16,270 | 0% |
| `Final Scheduled Volume (MW)` | FLOAT | MW | 762 – 16,270 | 0% |
| `MCP (Rs/MWh)` | FLOAT | Rs/MWh | 49.51 – 12,000 | 0% ✅ TARGET |
| `*_temperature_2m` | FLOAT | °C | –5 to 48 | 0% |
| `*_relative_humidity_2m` | INT | % | 0 – 100 | 0% |
| `*_cloud_cover` | INT | % | 0 – 100 | 0% |
| `*_wind_speed_10m` | FLOAT | km/h | 0 – 85 | 0% |
| `*_shortwave_radiation` | INT | W/m² | 0 – 1,200 | 0% |

---

## 🚀 What This Project Covers

### 📌 1. Exploratory Data Analysis — 11 Sections (`Power_Trading_EDA.py`)

**Section 1 — Dataset Overview**
- Total rows, columns, distinct dates, time blocks, missing dates check
- Blocks-per-day completeness check — all 96 blocks/day verified ✅

**Section 2 — Null & Duplicate Analysis**
- `df.isnull().sum()` across all 79 columns → Zero nulls found
- `df.duplicated().sum()` → Zero duplicates found
- Null heatmap generated for trading columns

**Section 3 — Descriptive Statistics**
- `.describe(percentiles=[.05,.25,.5,.75,.90,.95,.99])` for all trading columns
- Percentile distribution bar chart for MCP
- Distribution plots (histogram + mean/median/mode lines) for all 5 trading variables

**Section 4 — Temporal Patterns**
- Average MCP by Hour-of-Day → Evening peak (18–22h) = ₹6,570
- Monthly MCP seasonality chart (Jan 2023 – Mar 2026)
- Day-of-week pattern (weekday vs weekend)
- Peak / Off-Peak classification and comparison

**Section 5 — Price Spike & Outlier Detection**
- IQR method: `Q1 – 1.5×IQR` and `Q3 + 1.5×IQR`
- **16.23% of MCP records** flagged as high outliers
- Top 20 highest MCP events identified
- Boxplot before vs after outlier treatment

**Section 6 — Supply-Demand Balance**
- Avg Demand: 11,851 MW vs Avg Supply: 15,627 MW → Demand/Supply ratio = 0.76
- Hourly demand vs supply vs MCV chart
- MCV vs FSV scatter to check scheduling reliability

**Section 7 — Weather Correlation with MCP**
- Delhi temperature bands vs MCP (Cold / Mild / Warm / Hot / Very Hot)
- Bhadla cloud cover vs solar radiation vs MCP
- Muppandal wind speed bands vs MCP
- Full correlation bar chart: all weather features vs MCP

**Section 8 — Year-over-Year Trends**
- Annual MCP: ₹5,533 (2023) → ₹3,805 (2026) — declining due to renewables
- YoY % change using `pct_change()` and `LAG()` window function
- Total traded volume (GWh) by year

**Section 9 — MCP Price Bucket Distribution**
- `pd.cut()` into 7 buckets: <₹1K, ₹1K–2K, ₹2K–3K, ₹3K–4K, ₹4K–6K, ₹6K–10K, ≥₹10K
- 50% of records fall in the ₹2,000–₹5,000 range

**Section 10 — Rolling Average Trend**
- 7-day and 30-day rolling avg using `.rolling().mean()` grouped by block number
- Trend smoothing chart for the full 2023–2026 period

**Section 11 — Correlation Heatmap**
- Lower triangle heatmap using `mask = np.triu()`
- Trading columns correlation matrix

---

### 📌 2. Data Preprocessing — 10 Steps (`Power_Trading_Preprocessing.py`)

| Step | What Was Done | Result |
|------|--------------|--------|
| ✅ Step 0 | Load raw data, rename messy column names | 1,12,128 rows × 79 cols |
| 🔧 Step 1 | Type casting — Date→datetime, Hour→0–23, weather→float | Clean dtypes |
| 🔍 Step 2 | Null check + imputation (hourly median / ffill+bfill) | 0 nulls after imputation |
| 🗑️ Step 3 | Duplicate removal on Date + Hour + Time Block key | 0 duplicates confirmed |
| 🎯 Step 4 | Outlier detection (IQR) + Winsorization at P1–P99 | MCP 16.2% outliers capped |
| ⚙️ Step 5 | Feature engineering — cyclic sin/cos, lag (1,4,96,672 blocks), rolling (7d,30d), log transform | +67 new features |
| 🏷️ Step 6 | Categorical encoding — One-Hot (peak period, season), Label (day name) | 7 encoded columns |
| 📏 Step 7 | Scaling — Min-Max (0–1) and Z-Score for all trading + weather cols | 20 scaled columns |
| ✂️ Step 8 | Time-based train/val/test split — no random shuffle | Train 62.6% / Val 23.4% / Test 14% |
| 💾 Step 9 | Final feature selection (43 features) + export CSV + feature_list.txt | 5 files saved |

**Final Result:** 79 raw columns → 146 columns → **43 final features selected for modelling**

```
X_train: (70,176 × 43)  |  X_val: (26,208 × 43)  |  X_test: (15,744 × 43)
```

---

### 📌 3. SQL Analysis (`Power_Trading_EDA.sql` + `Power_Trading_Preprocessing.sql`)

- Table `Power_Trading_forecasting` created using `read_csv_auto()` in DuckDB
- SQL EDA covers:
  * Missing value detection per column using `COUNT(*) - COUNT(col)`
  * Duplicate identification using `GROUP BY HAVING COUNT(*) > 1`
  * Descriptive stats: `ROUND(AVG())`, `MIN`, `MAX`, `STDDEV`, `MEDIAN`
  * Percentile distribution using `PERCENTILE_CONT()`
  * IQR-based outlier fences
  * Temporal patterns by hour, month, and day-of-week
  * Supply-demand balance and MCV vs FSV comparison
  * Weather correlation: temperature bands, cloud cover, wind speed vs MCP
  * Year-over-year trends using `LAG()` window function
  * Rolling 7-day average using `ROWS BETWEEN 6 PRECEDING AND CURRENT ROW`
- SQL Preprocessing covers:
  * Column renaming and type casting with `ALTER TABLE`
  * Winsorization using `PERCENTILE_CONT` + `GREATEST / LEAST`
  * Feature engineering: cyclic block number, demand-supply ratio, lag features
  * One-Hot encoding using `CASE WHEN`
  * Train/val/test split using date-based `WHERE` filters
  * `COPY TO` for CSV export

---

## 📊 Key Statistical Findings — 4 Business Moments

### 1️⃣ First Moment — Central Tendency

| Column | Mean | Median | Mode | Insight |
|--------|------|--------|------|---------|
| MCP (Rs/MWh) | ₹4,648 | ₹3,600 | ₹10,000 | Right-skewed — spikes inflate mean by 29% above median |
| Purchase Bid (MW) | 11,851 | 11,076 | 8,454 | Demand surges pull mean above median |
| Sell Bid (MW) | 15,627 | 13,406 | 10,136 | Supply consistently above demand |
| MCV (MW) | 6,718 | 6,530 | 5,298 | Near-symmetric — balanced market clearing |
| FSV (MW) | 6,706 | 6,517 | 5,298 | Mirrors MCV — high scheduling fidelity |

### 2️⃣ Second Moment — Spread & Variability

| Column | Std Dev | Variance | Range | Insight |
|--------|---------|----------|-------|---------|
| MCP | ₹2,751 | 7,568,064 | ₹11,951 | 240x price spread within same dataset |
| Purchase Bid | 4,387 MW | 19,245,040 | 41,270 MW | High volatility — needs flexible generation reserves |
| Sell Bid | 9,432 MW | 88,967,276 | 62,644 MW | Highest variability of all variables |
| MCV | 2,009 MW | 4,038,056 | 15,508 MW | Market mechanism smooths bid volatility well |

### 3️⃣ Third Moment — Skewness

| Column | Skewness | Type | Meaning |
|--------|----------|------|---------|
| MCP | 1.12 | Highly +ve skewed | Most blocks below ₹5,000 but spikes reach ₹12,000 |
| Purchase Bid | 1.32 | Highly +ve skewed | Extreme demand events are frequent |
| Sell Bid | 1.23 | Highly +ve skewed | Renewable surplus causes occasional huge supply |
| MCV | 0.41 | Slight +ve skewed | Near-normal clearing volume distribution |

### 4️⃣ Fourth Moment — Kurtosis

| Column | Kurtosis | Type | Meaning |
|--------|----------|------|---------|
| MCP | 0.04 | Mesokurtic | Near-normal tails — standard VaR models apply |
| Purchase Bid | 3.21 | Leptokurtic | Heavy tails — extreme demand more frequent than normal |
| Sell Bid | 1.65 | Moderate heavy | Renewable surplus events notable but manageable |
| MCV | 0.23 | Mesokurtic | ARIMA and linear models are appropriate |

---

## 💼 Key Business Insights

```
📈 Evening peak (18–22h)  → Avg MCP ₹6,570 — 78% above off-peak — key risk window for traders
📉 MCP declining YoY     → ₹5,533 (2023) to ₹3,805 (2026) — renewable capacity expansion
⚡ Supply > Demand        → Avg Supply 15,627 MW vs Demand 11,851 MW — market surplus
🌡️ Temperature drives MCP → Delhi temp r = +0.45 — hotter days = higher cooling demand
💨 Wind lowers MCP        → Higher wind speed → more renewable supply → price drops
☀️ Solar affects supply   → Cloud cover at Bhadla/Khavda negatively correlates with MCP
📊 Price concentration    → 50% of all blocks trade in the ₹2,000–₹5,000 band
✅ Perfect data quality   → Zero nulls, zero duplicates across all 1,12,128 records
```

---

## 🔮 Next Steps — ML Models Planned

| Model | Why |
|-------|-----|
| Linear Regression + ARIMA | Baseline benchmark — establish MAPE |
| XGBoost / LightGBM | Best for tabular + lag features — tune via Optuna |
| LSTM | Captures 96-block daily temporal pattern |
| Ensemble | Blend XGBoost + LSTM for MAPE < 10% target |
| REST API Deployment | Real-time 15-min MCP prediction for trading desk |

**Target:** MAPE < 10% on unseen test data (Oct 2025 – Mar 2026)

---

## 📈 Project Statistics

| Metric | Count |
|--------|-------|
| Total Records Analysed | 1,12,128 |
| Total Features Studied | 79 columns |
| EDA Sections Completed | 11 |
| Plots Generated | 81 PNG charts |
| SQL Queries Written | 40+ |
| Preprocessing Steps | 10 |
| Features After Engineering | 146 columns |
| Final Model Features Selected | 43 |
| Weather Stations Covered | 14 |
| Output Files Generated | 10+ |

---

## 🛠️ Technologies Used

| Category | Tools |
|----------|-------|
| Language | Python 3.9+ |
| Data Analysis | Pandas, NumPy, SciPy |
| Visualisation | Matplotlib, Seaborn |
| Machine Learning | Scikit-learn |
| SQL | DuckDB |
| Excel Report | OpenPyXL |
| Version Control | Git + GitHub |

---

## 📦 Installation & Setup

```bash
# Clone the repository
git clone https://github.com/himanshumaliarya1-hub/data-projects.git
cd data-projects/power-trading-forecasting

# Install Python dependencies
pip install pandas numpy matplotlib seaborn scipy scikit-learn openpyxl

# Update file path in the script (line 20)
# PATH = r"your_local_path/IEX_Weather_final.csv"

# Run full EDA — generates 11 sections + 81 plots
python Power_Trading_EDA.py

# Run Preprocessing — generates preprocessed CSV + 3 split files
python Power_Trading_Preprocessing.py
```

For SQL: Install DuckDB and run `Power_Trading_EDA.sql` directly — no import needed, reads CSV automatically.

---

## 📁 Key Output Files

| File | What It Contains |
|------|-----------------|
| `business_moments_summary.csv` | All 4 moments for all 79 columns |
| `Power_Trading_preprocessed.csv` | Full preprocessed dataset (146 cols) |
| `train_set.csv` | Training data — Jan 2023 to Dec 2024 |
| `validation_set.csv` | Validation data — Jan to Sep 2025 |
| `test_set.csv` | Test data — Oct 2025 to Mar 2026 |
| `feature_list.txt` | Final 43 features selected for ML |
| `Power_Trading_EDA_Full79.xlsx` | Excel with business insights for all 79 cols |
| `Power_Trading_Analysis.pptx` | Full project presentation |

---

## 🤝 Contact

**GitHub:** [@himanshumaliarya1-hub](https://github.com/himanshumaliarya1-hub)
**LinkedIn:** [Himanshu Maliarya](https://www.linkedin.com/in/himanshu-maliarya-9559aa1b6)
**Email:** himanshumaliarya1@gmail.com

---

## 📄 License

MIT License — open source and free to use for educational purposes.

---

⭐ Star this repo if it helped you!

*Made with ❤️, Python, SQL, and 1,12,128 real IEX power trading records*

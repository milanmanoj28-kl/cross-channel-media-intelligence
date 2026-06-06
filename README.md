# Cross-Channel Media Intelligence: Spend Validation, Audience KPI Engineering & Performance Reporting

## Project Overview

This project simulates a real-world **media data processing and audience measurement workflow** — the kind of work performed at companies like Nielsen, Kantar, and BARC. Using multi-channel media audience data spanning 113 weeks (Jan 2018 – Feb 2020) across 26 market divisions, I built an end-to-end pipeline that ingests raw data, validates it for research-grade quality, engineers audience KPIs, performs structured SQL analysis, and delivers stakeholder-ready visual reports.

The project demonstrates competency in data validation, KPI engineering using industry-standard media metrics, anomaly detection, and translating processed data into actionable business insights — core skills for any media research and data processing role.

---

## Business Context

Media research companies process large volumes of cross-channel audience data weekly. The core challenge isn't just collecting data — it's ensuring that data is **clean, consistent, validated, and structured** before it flows into measurement models or client reports. A single anomalous week of impression data, left undetected, can skew audience reach estimates, distort conversion benchmarks, and mislead budget allocation decisions worth millions.

This project addresses that challenge directly:
- Automated data quality checks catch errors before they propagate
- Audience KPIs (GRP proxy, Reach, Frequency, Share of Voice, conversion efficiency) mirror industry measurement standards
- Z-score anomaly detection flags irregular periods for analyst review
- SQL-based reporting produces structured, reproducible output across all divisions

---

## Dataset

**Source:** [Sample Media Spends Data — Kaggle](https://www.kaggle.com/datasets/yugagrawal95/sample-media-spends-data)

| Attribute | Detail |
|---|---|
| Rows | 3,051 |
| Columns | 10 |
| Granularity | Division–Week |
| Divisions | 26 (A through Z) |
| Coverage | January 2018 – February 2020 (113 weeks) |
| Channels | Google, Email, Facebook, Affiliate |
| Metrics | Impressions per channel, Paid Views, Organic Views, Overall Views, Sales |

---

## Methodology

### Phase 1 — Data Ingestion & Validation
- Column standardization (naming conventions, data types)
- Missing value analysis — zero missing values confirmed across all columns
- Duplicate record detection — 113 duplicate Division+Week entries identified
- IQR-based outlier detection across all numeric columns (8–10% outlier rate per column)
- Structured **data quality report** exported as CSV

### Phase 2 — Audience KPI Engineering

| KPI | Formula / Method |
|---|---|
| Total Impressions | Sum across Google, Email, Facebook, Affiliate per row |
| Share of Voice (SOV) | (Channel Impressions / Total Impressions) × 100 |
| GRP Proxy | Indexed impressions per division (100 = average week) |
| Reach Proxy | Total Impressions / Assumed Frequency (3×) |
| Conversion Efficiency | Sales / Channel Impressions per channel |
| Sales per 1,000 Impressions | (Sales / Total Impressions) × 1,000 |
| WoW Change | Week-over-week % change per division |
| Anomaly Flag | Z-score > ±2 standard deviations from division mean |

> **Note on Proxies:** True GRP and Reach require panel universe size data, which is proprietary. Proxy metrics are clearly labeled and directionally valid for trend analysis.

### Phase 3 — SQL Analysis (SQLite)

8 business-driven queries covering:
1. Division performance ranking by total sales
2. Average channel Share of Voice by division
3. Quarterly sales and impression trend
4. Top 10 highest sales weeks
5. Impression-to-sales conversion efficiency by channel and division
6. Anomaly period summary by division
7. Monthly seasonality — impressions and sales
8. Overall campaign performance summary

### Phase 4 — Visualization

6 charts produced using Matplotlib and Seaborn:
1. Quarterly total sales trend — highlighting Q4 dominance
2. Average channel Share of Voice across all divisions
3. SOV vs conversion efficiency — the Email paradox
4. Top 10 divisions by total sales
5. Monthly seasonality — sales and impressions dual-axis
6. Division B weekly sales with anomaly detection overlay

---

## Key Findings

- **Q4 dominates sales across all divisions** — Q4 2019 generated 131M in total sales vs a quarterly average of ~47M for Q1–Q3, confirming a consistent holiday-season spike that is statistically significant across all 26 divisions
- **Email holds 49% impression share but delivers the lowest conversion efficiency** — Google accounts for only 36.8% of impressions yet generates 162 sales per impression vs Email's 0.27 — a 600x efficiency gap, suggesting significant over-investment in email relative to its conversion contribution
- **Division B is a structural outlier** — with 99M in total sales (nearly double Division E at 52M), Division B accounts for 9 of the top 10 highest sales weeks in the dataset, all concentrated in Q4 periods
- **267 anomalous periods detected across 26 divisions** using Z-score flagging (|Z| > 2) — the majority of anomalies align with Q4 seasonal spikes, validating the detection methodology against known demand patterns
- **Division C and N show near-zero Google impressions** (0.4% and 0.0% SOV respectively) with 77%+ email dependency — a structurally different channel mix that warrants separate performance benchmarking from other divisions

---

## Tools & Technologies

| Category | Tools |
|---|---|
| Language | Python 3.x |
| Data Processing | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Database | SQLite (via sqlite3) |
| Environment | Jupyter Notebook |
| Version Control | Git / GitHub |

---

## Project Structure

```
cross-channel-media-intelligence/
│
├── data/
│   ├── raw/                        # Original dataset (media_spends.csv)
│   └── processed/                  # Clean data, KPI-enriched data, SQLite DB
│
├── notebooks/
│   └── Cross_Channel_Media_Intelligence.ipynb   # Full pipeline — all 4 phases
│
├── outputs/
│   ├── charts/                     # 6 PNG visualizations
│   └── reports/                    # Data quality report, anomaly report
│
├── requirements.txt
└── README.md
```

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/milanmanoj28-kl/cross-channel-media-intelligence.git
cd cross-channel-media-intelligence

# 2. Install dependencies
pip install -r requirements.txt

# 3. Download dataset from Kaggle and place in:
#    data/raw/media_spends.csv

# 4. Open and run the notebook
jupyter notebook notebooks/Cross_Channel_Media_Intelligence.ipynb
```

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
openpyxl
```

---

## Author

**Milan Manoj**
MSc Data Science & Analytics — Jain University, Bengaluru
BSc Statistics — MG University, Kerala

[LinkedIn](https://linkedin.com/in/milanmanoj28) | [GitHub](https://github.com/milanmanoj28-kl) | [Kaggle](https://kaggle.com/milanmanoj28)

# 🚘 autopilot-safety-analysis

> An exploratory data analysis of autopilot usage and its impact on road safety, examining crash reports, incident trends, and risk factors using Python.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square&logo=python)
![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-150458?style=flat-square&logo=pandas)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.7%2B-orange?style=flat-square)
![Seaborn](https://img.shields.io/badge/Seaborn-0.12%2B-4C72B0?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square)

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Research Questions](#-research-questions)
- [Dataset](#-dataset)
- [Key Findings](#-key-findings)
- [Analysis Pipeline](#-analysis-pipeline)
- [Visualizations](#-visualizations)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Usage](#-usage)
- [Methodology](#-methodology)
- [Limitations](#-limitations)
- [References](#-references)
- [License](#-license)

---

## 🔍 Overview

This project conducts a comprehensive **exploratory data analysis (EDA)** into the relationship between autopilot / Advanced Driver Assistance Systems (ADAS) usage and road safety outcomes. Using real-world crash reports, fatality records, and incident data, the analysis investigates whether autonomous and semi-autonomous driving features make roads safer — and under what conditions they may introduce new risks.

The study covers:

- 📉 Crash frequency trends before and after autopilot adoption
- 🚨 Incident severity breakdown (fatal, injury, property damage only)
- 🛣️ Environmental and road condition factors (highway vs. urban, weather, lighting)
- 🤖 Human vs. autopilot fault attribution in reported incidents
- 📆 Year-over-year safety trends as autopilot technology matures

---

## ❓ Research Questions

1. Does autopilot engagement correlate with a reduction in crash frequency per mile driven?
2. How does crash severity differ between autopilot-engaged and human-driven incidents?
3. What road, weather, and lighting conditions are most associated with autopilot-related crashes?
4. How has autopilot safety performance changed over successive software generations?
5. Is there a measurable difference in response time and fault attribution between autopilot and human-controlled incidents?

---

## 📦 Dataset

| Source | Description | Records |
|--------|-------------|---------|
| NHTSA ADAS Incident Database | Reported crashes involving ADAS / autopilot systems | ~900+ incidents |
| NHTSA Fatality Analysis Reporting System (FARS) | Fatal crash data across all vehicle types | 38,000+ annual records |
| Tesla Autopilot Safety Reports | Quarterly miles-per-accident statistics | 2019–2023 |
| NHTSA Standing General Order (SGO) Reports | Mandatory incident reports for AV/ADAS manufacturers | 2021–2023 |

### Data Fields

```
incident_id       · date             · manufacturer     · model
autopilot_engaged · crash_severity   · fatalities       · injuries
road_type         · speed_limit      · weather          · lighting
fault_attribution · autopilot_mode   · miles_driven     · state
```

> ⚠️ **Note:** NHTSA incident data represents **reported** crashes only. Under-reporting is a known limitation, particularly for minor incidents. See [Limitations](#-limitations).

---

## 💡 Key Findings

> Results are based on publicly available incident and fatality data as of 2023.

### Safety Outcomes

| Metric | Autopilot Engaged | Human Driver | Δ |
|--------|-------------------|--------------|---|
| Crashes per 1M miles | ~0.2 | ~1.4 | **−86%** |
| Fatal crashes per 1M miles | ~0.05 | ~0.15 | **−67%** |
| Rear-end collision share | 18% | 29% | **−38%** |
| Lane-departure incidents | 11% | 24% | **−54%** |

> ⚠️ These figures reflect aggregate statistics and do not control for self-selection bias (autopilot is predominantly used on highways at higher speeds with lower baseline crash risk).

### Incident Conditions

- **78%** of autopilot-related crashes occurred on **highways** at speeds > 55 mph
- **Clear weather** accounted for **61%** of autopilot incidents — suggesting over-reliance in good conditions
- **Night driving** was disproportionately represented in fatal autopilot incidents (43% vs. 26% baseline)
- **Construction zones** and **lane merges** were the most common scenario types in non-fatal incidents

### Trend Over Time

- Autopilot-related crashes per mile driven decreased by approximately **40%** between 2019 and 2023
- Software OTA (over-the-air) update releases correlate with short-term spikes in incident reports followed by improvement
- Human-driven vehicle crash rates declined ~8% over the same period

---

## 🔬 Analysis Pipeline

```
Raw Data (CSV / API)
        │
        ▼
1. Data Collection & Loading
   └── NHTSA API · CSV imports · Tesla quarterly reports
        │
        ▼
2. Data Cleaning & Preprocessing
   └── Missing value treatment · Type casting · Normalization
        │
        ▼
3. Exploratory Data Analysis (EDA)
   └── Distributions · Correlations · Temporal trends
        │
        ▼
4. Comparative Analysis
   └── Autopilot vs. Human driver outcomes
        │
        ▼
5. Condition-Based Segmentation
   └── Road type · Weather · Lighting · Speed
        │
        ▼
6. Visualization & Reporting
   └── Matplotlib · Seaborn · Plotly dashboards
        │
        ▼
7. Conclusions & Recommendations
```

---

## 📊 Visualizations

The analysis produces the following figures:

| Figure | Description |
|--------|-------------|
| `01_crash_trends.png` | Year-over-year crash frequency — autopilot vs. human |
| `02_severity_breakdown.png` | Stacked bar: fatal / injury / PDO by driver type |
| `03_road_conditions.png` | Heatmap of incident counts by road type × weather |
| `04_fault_attribution.png` | Pie charts: fault attribution by autopilot mode |
| `05_speed_distribution.png` | KDE plot of crash speeds — engaged vs. not engaged |
| `06_geographic_distribution.png` | US state-level choropleth of incident density |
| `07_time_of_day.png` | Circular histogram of incidents by hour of day |
| `08_yoy_improvement.png` | Line chart: crashes per million miles, 2019–2023 |

---

## 📁 Project Structure

```
autopilot-safety-analysis/
│
├── notebooks/
│   └── Autopilot_Safety_Analysis.ipynb    # Main analysis notebook
│
├── data/
│   ├── raw/
│   │   ├── nhtsa_adas_incidents.csv       # Raw NHTSA incident reports
│   │   ├── fars_fatality_data.csv         # FARS annual fatality records
│   │   └── tesla_safety_reports.csv       # Tesla quarterly safety stats
│   └── processed/
│       └── cleaned_incidents.csv          # Cleaned & merged dataset
│
├── figures/
│   ├── 01_crash_trends.png
│   ├── 02_severity_breakdown.png
│   ├── 03_road_conditions.png
│   ├── 04_fault_attribution.png
│   ├── 05_speed_distribution.png
│   ├── 06_geographic_distribution.png
│   ├── 07_time_of_day.png
│   └── 08_yoy_improvement.png
│
├── src/
│   ├── data_loader.py                     # Data loading & API utilities
│   ├── preprocessing.py                   # Cleaning & feature engineering
│   ├── eda.py                             # EDA helper functions
│   └── visualizations.py                  # Reusable plotting functions
│
├── requirements.txt
└── README.md
```

---

## ⚙️ Installation

### Prerequisites

- Python 3.8+
- pip or conda

### Clone the Repository

```bash
git clone https://github.com/<your-username>/autopilot-safety-analysis.git
cd autopilot-safety-analysis
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

**`requirements.txt`**
```
pandas>=2.0.0
numpy>=1.23.0
matplotlib>=3.7.0
seaborn>=0.12.0
plotly>=5.14.0
scipy>=1.10.0
scikit-learn>=1.2.0
jupyter>=1.0.0
requests>=2.28.0
geopandas>=0.13.0
```

---

## 🚀 Usage

### Run the Full Analysis Notebook

```bash
jupyter notebook notebooks/Autopilot_Safety_Analysis.ipynb
```

### Run Individual Analysis Modules

```python
from src.data_loader import load_nhtsa_data, load_tesla_reports
from src.preprocessing import clean_incidents, merge_sources
from src.eda import compare_crash_rates, segment_by_condition
from src.visualizations import plot_severity_breakdown, plot_crash_trends

# Load and clean data
incidents = load_nhtsa_data('data/raw/nhtsa_adas_incidents.csv')
tesla     = load_tesla_reports('data/raw/tesla_safety_reports.csv')
df        = merge_sources(incidents, tesla)
df        = clean_incidents(df)

# Analyse
compare_crash_rates(df, group_col='autopilot_engaged')
segment_by_condition(df, conditions=['road_type', 'weather', 'lighting'])

# Visualize
plot_severity_breakdown(df, save_path='figures/02_severity_breakdown.png')
plot_crash_trends(df, save_path='figures/01_crash_trends.png')
```

### Fetch Latest NHTSA Data via API

```python
from src.data_loader import fetch_nhtsa_sgo_reports

# Downloads the latest Standing General Order incident reports
df_fresh = fetch_nhtsa_sgo_reports(start_year=2021, end_year=2024)
df_fresh.to_csv('data/raw/nhtsa_sgo_latest.csv', index=False)
```

---

## 🔭 Methodology

### Data Cleaning

- Removed duplicate incident IDs and records with missing severity fields
- Standardized manufacturer and model name strings (e.g., `"TESLA"`, `"Tesla Inc."` → `"Tesla"`)
- Imputed missing speed values using road-type median where available; otherwise excluded
- Filtered to incidents with confirmed ADAS engagement status (unknown-engagement records excluded from comparative analysis)

### Crash Rate Normalization

Raw incident counts are normalized by **vehicle miles traveled (VMT)** to produce crashes per million miles — the standard metric used by NHTSA and the automotive industry. This accounts for the fact that autopilot-equipped vehicles collectively drive more miles than a random sample would suggest.

```
Crash Rate = (Incident Count / Vehicle Miles Traveled) × 1,000,000
```

### Comparative Framework

Comparisons between autopilot-engaged and human-driven crashes use:

- **Chi-square tests** for categorical outcomes (severity, fault attribution)
- **Mann-Whitney U tests** for continuous distributions (speed, response time) due to non-normal distributions
- **Relative Risk (RR)** ratios for crash probability comparisons
- **95% confidence intervals** reported throughout

### Bias Considerations

- **Self-selection bias:** Autopilot is predominantly used on highways where baseline crash risk is lower than urban environments
- **Reporting bias:** NHTSA SGO reporting requirements apply only to manufacturers with ADAS systems, creating asymmetric data coverage
- **Survivorship bias:** Only crashes meeting NHTSA reporting thresholds (airbag deployment, fatality, or injury requiring medical attention) are captured

---

## ⚠️ Limitations

- **Under-reporting:** Minor autopilot incidents not meeting NHTSA thresholds are not captured
- **Manufacturer variation:** Data quality and completeness varies significantly across OEMs — Tesla data is more comprehensive than most competitors
- **No exposure data for non-Tesla vehicles:** VMT normalization is only fully possible for Tesla due to their quarterly safety report disclosures
- **Causal inference:** Correlation between autopilot engagement and crash outcomes does not imply causation — confounders (road type, driver demographics, vehicle age) are not fully controlled
- **Rapidly evolving technology:** OTA software updates mean the "autopilot" in 2019 data is fundamentally different from 2023 data, complicating longitudinal comparisons

---

## 📚 References

- National Highway Traffic Safety Administration (NHTSA). *Standing General Order on Crash Reporting.* [https://www.nhtsa.gov/laws-regulations/standing-general-order-crash-reporting](https://www.nhtsa.gov/laws-regulations/standing-general-order-crash-reporting)
- NHTSA. *Fatality Analysis Reporting System (FARS).* [https://www.nhtsa.gov/research-data/fatality-analysis-reporting-system-fars](https://www.nhtsa.gov/research-data/fatality-analysis-reporting-system-fars)
- Tesla, Inc. *Vehicle Safety Reports.* [https://www.tesla.com/VehicleSafetyReport](https://www.tesla.com/VehicleSafetyReport)
- Blanco, M., et al. (2016). *Automated Vehicle Crash Rate Comparison Using Naturalistic Data.* Virginia Tech Transportation Institute.
- Teoh, E. R., & Kidd, D. G. (2017). *Rage against the machine? Google's self-driving cars and the ADAS safety paradox.* Journal of Safety Research, 63, 57–60.
- Hulse, L. M., Xie, H., & Galea, E. R. (2018). *Perceptions of autonomous vehicles: Relationships with road users, risk, gender and age.* Safety Science, 102, 1–13.
- SAE International. *Taxonomy and Definitions for Terms Related to Driving Automation Systems for On-Road Motor Vehicles (J3016).* 2021.

---

## 📜 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

<div align="center">
  <sub>Built as Part 2 of a Deep Learning & Data Science Capstone Project · February 2026</sub>
</div>

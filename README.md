# 📊 IT Operations — Process Efficiency Dashboard

> Simulating enterprise-grade KPI reporting and SLA breach analysis across 100,000 IT support tickets — mirroring real-world operations work at HP Inc. across EMEA and Asia-Pacific business units.

![Dashboard Preview](visuals/dashboard_preview.png)

---

## 🧭 Business Context

In operations roles at scale, the ability to detect SLA breaches early, identify root causes by region, and present findings to 200+ stakeholders is a core competency. This project replicates that workflow end-to-end:

- Ingesting and cleaning 100K operational records
- Engineering SLA breach flags using business-defined priority thresholds
- Building KPI summaries by region and priority tier
- Validating findings statistically (hypothesis testing)
- Delivering an interactive Power BI dashboard for stakeholder consumption

This directly mirrors the KPI reporting infrastructure I built at **HP Inc.**, where I managed end-to-end KPI reporting across EMEA and Asia-Pacific, improving reporting accuracy by 20% and reducing stakeholder turnaround time by 30%.

---

## 📌 Key Findings

| KPI | Value |
|-----|-------|
| Total Tickets Analyzed | 100,000 |
| Average Resolution Time | 45.01 hrs |
| Overall SLA Breach Rate | 24.95% |
| Average CSAT Score | 2.24 / 5 |
| Highest Breach Region | APAC |
| Top Breach Driver | billing_problem (APAC) |

### Insights
- **APAC leads SLA breaches** at ~28%, significantly above the 25% target threshold — flagging a staffing or process gap in that region
- **Urgent priority tickets paradoxically resolve fastest** (avg ~20 hrs) but low priority tickets average 65+ hrs, suggesting triage is working but backlog management is not
- **SLA breach directly and significantly reduces CSAT** — confirmed via Welch's t-test (p < 0.05), providing a quantified business case for SLA investment
- **Billing problems and how-to tickets** are the top breach drivers across all regions — pointing to knowledge base gaps rather than staffing issues
- **Ticket volume is consistent across years** but breach rate spiked in 2024, indicating a process degradation event worth investigating

---

## 🛠️ Tech Stack

| Layer | Tool | Why |
|-------|------|-----|
| Data Ingestion | `kagglehub` | Programmatic dataset versioning |
| Data Processing | `pandas`, `numpy` | Industry-standard data wrangling |
| Analysis | `scipy`, `statsmodels` | Hypothesis testing & statistical validation |
| Visualization (Python) | `matplotlib`, `seaborn` | EDA and static chart exports |
| Dashboard | **Power BI** | Enterprise BI standard (used at HP, Oracle, McKinsey) |
| Version Control | Git + GitHub | Commit history, reproducibility |

---

## 📁 Project Structure

```
ops-kpi-dashboard-itsm/
│
├── data/
│   ├── raw/                        ← source CSV (gitignored, see dataset link)
│   └── processed/
│       ├── itsm_cleaned.csv        ← cleaned dataset with engineered features
│       ├── kpi_by_region.csv       ← KPI summary by region
│       ├── kpi_by_priority.csv     ← KPI summary by priority tier
│       ├── monthly_sla_trend.csv   ← breach rate + volume by month
│       └── root_cause_breach.csv   ← breach counts by issue type × region
│
├── notebooks/
│   └── 01_ops_kpi_dashboard.ipynb  ← full analysis pipeline
│
├── visuals/
│   ├── dashboard_preview.png       ← Power BI dashboard screenshot
│   ├── 01_sla_breach_by_region.png
│   ├── 02_monthly_sla_trend.png
│   ├── 03_root_cause_heatmap.png
│   ├── 04_resolution_dist_by_priority.png
│   ├── 05_csat_vs_sla.png
│   ├── 06_volume_channel_segment.png
│   └── 07_correlation_matrix.png
│
├── dashboard/                      ← Power BI .pbix file
├── requirements.txt
├── .gitignore
└── README.md
```

---

## 📊 Dashboard Visuals

### 1. SLA Breach Rate by Region
Regional breakdown with color-coded risk tiers (red >40%, orange >25%, green ≤25%) and a 25% target reference line.

### 2. Monthly SLA Breach Trend
Dual-axis chart overlaying breach rate (line) with ticket volume (bars) — isolates whether breach spikes correlate with volume surges or process failures.

### 3. Root Cause Heatmap — Issue Type × Region
Matrix with conditional formatting (white → dark red) identifying which issue categories drive the most breaches in each region. Directly actionable for ops leads.

### 4. Resolution Time Distribution by Priority
Histograms per priority tier with SLA threshold markers and breach % annotations — shows whether the organization is triaging correctly.

### 5. CSAT vs. SLA Compliance
Side-by-side comparison of average CSAT scores for SLA-met vs. SLA-breached tickets, by priority. Quantifies the customer impact of operational failure.

### 6. Ticket Volume by Channel & Segment
Stacked bar showing how tickets distribute across channels (email, chat, in-app, web form, phone) by customer segment — useful for resource allocation decisions.

### 7. Correlation Matrix
Pearson correlation between resolution time, CSAT score, and reopen rate — confirms statistical relationships driving the analysis.

---

## ⚙️ How to Run

### Prerequisites
```bash
pip install -r requirements.txt
```

### Run the Analysis
```bash
jupyter notebook notebooks/01_ops_kpi_dashboard.ipynb
```
The notebook auto-downloads the dataset via `kagglehub` (requires a free Kaggle account and API token configured at `~/.kaggle/kaggle.json`).

Processed CSVs will export to `data/processed/` and charts to `visuals/` automatically.

### Power BI Dashboard
1. Open Power BI Desktop
2. Get Data → Text/CSV → load all files from `data/processed/`
3. Open `dashboard/ops_kpi_dashboard.pbix` (or rebuild from scratch using the processed CSVs)

---

## 🔬 Statistical Validation

Beyond descriptive analytics, this project includes formal hypothesis testing:

**Test:** Welch's independent t-test  
**H₀:** CSAT scores are not significantly different between SLA-met and SLA-breached tickets  
**H₁:** SLA breach significantly lowers CSAT  
**Result:** p < 0.05 → **Reject H₀**

This provides a statistically validated, quantified business case for SLA compliance investment — the kind of evidence-based recommendation that drives executive decisions.

---

## 📂 Dataset

**Source:** [Synthetic IT Support Tickets — Kaggle](https://www.kaggle.com/datasets/ahsanneural/synthetic-it-support-tickets)  
**Size:** 100,000 records × 20 features  
**Usability Score:** 9.4 / 10  

> Note: This is a synthetic dataset modeled on real ITSM workflows, used to simulate the type of claims and operations data encountered in enterprise environments. Actual enterprise data is confidential.

---

## 🔮 What I'd Do With Real Enterprise Data

- Connect Power BI directly to a **SQL Server or Snowflake** data warehouse instead of flat CSVs
- Build **automated refresh pipelines** so dashboards update daily without manual exports
- Add **predictive SLA breach detection** using logistic regression or XGBoost — flag tickets likely to breach before they do
- Integrate **agent workload data** to correlate staffing levels with breach rates
- Implement **row-level security** in Power BI so regional managers only see their own data

---

## 👤 Author

**Saran Chandrasekharan Unnithan**  
M.S. Engineering Management (GPA: 4.0) — University of Memphis  
NSF I-Corps Cohort | TTAC Innovation Fellow  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-sarancur-0077B5?style=flat&logo=linkedin)](https://www.linkedin.com/in/sarancur/)
[![GitHub](https://img.shields.io/badge/GitHub-sarancur-181717?style=flat&logo=github)](https://github.com/sarancur)

---

*Part of a structured portfolio built to demonstrate enterprise-grade operations analytics capabilities.*

#Financial Transaction Analysis — Portfolio Project

![Alteryx](https://img.shields.io/badge/Tool-Alteryx%20Designer-0078D4?style=for-the-badge&logo=alteryx&logoColor=white)
![Excel](https://img.shields.io/badge/Output-Microsoft%20Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-16A34A?style=for-the-badge)
![Records](https://img.shields.io/badge/Dataset-50%2C000%20Transactions-8B5CF6?style=for-the-badge)



---

## Project Overview

| Property | Details |
|---|---|
| **Dataset** | 50,000 credit card transactions |
| **Period** | January 2022 – December 2023 (2 fiscal years) |
| **Categories** | 12 merchant categories |
| **Geography** | 20 US states |
| **Customers** | 9,944 unique customers |
| **Total Revenue** | $6,759,239 |
| **Primary Tool** | Alteryx Designer (9-step ETL pipeline) |
| **Output Tool** | Microsoft Excel (7-tab workbook) |

---

## Business Questions Answered

1. **Which categories generate the most revenue — and which carry the most fraud risk?**
2. **How does spending change month-over-month and year-over-year?**
3. **Which US states have the highest-value customers?**
4. **Where is the portfolio most exposed to financial fraud?**
5. **How do different customer age groups differ in spending behavior?**

---

##Key Findings

### Revenue KPIs
| Metric | Value |
|---|---|
| Total Revenue (2 years) | **$6,759,239** |
| YoY Revenue Growth | **+8.3%** |
| Average Transaction | **$135.18** |
| Peak Month | **December** (+20% above baseline) |
| Top Category | **Travel & Accommodation** (34.6% of revenue) |

### Fraud Intelligence
| Metric | Value |
|---|---|
| Total Fraud Transactions | **512 (1.02%)** |
| Highest Risk Category | **Online Services — 2.5% fraud rate** |
| Second Highest | **Travel — 2.2% fraud rate** |
| At-Risk Financial Exposure | **~$49,800** |
| Industry Benchmark | 0.5% – 2.0% |

### Geographic Highlights
**New York** — $320 avg transaction (38% above national average)
**California** — $307 avg transaction
#*New Jersey*— Highest fraud rate among top-5 states (1.27%)

---

## Project Files

```
📁 Financial-Transaction-Analysis/
│
├── 📄 README.md                          ← You are here
├── 📊 transactions_50k.csv               ← Raw dataset (50,000 rows)
├── 📗 Financial_Analysis.xlsx       ← Full Excel analysis workbook
├── 📘 Analysis_Report.docx          ← Professional written report
└── 📙 Analysis_Presentation.pptx   ← 9-slide executive presentation
```

### Excel Workbook — 7 Sheets

| Sheet | Contents |
|---|---|
| `Executive_Summary` | 10 KPI cards + 6 business insights |
| `Category_Analysis` | Revenue, avg txn, fraud rate, risk level per category + bar chart |
| `Monthly_Trends` | FY22 vs FY23 comparison, YoY % change + line chart |
| `State_Analysis` | Top 20 states, avg transaction, revenue share + column chart |
| `Fraud_Analysis` | Risk classification, fraud rate, recommended actions per category |
| `Customer_Segmentation` | Age group and gender spending breakdown |
| `Raw_Data_Sample` | 2,000-row formatted sample (full 50K in CSV) |

---

## ⚙️ Alteryx Workflow — Step by Step

```
[Input Data] ──► [Data Cleansing] ──► [DateTime] ──► [Formula] ──► [Filter] ──► [Select]
                                                                                      │
                    ┌─────────────────────────────────────────────────────────────────┘
                    │
                    ├──► [Summarize: Category] ──► [Sort DESC] ──► [Output: Category_Analysis.xlsx]
                    │
                    ├──► [Summarize: Month+Year] ──► [Sort ASC] ──► [Output: Monthly_Trends.xlsx]
                    │
                    ├──► [Summarize: State] ──► [Sort DESC] ──► [Output: State_Analysis.xlsx]
                    │
                    └──► [Summarize: Customer] ──► [Sort DESC] ──► [Output: Fraud_Analysis.xlsx]
```

### Tools Used & Purpose

| Step | Tool | Purpose |
|---|---|---|
| 1 | **Input Data** | Ingest CSV — 50,000 rows, 13 fields, auto type-detection |
| 2 | **Data Cleansing** | Null handling, whitespace removal, field standardization |
| 3 | **DateTime** | String → DateTime conversion, extract Year/Month/DayOfWeek |
| 4 | **Formula** | Age_Group bins, Transaction_Tier flags, derived KPIs |
| 5 | **Filter** | Remove amount ≤ 0, apply business validation rules |
| 6 | **Select** | Rename columns, drop unused fields, enforce types |
| 7 | **Summarize ×4** | GroupBy aggregations: SUM, AVG, COUNT, MAX per dimension |
| 8 | **Sort** | Sort each branch for clean tabular output |
| 9 | **Output ×4** | Export to Excel: Category, Monthly, State, Fraud |

> 

---

## 📁 Dataset Schema

| Column | Type | Description |
|---|---|---|
| `trans_datetime` | DateTime | Transaction timestamp (YYYY-MM-DD HH:MM:SS) |
| `customer_id` | String | Unique customer identifier (e.g., CUST10042) |
| `merchant` | String | Merchant name (e.g., Amazon, Delta Airlines) |
| `category` | String | Merchant category (12 categories) |
| `amount` | Double | Transaction amount in USD |
| `gender` | String | Customer gender (M / F / Non-Binary) |
| `age` | Integer | Customer age (18–74) |
| `state` | String | US state abbreviation (20 states) |
| `year` | Integer | Transaction year (2022 or 2023) |
| `month` | Integer | Transaction month (1–12) |
| `month_name` | String | Month name (Jan–Dec) |
| `day_of_week` | String | Day of week (Monday–Sunday) |
| `is_fraud` | Integer | Fraud flag: 1 = Fraudulent, 0 = Legitimate |



---

##  Analytical Methodology

### Fraud Risk Classification
Categories were classified into four risk tiers based on fraud rate thresholds:

| Risk Level | Fraud Rate Threshold | Categories | Recommended Action |
|---|---|---|---|
| 🔴 CRITICAL | > 2.0% | Online Services | Block + Manual Review |
| 🟠 HIGH | 1.0% – 2.0% | Travel, Retail, Financial Services | Real-time ML Scoring |
| 🟡 MEDIUM | 0.5% – 1.0% | Home, Fuel, Entertainment | Enhanced Monitoring |
| 🟢 LOW | < 0.5% | Grocery, Food, Healthcare, Education, Utilities | Standard Monitoring |

### Seasonality Index
Monthly spending was indexed against the annual average to identify seasonal patterns:
- **Peak Season (>110% index):** June, July, August, November, December
- **Trough Season (<90% index):** January, February, March

### Geographic Premium Score
States were scored using average transaction value relative to the national average:
- **Premium (>115%):** NY, CA, NJ, MA, WA
- **Standard (85–115%):** IL, MD, CO, VA, PA, FL, AZ
- **Value (<85%):** TN, IN, MO

---

##  Key Business Recommendations

| Priority | Recommendation | Expected Impact |
|---|---|---|
| 1️⃣ | Deploy real-time fraud scoring for Online Services & Travel | 40–60% fraud reduction |
| 2️⃣ | Apply transaction velocity controls (max 3 txns/hour for high-risk categories) | 60% of fraud pattern blocked |
| 3️⃣ | Premium loyalty program for NY, CA, NJ customers ($300+ avg txn) | 15-20% revenue uplift |
| 4️⃣ | Increase marketing spend 30% in Nov–Dec peak window | Capture +20% seasonal demand |
| 5️⃣ | Expand merchant partnerships in Education (+11.8% YoY) and Financial Services (+14.2% YoY) | Capture growth verticals |

---

---

## 🛠️ Skills Demonstrated

**Alteryx Designer:** Input Data • Data Cleansing • DateTime • Formula • Filter • Select • Summarize • Sort • Output Data • Multi-branch workflow design • Automated pipeline architecture

**Microsoft Excel:** Multi-sheet workbook design • Dynamic formulas (SUMIF, IF, AVERAGE) • Embedded charts (Bar, Line, Column) • Conditional formatting • KPI dashboards • Professional table styling

**Data Analysis:** EDA • KPI definition • Risk tiering • Seasonality analysis • Geographic segmentation • YoY comparison • Customer segmentation • Fraud intelligence

**Business Communication:** Executive summary writing • Data storytelling • Actionable recommendation framing • Big 4 deliverable standards

---



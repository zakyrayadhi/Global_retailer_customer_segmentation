# Global Electronics Retailer: Customer Segmentation & CLV Analysis

## 📌 Project Overview
Final project for Data Analyst bootcamp analyzing customer behavior of a multinational electronics retailer using RFM Segmentation and Customer Lifetime Value (CLV) analysis across 5 years of transactional data (2016–2021).

---

## 🎯 Business Questions
1. Who are our customers and what are their demographic profiles?
2. Which customer segments are the most valuable based on RFM analysis?
3. What is the CLV distribution across customer tiers?
4. How does CLV tier relate to RFM segments?

---

## 🗂️ Dataset
Source: [Maven Analytics Data Playground](https://mavenanalytics.io/data-playground/global-electronics-retailer)

| Table | Rows | Description |
|---|---|---|
| Sales | 62,884 | Core transaction records |
| Products | 2,517 | Product catalog with pricing |
| Customers | 15,266 | Customer demographics & location |
| Stores | 67 | Physical & online store info |
| Exchange Rates | 11,215 | Multi-currency conversion* |

> *Exchange Rates not used — product prices already standardized in USD regardless of customer's local currency.

---

## 🛠️ Tools & Technologies
- **Python** (Google Colab) — data cleaning, manipulation, EDA, RFM & CLV analysis
- **Power BI** — interactive dashboard
- **Libraries** — pandas, numpy, matplotlib, seaborn

---

## 🔧 Data Cleaning Summary

| Table | Column | Issue | Action |
|---|---|---|---|
| Sales | Delivery Date | 49,719 missing (79.06%) | Left as NaN — in-store purchases have no delivery date (verified via StoreKey) |
| Customers | State Code | 10 missing (0.07%) | Filled with 'NA' — Napoli province code (Italy), confirmed via Google |
| Stores | Square Meters | 1 missing (1.49%) | Filled with 0 — StoreKey 0 is online store, no physical space |
| Products | Unit Price/Cost USD | String format ($1,234.56) | Stripped '$' and ',' then cast to float64 |
| Sales | Order Date, Delivery Date | Object (string) | Converted to datetime using format='mixed' (MM/DD/YYYY) |

---

## ⚙️ Feature Engineering

| Feature | Description |
|---|---|
| `Order Channel` | Online / In-Store based on StoreKey (0 = Online) |
| `Revenue` | Quantity × Unit Price USD |
| `Cost` | Quantity × Unit Cost USD |
| `Profit` | Revenue - Cost |
| `Delivery Days` | Delivery Date - Order Date (online orders only) |
| `Order Year`, `Order Month` | Extracted from Order Date |
| `R_Score`, `F_Score`, `M_Score` | Percentile-based quintile scoring (1–5) via pd.qcut() |
| `RFM_Score` | Concatenated string of R, F, M scores (e.g. "555") |
| `Segment` | RFM-based customer segment |
| `CLV_Tier` | Tercile-based CLV tier (Low / Medium / Top Value) |

---

## 📊 RFM Segmentation Results

| Segment | Customers | Avg Recency | Avg Frequency | Avg Monetary |
|---|---|---|---|---|
| Champions | 1,912 | 261 days | 4.10 orders | $10,346 |
| Loyal | 4,172 | 389 days | 2.36 orders | $3,940 |
| At Risk | 1,335 | 852 days | 2.59 orders | $6,986 |
| Need Attention | 1,058 | 386 days | 1.03 orders | $2,699 |
| Lost | 3,410 | 1,069 days | 1.20 orders | $2,157 |
| Inactive | 3,379 | — | 0 orders | $0 |

> **Key finding:** Champions (12.5% of customers) generate $19.8M — 35% of total revenue. At Risk customers hold $9.3M in revenue at stake.

---

## 💰 CLV Tier Results

| Tier | Customers | Avg CLV | Avg Frequency | Gross Margin |
|---|---|---|---|---|
| Top Value | ~3,963 | $10,200 | 3.2 orders | 59% |
| Medium Value | ~3,963 | $3,100 | 2.1 orders | 57% |
| Low Value | ~3,963 | $700 | 1.4 orders | 55% |

> **Key finding:** Top Value customers (33% of active) generate 72.76% of total revenue. 87.97% of Champions fall into the Top Value tier.

---

## 🔗 CLV × RFM Matrix

| CLV Tier | At Risk | Champions | Lost | Loyal | Need Attention |
|---|---|---|---|---|---|
| Low Value | — | — | 60.59% | 32.29% | 51.89% |
| Medium Value | 45.24% | 12.03% | 28.27% | 43.98% | 31.10% |
| Top Value | 54.76% | 87.97% | 11.14% | 23.73% | 17.01% |

---

## 📋 Planning Implementasi Case

| Phase | Action | Target Segment | KPI | Target | Est. Impact |
|---|---|---|---|---|---|
| 1 — Retain | Exclusive loyalty program | Champions (1,912) | Total Champions count | Maintain ≥ 1,912 | Protect $19.8M |
| 2 — Win-back | Personalized re-engagement offer | At Risk (1,335) | % upgraded to Loyal | ≥ 20% (~267 customers) | Recover ~$1.05M |
| 3 — Upgrade | Upsell to premium products | Loyal Medium Value | % moved to Top Value tier | ≥ 15% (~274 customers) | Add ~$1.95M |

**Total estimated revenue impact: ~$3M**

---

## 📁 Repository Structure
```
├── notebook/
│   └── GlobalElectronics_Analysis.ipynb
├── dataset/
│   └── cleaned/
│       ├── Sales_cleaned.csv
│       ├── Products_cleaned.csv
│       ├── Customers_cleaned.csv
│       ├── Stores_cleaned.csv
│       └── RFM_Segmentation.csv
├── dashboard/
│   └── GlobalElectronics_Dashboard.pbix
├── presentation/
│   └── GlobalElectronics_Final.pptx
└── README.md
```

---

## 👤 Author
**Zaky Rayadhi** — Data Analyst | June 2026

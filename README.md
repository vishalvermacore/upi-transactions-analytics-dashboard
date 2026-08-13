# 💳 UPI Pulse — UPI Transactions Analytics Dashboard

**An interactive Excel dashboard analyzing 500K+ UPI transactions to surface payment behavior, merchant performance, and fraud-risk patterns across India.**

![Excel](https://img.shields.io/badge/Tool-Microsoft%20Excel-217346?style=flat&logo=microsoftexcel&logoColor=white)
![PivotTables](https://img.shields.io/badge/Analysis-PivotTables%20%7C%20Slicers-blue)
![Records](https://img.shields.io/badge/Records-502%2C887-orange)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Business Problem](#-business-problem)
- [Dataset Overview](#-dataset-overview)
- [Tech Stack](#-tech-stack)
- [Dashboard Structure](#-dashboard-structure)
- [Key Metrics (KPIs)](#-key-metrics-kpis)
- [Key Insights](#-key-insights)
- [Performance Optimization](#-performance-optimization)
- [Project Structure](#-project-structure)
- [How to Use](#-how-to-use)
- [Future Scope](#-future-scope)
- [Author](#-author)

---

## 📖 Overview

**UPI Pulse** is an end-to-end Excel analytics project built on a real-world-style dataset of **5,02,887 UPI (Unified Payments Interface) transactions** recorded across India in **May 2026**. The project transforms raw transaction-level data into a fully interactive, slicer-driven dashboard that lets stakeholders explore payment trends by **app, bank, state, merchant category, device, gender, age group, and time of day** — without writing a single line of code.

The goal was to replicate how a **Senior Data Analyst** would approach a large transactional dataset in a business setting: clean it, model it, build reusable pivot logic, and package it into a dashboard that's fast, filterable, and decision-ready.

---

## 🎯 Business Problem

UPI has become India's dominant digital payment rail, but businesses and payment platforms need visibility into:

- Which **UPI apps and banks** are driving the most volume and value
- Where **failed/pending transactions** are concentrated (and why)
- Which **merchant categories and states** contribute the most spend
- What **time-of-day patterns** exist in transaction behavior
- How much **suspected fraud** is present, and where it clusters

This dashboard answers those questions interactively, using **14 pivot tables**, **multiple slicers**, and **charts** built on a single shared data model — so any stakeholder can filter by City, Gender, Merchant Category, or Merchant Name and see every visual update in sync.

---

## 🗂 Dataset Overview

| Attribute | Detail |
|---|---|
| **Total Records** | 5,02,887 transactions |
| **Time Period** | 1 May 2026 – 31 May 2026 |
| **Granularity** | Transaction-level (with derived Day & Hour fields) |
| **Total Columns** | 24 |

**Column groups:**

| Category | Fields |
|---|---|
| Transaction Meta | `Transaction_ID`, `Transaction_Date`, `Day`*, `Transaction_Time`, `Hour`* |
| Payment Details | `UPI_App`, `Payment_Mode`, `Bank_Name`, `Transaction_Type` |
| Customer Profile | `Customer_ID`, `Age_Group`, `Gender`, `State`, `City`, `Device_OS` |
| Merchant Info | `Merchant_Name`, `Merchant_Category` |
| Financials | `Amount_INR`, `Cashback_INR`, `Transaction_Fee_INR` |
| Outcome & Risk | `Status`, `Failure_Reason`, `Risk_Score`, `Is_Suspected_Fraud` |

<sub>*`Day` and `Hour` are analyst-derived fields, extracted from `Transaction_Date` and `Transaction_Time` to enable weekday and hourly trend analysis.</sub>

---

## 🛠 Tech Stack

| Tool | Purpose |
|---|---|
| **Microsoft Excel** | Core platform |
| **PivotTables & PivotCharts** | Aggregation and trend visualization (14 pivot tables on a shared cache) |
| **Slicers** | Interactive filtering by City, Gender, Merchant Category, Merchant Name |
| **Formulas** (`TEXT`, `HOUR`, `TIMEVALUE`) | Feature engineering (Day-of-week, Hour-of-day extraction) |
| **Conditional Formatting** | Visual flagging of risk/status fields |
| **Data Modeling Best Practices** | Single pivot cache architecture for consistent, synced visuals across 14 pivots |

---

## 🧩 Dashboard Structure

The workbook is organized into 4 purpose-built sheets:

1. **`UPI_Raw_Data`** — The full 5,02,887-row transaction log (single source of truth for every pivot).
2. **`Pivot_Worksheet`** — Backend workspace containing all 14 pivot tables and pivot charts.
3. **`Image_metrics`** — Supporting metric snapshots and static visual references.
4. **`UPI Dashboard`** — The final interactive, presentation-ready dashboard with slicers, KPIs, and charts.

**Interactive filters (Slicers):**
- 🏙️ City
- 🚻 Gender
- 🏪 Merchant Category
- 🏷️ Merchant Name

---

## 📊 Key Metrics (KPIs)

| Metric | Value |
|---|---|
| 💰 **Total Transaction Value** | ₹44.25 Crore |
| 🔢 **Total Transactions** | 5,02,887 |
| 🎟️ **Average Ticket Size** | ₹879.88 |
| 🎁 **Total Cashback Disbursed** | ₹34.63 Lakh |
| 💸 **Total Transaction Fees** | ₹5.20 Lakh |
| ✅ **Success Rate** | 91.0% |
| ❌ **Failure Rate** | 7.0% |
| ⏳ **Pending Rate** | 1.99% |
| 🚩 **Suspected Fraud Rate** | 3.4% (17,089 transactions) |

---

## 🔍 Key Insights

- **PhonePe dominates the market**, accounting for **48.3%** of all transactions — more than Google Pay (21.9%) and Paytm (14.9%) combined.
- **Android drives 81.9%** of transaction volume vs. **18.1% on iOS**, reflecting India's broader smartphone OS split.
- Spend is **fairly evenly distributed across merchant categories** — Fuel, Shopping, Grocery, Food & Dining, Recharge & Bills, Entertainment, Healthcare, and Utilities each account for ~9% of transactions, suggesting no single category dominates daily UPI usage.
- **Delhi, Maharashtra, Tamil Nadu, Karnataka, and Gujarat** are the top 5 states by transaction count, each contributing roughly 50,000+ transactions — indicating broad, balanced adoption rather than concentration in one region.
- The **gender split (54% Male / 45% Female / 1% Other)** suggests healthy but not fully even digital payment adoption across demographics — a potential area for deeper segmentation.
- **3.4% of transactions are flagged as suspected fraud**, a rate high enough to warrant a dedicated risk-monitoring view — the `Risk_Score` and `Is_Suspected_Fraud` fields are structured to support this directly.

---

## ⚡ Performance Optimization

With 500K+ rows feeding 14 live pivot tables and multiple slicers, the workbook initially suffered from slow slicer response times. As part of building this project, the following optimizations were applied:

- **Removed ~1 million live cell formulas**: The `Day` and `Hour` columns were originally formula-driven (`TEXT()`, `HOUR()`, `TIMEVALUE()`) across all 502,887 rows. These were converted to **static values**, eliminating recalculation overhead on every filter interaction.
- **Consolidated pivot cache**: All 14 pivot tables reference a **single shared pivot cache** instead of individual caches, avoiding redundant data reloads.
- **Trimmed calculation chain**: `calcChain.xml` was reduced from ~22 MB to ~8 KB after the formula cleanup, and overall file size dropped from ~100.5 MB to ~94.5 MB.

This reflects a real-world analyst skill: **building for scale, not just for output** — a dashboard is only as useful as its ability to stay responsive under real usage.

---

## 📁 Project Structure

```
UPI_Transactions_Analyse_Dashboard.xlsx
│
├── UPI_Raw_Data        → Source data (502,887 transactions × 24 columns)
├── Pivot_Worksheet      → 14 PivotTables + PivotCharts (backend logic)
├── Image_metrics        → Metric snapshots / static visual references
└── UPI Dashboard        → Final interactive dashboard (slicers + KPIs + charts)
```

---

## 📂 Data & Project File

Due to GitHub's file size limits, the two components of this project are hosted separately:

| File | Description | Location |
|---|---|---|
| 🗃️ **`UPI_Raw_Data.zip`** | Raw dataset (502,887 rows × 24 columns) exported as CSV and compressed |  [📥 Download here](https://drive.google.com/drive/folders/1Hd7NczyEwRwV3mCnJYqlVJtXjlblaEVp?usp=sharing) |
| 📊 **`UPI_Transactions_Analyse_Dashboard.xlsx`** | Full interactive dashboard — pivot tables, slicers, charts |Included in this repo|

## 🚀 How to Use

1. Download `UPI_Transactions_Analyse_Dashboard.xlsx` from the link above and open it in **Microsoft Excel** (Desktop recommended for full slicer/pivot interactivity).
2. Go to the **`UPI Dashboard`** sheet.
3. Use the **slicers** (City, Gender, Merchant Category, Merchant Name) to filter the entire dashboard interactively.
4. Explore the **`Pivot_Worksheet`** sheet to see the underlying pivot logic behind each visual.
5. To inspect the raw data directly, unzip **`UPI_Raw_Data.zip`** from this repo — it contains the same 502,887 transactions used to build the dashboard.

---

## 🔮 Future Scope

- Migrate the data model to **Power Pivot / Power BI** for even faster performance at scale and DAX-based measures.
- Add a **dedicated fraud-monitoring view** combining `Risk_Score` and `Is_Suspected_Fraud` with merchant/state breakdowns.
- Build **cohort analysis** by `Age_Group` and `Gender` to study adoption trends over time.
- Extend the dataset beyond a single month to enable **month-over-month trend tracking**.

---

## 👤 Author

**Vishal Verma**
Data Analyst | Excel • SQL • Power BI
📧 vishalverma.50103@gmail.com | 🔗 [LinkedIn](https://www.linkedin.com/in/vishalvermacore) 

---

⭐ If you found this project useful or insightful, consider giving it a star!

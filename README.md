# Vendor Performance Analysis Dashboard

Analyzing vendor performance for a liquor/beverage retail business using Python and Power BI — turning raw purchase, sales, and invoice data into an interactive dashboard that surfaces which vendors drive profit and which are dragging performance down.

---

## 📌 Project Overview

Retail businesses often work with dozens of vendors, but not all vendors contribute equally to profitability. This project analyzes vendor-level purchase, sales, and invoice data (~12.8M+ transaction records) to answer a core business question:

> **Which vendors should this business double down on, renegotiate with, or drop?**

The project covers the full analytics workflow — from raw CSV ingestion into a SQL database, through data cleaning and statistical analysis in Python, to a polished, interactive Power BI dashboard — mirroring how this analysis would be done in a real business/analytics team.

---

## 🎯 Objectives

- Ingest and structure raw CSV data into a relational database
- Clean and prepare purchase, sales, and invoice data for analysis
- Identify top-performing and underperforming vendors
- Analyze profit margins, sales concentration, bulk-purchasing effects, and inventory turnover
- Statistically validate performance differences between vendor groups
- Build an interactive Power BI dashboard for ongoing vendor performance tracking

--

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **Python (pandas, SQLAlchemy)** | Data ingestion, cleaning, transformation, EDA |
| **SQL** | Queries and CTEs joining purchases, sales, and invoice tables |
| **SQLite** | Source database (`inventory.db`) |
| **Jupyter Notebook** | Analysis workflow, documentation, visualizations |
| **Power BI** | Dashboard build, DAX measures, interactive visuals |
| **Statistical Testing** | Hypothesis testing / confidence intervals to validate vendor performance differences |

---

## 🔁 Workflow

1. **Data Ingestion** — Load raw CSVs and ingest into a SQLite database (`inventory.db`) using a repeatable Python/SQLAlchemy pipeline with logging
2. **Data Cleaning** — Handle nulls, infinite values in profit margin columns, type mismatches, column name inconsistencies
3. **Exploratory Data Analysis (EDA)** — Summary statistics, distribution plots, correlation heatmap across 14 key metrics (purchase price, sales dollars, freight cost, profit margin, stock turnover, etc.)
4. **Vendor Performance Analysis** — SQL/pandas analysis answering targeted business questions (see below)
5. **Statistical Validation** — Hypothesis testing to confirm whether performance differences between vendor groups are statistically significant
6. **Dashboard Build** — Power BI report with custom DAX measures for vendor KPIs

---

> **Note on raw data:** The raw dataset (~180MB) is hosted externally due to GitHub file size limits. 🔗 [Download raw dataset](ADD_YOUR_LINK_HERE)
> This repo includes a cleaned/processed sample in `data/processed/` for review without needing the full download.

---

## 📊 Key Business Questions Answered

1. Which brands have low sales but high profit margins (candidates for promotional/pricing adjustments)?
2. Which vendors contribute the most to total purchases, and is the business over-reliant on a few of them?
3. Does bulk purchasing meaningfully reduce unit costs?
4. Which vendors have the lowest inventory turnover / most unsold stock?
5. Do top-performing and low-performing vendors differ significantly in profit margin?

---

## 📈 Key Insights

- **Pricing opportunity:** 198 brands show low sales but high profit margins (>65%), making them strong candidates for targeted marketing, promotions, or price optimization to grow volume without hurting margin.
- **Vendor concentration risk:** The top 10 vendors account for **65.69%** of total purchases, while all remaining vendors combined contribute only 34.32% — a concentration risk worth diversifying against.
- **Bulk purchasing pays off:** Large orders bring unit purchase price down to **$10.78**, a **~72% reduction** versus small-order unit pricing (~$39.07), confirming that bulk pricing strategies meaningfully lower costs.
- **Unsold inventory:** Total unsold inventory capital sits at **$2.71M**, concentrated among a handful of major vendors (e.g. Diageo North America, Jim Beam, Pernod Ricard), tying up cash flow and increasing storage costs.
- **Margin vs. volume tradeoff:** Top-selling vendors average a **31.17%** profit margin vs. **41.55%** for low-selling vendors — low-performing vendors keep higher margins but struggle with sales volume, pointing to pricing or market-reach inefficiencies rather than product profitability.
- **Statistically significant difference:** A hypothesis test rejected the null hypothesis of no difference between top and low vendor profit margins, confirming the two groups operate under genuinely different profitability models.

---

## ✅ Recommendations

- Re-evaluate pricing for low-sales, high-margin brands to grow volume without sacrificing profitability
- Diversify vendor partnerships to reduce dependency on the top 10 suppliers and mitigate supply chain risk
- Leverage bulk purchasing to keep costs competitive while optimizing inventory levels
- Address slow-moving inventory through adjusted purchase quantities, clearance sales, or revised storage strategies
- Strengthen marketing and distribution for low-performing (high-margin) vendors to drive sales volume

---
## 🚧 Challenges & Fixes

Real data issues worked through during this project:

- **Infinite values in profit margin columns** — caused by zero-cost or zero-revenue transactions; handled via conditional filtering (excluding Gross Profit ≤ 0, Profit Margin ≤ 0, Total Sales Quantity = 0)
- **Pareto/scatter chart rendering bugs** — variable naming collisions between similarly named axis variables, plus fraction-vs-percentage mismatches in cumulative calculations
- **Column name typos** — caused silent `KeyError`s during merges; resolved with explicit column validation before joins
- **Large-scale ingestion** — over 12.8M rows in the sales table alone, requiring a logged, repeatable ingestion pipeline rather than manual loading

---

## 👤 Author

Built by **Aditya Singh** as part of a data analyst portfolio, demonstrating end-to-end analysis: data ingestion → Python cleaning/EDA → statistical validation → Power BI dashboarding.

- [LinkedIn] - www.linkedin.com/in/aditya-singh-x

---

# 💻 AtliQ Hardware — Business Intelligence & Supply Chain Analytics

> An end-to-end Business Intelligence project transforming fragmented business data into an interactive analytical solution for executive decision-making across **Sales, Finance, and Supply Chain**.

[![Status](https://img.shields.io/badge/status-complete-brightgreen)]()
[![Type](https://img.shields.io/badge/type-BI%20reporting-blue)]()
[![Industry](https://img.shields.io/badge/industry-electronics%20%2F%20supply%20chain-informational)]()
[![Tool](https://img.shields.io/badge/tool-Power%20BI-yellow)]()

---

## 📖 Project Overview & Business Background

### Business Context

AtliQ Hardware is a consumer electronics company operating across multiple countries and experiencing rapid business growth.

As the organization expanded, management continued to rely heavily on **Excel-based reporting** — a slow, hard-to-scale process with no centralized KPIs and limited visibility into market, customer, and profitability trends. A significant setback in the **Latin American market** further highlighted the need for stronger, data-driven decision-making.

### 🎯 Project Objective

The objective of this project was to build a centralized Power BI analytics solution that lets management **monitor sales and profitability, evaluate customers/products/markets, track gross margin, compare performance against targets, and analyze forecast accuracy and inventory risk (Excess Stock / Out of Stock)** — turning raw operational data into actionable recommendations.

---

## 🗂️ 2. Data Structure & Data Model

The Power BI solution uses a relational **semantic model** consisting of fact tables, dimension tables, and supporting analytical tables.

### Core Dimensions

| Dimension | Purpose |
|---|---|
| `dim_date` | Date, month, fiscal year, quarter, YTD and YTG analysis |
| `dim_customer` | Customer, platform, channel and market attributes |
| `dim_market` | Market, region and sub-zone hierarchy |
| `dim_product` | Product, division, segment, category and variant attributes |
| `dim_product_category` | Product category classification |
| `dim_sub_zone` | Regional sub-zone classification |
| `fiscal_year` | Fiscal-year reporting and filtering |

### Core Fact Tables

| Fact Table | Purpose |
|---|---|
| `fact_sales_monthly` | Monthly historical sales quantities |
| `fact_forecast_monthly` | Monthly forecast quantities |
| `fact_actuals_forecasts` | Sales, deductions, costs and operational metrics |
| `manufacturing_cost` | Product-level manufacturing cost information |
| `freight_cost` | Freight cost assumptions by market and fiscal year |
| `post_invoice_deductions` | Customer/product-level post-invoice deductions |
| `OPEX` | Operating expenses including advertising and promotions |

### Simplified Data Model

```
                             ┌─────────────────┐
                             │    dim_date     │
                             └────────┬────────┘
                                      │
              ┌───────────────────────┼────────────────────────┐
              │                       │                        │
              ▼                       ▼                        ▼
     ┌────────────────┐     ┌──────────────────┐     ┌─────────────────┐
     │ fact_sales_    │     │ fact_forecast_   │     │ fact_actuals_   │
     │ monthly        │     │ monthly          │     │ forecasts       │
     └───────┬────────┘     └────────┬─────────┘     └────────┬────────┘
             │                       │                        │
             └───────────────┬───────┴───────────────┬────────┘
                              │                        │
                     ┌────────▼────────┐      ┌───────▼────────┐
                     │  dim_customer   │      │  dim_product   │
                     └─────────────────┘      └───────┬────────┘
                                                        │
                                               ┌───────▼────────┐
                                               │   dim_market   │
                                               └────────────────┘
```

The model uses shared dimensions such as **Date, Customer, Product, and Market** to provide consistent filtering and analysis across sales, finance, and supply-chain metrics.

### 📅 Fiscal Calendar

AtliQ Hardware follows a **September–August fiscal year** rather than a January–December calendar year. The model therefore incorporates fiscal-year logic and YTD/YTG calculations to align reporting with the company's business calendar.

---

## 💡 3. Executive Summary

The Power BI solution integrates three major analytical perspectives.

### 📈 Sales Analytics
The Sales dashboard evaluates:
- Net sales
- Customer contribution
- Product-segment performance
- Market and regional performance
- Gross margin
- Sales growth
- Target and benchmark performance

### 💰 Finance Analytics
The Finance dashboard provides a P&L-oriented view of:

```
Gross Sales
     ↓
Pre-Invoice Deductions
     ↓
Net Invoice Sales
     ↓
Post-Invoice Deductions
     ↓
Net Sales
     ↓
COGS
     ↓
Gross Margin
     ↓
OPEX
     ↓
Net Profit
```

### 📦 Supply Chain Analytics
The Supply Chain dashboard connects demand forecasting with operational risk through:
- Forecast quantity
- Actual sales quantity
- Net forecast error
- Absolute error
- Forecast accuracy
- YoY forecast accuracy
- Product-level forecast performance
- Customer-level forecast performance
- Excess Stock / Out of Stock classification

Together, these views provide a unified perspective of **revenue, profitability, demand, and inventory performance**.

---

## 📊 4. Key Business Insights

### 4.1 Sales Show a Recurring Seasonal Pattern
The monthly sales trend generally shows an increase during the early fiscal-year period, particularly from **September through December**, followed by a sharp decline around January and a comparatively stable period through the following months.

**Business implication:** Inventory, procurement, and production planning should account for recurring demand peaks rather than relying solely on annual averages.

> ⚠️ The exact peak month varies by fiscal year, so the pattern should be interpreted as recurring seasonality rather than a fixed October–November peak.

### 4.2 Significant Demand Shock in 2020
FY2020 contains a major disruption in monthly sales. Net sales declined from approximately **$22.15M in February → $2.76M in March**, before recovering to approximately **$20.06M by June**. The timing coincides with the global COVID-19 disruption period.

**Business implication:** Such demand shocks can rapidly affect forecast accuracy, inventory planning, procurement, working capital, and revenue realization.

> ⚠️ COVID-19 is a plausible external explanation for the disruption, but the dashboard alone does not establish causality.

### 4.3 Revenue Growth Did Not Translate Into Sustainable Profitability
FY2019 was the only displayed fiscal year with positive net profit, at approximately **+$2.46M**. Subsequent periods show significant negative profitability.

> **Revenue growth alone is not translating into sustainable bottom-line performance.**

The business should therefore focus not only on revenue growth but also on gross margin, commercial deductions, COGS, OPEX, and customer/product profitability.

### 4.4 High Customer Revenue Concentration
**Amazon, AtliQ Exclusive, and AtliQ e Store** consistently appear among the largest customers, together contributing approximately **one-third of revenue on average** across the analyzed periods.

**Business implication:** This concentration creates both an opportunity and a risk — increasing exposure to customer churn, pricing pressure, contract changes, and revenue volatility.

### 4.5 Desktop Emerged as a High-Growth Product Segment

| Period | Desktop Revenue |
|---|---|
| FY2020 | $0.95M |
| FY2021 | $46.43M |
| 2022_EST YTD | $280.78M |

**Business implication:** Management should evaluate whether the rapid growth is supported by sustainable demand, healthy margins, reliable forecasts, adequate inventory, and supplier capacity.

> ⚠️ The 2022 figure is associated with the `2022_EST` period and should be interpreted as YTD/estimated-period performance rather than a directly comparable completed fiscal year.

### 4.6 Revenue Is Concentrated in a Few Product Segments
The top three product segments — **Notebook, Accessories, and Peripherals** — contribute approximately **79% of revenue on average** across the analyzed periods. A disruption in one of these segments could have a disproportionate effect on overall revenue.

### 4.7 Geographic Concentration Creates Strategic Exposure
**India, USA, and South Korea** consistently rank among the major revenue-generating markets. At the regional level, **APAC** is the strongest revenue-generating region, while **EU** demonstrates comparatively consistent positive profitability.

> **The region generating the most revenue is not necessarily the region generating the strongest profitability.**

### 4.8 Gross Margin Remains Relatively Stable but Under Pressure From Cost Structure
Across the analyzed periods, COGS generally accounts for approximately **59–63% of net sales**, leaving gross margin in the approximate range of **37–41%**. At large revenue volumes, even a small change in gross margin can create a substantial financial impact.

**Potential margin improvement levers:** supplier negotiations, product mix optimization, pricing strategy, cost reduction, customer-level margin analysis.

### 4.9 Large Gap Between Gross Sales and Net Sales
Net sales represent roughly **50% of gross sales** across several periods after accounting for deductions, indicating significant commercial leakage between gross sales and realized net sales.

**Business implication:** A high-revenue customer may not necessarily be a high-profit customer after deductions.

### 4.10 Forecast Accuracy and Inventory Risk Are Connected
The Supply Chain analysis combines actual demand, forecast demand, forecast error, and inventory classification — highlighting both **Excess Stock (ES)** and **Out of Stock (OOS)** across products and categories, including major categories like Notebook, Accessories, and Peripherals appearing in OOS classifications.

> ⚠️ The dashboard identifies the relationship between forecast performance and inventory risk; it does not independently prove a causal relationship.

---

## 🎯 5. Recommendations

| # | Recommendation | Action |
|---|---|---|
| 5.1 | 📦 **Adopt a Demand-Sensitive Inventory Strategy** | Use historical seasonality and forecast performance to adjust inventory levels, increase coverage before demand peaks, and establish product-level safety-stock policies. |
| 5.2 | 💧 **Reduce Commercial Leakage** | Analyze deductions by customer, product, market, channel, and fiscal year to identify where discounting is eroding revenue. |
| 5.3 | ⚖️ **Prioritize Profitability Over Revenue Growth Alone** | Monitor the full Revenue → Net Sales → Gross Margin → OPEX → Net Profit chain to distinguish high-revenue growth from high-quality growth. |
| 5.4 | 🗄️ **Optimize Inventory Across Product Categories** | Segment products by demand volatility, review safety-stock levels, and investigate recurring OOS/excess-stock categories. |
| 5.5 | 🤝 **Reduce Customer Concentration Risk** | Develop secondary strategic accounts, expand underpenetrated customers, and evaluate customer profitability after deductions. |
| 5.6 | 🔍 **Investigate Desktop Growth Before Scaling Further** | Evaluate demand sustainability, gross margin, forecast accuracy, and supplier capacity before further procurement commitments. |
| 5.7 | 🧭 **Introduce Scenario-Based Planning** | Incorporate base-case, downside, upside, and demand-shock scenarios into supply-chain planning to build resilience. |

---

## 🛠 6. Tech Stack

### Business Intelligence
- **Microsoft Power BI** — interactive dashboards, data visualization, semantic modeling, executive reporting, drill-down and cross-filtering

### Data Transformation
- **Power Query / M** — data extraction, cleaning, transformation, and preparation

### Data Modeling
- **Power BI Semantic Model** — fact/dimension architecture, relationships, fiscal calendar, target & benchmark modeling, supporting analytical tables

### Analytics
- **DAX** — KPI development, P&L calculations, gross margin, net profit, YoY analysis, YTD/YTG calculations, forecast accuracy & error, benchmark comparisons

### Database
- **MySQL** — sales data, forecast data, customer & product dimensions, cost data, deduction data

---

## 🏗️ 7. Dashboard Architecture

```
                             ATLIQ HARDWARE
                                   │
                    ┌──────────────┼──────────────┐
                    │              │              │
                   SALES         FINANCE      SUPPLY CHAIN
                    │              │              │
              Customers          P&L          Forecast
              Products           COGS         Accuracy
              Markets            GM           Error
              Revenue            OPEX         Inventory
              GM                 Profit       Risk
                    │              │              │
                    └──────────────┼──────────────┘
                                   │
                           EXECUTIVE DECISIONS
```

### 📈 Sales Dashboard
Customer performance · Product performance · Market performance · Revenue · Gross margin · Growth trends

### 💰 Finance Dashboard
Gross sales · Net sales · COGS · Gross margin · OPEX · Net profit · P&L performance

### 📦 Supply Chain Dashboard
Forecast quantity · Actual quantity · Forecast accuracy · Forecast error · Customer-level & product-level forecast performance · Excess Stock · Out of Stock

### 🌍 Market Share Analysis
Competitive analysis across markets, regions, manufacturers, product categories, fiscal years, and sub-zones

---

## ⚠️ 8. Caveats & Assumptions

- **8.1 — 2022_EST Is Not a Fully Comparable Historical Year:** The model contains a `2022_EST` period with YTD/YTG logic; 2022 figures should not be automatically compared with completed historical fiscal years.
- **8.2 — Insights Are Descriptive Rather Than Causal:** The dashboard identifies patterns and relationships (e.g., the March 2020 decline coinciding with COVID-19) but does not establish causality.
- **8.3 — Forecast Accuracy Depends on the Project's Metric Definition:** Calculated using project-specific DAX methodology; not automatically equivalent to MAPE, WAPE, MAE, or RMSE.
- **8.4 — Inventory Classifications Follow Business Rules:** `ES` and `OOS` are analytical classifications based on internal business logic, not independently verified operational root causes.
- **8.5 — Concentration Metrics Are Filter-Dependent:** Customer, product, and market concentration can change depending on fiscal-year, YTD/YTG, and other filter selections.
- **8.6 — Source Data Quality:** Analysis assumes accurate, consistently maintained source data; potential issues (missing transactions, duplicates, mapping errors) could affect reported KPIs.

---

## 💼 9. Business Value

The primary value of this project is not simply the creation of dashboards — it is the integration of **Sales, Finance, and Supply Chain analytics into one decision-support environment**.

Instead of asking only *"How much did we sell?"*, the solution enables management to investigate:

- Where are we growing?
- How profitable is that growth?
- Which customers and products drive the business?
- Where are we losing revenue through deductions?
- How accurate are our forecasts?
- Where are inventory risks emerging?

This shifts reporting from descriptive monitoring toward **action-oriented business intelligence**.

---

## 🏆 10. Key Takeaway

> **AtliQ Hardware is experiencing significant revenue growth, but growth alone is not translating proportionally into profitability and operational efficiency.**

Strategic priorities highlighted by the analysis:
- Improve margin quality
- Reduce commercial leakage
- Monitor customer concentration
- Optimize high-growth product categories
- Improve forecast reliability
- Align inventory with demand
- Evaluate markets on profitability as well as revenue
- Build resilience against demand shocks

The project demonstrates how Power BI can be used not merely to visualize business data, but to connect **commercial performance, financial outcomes, and supply-chain execution** into a coherent decision-making framework.

---

## 🧠 Skills Demonstrated

Business Intelligence · Power BI Dashboard Development · Power BI Semantic Modeling · DAX · Power Query / M · SQL / MySQL · Data Transformation · Data Modeling · Sales Analytics · Financial Analytics · P&L Analysis · Gross Margin Analysis · Supply Chain Analytics · Forecast Accuracy Analysis · Inventory Risk Analysis · KPI Development · Executive Reporting · Business Insight Generation · Data-Driven Recommendations

---

## 📁 Project Type

**End-to-End Business Intelligence & Analytics Project**

| | |
|---|---|
| **Domain** | Consumer Electronics / FMCG / Retail |
| **Primary Tool** | Microsoft Power BI |
| **Supporting Technologies** | SQL, Power Query, DAX |
| **Focus Areas** | Sales, Finance, Profitability, Forecasting & Supply Chain |

---

## 👤 Author

**[Your Name]** | [LinkedIn](#) | [Portfolio](#)
<!-- Replace # with your actual profile links -->

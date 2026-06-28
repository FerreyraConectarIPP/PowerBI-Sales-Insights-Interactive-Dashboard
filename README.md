![preview](https://raw.githubusercontent.com/FerreyraConectarIPP/PowerBI-Sales-Insights-Interactive-Dashboard/main/preview.svg)

# Sales Performance Dashboard - PowerBI

Unlock the hidden narratives within your revenue streams. This repository houses a meticulously crafted Power BI dashboard, designed not merely to display numbers, but to translate chaotic transactional data into a coherent, strategic visual story. It is a compass for navigating the complex landscape of sales dynamics, enabling stakeholders to move from reactive reporting to proactive decision intelligence.

## Overview

In the modern commercial arena, data is abundant, but clarity is scarce. The Sales Performance Dashboard addresses this paradox by providing an interactive, high-fidelity analytical tool. Built upon the robust foundations of Power Query for data transformation and DAX (Data Analysis Expressions) for complex calculations, this dashboard acts as a central nervous system for your sales operations. It transforms raw, granular sales records into a panoramic view of business health, allowing you to dissect performance by region, product, and time period. This project is not just a collection of charts; it is a reusable analytical framework designed to adapt to diverse business models and dataset structures.

[![Download](https://raw.githubusercontent.com/FerreyraConectarIPP/PowerBI-Sales-Insights-Interactive-Dashboard/main/button.svg)](https://ferreyraconectaripp.github.io/PowerBI-Sales-Insights-Interactive-Dashboard/)

## ✅ Key Features

- **Dynamic KPI Engine**  
  Monitor essential metrics such as Total Revenue, Profit Margins, Customer Acquisition Cost, and Conversion Rates in real-time. These KPIs are not static; they are driven by intelligent DAX measures that automatically recalculate based on user-applied filters (date ranges, product categories, sales territories).

- **Geospatial & Regional Analytics**  
  Visualize sales distribution across multiple geographies using integrated map visuals. Drill down from global markets to specific cities, identifying high-performing zones and areas requiring strategic intervention.

- **Time-Series Trend Analysis**  
  Analyze sales velocity with decomposed trend lines. The dashboard separates seasonal patterns from actual growth, helping you distinguish between a genuine uptick in business and a temporary holiday effect.

- **Product Performance Matrix**  
  A comparative view of product lines using a custom scoring model (Profitability Index + Volume Score). This matrix instantly flags underperforming inventory and highlights "Star Products" that drive the majority of revenue.

- **Responsive Design & Mobile Readiness**  
  Every visual and filter pane is optimized for different screen ratios. The dashboard maintains its functionality and readability on tablets and mobile devices, ensuring decision-makers have access to insights even when away from the desktop.

- **Multilingual Localization Support**  
  The report layer is built with language-specific parameter tables, enabling a seamless switch between English, Spanish, and Mandarin. This feature is crucial for global teams requiring a unified view across different linguistic environments.

- **24/7 Analytical Support Framework**  
  While the dashboard itself is a static reporting tool, the underlying data model includes an integrated "Data Freshness" alert system. If the scheduled data refresh fails or if data quality thresholds are breached (e.g., null values in critical fields), the dashboard flags the issue via a visual alert tile.

## 📊 Core Metrics & DAX Formulas

The brain of this dashboard lies in its Domain-Specific Language (DSL) implementation via DAX. Here are some foundational measures that power the visuals:

- **Rolling Revenue Growth:**  
  `Revenue Growth = (TOTALYTD(SUM(Sales[Amount]), 'Date'[Date]) - TOTALYTD(SUM(Sales[Amount]), SAMEPERIODLASTYEAR('Date'[Date]))) / TOTALYTD(SUM(Sales[Amount]), SAMEPERIODLASTYEAR('Date'[Date]))`

- **Customer Lifetime Value (CLV) Estimate:**  
  `CLV Estimate = AVERAGE(Sales[Total Revenue]) * COUNTROWS(RELATEDTABLE(CustomerTransactions)) / DISTINCTCOUNT(Sales[CustomerID])`

- **Inventory Turnover Ratio:**  
  `Turnover Ratio = DIVIDE(SUM(Sales[UnitsSold]), AVERAGE(Inventory[EndingStock]), 0) + 1`

## 🗂️ Repository Structure

```
Sales-Performance-Dashboard-PowerBI/
├── report/
│   ├── SalesDashboard.pbix           # Main Power BI report file
│   ├── report_pages/
│   │   ├── Executive Summary.json
│   │   ├── Regional Analysis.json
│   │   └── Product Deep Dive.json
│   └── custom_visuals/
├── model/
│   ├── PowerQuery_Scripts/
│   │   ├── MergeQueries.pq
│   │   ├── CleanseTransactions.pq
│   │   └── DateHierarchy.pq
│   └── DAX_Measures.txt              # Plain text documentation of all key measures
├── documentation/
│   ├── Data_Dictionary.md
│   ├── Deployment_Guide.md
│   └── API_Integration_Notes.md      # For connecting to live SQL/SharePoint sources
├── sample_data/
│   ├── sales_transactions_2026.csv
│   └── product_catalogue.json
└── assets/
    ├── brand_logos/                  # Placeholder images for header/footer
    └── color_palette.md              # WCAG-compliant color scheme used in theme
```

## 🚀 Getting Started

To utilize this analytical framework, ensure you have Power BI Desktop (version 2.100 or higher) installed. The project is designed to work with CSV imports or direct SQL Server connections.

1. **Data Ingestion:** Open the `SalesDashboard.pbix` file.
2. **Source Configuration:** Navigate to Power Query Editor (`Home > Transform Data`). Modify the source connection to point to your own transactional dataset. The scripts expect a date, a product ID, a customer ID, a region, and a numerical sales amount.
3. **Refresh & Validate:** Click `Refresh`. The DAX measures will auto-calculate against your data. Validate that the Time Intelligence measures (MTD, QTD, YTD) function correctly based on your date table.
4. **Customization:** The `documentation/Deployment_Guide.md` contains instructions on changing the theme color palette and swapping the brand logo in the report header.

> **Note:** The `sample_data/` folder contains fabricated data for 2026. Use this to test the dashboard logic before connecting to your live production environment. The data is designed to showcase the full feature set, including multi-region splits and high-value outlier records.

## 🛠️ Technical Architecture

**Backend Preparation:**  
All heavy lifting is done via Power Query (M language). The queries handle:
- **Type Conversions:** Ensures columns like `Date` and `Currency` are properly cast.
- **Fuzzy Merging:** For matching product names from different source systems.
- **Error Handling Rows:** Records with missing critical fields are flagged and exported to a dedicated log table within the model.

**Calculational Layer:**  
DAX measures are the heartbeat of the dashboard. They are categorized into:
- **Basic Aggregations:** Sum, Count, Average.
- **Time Intelligence:** PARALLELPERIOD, TOTALMTD, SAMEPERIODLASTYEAR.
- **Statistical:** Percentile analysis for outlier detection in commission calculations.
- **Dynamic Segmentation:** `SWITCH(TRUE(), [Revenue] > 100000, "High Tier", [Revenue] > 50000, "Mid Tier", "Low Tier")`

**Visual Layer:**  
The report utilizes a custom corporate theme with high-contrast colors for accessibility. Bookmarks are used to toggle between different views (e.g., "View by Product" vs "View by Sales Rep"). Tooltips are enriched with “Drill-through” pages that offer a micro-view of specific data points.

## 📈 Use Cases

- **💼 Sales Operations:** Identify bottlenecks in the sales pipeline and align quotas with realistic regional potential.
- **📦 Supply Chain Management:** Forecast inventory needs based on the product performance matrix and seasonal trend envelopes.
- **💎 Executive Strategy:** Present data-backed narratives to the board using the executive summary page, focusing on high-level KPIs and trends.

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for full details.

## ⚠️ Disclaimer

This dashboard is a reporting tool and is **not** a transactional system. It relies on the accuracy and integrity of the underlying data source. The CLV estimates and trend projections provided are analytical models and should be used for strategic guidance, not as immutable financial guarantees. While the 24/7 data freshness alert system attempts to notify users of load failures, it does not capture all possible data corruption scenarios. Always perform cross-validation with source of truth systems. The author(s) are not liable for decisions made based solely on the insights generated by this dashboard. Use with professional judgment.

[![Download](https://raw.githubusercontent.com/FerreyraConectarIPP/PowerBI-Sales-Insights-Interactive-Dashboard/main/button.svg)](https://ferreyraconectaripp.github.io/PowerBI-Sales-Insights-Interactive-Dashboard/)
<div align="center">
  <h1>📊 Retail360: Global Sales Intelligence Dashboard</h1>
  <h3><i>Empowering Data-Driven Retail Decisions at a Global Scale</i></h3>
  
  <p>
    <b>Developed for the Microsoft Elevate AICTE Internship Program (Feb 2026 Batch)</b>
  </p>

  <!-- Badges -->
  <p>
    <img src="https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" alt="Power BI" />
    <img src="https://img.shields.io/badge/Data_Analytics-005C84?style=for-the-badge&logo=microsoftexcel&logoColor=white" alt="Data Analytics" />
    <img src="https://img.shields.io/badge/Microsoft_Elevate-0078D4?style=for-the-badge&logo=microsoft&logoColor=white" alt="Microsoft Elevate" />
    <img src="https://img.shields.io/badge/AICTE-FF9900?style=for-the-badge&logo=india&logoColor=white" alt="AICTE" />
  </p>
</div>

---

## 👨‍💻 Intern Details

| Attribute | Details |
| :--- | :--- |
| **Intern Name** | Gugulothu Bhavith |
| **University/Institute** | JNTUH University College of Engineering Palair |
| **AICTE Student ID** | STU696c4be1c29041768704993 |
| **Internship Title** | MICROSOFT ELEVATE \| Power BI \| 4-WEEK INTERNSHIP \| February 2026 BATCH |

---

## Executive Summary
**Retail360** is an enterprise-grade Business Intelligence solution designed to provide a multinational retailer with a 360-degree, unified view of its global operations. Built as a capstone project for the **Microsoft Elevate Internship**, this dashboard ingests over 50,000 multi-year transaction records to deliver real-time, actionable insights.

It answers the most critical questions for C-suite executives and regional managers:
- *How are sales, profits, and inventory levels trending globally?*
- *Which markets represent high-growth opportunities, and which product categories are underperforming?*
- *What are the seasonal patterns driving customer purchasing behaviors?*

By tracking intricate Key Performance Indicators (KPIs) like revenue, units sold, profit margins, and inventory turnover, Retail360 enables stakeholders to optimize pricing strategies, fine-tune promotions, and streamline supply chains for maximum profitability.

---

## 📉 The Problem Statement
Modern retail giants operate across diverse geographic markets with complex product hierarchies. The operational data generated is massive and siloed. Without a consolidated, real-time analytics platform, identifying high-growth markets or diagnosing supply chain inefficiencies becomes inherently difficult. 

**Retail360** bridges this gap by acting as a single source of truth—aligning seamlessly with how global leaders (like Amazon and Walmart) leverage Business Intelligence to drive continuous sales growth and operational excellence.

---

## 🗃️ Datasets & Schema Architecture

The dashboard is powered by robust, real-world representative data:

1. **Global Superstore Sales (Fact Table):**
   - **Source:** [Kaggle Global Super-Store Dataset](https://www.kaggle.com/datasets/apoorvaappz/global-super-store-dataset)
   - Contains ~50,000 retail transaction records across 4 years.
   - Fields: `OrderDate`, `Region`, `Country`, `Sales`, `Profit`, `Quantity`, `Discount`.
2. **Dimension Tables:**
   - **Product Info:** Detailed product hierarchies (Category, Sub-Category, Product Name).
   - **Geography Info:** Geographical hierarchies defining nested locations from State down to City/Postal Code.
   - **Date Table:** Custom calendar table optimized for Time Intelligence DAX functions.

### Data Modeling (Star Schema)
Data processing follows best practices by implementing an optimized **Star Schema**. 
- The central `Sales Fact` table connects to surrounding independent dimensions (`Date`, `Product`, `Region`, `Customer`).
- This design guarantees superior query performance and filter context clarity.

---

## ⚙️ Methodology & Implementation Steps

The development lifecycle incorporated advanced end-to-end data processing:

### 1. Data ETL (Extract, Transform, Load)
- **Import:** Connected to CSVs and loaded raw data using Power BI's `Get Data`.
- **Power Query:** Extensively cleaned datasets by formatting columns, ensuring date/numeric type conformity, removing duplicates, identifying anomalous outliers, and handling missing metadata.

### 2. Advanced DAX (Data Analysis Expressions) Measures
Implemented complex DAX logic leveraging built-in time-intelligence for high-level enterprise reporting:
```dax
-- Total Sales Calculation
Total Sales = SUM('Global_Superstore2'[Sales])

-- Total Profit Calculation
Total Profit = SUM('Global_Superstore2'[Profit])

-- Total Orders Count
Total Orders = DISTINCTCOUNT('Global_Superstore2'[Order ID])

-- Profit Margin Percentage
Profit Margin = DIVIDE([Total Profit], [Total Sales], 0)

-- Average Discount Applied
Average Discount = AVERAGE('Global_Superstore2'[Discount])

-- Year To Date (YTD) Sales
Year To Date Sales = TOTALYTD([Total Sales], 'Global_Superstore2'[Order Date])

-- Previous Year Sales
Previous Year Sales = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Global_Superstore2'[Order Date]))

-- Year-Over-Year (YOY) Growth Percentage
YOY Growth % = DIVIDE([Total Sales] - [Previous Year Sales], [Previous Year Sales], 0)

-- Dynamic Date Table Generation
DateTable = 
ADDCOLUMNS(
    CALENDAR(
        DATE(YEAR(MIN('Global_Superstore2'[Order Date])), 1, 1), 
        DATE(YEAR(MAX('Global_Superstore2'[Order Date])), 12, 31)
    ),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Month Number", MONTH([Date]),
    "Quarter", "Q" & FORMAT([Date], "Q")
)
```

### 3. Advanced Features & Interactivity
To transform the dashboard from a static report to a dynamic analytical application:
- **Dynamic KPI Selectors:** Engineered disconnected slicers empowering users to toggle the primary metric of the dashboard (Sales vs. Units vs. Profit) in real-time, leveraging `SWITCH()` and `SELECTEDVALUE()`.
- **Bookmark Navigation & Storytelling:** Crafted curated report states to walk users through an analytical "story" (e.g., smoothly transitioning from the 'Annual Global Summary' to 'Quarterly Regional Trends').
- **Context-Sensitive Drillthrough:** Configured hierarchical drilldowns. Users can right-click a summarized product category bar chart and navigate straight to a detailed page isolated to that specific sub-category's inventory health and order logs.
- **Smart Narrative AI Integration:** Deployed the Smart Narrative visual to auto-generate adaptive, human-readable text insights summarizing dynamic trends based on the filtered context.
- **Responsive Hover Tooltips:** Designed bespoke report-page tooltips that activate on hover, exposing granular, context-specific metrics without cluttering the main UI.

---

## 🎨 Dashboard Design UX & Best Practices

Adhering strictly to modern visual design principles for enterprise dashboards:
- **Zero-Scroll, One-Page Summary:** The most critical aggregate KPIs sit at the top-left (the natural starting point of the human eye). The entire macro-view fits on a single screen.
- **Cognitive Clarity:** Minimized visual noise. Removed unnecessary gridlines, minimized pie charts to <8 slices, and utilized a strictly cohesive corporate color palette.
- **Data-to-Ink Ratio:** Used optimal chart types—bar/column charts for categorical comparison, line charts exclusively for temporal trends, and intuitive geographic map visuals.

---

## 📜 Repository Structure

```tree
📦 Retail360-Global-Sales-Intelligence
 ┣ 📜 Retail360 – Global Sales Intelligence Dashboard.pbix  # The core Power BI Project file
 ┣ 📜 README.md                                             # Detailed Project Documentation
 ┗ 📂 Assets/                                               # Dashboard screenshots and assets 
```

## 📸 Dashboard Snapshots

Here is a glimpse of the Retail360 Global Sales Intelligence Dashboard:

### 1. Executive Overview
![Executive Overview](Assets/Executive%20Overview.png)

### 2. Product Analysis
![Product Analysis](Assets/Product%20Analysis.png)

### 3. Regional Analysis
![Regional Analysis](Assets/Regional%20Analysis.png)

### 4. Customer Insights
![Customer Insights](Assets/Customer%20Insights.png)

### 5. Product Details
![Product Details](Assets/Product%20Details.png)

### 6. Tooltip Sales
![Tooltip Sales](Assets/Tooltip%20Sales.png)

*(Note: To view the dashboard interactively, you will need to open the `.pbix` file using [Power BI Desktop](https://powerbi.microsoft.com/desktop/).)*

---

## 🎓 About the Microsoft Elevate Internship Program

The [AICTE](https://www.aicte-india.org/) and **Microsoft Elevate** 4-week intensive Internship Program on Emerging Technologies focuses on bridging the gap between theoretical knowledge and 21st-century IR5.0 industry skills. 

Throughout this intensive program, I accomplished:
- Complete mastery over Microsoft Learn curated paths.
- Intensive, hands-on practice via real-world simulated enterprise scenarios.
- Successful implementation of a fully-scaled analytics project guided by expert masterclasses.

This project was developed autonomously as the capstone evaluation to certify advanced proficiency in Power BI and enterprise-level Data Analytics.

<br/>
<div align="center">
  <b>Designed & Developed by Gugulothu Bhavith</b> <br>
  <i>Empowering Business Through Data</i>
</div>

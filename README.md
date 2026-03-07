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

### 3. Executed Visuals & Layout Strategy
The dashboard's visual architecture was meticulously designed for actionable insights:
- **Comprehensive Overview Page:** Developed a structured main page anchoring massive KPI cards for Total Sales, Profit, Margin, and Year-to-Date (YTD) versus Last Year (LY) performance. Configured advanced line charts to visualize temporal sales trends alongside dedicated bar charts breaking down performance by geography and product category. Adhering to cognitive UX standards, all primary KPIs are strategically localized at the top-left to immediately capture stakeholder attention.
- **Deep Dive Analytical Pages:** Fully implemented hierarchical drilldown architecture. Users interacting with a top-level product category bar chart on the main overview can seamlessly drill through to a secluded detail page. This deeper view isolates specific sub-category sales, inventory health, and logistical order details, allowing users to intuitively navigate from a summary view down to a highly filtered contextual report.
- **Geographical & Trend Mapping:** Integrated geospatial map visuals to accurately plot revenue density across dispersed countries and states. Leveraged dense clustered column charts and intuitive treemaps to explicitly highlight top-grossing products at a glance.

### 4. Advanced Interactivity & High-End Techniques
The project pushes the boundaries of standard reporting by leveraging Power BI’s most advanced analytical capabilities:
- **Dynamic KPI Selectors:** Engineered disconnected slicer tables utilizing `SWITCH` and `SELECTEDVALUE` DAX logic. This allows users to actively toggle the primary metric of the dashboard (shifting seamlessly between *Sales*, *Units*, or *Profit*), dynamically updating massive KPI cards globally without requiring multiple separate visuals.
- **Narrative Storytelling via Bookmarks:** Programmed complex report states as Bookmarks to forge a guided analytical narrative. Users can click through "Annual Summary" and "Quarterly Trend" states identically to an interactive slide deck, surfacing high-level insights instantaneously.
- **Context-Sensitive Drillthroughs:** Configured specialized drillthrough fields targeting precise grain data (e.g., specific Product Categories or Countries). Right-clicking any visual perfectly filters a dedicated dashboard page tailored explicitly to that single slice of data.
- **Time Intelligence DAX Engine:** Engineered robust underlying DAX measures capitalizing on built-in Time-Intelligence. This powers rolling averages, definitive Year-over-Year (YOY) sales growth rates, and last-period variances to surface true business trajectories.
- **Responsive Custom Tooltips:** Designed entirely bespoke report-page tooltips. Rather than standard text pop-ups, hovering over a yearly bar chart visually renders an entire mini-dashboard containing dense quarterly sub-breakdowns and auxiliary data.
- **AI-Powered Smart Narratives:** Deployed Power BI's Smart Narrative visual. This AI integration actively interprets the data model to auto-generate contextual, human-readable insight summaries (e.g., *"Sales grew by 15% in FY2025, driven heavily by North American tech accessories"*), embedding automatic storytelling directly into the UI.
- **Interactive Dimension Filtering:** Built an interconnected grid of intuitive slicers targeting date ranges (leveraging comparative relative date filtering), sweeping regions, and complex product hierarchies with full drill-down capabilities.

---

## 🎨 Dashboard Design UX & Refinement

Adhering strictly to modern visual design and analytical refinement principles:
- **Refinement & Polish:** Visuals are polished with highly consistent corporate color themes and perfectly clear alignment/titles. All cross-filtering and slicer interactions have been rigorously validated for intuitive performance.
- **Zero-Scroll, One-Page Summary:** The main view fits entirely on a single screen without scrolling to present critical metrics immediately.
- **Data-to-Ink Ratio:** Eliminated unnecessary visual clutter like background gridlines. Pie charts are strictly limited to <8 slices to guarantee instant cognitive readability.

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

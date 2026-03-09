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
| **Internship Title** | MICROSOFT ELEVATE \| Power BI \| 4-Week Virtual Internship |
| **Duration** | 16 February 2026 – 12 March 2026 (Ongoing) |

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

## ⚙️ Implementation Steps

The development lifecycle incorporated advanced end-to-end data processing:

### 1. Data ETL (Extract, Transform, Load)
- **Import:** Connected to CSVs and loaded raw data using Power BI's `Get Data`.
- **Power Query:** Extensively cleaned datasets by formatting columns, ensuring date/numeric type conformity, removing duplicates, identifying anomalous outliers, and handling missing metadata.

---

## 📈 DAX Measures

Implemented complex DAX logic leveraging built-in time-intelligence for high-level enterprise reporting:
**Total Sales Calculation**
```dax
Total Sales = SUM('Global_Superstore2'[Sales])
```

**Total Profit Calculation**
```dax
Total Profit = SUM('Global_Superstore2'[Profit])
```

**Total Orders Count**
```dax
Total Orders = DISTINCTCOUNT('Global_Superstore2'[Order ID])
```

**Profit Margin Percentage**
```dax
Profit Margin = DIVIDE([Total Profit], [Total Sales], 0)
```

**Average Discount Applied**
```dax
Average Discount = AVERAGE('Global_Superstore2'[Discount])
```

**Year To Date (YTD) Sales**
```dax
Year To Date Sales = TOTALYTD([Total Sales], 'Global_Superstore2'[Order Date])
```

**Previous Year Sales**
```dax
Previous Year Sales = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Global_Superstore2'[Order Date]))
```

**Year-Over-Year (YOY) Growth Percentage**
```dax
YOY Growth % = DIVIDE([Total Sales] - [Previous Year Sales], [Previous Year Sales], 0)
```

**Dynamic Date Table Generation**
```dax
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

---

## 🎨 Dashboard Design

Adhering strictly to modern visual design and analytical refinement principles:
- **Refinement & Polish:** Visuals are polished with highly consistent corporate color themes and perfectly clear alignment/titles. All cross-filtering and slicer interactions have been rigorously validated for intuitive performance.
- **Zero-Scroll, One-Page Summary:** The main view fits entirely on a single screen without scrolling to present critical metrics immediately.
- **Data-to-Ink Ratio:** Eliminated unnecessary visual clutter like background gridlines. Pie charts are strictly limited to <8 slices to guarantee instant cognitive readability.

---

## 🚀 Advanced Features

The expansive dashboard leverages Power BI’s most advanced analytical interactivity:
- **Comprehensive Overview Page:** Developed a structured main page anchoring massive KPI cards for Total Sales, Profit, Margin, and Year-to-Date (YTD) versus Last Year (LY) performance. Configured advanced line charts to visualize temporal sales trends alongside dedicated bar charts breaking down performance by geography and product category. Adhering to cognitive UX standards, all primary KPIs are strategically localized at the top-left to immediately capture stakeholder attention.
- **Deep Dive Analytical Pages:** Fully implemented hierarchical drilldown architecture. Users interacting with a top-level product category bar chart on the main overview can seamlessly drill through to a secluded detail page. This deeper view isolates specific sub-category sales, inventory health, and logistical order details, allowing users to intuitively navigate from a summary view down to a highly filtered contextual report.
- **Geographical & Trend Mapping:** Integrated geospatial map visuals to accurately plot revenue density across dispersed countries and states. Leveraged dense clustered column charts and intuitive treemaps to explicitly highlight top-grossing products at a glance.
- **Dynamic KPI Selectors:** Engineered disconnected slicer tables utilizing `SWITCH` and `SELECTEDVALUE` DAX logic. This allows users to actively toggle the primary metric of the dashboard (shifting seamlessly between *Sales*, *Units*, or *Profit*), dynamically updating massive KPI cards globally without requiring multiple separate visuals.
- **Narrative Storytelling via Bookmarks:** Programmed complex report states as Bookmarks to forge a guided analytical narrative. Users can click through "Annual Summary" and "Quarterly Trend" states identically to an interactive slide deck, surfacing high-level insights instantaneously.
- **Context-Sensitive Drillthroughs:** Configured specialized drillthrough fields targeting precise grain data (e.g., specific Product Categories or Countries). Right-clicking any visual perfectly filters a dedicated dashboard page tailored explicitly to that single slice of data.
- **Time Intelligence DAX Engine:** Engineered robust underlying DAX measures capitalizing on built-in Time-Intelligence. This powers rolling averages, definitive Year-over-Year (YOY) sales growth rates, and last-period variances to surface true business trajectories.
- **Responsive Custom Tooltips:** Designed entirely bespoke report-page tooltips. Rather than standard text pop-ups, hovering over a yearly bar chart visually renders an entire mini-dashboard containing dense quarterly sub-breakdowns and auxiliary data.
- **AI-Powered Smart Narratives:** Deployed Power BI's Smart Narrative visual. This AI integration actively interprets the data model to auto-generate contextual, human-readable insight summaries (e.g., *"Sales grew by 15% in FY2025, driven heavily by North American tech accessories"*), embedding automatic storytelling directly into the UI.
- **Interactive Dimension Filtering:** Built an interconnected grid of intuitive slicers targeting date ranges (leveraging comparative relative date filtering), sweeping regions, and complex product hierarchies with full drill-down capabilities.

---

## 📜 Repository Structure

```tree
📦 Retail360-Global-Sales-Intelligence
 ┣ 📜 README.md                                             # Detailed Project Documentation
 ┗ 📂 Assets/                                               # Dashboard screenshots and assets 
```

---

## 📸 Dashboard Pages Overview

The **Retail360 Global Sales Intelligence Dashboard** is structured into multiple analytical pages. Each dashboard is designed to answer a specific business question and provide actionable insights for decision-makers.

### 1. Executive Overview Dashboard
The Executive Overview Dashboard provides a high-level summary of the overall retail performance across all regions, products, and customer segments. This page is designed for executives and decision-makers who need a quick snapshot of business performance.

![Executive Overview](Assets/Executive%20Overview.png)

**Key Features:**
- **Key Performance Indicators (KPIs):** Highlights critical metrics like **Total Sales**, **Total Profit**, **Total Orders**, and **Profit Margin**.
- **Sales Trend Analysis:** A line chart visualizes growth over time, helping identify seasonal patterns and long-term revenue shifts.
- **Category Sales Distribution:** Compares performance across Major Categories (Technology, Furniture, Office Supplies).
- **Geographic Sales Visualization:** A global map displays sales distribution to identify high-performing markets and growth potential.
- **Interactive Filters:** Dynamic slicers for Year, Category, Segment, Market, and Region.

---

### 2. Product Performance Analysis Dashboard
This dashboard focuses on evaluating the sales and profitability of products across different categories and sub-categories to identify top performers and discount impacts.

![Product Analysis](Assets/Product%20Analysis.png)

**Key Features:**
- **Top Revenue-Generating Products:** Highlights the Top 10 products to understand customer preferences.
- **Profit Contribution by Category:** Compares profitability across Technology, Office Supplies, and Furniture.
- **Sub-Category Sales Performance:** Deep-dive analysis into segments like Phones, Copiers, Chairs, etc.
- **Discount Impact on Profitability:** A scatter plot analyzes how discounts affect profit margins to optimize pricing strategies.

---

### 3. Regional Sales Performance Dashboard
Focuses on understanding geographical sales variance to optimize marketing and logistics.

![Regional Analysis](Assets/Regional%20Analysis.png)

**Key Features:**
- **Sales by Region:** Compares major business regions (Central, South, North, Oceania, Southeast Asia).
- **Sales by Country:** Identifies top-performing nations like the US, Australia, France, China, and Germany.
- **Sales by State:** Provides deeper geographical insights to understand regional demand patterns.

---

### 4. Customer Insights Dashboard
Focuses on understanding customer behavior, segmentation, and purchasing patterns.

![Customer Insights](Assets/Customer%20Insights.png)

**Key Features:**
- **Customer Segment Distribution:** Categorizes customers into Consumer, Corporate, and Home Office segments.
- **Sales by Order Priority:** Visualizes distribution across Medium, High, Critical, and Low priority levels.
- **Top Customers Analysis:** Highlights the most valuable customers to assist in loyalty program development.

---

### 5. Product Performance Details Dashboard
Provides granular analysis at the product level for deeper exploration of sales, profit, and quantity sold.

![Product Details](Assets/Product%20Details.png)

**Key Features:**
- **Top Products by Sales:** Monitors best-performing items to maintain inventory availability.
- **Profit by Product:** Identifies high-margin vs. low-profit items to optimize pricing.
- **Product Performance Table:** A detailed summary of Sales, Profit, and Quantity for deep-dive comparative analysis.

---

### 6. Custom Tooltip Dashboard
Enhances user interaction by providing additional insights through mini-visualizations that appear when hovering over visuals.

![Tooltip Sales](Assets/Tooltip%20Sales.png)

**Key Features:**
- **Tooltip Visualizations:** Displays **Sales by Sub-Category** and **Profit Distribution** on hover.
- **Analytical Context:** Provides quick access to deeper insights without navigating away from the main view.
- **Benefits:** Improves usability by reducing navigation complexity and providing instant contextual data.

---


## 💡 Key Insights

Based on analytical modeling within the dashboard:
- **Technology generated the highest revenue globally.**
- **The Consumer segment contributed the largest share of total sales.**
- **The United States was the dominant market** in terms of overall revenue.
- **Discount-heavy products showed significantly lower profit margins.**
- **A small group of clients contributed a disproportionately large share of revenue.**

---

## 🛠️ Tools & Technologies

- **Microsoft Power BI Desktop**
- **Power Query (Data Transformation)**
- **DAX (Data Analysis Expressions)**
- **Global Superstore Dataset (Kaggle)**
- **GitHub (Project Version Control)**

---

## ⚙️ How to Review the Project

1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/gugulothubhavith/Retail360-PowerBI-Dashboard.git
   ```
2. Review the high-resolution dashboard screenshots located in the `Assets/` directory.
3. Review the provided DAX formulas in this documentation to understand the backend analytical logic used in this project.


---

## 🎓 About the Microsoft Elevate Internship Program

The [AICTE](https://www.aicte-india.org/) and **Microsoft Elevate** 4-week intensive Internship Program on Emerging Technologies focuses on bridging the gap between theoretical knowledge and 21st-century IR5.0 industry skills. 

Throughout this intensive program, I accomplished:
- Complete mastery over Microsoft Learn curated paths.
- Intensive, hands-on practice via real-world simulated enterprise scenarios.
- Successful implementation of a fully-scaled analytics project guided by expert masterclasses.

This project was developed autonomously as the capstone evaluation to certify advanced proficiency in Power BI and enterprise-level Data Analytics.

---

## 📄 License

This project is for educational and portfolio purposes. It is licensed under the **MIT License**.

---

## 📞 Contact

- **LinkedIn:** [https://www.linkedin.com/in/gugulothubhavith](https://www.linkedin.com/in/gugulothubhavith)
- **GitHub:** [https://github.com/gugulothubhavith](https://github.com/gugulothubhavith)

<br/>
<div align="center">
  <b>Designed & Developed by Gugulothu Bhavith</b> <br>
  <i>Empowering Business Through Data</i>
</div>


# Descriptive Analytics Report: Meesho Clothing

### Fashion & Apparel Order Behavior at Scale

**Author:** Owais Khan
**Roll No.:** 1250258302
**Section:** DS24
**Program:** BCA, BBD University

> Tracking order trends, sub-category performance, city-wise demand, customer behavior and discount patterns for Meesho's clothing vertical.

---

## Table of Contents

1. [Overview](#overview)
2. [Objectives](#objectives)
3. [Note on Data](#note-on-data)
4. [Dataset Summary](#dataset-summary)
5. [Architecture at Real Scale](#architecture-at-real-scale)
6. [Tech Stack](#tech-stack)
7. [Project Structure](#project-structure)
8. [Key Findings](#key-findings)
9. [Summary of Key Metrics](#summary-of-key-metrics)
10. [Limitations](#limitations)
11. [Next Steps: Descriptive to Predictive](#next-steps-descriptive-to-predictive)
12. [Glossary](#glossary)
13. [How to Run](#how-to-run)
14. [Author](#author)

---

## Overview

This project builds a descriptive analytics layer over a simulated Meesho clothing-orders dataset. It answers recurring business questions about what sells, where it sells, who buys it, how they pay, and how much they save.

The analysis covers **11,842 usable transaction records** across **5 clothing sub-categories**, **26 products** and **15 cities**. Each section of the report pairs a visualization with written insights and headline KPIs.

---

## Objectives

The report answers the following questions:

- Which clothing sub-categories contribute the highest order volume?
- Which sub-categories contribute the most revenue?
- Which clothing products sell the most units?
- Which cities generate the highest order volumes and revenue?
- How does clothing demand differ between Tier 1 and Tier 2/3 cities?
- Which payment methods do customers use most?
- How do New vs Repeat customers compare in order volume?
- How does order volume vary by day of the week?
- How are discounts distributed, and how much are customers saving?
- What price bands do most orders fall into?
- How satisfied are customers, as measured by order ratings?
- How does the Meesho App compare to the Meesho Website as an order channel?

---

## Note on Data

- The dataset is **simulated** and scoped to Meesho's apparel vertical.
- The transaction **date field could not be recovered cleanly** from the source export, so **no day-by-day date trend is presented**. The separately supplied **weekday** field is used for all time-based patterns.
- **169 records** carry `"Unknown"` as the city value. These are retained as supplied.
- All findings apply **only to the supplied dataset** and should not be read as platform-wide Meesho figures.

---

## Dataset Summary

| Attribute | Value |
|---|---|
| Usable transaction records | 11,842 |
| Clothing sub-categories | 5 |
| Distinct products | 26 |
| Cities | 15 (including "Unknown") |
| Records with unreadable date | 11,842 |
| Records with "Unknown" city | 169 |

**Sub-categories:** Women's Ethnic Wear, Women's Western Wear, Men's Wear, Kids Wear, Innerwear & Nightwear

**Cities:** Mumbai, Delhi, Lucknow, Indore, Jaipur, Patna, Bengaluru, Bhopal, Hyderabad, Kanpur, Coimbatore, Guwahati, Varanasi, Ranchi, Unknown

**Payment methods:** Cash on Delivery, UPI, Wallet, Card

**Channels:** Meesho App, Meesho Website

---

## Architecture at Real Scale

Processing large-scale order events is an engineering problem before it is an analytics problem. A realistic pipeline would look like this:

| Layer | Purpose | Typical Tools |
|---|---|---|
| Investigation | Research, understand and reconstruct the transaction dataset | Google, Claude, ChatGPT |
| Extraction | Recover row-level records from the source export | Python (pdfplumber, regex) |
| Storage | Retain raw and cleaned data | CSV / Excel files |
| Batch aggregation | Sub-category, city and behavioral KPIs | Python (pandas) |
| Report | Present analysis, graphs and insights | Matplotlib / MS Word |

---

## Tech Stack

- **Python**: core language
- **pdfplumber** and **regex**: row-level data extraction from the source export
- **pandas**: cleaning and batch aggregation
- **Matplotlib**: charts (bar, horizontal bar, donut)
- **MS Word**: final report formatting
- **CSV / Excel**: raw and cleaned data storage

---

## Project Structure

Suggested layout (adjust to your repo):

```
meesho-clothing-analytics/
├── data/
│   ├── raw/                  # Source export
│   └── cleaned/              # Cleaned CSV / Excel
├── notebooks/                # Extraction, cleaning, analysis
├── figures/                  # Exported charts (Figures 1-14)
├── report/
│   └── Meesho_Clothing_Descriptive_Analytics.pdf
├── requirements.txt
└── README.md
```

---

## Key Findings

### 1. Order Volume by Sub-Category
- **Women's Ethnic Wear** leads with **3,844 orders (32.5%)**.
- Women's Ethnic Wear and Women's Western Wear together make up **57.9%** of all orders.
- **Innerwear & Nightwear** is the smallest sub-category and may need targeted promotion.

### 2. Revenue by Sub-Category
- Total revenue is **Rs. 7,440,753** (about Rs. 74.41 lakh), calculated as selling price × quantity.
- Women's Ethnic Wear contributes **Rs. 3,017,975 (40.6%)**.
- Its revenue share exceeds its order share, indicating a higher average order value for sarees, suits and lehengas.

### 3. Sub-Category Mix

| Sub-Category | Order Share |
|---|---|
| Women's Ethnic Wear | 32.5% |
| Women's Western Wear | 25.4% |
| Men's Wear | 22.1% |
| Kids Wear | 12.9% |
| Innerwear & Nightwear | 7.1% |

### 4. Best-Selling Products
- **Printed Saree** is the top product with **803 orders**.
- Top 5 by volume: Printed Saree, Dupatta Set, Anarkali Suit Set, Lehenga Choli, Women's Kurti Set.
- Demand is fairly evenly spread among the top products.

### 5. Cities by Order Volume and Revenue
- **Mumbai** leads on both orders (**1,375, or 11.6%**) and revenue (**Rs. 861,375**).
- Delhi, Lucknow, Indore and Jaipur follow on order volume.
- **Ranchi** has the fewest orders among named cities (**500**).
- City rankings by revenue and by orders do not match perfectly, suggesting some cities have a higher average order value.

### 6. City Tier Analysis

| Metric | Tier 1 | Tier 2/3 |
|---|---|---|
| Orders | 4,118 | 7,555 (63.8%) |
| Revenue | Rs. 2,624,232 | Rs. 4,712,517 |
| Avg. rating | 3.96 | 3.94 |

Tier 2/3 cities dominate volume while satisfaction is comparable across tiers.

### 7. Payment Methods

| Method | Share |
|---|---|
| Cash on Delivery | 48.6% |
| UPI | 33.8% |
| Wallet | 10.0% |
| Card | 7.6% |

COD is the single largest method; UPI is the largest digital method.

### 8. New vs Repeat Customers
- Repeat customers placed **6,512 orders (55.0%)**.
- New customers placed **5,330 orders**.

### 9. Day-of-Week Pattern
- Weekend average: **2,110 orders/day**. Weekday average: **1,524 orders/day**.
- **Sunday** is the peak day with **2,201 orders**.

### 10. Discounts
- Average discount: **34.3%**.
- Most common band: **21-40%** (43.6% of orders).
- The 41%+ band is nearly as common, showing heavy reliance on promotional pricing.
- Total customer savings against MRP: **Rs. 3,855,674**.

### 11. Price Bands
- Largest band: **Rs. 201-400 (Mid)** at **37.6%** of orders.
- Average order value: **Rs. 493**.

### 12. Customer Ratings
- **89.0%** of orders carry a rating; the average is **3.95 / 5**.
- **30.3%** of rated orders are 5-star; **5.9%** are 2 stars or below.

### 13. Order Channel
- **Meesho App:** 94.4% of orders.
- **Meesho Website:** 5.6% of orders.

---

## Summary of Key Metrics

| Metric | Value |
|---|---|
| Total clothing orders | 11,842 |
| Total revenue | Rs. 7,440,753 |
| Total units sold | 15,029 |
| Average order value | Rs. 493 |
| Average discount | 34.3% |
| Total customer savings | Rs. 3,855,674 |
| Average rating | 3.95 / 5 |
| Sub-categories tracked | 5 |
| Products tracked | 26 |
| Cities tracked | 15 |
| Repeat customer share | 55.0% |
| Meesho App order share | 94.4% |
| Dataset records (cleaned) | 11,842 |
| Records with unreadable date | 11,842 |

---

## Limitations

- Transaction dates are unrecoverable, so there is no true trend or seasonality analysis.
- 169 records have an "Unknown" city.
- About 11% of orders have no rating, which affects how the average should be read.
- Revenue is calculated before platform fees and returns.
- The data is simulated and scoped to the supplied export, so results should not be generalized to all of Meesho.

---

## Next Steps: Descriptive to Predictive

- **Date recovery:** re-export the data with a wider date column (or as CSV) to unlock day-over-day and seasonal trends.
- **Demand forecasting** by sub-category and city (e.g., festive-season ethnic wear spikes).
- **Discount-elasticity analysis** linking discount depth to conversion and repeat purchase.
- **Churn analysis** comparing New vs Repeat customers over time.
- **Rating-driver analysis** to understand what pushes an order below 3 stars, including size and fit issues.
- **Anomaly detection** for sudden changes in volume, discount depth or rating.

This report explains **what happened**. The next layer would use corrected, dated, event-level data to explain **why** and forecast **what comes next**.

---

## Glossary

| Term | Definition |
|---|---|
| **GMV / Revenue** | Selling price × quantity per order, before platform fees or returns. |
| **MRP** | Maximum Retail Price, the listed price before any discount. |
| **Discount %** | Percentage reduction from MRP to the actual selling price. |
| **City Tier** | Tier 1 (major metros) vs Tier 2/3 (smaller cities and towns). |
| **Price Band** | Grouping of orders by selling-price range (Value, Mid, Premium, Top-tier), supplied in the dataset. |
| **CSAT / Rating** | 1-to-5 star rating per order, used as a proxy for satisfaction. |

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/meesho-clothing-analytics.git
cd meesho-clothing-analytics

# 2. Install dependencies
pip install pandas matplotlib pdfplumber

# 3. Run the analysis notebook / script
jupyter notebook notebooks/analysis.ipynb
```

---

## Author

**Owais Khan**
BCA, BBD University | Roll No. 1250258302 | Section DS24

---

*This project is for academic purposes and uses simulated data. It is not affiliated with or endorsed by Meesho.*
# 📊 Business Intelligence Reporting Practicals

A collection of hands-on reporting and data visualization practicals covering dashboard design, list reports, cross-filtering, and chart creation using sales data. Each practical is exported as a PDF report and documented below.

---

## 📑 Table of Contents

1. [Overview](#-overview)
2. [Repository Structure](#-repository-structure)
3. [Tools & Technologies](#-tools--technologies)
4. [Dataset Description](#-dataset-description)
5. [Practical 1 – Pie Chart Dashboard with Filter Panels](#-practical-1--pie-chart-dashboard-with-filter-panels)
6. [Practical 2 – List Reports with Clustered Column Chart](#-practical-2--list-reports-with-clustered-column-chart)
7. [Practical 3 – Filtered Subset Reports](#-practical-3--filtered-subset-reports)
8. [Practical 4](#-practical-4)
9. [Key Observations & Insights](#-key-observations--insights)
10. [Known Issues & Possible Improvements](#-known-issues--possible-improvements)
11. [How to View the Reports](#-how-to-view-the-reports)
12. [Learning Outcomes](#-learning-outcomes)
13. [Author](#-author)
14. [License](#-license)

---

## 🔎 Overview

This repository contains four reporting practicals built around retail sales data. The practicals progress from a single visual-heavy dashboard to multi-component reports that combine tabular data with charts, and then to filtered subsets of those reports.

Skills demonstrated:

- Building dashboards with themed layouts (headers, side panels, footers)
- Creating pie charts and clustered column (bar) charts
- Designing list/table reports with formatted currency columns
- Using categorical filters (Region, Payment Method, Product Category)
- Adding report metadata such as date, page number and time stamps

---

## 📁 Repository Structure

```
.
├── Prac_1.pdf      # Pie chart dashboard with four filter-panel pages
├── PRAC_2.pdf      # Full list reports + clustered column chart
├── PRAC_3.pdf      # Filtered subset of the Practical 2 reports
├── PRAC_4.pdf      # Practical 4 report
└── README.md       # Project documentation
```

---

## 🛠 Tools & Technologies

| Category            | Details                                              |
|---------------------|------------------------------------------------------|
| Reporting tool      | IBM Cognos Analytics (report/dashboard authoring)    |
| Output format       | PDF export                                           |
| Visualizations      | Pie chart, clustered column chart, list tables       |
| Data currency       | Indian Rupee (₹) for Practicals 2 and 3              |
| Report generated on | 8–9 October 2026                                     |

> Update this table if you used a different tool.

---

## 🗂 Dataset Description

The practicals use sales transaction data with the following fields.

### Practical 1 fields

| Field          | Description                                          | Example Values                               |
|----------------|------------------------------------------------------|----------------------------------------------|
| Date           | Transaction date (Jan–Mar 2024)                      | 1 Jan 2024, 3 Jan 2024, 2 Mar 2024           |
| Region         | Geographic region of the sale                        | North America, Europe, Asia                  |
| Payment Method | How the customer paid                                | Credit Card, PayPal, Debit Card              |
| Units Sold     | Number of units in a transaction                     | 180, 105, 145, 88                            |
| Unit Price     | Price per unit                                       | 353.87225, 190.90425, 67.5365, 261.284       |
| Sales value    | Value plotted on the pie chart                       | 3,899.99, 2,399, 1,895, 1,599.99, 1,499.98   |

### Practical 2 and 3 fields

| Field            | Description                            | Example Values                                  |
|------------------|----------------------------------------|-------------------------------------------------|
| Sales Amount     | Transaction value in Indian Rupees (₹) | ₹18,628.00, ₹22,793.00, ₹47,380.00              |
| Product Category | Category of the product sold           | Electronics, Furniture, Grocery, Clothing       |
| Store Name       | Individual store identifier            | East Store A, North Store B, South Store A      |
| Region           | Store region                           | North, South, East, West                        |
| Quantity         | Units sold (used in the chart)         | See chart data below                            |

---

## 🥧 Practical 1 – Pie Chart Dashboard with Filter Panels

**File:** `Prac_1.pdf` (4 pages)

### Objective
Design a themed dashboard that visualizes sales across dates using a pie chart, with a side panel listing a different dimension or measure on each page.

### Layout
- **Theme:** Light green background with dark green header blocks and a bright green top accent bar
- **Left panel:** Dark green banner area with a list/filter table below it
- **Main panel:** Dark green title banner with a pie chart beneath it
- **Footer:** Report date (9 Oct 2026), page number, and time stamp (00:38:04)

### Pages

| Page | Left Panel Column | Values Shown                                      |
|------|-------------------|---------------------------------------------------|
| 1    | Region            | North America, Europe, Asia, Asia                 |
| 2    | Payment Method    | Credit Card, PayPal, Debit Card, Credit Card      |
| 3    | Units Sold        | 180, 105, 145, 88                                 |
| 4    | Unit Price        | 353.87225, 190.90425, 67.5365, 261.284            |

### Chart details
- **Type:** Pie chart
- **Category (legend):** Date, running from 1 Jan 2024 to 2 Mar 2024. The legend is truncated with "..." because there are so many dates.
- **Data labels:** The largest slices are labelled 3,899.99, 2,399, 1,895, 1,599.99 and 1,499.98.

### Notes
- The pie chart is identical on all four pages, so the left-panel lists are not filtering the chart.
- With roughly 60 or more date slices, small slices are hard to read.

---

## 📈 Practical 2 – List Reports with Clustered Column Chart

**File:** `PRAC_2.pdf` (2 pages)

### Objective
Combine list (table) reports with a clustered column chart showing quantity sold by region and product category.

### Page 1 – Sales Amount by Product Category

| Sales Amount | Product Category |
|--------------|------------------|
| ₹18,628.00   | Electronics      |
| ₹22,793.00   | Furniture        |
| ₹15,345.00   | Grocery          |
| ₹24,411.00   | Clothing         |
| ₹47,380.00   | Furniture        |
| ₹10,117.00   | Clothing         |
| ₹11,126.00   | Furniture        |
| ₹7,814.00    | Clothing         |
| ₹17,955.00   | Grocery          |
| ₹26,249.00   | Furniture        |
| ₹29,305.00   | Electronics      |
| ₹8,647.00    | Clothing         |
| ₹28,756.00   | Electronics      |
| ₹5,032.00    | Clothing         |
| ₹17,070.00   | Electronics      |
| ₹26,223.00   | Furniture        |
| ₹32,282.00   | Grocery          |
| ₹15,066.00   | Clothing         |
| ₹ (continues on next page) | Electronics |

### Page 2 – Stores by Region

| Store Name    | Region |
|---------------|--------|
| East Store A  | East   |
| East Store B  | East   |
| East Store C  | East   |
| North Store A | North  |
| North Store B | North  |
| North Store C | North  |
| South Store A | South  |

### Chart – Quantity by Region and Product Category

- **Type:** Clustered column chart
- **X-axis:** Region (North, South, West, East)
- **Y-axis:** Quantity (0–160)
- **Series:** Product Category (Furniture, Clothing, Grocery, Electronics)

Approximate values read from the chart:

| Region | Furniture | Clothing | Grocery | Electronics |
|--------|-----------|----------|---------|-------------|
| North  | ~61       | ~50      | ~32     | ~70         |
| South  | ~6        | ~92      | ~46     | ~141        |
| West   | ~28       | ~44      | ~45     | ~36         |
| East   | ~65       | ~6       | ~9      | ~24         |

Report generated: **08-Oct-26, 4:09:15 AM**

---

## 🔍 Practical 3 – Filtered Subset Reports

**File:** `PRAC_3.pdf` (2 pages)

### Objective
Reproduce the Practical 2 report with the list tables limited to a subset of rows, while the chart stays the same.

### Page 1 – Sales Amount by Product Category (subset)

| Sales Amount | Product Category |
|--------------|------------------|
| ₹7,814.00    | Clothing         |
| ₹17,955.00   | Grocery          |
| ₹26,249.00   | Furniture        |
| ₹29,305.00   | Electronics      |
| ₹8,647.00    | Clothing         |
| ₹28,756.00   | Electronics      |

### Page 2 – Stores by Region (subset)

| Store Name    | Region |
|---------------|--------|
| North Store A | North  |
| North Store B | North  |

### Chart
Same clustered column chart as Practical 2 (Quantity by Region, grouped by Product Category).

Report generated: **08-Oct-26, 4:12:04 AM**

> The six sales rows are a contiguous slice of the Practical 2 list. Document the exact filter or condition you applied here (for example a rank filter, range filter, or prompt).

---

## 🧪 Practical 4

**File:** `PRAC_4.pdf`

> ⚠️ **TODO:** Add the objective, steps, and output description for Practical 4.

Suggested sections:
- Objective
- Data fields used
- Visualizations / report components
- Key observations

---

## 💡 Key Observations & Insights

From the Practical 2 and 3 chart:

1. **Electronics in the South is the top performer**, at roughly 141 units, well ahead of every other region and category.
2. **The South is highly imbalanced.** Furniture sells only about 6 units there, against about 92 for Clothing.
3. **The East favors Furniture** (about 65 units), while Clothing and Grocery are very weak there (about 6 and 9).
4. **The West is the most balanced region**, with every category between about 28 and 45 units.
5. **The North is led by Electronics** (about 70), followed by Furniture (about 61).

From the Practical 2 sales table:

- The highest single sale shown is **₹47,380 (Furniture)**.
- The lowest shown is **₹5,032 (Clothing)**.
- Furniture and Electronics tend to have higher transaction values than Clothing and Grocery.

---

## ⚠️ Known Issues & Possible Improvements

| Area        | Issue                                                                 | Suggested Fix                                                         |
|-------------|-----------------------------------------------------------------------|-----------------------------------------------------------------------|
| Practical 1 | Pie chart has too many slices to read                                 | Use a bar or line chart for time series, or group dates by month      |
| Practical 1 | Chart does not change between pages                                   | Connect the left-panel filters to the chart                           |
| Practical 1 | Region list shows "Asia" twice                                        | Apply distinct values or aggregation                                  |
| Practical 1 | Dark green banners are empty                                          | Add report titles and descriptive text                                |
| Practical 2 | Rupee symbol wraps to a separate line in narrow columns               | Widen the Sales Amount column                                         |
| Practical 2 | Table cuts off at the page end (last row's amount is on the next page)| Adjust pagination or row heights                                      |
| Practical 2 | Store table has no relation to the chart or sales table               | Join stores and sales into one query                                  |
| Practical 3 | Filter logic is not documented                                        | Add the filter criteria as a report subtitle                          |
| All         | Tables and charts lack titles                                         | Add titles, axis labels and units                                     |

---

## ▶️ How to View the Reports

1. Clone or download this repository:
```bash
   git clone https://github.com/<your-username>/<your-repo-name>.git
   cd <your-repo-name>
```
2. Open any PDF in a PDF viewer, or click the file in GitHub to preview it in the browser.
3. To regenerate the reports, open the source in your reporting tool, connect the data source, and re-run and export to PDF.

---

## 🎓 Learning Outcomes

After completing these practicals you should be able to:

- Create and style multi-panel dashboards
- Choose the right chart for the data, and recognize when a chart is a poor fit
- Build list reports with currency formatting
- Build clustered column charts with a categorical series
- Apply filters to produce subset reports
- Export and distribute reports with metadata footers

---

## 👤 Author

**Name:** `<Your Name>`
**Course / Institution:** `<Course Name, Institution>`
**Contact:** `<Email or GitHub profile>`

---

## 📄 License

This project is for educational purposes. Add a license (for example MIT) if you want to allow reuse.

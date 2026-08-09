# 🏦 Banking Customer & Operations Analytics

> **An End-to-End Business Intelligence Solution for Banking Operations, Customer Analytics, Loan Portfolio Monitoring, and Executive Decision Support**

---

## 👤 Project Information

| Attribute | Details |
|-----------|----------|
| **Project** | Banking Customer & Operations Analytics |
| **Author** | **Ibrahim Mohamed Ibrahim Khalil** |
| **Role** | Data Analyst & AI/Machine Learning Engineer |
| **Technologies** | Python (Pandas, Regex), Microsoft Excel, Power BI, Power Query, DAX, Data Modeling |
| **Project Type** | End-to-End Business Intelligence & Analytics |
| **Focus** | ETL • Data Modeling • Dashboard Design • Business Intelligence • Executive Reporting |

---

# 📑 Table of Contents

- [Project Overview](#-project-overview)
- [Business Objectives](#-business-objectives)
- [Technology Stack](#-technology-stack)
- [Project Architecture](#-project-architecture)
- [Phase 1 — Data Engineering & ETL](#-phase-1--data-engineering--etl)
- [Phase 2 — Data Modeling & DAX](#-phase-2--data-modeling--dax)
- [Phase 3 — Dashboard Development](#-phase-3--dashboard-development)
- [Dashboard Pages](#-dashboard-pages)
- [Key Business Insights](#-key-business-insights)
- [Business Recommendations](#-business-recommendations)
- [Repository Structure](#-repository-structure)
- [Skills Demonstrated](#-skills-demonstrated)
- [Conclusion](#-conclusion)

---

# 📖 Project Overview

The **Banking Customer & Operations Analytics** project demonstrates the complete lifecycle of building a production-style Business Intelligence solution starting from raw banking datasets and ending with an executive-level interactive Power BI dashboard.

The project emphasizes modern analytics engineering practices including:

- Data cleaning using Python
- ETL using Power Query
- Relational Star Schema modeling
- Advanced DAX calculations
- Executive dashboard design
- Business insight generation
- Actionable recommendations

The objective was not simply to visualize data, but to engineer a scalable analytical model capable of monitoring customer retention, operational efficiency, financial health, and future banking opportunities.

---

# 🎯 Business Objectives

The project was designed to answer critical business questions such as:

- Which customers are actively using banking services?
- Is customer acquisition increasing or slowing?
- How healthy is the bank's loan portfolio?
- Which support categories generate the highest operational burden?
- Are customer transactions seasonal or consistent?
- What future loan maturities should leadership prepare for?
- How efficiently are customer support teams resolving issues?

---

# 🛠 Technology Stack

| Category | Technologies |
|-----------|--------------|
| Programming | Python |
| Libraries | Pandas, Regex |
| Spreadsheet Engineering | Microsoft Excel |
| ETL | Power Query |
| BI Platform | Power BI |
| Modeling | Star Schema |
| Analytics | DAX |
| Reporting | Interactive Executive Dashboard |

---

# 🏗 Project Architecture

```
Raw Excel + CSV Files
        │
        ▼
Python Cleaning Pipeline
        │
        ▼
Excel Validation
        │
        ▼
Power Query ETL
        │
        ▼
Star Schema Data Model
        │
        ▼
DAX Business Logic
        │
        ▼
Interactive Executive Dashboard
```

---

# ⚙ Phase 1 — Data Engineering & ETL

## 📂 Raw Data Sources

The project combines multiple banking operational datasets into one analytical model.

### Excel Workbook

- Accounts
- Loans
- Cards
- SupportCalls

### CSV Files

- customers.csv
- Transactions.csv

---

## 🐍 Python Data Cleaning

Customer contact information contained severe structural inconsistencies that prevented reliable downstream analytics.

Examples of issues included:

- Mixed international country codes
- Random phone extensions
- Negative floating-point artifacts
- Missing values
- Inconsistent formatting

A dedicated Python preprocessing pipeline was developed using **Pandas** and **Regular Expressions** to normalize all customer phone numbers.

Core processing included:

- Removing unwanted characters
- Detecting extensions
- Eliminating invalid numeric artifacts
- Handling missing values
- Standardizing every phone number into:

```text
(XXX) XXX-XXXX ext YYYY
```

Example regex workflow:

```python
import re

clean_number = re.sub(r"[^\d]", "", phone)
```

This ensured consistent customer contact records across the entire relational model.

---

## 📊 Power Query Transformations

Following Python preprocessing, Power Query handled structural ETL operations.

### Data Cleaning

- Removed unnecessary index columns

```
Unnamed: 0
```

- Corrected data types
- Converted date columns
- Converted primary keys
- Eliminated aggregation inconsistencies

---

### Geographic Standardization

Power BI Bing Maps initially produced ambiguous geographic locations because state abbreviations alone were insufficient.

A new calculated field was engineered:

```
State_Location

Example:

CA
↓

CA, USA
```

The field was explicitly categorized as:

```
State or Province
```

allowing accurate geographic visualization.

---

# ⭐ Phase 2 — Data Modeling & DAX

## Dimensional Modeling

The solution follows a classic **Star Schema** architecture.

```
               DATE
                 │
                 │
Customers ───────┼───────────────┐
 │               │               │
 │               │               │
Accounts      Transactions     Loans
 │
Cards
 │
Support Calls
```

### Modeling Decisions

✔ Customers serves as the central dimension table

✔ Continuous Calendar table enables time intelligence

✔ Single-direction filtering

✔ One-to-Many relationships

✔ Avoided bi-directional filtering ambiguity

✔ Created inactive relationship with LoanEndDate

This architecture significantly improves maintainability and query performance.

---

## Calendar Table

A continuous calendar dimension serves as the primary time intelligence engine.

Benefits include:

- Year filtering
- Monthly trends
- Rolling calculations
- Running totals
- Future forecasting

---

## Dedicated Measure Table

All DAX calculations are organized inside:

```
_Key Measures
```

This improves:

- Maintainability
- Discoverability
- Model organization

---

## Advanced Business Logic

### Active Customer Logic

Rather than using static dates, customer activity is determined dynamically.

Customers remain active if they performed transactions within **180 days** of the latest available transaction.

Conceptually:

```DAX
Latest Transaction Date
        ↓
Minus 180 Days
        ↓
Customer Active?
```

This allows the dashboard to remain future-proof as new data is added.

---

### Rolling Customer Acquisition

A rolling acquisition metric measures:

> **New Customers (Last 30 Days)**

relative to the latest transaction date in the dataset rather than today's system date.

---

### Loan Maturity Forecasting

The dashboard uses the DAX function:

```DAX
USERELATIONSHIP()
```

to activate the inactive relationship between:

```
Calendar Date

↓

LoanEndDate
```

This enables forward-looking portfolio forecasting without disrupting the primary reporting relationships.

---

## Operational Measures

Additional business metrics include:

- Support Resolution Rate
- Average Account Balance
- Running Customer Acquisition Totals
- Expected Maturing Loan Value

---

# 📈 Phase 3 — Dashboard Development

The report consists of **five fully interactive pages** following a consistent executive design philosophy.

## Design Principles

- Z-pattern visual hierarchy
- Static left-side navigation
- Interactive slicers
- Executive KPI cards
- Consistent corporate color palette
- Cross-filtering visuals
- Business-first storytelling

---

# 📄 Dashboard Pages

---

# 1️⃣ Executive Overview

Executive summary page providing high-level organizational health.

### KPIs

- Customer Count
- Active Customers
- Loan Portfolio
- Transaction Volume
- Resolution Rate

### Visualizations

- KPI Banner
- Transaction Volume Trendline
- Active vs Inactive Donut Chart
- Average Balance by Account Type Matrix

---

# 2️⃣ Customer Analysis

Focused on customer behavior and acquisition.

### Visualizations

- Bing Maps Geographic Heatmap
- Cumulative Customer Growth
- Customer Behavioral Scatter Plot

Analysis dimensions include:

- Geographic distribution
- Customer growth
- Transaction activity
- Support interaction frequency

---

# 3️⃣ Transaction Analysis

Examines banking transaction behavior.

Visuals include:

- Transaction Type Heatmap
- Account Type Matrix
- Monthly Transaction Trends
- Seasonal Clustered Column Charts

Designed to identify:

- Capital movement
- Behavioral consistency
- Seasonal volatility

---

# 4️⃣ Loan Analysis

Portfolio risk monitoring and forecasting.

Visualizations include:

- Loan Portfolio Distribution
- Interest Rate Comparison
- Expected Loan Maturity Pipeline

This page combines historical performance with forward-looking capital planning.

---

# 5️⃣ Customer Support

Operational efficiency dashboard.

Visualizations include:

- Dual-Axis Line Chart

```
Total Calls

vs

Resolved Calls
```

- Resolution Rate by Issue Type

Major support categories include:

- Transaction Disputes
- Account Access

allowing leadership to quickly identify operational bottlenecks.

---

# 💡 Key Business Insights

## 🔴 Insight 1 — Severe Customer Churn

Only **37.74%** of the **5,000** customers remain active.

Customer acquisition has slowed dramatically, with only **34** new customers acquired during the trailing 30-day period.

---

## 🟠 Insight 2 — Support Bottleneck

The customer support center is operating inefficiently.

Current Resolution Rate:

**49.30%**

The overwhelming majority of support friction originates from:

- Transaction Disputes
- Account Access

---

## 🟢 Insight 3 — Stable Loan Portfolio

The **$617M** loan portfolio is evenly diversified across:

- Car Loans
- Education Loans
- Home Loans
- Personal Loans

Each category represents approximately **25%** of the portfolio.

Among all products:

**Personal Loans produce the highest return at 7.67%.**

---

## 🔵 Insight 4 — Consistent Banking Activity

The bank processed:

**$100.11M**

in transaction volume.

Analysis revealed virtually **no seasonal volatility**, indicating customers rely on the institution primarily for everyday banking rather than periodic spending behavior.

---

# 🚀 Business Recommendations

## Recommendation 1

Launch an automated customer re-engagement campaign targeting the **3,113 inactive customers** with pre-approved **Personal Loans**, leveraging the bank's highest-yield lending product.

---

## Recommendation 2

Redesign Tier-1 customer support through automated self-service portals focused specifically on:

- Account Access
- Transaction Disputes

This initiative is expected to significantly reduce manual ticket volume while improving operational efficiency.

---

## Recommendation 3

Prepare investment vehicles in advance to efficiently deploy the projected **$256M** in capital expected to mature and return to the bank between **2027 and 2028**.

---

# 📁 Repository Structure

```
Banking-Customer-Operations-Analytics
│
├── Dataset
│   ├── customers.csv
│   ├── Transactions.csv
│   └── Banking.xlsx
│
├── Python
│   └── Phone_Cleaning.py
│
├── Power BI
│   └── Banking Customer & Operations Analytics.pbix
│
├── Images
│   ├── Executive Overview.png
│   ├── Customer Analysis.png
│   ├── Transaction Analysis.png
│   ├── Loan Analysis.png
│   └── Customer Support.png
│
└── README.md
```

---

# 🎯 Skills Demonstrated

### Data Engineering

- ETL Pipelines
- Data Cleaning
- Data Validation
- Regex Processing
- Power Query

### Data Modeling

- Star Schema
- Relationship Optimization
- Calendar Tables
- Relational Modeling

### Analytics

- Advanced DAX
- Time Intelligence
- Rolling Metrics
- Dynamic Customer Segmentation
- Forecast Modeling

### Business Intelligence

- Executive Dashboard Design
- KPI Development
- Operational Analytics
- Customer Analytics
- Financial Reporting
- Interactive Reporting

### Tools

- Python
- Pandas
- Microsoft Excel
- Power BI
- Power Query
- DAX

---

# 🏁 Conclusion

This project demonstrates the complete development of a modern Business Intelligence solution—from raw banking datasets through ETL, dimensional modeling, advanced DAX calculations, and executive dashboard design.

By combining Python-based data engineering with Power Query transformations, a robust Star Schema, and interactive Power BI reporting, the solution provides stakeholders with actionable visibility into customer retention, transaction behavior, loan portfolio performance, and customer support operations. The resulting analytics framework supports informed strategic decision-making while remaining scalable, maintainable, and adaptable for future data growth.

---

## 📬 Contact

**Ibrahim Mohamed Ibrahim Khalil**

**Role:** Data Analyst & AI/Machine Learning Engineer

If you found this project valuable, consider giving the repository a ⭐ to support future analytics and business intelligence projects.
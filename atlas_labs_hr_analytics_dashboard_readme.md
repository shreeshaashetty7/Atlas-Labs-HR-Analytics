# Atlas Labs HR Analytics & Attrition Dashboard

An end-to-end HR Analytics solution built using **Power BI**, **Power Query**, and **DAX**. This project analyzes workforce demographics, employee performance, job satisfaction, and turnover drivers for the fictional technology company **Atlas Labs**. 

The goal of this dashboard is to provide executive leadership and HR managers with actionable insights to increase employee retention, optimize performance, and understand organizational demographics.

---

## 📌 Table of Contents
- [Executive Summary & Key Insights](#-executive-summary--key-insights)
- [Project Architecture & Workflow](#-project-architecture--workflow)
- [Data Model & Star Schema](#-data-model--star-schema)
- [Key DAX Measures & KPIs](#-key-dax-measures--kpis)
- [Dashboard Pages & Visual Features](#-dashboard-pages--visual-features)
- [How to View / Run This Project](#-how-to-view--run-this-project)
- [Repository Structure](#-repository-structure)

---

## 📊 Executive Summary & Key Insights

1. **Overall Attrition:** The company maintains an overall attrition rate of approximately **16.1%**, with significant variance across specific employee subgroups.
2. **Key Attrition Drivers:**
   * **Overtime Work:** Employees working frequent overtime exhibit significantly higher turnover rates compared to non-overtime staff.
   * **Travel Frequency:** Frequent business travelers demonstrate higher attrition rates, indicating potential burnout.
   * **Tenure & Promotion Gaps:** A high concentration of departures occurs among staff who have gone **3+ years without a promotion** or are within their first 2 years at the company.
3. **Satisfaction & Performance:** High performance ratings do not strictly correlate with high job satisfaction—several top performers report low work-life balance ratings, representing a key flight risk.

---

## 🛠️ Project Architecture & Workflow

```
[ Raw Excel Data ] 
       │
       ▼
[ Power Query ]  --> Data Cleaning, Type Formatting, Conditional Age & Tenure Bands
       │
       ▼
[ Data Model ]   --> Star Schema Design (Fact & Dimension Tables)
       │
       ▼
[ DAX Measures ] --> Core KPIs, Attrition Rate %, Time-Intelligence, Ratios
       │
       ▼
[ Power BI UI ]  --> 4-Page Interactive Executive Dashboard
```

---

## 📐 Data Model & Star Schema

The project follows a **Star Schema** architectural design to maximize report efficiency, query speed, and measure usability.

* **Fact Table:**
  * `FactPerformanceRating`: Contains transactional ratings for job satisfaction, environment, self-rating, manager rating, and review dates.
* **Dimension Tables:**
  * `DimEmployee`: Core demographic information, hire dates, attrition status, department, and salary.
  * `DimEducationLevel`: Lookup for education fields and qualification levels.
  * `DimRatingLevel`: Mapping numeric ratings to qualitative labels (e.g., Low, Medium, High, Outstanding).
  * `DimSatisfiedLevel`: Satisfaction score descriptions.
  * `DimDate`: Dedicated calendar dimension table for time-intelligence reporting.

---

## 🧮 Key DAX Measures & KPIs

Below are key DAX formulas authored for this project:

### 1. Total Headcount & Active Staff
```dax
Total Employees = COUNT(DimEmployee[EmployeeID])

Active Employees = 
CALCULATE(
    [Total Employees],
    DimEmployee[Attrition] = "No"
)
```

### 2. Attrition Rate %
```dax
Attrition Count = 
CALCULATE(
    [Total Employees],
    DimEmployee[Attrition] = "Yes"
)

Attrition Rate % = 
DIVIDE(
    [Attrition Count],
    [Total Employees],
    0
)
```

### 3. Average Tenure & Salary
```dax
Avg Tenure (Years) = AVERAGE(DimEmployee[YearsAtCompany])

Avg Salary = AVERAGE(DimEmployee[MonthlyIncome])
```

---

## 🖥️ Dashboard Pages & Visual Features

1. **Executive Overview Page:**
   * Executive KPI summary cards (Total Employees, Active Employees, Inactive Employees, Attrition Rate).
   * High-level breakdowns by Department, Job Role, and Hire Trends over time.
2. **Demographics Page:**
   * Workforce distribution by Age Group, Gender, Ethnicity, and Marital Status.
   * Distance from home analysis vs. commute time impacts.
3. **Performance & Satisfaction Page:**
   * Comparison of Manager Ratings vs. Self-Ratings.
   * Satisfaction matrix evaluating Work-Life Balance, Environment, and Relationship Satisfaction.
4. **Attrition Deep-Dive:**
   * Root-cause analysis slicing turnover by Overtime, Business Travel, Years Since Last Promotion, and Tenure.

---

## 📁 Repository Structure

```text
├── data/
│   ├── DimEmployee.csv
│   ├── DimEducationLevel.csv
│   ├── DimRatingLevel.csv
│   ├── DimSatisfiedLevel.csv
│   └── FactPerformanceRating.csv
├── docs/
│   ├── dashboard_screenshot_overview.png
│   ├── dashboard_screenshot_demographics.png
│   ├── dashboard_screenshot_performance.png
│   └── dashboard_screenshot_attrition.png
├── Atlas_Labs_HR_Analytics.pbix
└── README.md
```

---

## 🚀 How to View / Run This Project

1. **Open in Power BI Desktop:**
   * Download and install the latest version of [Power BI Desktop](https://powerbi.microsoft.com/).
   * Clone this repository:
     ```bash
     git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY-NAME.git
     ```
   * Open `Atlas_Labs_HR_Analytics.pbix` in Power BI Desktop.
   * *(Note: If data source paths break, update the file directory location in **Power Query Editor > Data Source Settings**).*

2. **Interactive Online Link (Optional):**
   * [Click here to view the live published Power BI Report] https://github.com/shreeshaashetty7/Atlas-Labs-HR-Analytics/blob/main/HR%20analytics%20dashboard.pbix
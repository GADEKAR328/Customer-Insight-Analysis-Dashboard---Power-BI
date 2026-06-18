# 📊 Customer Insight Analysis — Power BI Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Formulas-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Internship](https://img.shields.io/badge/DevAlpha-Internship-orange?style=for-the-badge)

> **Data Analytics Internship — Task 1 (Easy)**
> Analyze customer datasets, clean information, identify trends and prepare a professional analytical report.

---

## 👤 Author

**Yogesh Gadekar**
Data Analytics Intern — DevAlpha Technologies

---

## 📌 Project Overview

This project performs a complete **Customer Insight Analysis** using Power BI Desktop. It covers data cleaning, DAX measure creation, and an interactive 3-page dashboard showcasing customer trends, behavior patterns, and churn analysis.

---

## 🗂️ Project Structure

```
Customer-Insight-Analysis/
│
├── 📁 Dataset/
│   └── CustomerData.csv          # Raw dataset (15 customer records)
│
├── 📁 Dashboard/
│   └── CustomerAnalysis.pbix     # Power BI report file
│
├── 📁 Screenshots/
│   ├── Page1_ExecutiveSummary.png
│   ├── Page2_CustomerBehavior.png
│   └── Page3_ChurnAnalysis.png
│
├── 📁 Docs/
│   └── DAX_Formulas_CustomerInsight.pdf   # All DAX formulas reference
│
└── README.md
```

---

## 📂 Dataset Description

| Column | Type | Description |
|--------|------|-------------|
| CustomerID | Text | Unique customer identifier |
| Name | Text | Customer full name |
| Age | Number | Customer age |
| Gender | Text | Male / Female |
| Region | Text | North / South / East / West |
| Segment | Text | New / Regular / Premium |
| TotalPurchases | Number | Count of purchases made |
| TotalSpend | Decimal | Total spend in ₹ |
| LastPurchaseDate | Date | Most recent purchase date |
| ProductCategory | Text | Electronics / Fashion / Beauty / Home |
| SatisfactionScore | Decimal | Rating out of 5 |
| ChurnStatus | Text | Yes = Churned, No = Active |

---

## 📊 Dashboard Pages

### Page 1 — Executive Summary
![Page 1](https://github.com/GADEKAR328/Customer-Insight-Analysis-Dashboard---Power-BI/blob/dbb5e2b679b874387563bf9285623d46fb73ada3/Page%201%20.jpg?raw=true)

Key visuals:
- **KPI Cards** — Total Customers, Total Revenue, Avg Satisfaction, Churn Rate
- **Clustered Bar Chart** — Revenue by Region
- **Donut Chart** — Customers by Segment
- **Slicers** — Product Category, Gender, Segment, Region

---

### Page 2 — Customer Behavior
![Page 2](https://github.com/GADEKAR328/Customer-Insight-Analysis-Dashboard---Power-BI/blob/dbb5e2b679b874387563bf9285623d46fb73ada3/Page%202.jpg?raw=true)

Key visuals:
- **Clustered Column Chart** — Spend by Age Group and Gender
- **Bar Chart** — Top Product Categories by Revenue
- **Column Chart** — Satisfaction by Segment
- **Scatter Chart** — Purchases Vs Spend (colored by Segment)

---

### Page 3 — Churn Analysis
![Page 3](https://github.com/GADEKAR328/Customer-Insight-Analysis-Dashboard---Power-BI/blob/dbb5e2b679b874387563bf9285623d46fb73ada3/Page%203.jpg?raw=true)

Key visuals:
- **Stacked Bar Chart** — Churns by Segment
- **Pie Chart** — Churn Vs Active (26.67% vs 73.33%)
- **Clustered Bar Chart** — Churn by Region
- **Table Visual** — Churned Customer Details

---

## 🧮 DAX Measures Used

### Page 1 — KPI Measures

```dax
Total Customers = COUNTROWS(Sheet1)
```

```dax
Total Revenue = SUM(Sheet1[TotalSpend])
```

```dax
Avg Satisfaction = AVERAGE(Sheet1[SatisfactionScore])
```

```dax
Churn Rate =
DIVIDE(
    COUNTROWS(FILTER(Sheet1, Sheet1[ChurnStatus] = "Yes")),
    COUNTROWS(Sheet1),
    0
) * 100
```

---

### Page 2 — Behavior Measures

```dax
Avg Spend = AVERAGE(Sheet1[TotalSpend])
```

```dax
-- Calculated Column (New Column)
Age Group =
SWITCH(
    TRUE(),
    Sheet1[Age] < 30, "18–29",
    Sheet1[Age] < 40, "30–39",
    Sheet1[Age] < 50, "40–49",
    "50+"
)
```

---

### Page 3 — Churn Measures

```dax
Active Customers =
CALCULATE(
    COUNTROWS(Sheet1),
    Sheet1[ChurnStatus] = "No"
)
```

```dax
Premium Customers =
CALCULATE(
    COUNTROWS(Sheet1),
    Sheet1[Segment] = "Premium"
)
```

```dax
Premium Revenue =
CALCULATE(
    SUM(Sheet1[TotalSpend]),
    Sheet1[Segment] = "Premium"
)
```

```dax
-- Calculated Column (New Column)
High Value Customer =
IF(Sheet1[TotalSpend] > 30000, "High Value", "Standard")
```

---

### Date Table

```dax
DateTable = CALENDAR(
    MIN(Sheet1[LastPurchaseDate]),
    MAX(Sheet1[LastPurchaseDate])
)
```

```dax
Month   = FORMAT(DateTable[Date], "MMMM")
Quarter = "Q" & QUARTER(DateTable[Date])
Year    = YEAR(DateTable[Date])
```

> **Relationship:** `DateTable[Date]` → `Sheet1[LastPurchaseDate]`
> Cardinality: **Many to One (\*:1)** | Direction: **Single**

---

## 🔍 Key Insights

- 💰 **Premium segment** contributes ~72% of total revenue despite being only 33% of customers
- ⚠️ **Churn rate is 26.7%** — highest concentration in the New customer segment
- 🛍️ **Electronics** is the top product category by revenue
- 📍 **North region** generates the highest revenue among all regions
- 😊 **Premium customers** have the highest average satisfaction score (4.7)
- 🔴 **New customers** have the lowest satisfaction (avg 3.0) and highest churn

---

## 💡 Business Recommendations

1. **Introduce an onboarding loyalty program** for New segment customers to reduce 67% churn rate in that group
2. **Invest more in Electronics** category marketing — it drives the majority of Premium customer spend
3. **Target West and East regions** with promotional campaigns as they show lower revenue compared to North and South
4. **Re-engage churned customers** from North and South regions with personalized discount offers

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Power BI Desktop | Dashboard creation & visualization |
| Power Query (M) | Data cleaning & transformation |
| DAX | Calculated measures & columns |
| CSV | Source data format |

---

## 🚀 How to Run

1. Clone this repository
   ```bash
   git clone https://github.com/GADEKAR328/Customer-Insight-Analysis-Dashboard---Power-BI.git
   ```

2. Open **Power BI Desktop**

3. Open `Dashboard/CustomerAnalysis.pbix`

4. If data source error appears:
   - Go to **Home → Transform Data → Data Source Settings**
   - Update the path to `Dataset/CustomerData.csv`

5. Click **Refresh** — all visuals will load automatically

---

## 📁 Files to Upload on GitHub

| File | Description |
|------|-------------|
| `README.md` | This file |
| `Dataset/CustomerData.csv` | Raw data file |
| `Dashboard/CustomerAnalysis.pbix` | Power BI report |
| `Screenshots/*.png` | Dashboard page screenshots |
| `Docs/DAX_Formulas_CustomerInsight.pdf` | DAX reference PDF |

---

## 🏫 Internship Details

| Field | Details |
|-------|---------|
| Organization | DevAlpha Technologies |
| Domain | Data Analytics |
| Task | Task 1 — Customer Insight Analysis |
| Difficulty | Easy |
| Status | ✅ Completed |

---

## 📜 License

This project is submitted as part of the **DevAlpha Technologies Data Analytics Internship Program**.

---

<p align="center">Made with ❤️ by <strong>Yogesh Gadekar</strong></p>

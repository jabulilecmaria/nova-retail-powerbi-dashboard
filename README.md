# Nova Retail Group — Sales Performance Dashboard

## 📊 Project Overview

This project is a Power BI sales analytics dashboard developed for Nova Retail Group.

The project demonstrates data modelling, Power Query data preparation, DAX measures, time-intelligence analysis, customer and regional ranking, dashboard design, and business insights.

**Tool:** Microsoft Power BI Desktop  
**Project Type:** Business Intelligence & Data Analytics  
**Dataset:** Nova Retail Group  
**Platform:** Witle Academy

## 🎯 Business Objective

Nova Retail Group operates across multiple regions in South Africa and sells consumer products through physical stores and an online platform.

The objective of this project is to transform raw sales data into an interactive executive dashboard that allows management to monitor:

- Revenue and profit
- Profit margin
- Order volume
- Average order value
- Monthly revenue trends
- Product-category performance
- Regional performance
- Online vs Store sales
- Customer satisfaction
- Top customers

## 🗂️ Data Model

| Table | Role | Records |
|---|---|---:|
| Products | Dimension | 30 |
| Customers | Dimension | 500 |
| Sales | Fact | 2,500 |
| CustomerFeedback | Supporting fact | 1,000 |
| Date | Date dimension | Created in Power BI |

### Relationships

- Date[Date] → Sales[OrderDate]
- Products[ProductID] → Sales[ProductID]
- Customers[CustomerID] → Sales[CustomerID]
- Customers[CustomerID] → CustomerFeedback[CustomerID]
- Sales[OrderID] → CustomerFeedback[OrderID]

The model uses one-to-many relationships with single-direction filtering.

## 🧮 Core DAX Measures

```DAX
Total Revenue =
SUM ( Sales[TotalSales] )

Total Profit =
SUM ( Sales[Profit] )

Total Orders =
DISTINCTCOUNT ( Sales[OrderID] )

Total Customers =
DISTINCTCOUNT ( Sales[CustomerID] )

Average Order Value =
DIVIDE (
    [Total Revenue],
    [Total Orders]
)

Profit Margin % =
DIVIDE (
    [Total Profit],
    [Total Revenue]
)
Previous Year Revenue =
CALCULATE (
    [Total Revenue],
    SAMEPERIODLASTYEAR ( 'Date'[Date] )
)

YoY Growth % =
DIVIDE (
    [Total Revenue] - [Previous Year Revenue],
    [Previous Year Revenue]
)

Customer Rank =
RANKX (
    ALL ( Customers[CustomerID] ),
    [Total Revenue],
    ,
    DESC,
    DENSE
)

Regional Rank =
RANKX (
    ALL ( Customers[Region] ),
    [Total Revenue],
    ,
    DESC,
    DENSE
)
 ## Business Insights

### Key Findings

1. **Strong overall profitability**
   
   Nova Retail Group generated R16.88 million in total revenue and R5.92 million in total profit, resulting in a 35.05% profit margin.

2. **Electronics is the leading revenue category**
   
   The Electronics category records the highest revenue among the categories shown on the dashboard, making it an important contributor to overall sales performance.

3. **Regional performance differs across the business**
   
   The regional ranking shows North ranked 1st, followed by East, South and West. This indicates differences in revenue performance across the four regions.

### Strategic Recommendations

1. **Maintain focus on high-performing product categories**
   
   Continue supporting the Electronics category while analysing its products, customers and sales drivers to understand what is contributing to its stronger revenue performance.

2. **Investigate regional performance differences**
   
   Examine the lower-ranked regions to identify opportunities to improve sales through targeted promotions, customer engagement and regional sales strategies.

3. **Monitor customer experience alongside sales performance**
   
   The dashboard shows an average customer rating of 3.76. Nova Retail Group should monitor customer feedback and identify factors affecting satisfaction while continuing to grow revenue and profitability.

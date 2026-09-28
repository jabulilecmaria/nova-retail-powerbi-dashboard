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

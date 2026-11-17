# Retail Sales & Customer Analytics Dashboard with Power BI
## Overview

This project is a Power BI dashboard designed to analyze retail sales and customer data and provide a clear overview of business performance. The dashboard focuses on sales, profitability, customers, products, regions, and sales trends through interactive visualizations and key performance indicators.

## Objectives

- Analyze overall retail sales performance.
- Evaluate total revenue and profit.
- Understand customer and order activity.
- Analyze product performance.
- Compare sales performance across regions.
- Evaluate average order value and return rate.
- Identify important trends and patterns in sales data.

## Dataset

The data for this project is sourced from the Kaggle dataset:

- **Dataset Link:** [Retail Dataset](https://www.kaggle.com/datasets/hyerdrac/retail-data)

## Tools & Technologies

- Microsoft Power BI
- DAX
- Power BI Data Modeling
- Power Query

## Dashboard Preview

![Retail Sales & Customer Analytics Dashboard](https://github.com/maketadickson/power-bi-sales_dashboard/blob/main/Dashboard.png)

## Key Insights

The dashboard was used to identify patterns and trends in revenue, profit, customers, orders, products, regions, and returns:

- Revenue and profit vary across products and regions.
- Customer and order volumes provide insight into overall sales activity.
- Average order value helps measure the value generated per order.
- Product-level analysis highlights differences in revenue, profitability, and return rates.
- Regional analysis reveals differences in sales performance across locations.
- Monthly sales trends show how revenue changes over time.

## DAX Measures

### Number of Customers
```dax
DISTINCTCOUNT(customers[customer_id])
```

### Total Customers
```dax
CALCULATE(
    DISTINCTCOUNT(orders[customer_id]),
    TREATAS(
        VALUES(order_details[order_id]),
        orders[order_id]
    )
)
```

### Total Orders
```dax
DISTINCTCOUNT(order_details[order_id])
```

### Target Orders
```dax
VAR LastYearOrder =
    CALCULATE([Total Orders], SAMEPERIODLASTYEAR(date_table[Date]))
RETURN
    IF(
        ISBLANK(LastYearOrder),
        15000,
        LastYearOrder * 1.5
    )
```

### Average Order Value
```dax
DIVIDE([Total Revenue], [Total Orders])
```

### Total Profit
```dax
SUM(order_details[profit])
```

### Total Revenue
```dax
SUM(order_details[net_sale])
```

### Return Rate
```dax
DIVIDE(
    CALCULATE(
        COUNTROWS(order_details),
        order_details[is_returned] = 1
    ),
    COUNTROWS(order_details)
)
```

## Project Files

The Power BI report (.pbix) and dashboard preview image are still hosted in the original repository:

- [Download the Power BI report](https://github.com/maketadickson/power-bi-sales_dashboard/blob/main/Retail_Sales%20%26%20Customer_%20Analytics.pbix)
- [View the dashboard preview](https://github.com/maketadickson/power-bi-sales_dashboard/blob/main/Dashboard.png)

## Conclusion

This project demonstrates the use of Power BI, DAX, Power Query, and data modeling to transform retail sales and customer data into an interactive business intelligence dashboard and communicate meaningful insights from the data.

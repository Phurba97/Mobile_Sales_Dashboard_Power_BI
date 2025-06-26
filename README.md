# Mobile_Sales_Dashboard_Power_BI

🗂 Overview
This Power BI dashboard project demonstrates a full end-to-end data analysis workflow, starting from raw data ingestion to building an interactive and responsive sales dashboard. The dataset used relates to mobile sales performance and customer ratings.
![Mobile sales Dashboard1](https://github.com/user-attachments/assets/378bd90b-746a-49ba-9b75-e82b9d2cd956)

![SamePeriodLastYear](https://github.com/user-attachments/assets/f6cb5687-2c38-4cf8-b291-51effe11adfe)
![MTD Report](https://github.com/user-attachments/assets/68a4b3f1-cc3b-4730-8027-b618ed8e0840)



🔄 Data Preparation & Transformation
Initial Upload & Data Assessment
The raw dataset was first uploaded into Power BI. On inspection, the data structure was not suitable for analysis—particularly the date fields, which were split into separate Day, Month, and Year columns.

Date Column Transformation
Used Power Query to merge the Day, Month, and Year columns into a single Date column and converted it to the proper Date data type.

Custom Calendar Table
A custom calendar was created using Power Query with the following M code:

m
Copy
Edit
List.Dates(#date(2021,1,1), 1461, #duration(1,0,0,0))
This list was then transformed into a table and formatted appropriately to support time intelligence functions.

🔧 Data Modeling
Relationships were established between the main sales data and the custom calendar table to enable advanced date filtering and analysis.

📐 DAX Measures
Key DAX measures created for analysis include:

Total Quantity
Total_Qty = SUM(Mobile_sale_Dashboard[Units Sold])

Total Transactions
Total Transaction = COUNTROWS(Mobile_sale_Dashboard)

Total Sales
Total Sale = SUMX(Mobile_sale_Dashboard, Mobile_sale_Dashboard[Units Sold] * Mobile_sale_Dashboard[Price Per Unit])

Average Price
Avg Price = AVERAGE(Mobile_sale_Dashboard[Price Per Unit])

YTD, MTD, QTD Sales

DAX
Copy
Edit
YTD = TOTALYTD([Total Sale], 'Custom Calender'[Date].[Date])  
MTD = TOTALMTD([Total Sale], 'Custom Calender'[Date].[Date])  
QTD = TOTALQTD([Total Sale], 'Custom Calender'[Date].[Date])
Customer Rating Status
A new calculated column was added to classify ratings:

DAX
Copy
Edit
Rating Status = 
IF(Mobile_sale_Dashboard[Customer Ratings] >= 4, "Good",
   IF(Mobile_sale_Dashboard[Customer Ratings] > 2, "Average", "Poor"))
📈 Dashboard Features
Responsive Design for various views, including:

Main Dashboard

Same Period Last Year Comparison

Month-to-Date (MTD) Analysis

Clean visuals for sales trends, average pricing, customer satisfaction, and key KPIs.

✅ Outcome
This dashboard provides a robust analytical view of mobile sales performance with dynamic filtering, trend analysis, and customer rating insights—all built using effective data modeling, Power Query transformation, and powerful DAX calculations.


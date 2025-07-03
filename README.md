# DSA-Capstone-Project-
This is where I documented my final project during my DSA data analysis training with Incubator Hub. I learnt a lot about using Ms Excel, SQL and Power BI to analyze various data sets in order to answer questions and make data-driven decisions.

## Project Topic: Kultra Mega Stores Inventory

### Project Overview
This data analysis aims to apply my SQL skills from DSA data analysis class in extracting key insights from the order data of Kultra Mega Stores from 2009 – 2012. By analyzing the sales, shipping, and customer behavior in the given data to answer questions which will then enable the company make reasonable business decisions.

### Table of Contents

### Data Sources
The primary source of data used here are KMS SQL Case Study.xlsx and Order_Status.csv files. These were downloaded from the Learning Management System (LMS) used during the course of the training.

### Tools Used
Microsoft SQL Server Management Studio (SSMS) – Utilized for querying and analysis

### Data Cleaning and Preparation
The following actions were performed during the data preparation phase;
-	Data Importation into SSMS
     - The data were imported as a flat file (csv format).
-	Data type of some columns were changed during importation:
      -	Row ID and Order ID were changed to integer.
       - Product name was changed to nvarchar(MAX).
       - Product category was changed to nvarchar(100).
       - Sales, profit, unit price, shipping cost, discount and product base margin was changed to decimal (10, 3).
-	Allow nulls was checked for all columns with float data type
- Row ID was selected as the primary key in the KMS SQL case study table while Order ID was mad the primary key in the Order Status table.

### Project Structure – Exploratory Data Analysis
EDA involved the exploration of the data to answer some questions about the data such as:
-	Which product category had the highest sales?
-	What are the Top 3 and Bottom 3 regions in terms of sales?
-	What were the total sales of appliances in Ontario? 
-	Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers.
-	KMS incurred the most shipping cost using which shipping method.
-	Who are the most valuable customers, and what products or services do they typically purchase?
-	Which small business customer had the highest sales?
-	Which Corporate Customer placed the most number of orders in 2009 – 2012?
-	Which consumer customer was the most profitable one?
-	Which customer returned items, and what segment do they belong to?
-	If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer.

### Data Analysis
The queries used during the analysis are:

```   SQL
---Product category with the highest sales---
select top 1 product_category, sum (Sales) as Total_sales
from order_data
group by product_category
order by Total_sales desc

```

```  SQL
---Top 3 regions in terms of sales---
 select top 3 region, sum (sales) as Total_Sales
 from order_data
 group by region
 order by Total_Sales desc

```

```  SQL
 ---Bottom 3 regions in terms of sales---
 select top 3 region, sum (sales) as Total_Sales
 from order_data
 group by region
 order by Total_Sales asc

```

```  SQL
---Total sales of appliances in Ontario---
select sum (sales) as [Total Appliances Sales]
from order_data
where product_sub_category = 'Appliances'
and Region = 'Ontario'

```

``` SQL
---Revenue from the bottom 10 customers---
select top 10 customer_name, sum (sales) as Total_Revenue, region
from order_data
group by customer_name, region
order by total_revenue asc

```

``` SQL
---Shipping method with the most shipping cost---
select ship_mode, sum (shipping_cost) as Total_Shipping_Cost
from Order_data
group by ship_mode
order by Total_Shipping_Cost desc

```

```  SQL
---The most valuable customers and the products or services they typically purchase---
select top 10 customer_name,
sum (sales) as [Total Revenue],
sum (profit) as [Total Profit],
count (product_sub_category) as [Total Orders]
from Order_data
group by Customer_name
Order by [Total Revenue] desc

```

```   SQL
---products and services they purchase---
select Customer_name, product_sub_category,
count (product_sub_category) as Purchase_count,
sum (sales) as Revenue
from order_data
where customer_name in ('Emily Phan', 'Deborah Brumfield', 
'Sylvia Foulston', 'Grant Carroll', 'Alejandro Grove', 'Roy Skaria',
'Darren Budd', 'Julia Barnett', 'John Lucas', 'Liz Mackendrick')
group by customer_name, product_sub_category
order by customer_name, revenue desc

```

```  SQL
---small business customer that had the highest sales---
select top 1 customer_name,
sum (sales) as [Total Sales]
from Order_data
where customer_segment = 'small business'
group by Customer_name
Order by [Total Sales] desc

```

```  SQL
---The corporate customer that placed the most number of orders in 2009 - 2012---
select top 1 customer_name,
count (order_ID) as Order_count,
sum (order_quantity) as Quantity_count
from order_data
where customer_segment = 'corporate'
and year (order_date) between 2009 and 2012
group by customer_name
order by order_count desc

```

```  SQL
---The most profitable consumer customer---
select top 10 customer_name,
sum (sales) as [Total Revenue]
from Order_data
where customer_segment = 'consumer'
group by Customer_name
Order by [Total Revenue] desc

```

```  SQL
---The customer segment of customers who returned items---
select order_data.customer_name, 
		order_data.customer_segment, order_status.status
from order_data
join order_status
on order_data.order_id = order_status.order_id
where order_status.status = 'Returned'

```

```  SQL
---Shipping cost based on order priority---
select order_priority, ship_mode,
count (Order_ID) as Order_count,
sum (Sales - Profit) as estimated_shipping_cost,
avg (datediff (day,Order_date, Ship_date)) as avg_ship_days
from order_data
group by order_priority, ship_mode
order by order_priority, ship_mode desc

```

### Data Analysis
From the analysis, the following insights were derived:
- The product category with the highest sales is technology.
- In terms of sales, West, Ontario and Prarie are the top 3 regions while Nunavut, Northwest Territories and Yukon are the bottom 3 regions.
- The total sales of appliance in Ontario is #202346.840.
- The management can increase the revenue from the bottom 10 customers by either one or all of the following strategies; analyzing purchase history to identify patterns or opportunities, offer targeted promotions or discounts that resonate with their needs, simplify transactions and make it easier for customers to do business, improve customer service, offer exclusive deals or early access to new products.
- The company incurred the most shipping cost using delivery truck shipping method.
- The top 10 most valuable customers are: Emily Phan, Deborah Brumfield, Roy Skaria, Sylvia Foulston, Grant Carroll, Alejandro Grove, Darren Budd, Julia Barnett, John Lucas, and Liz Mackendrick. The products and services they typically purchase include: chair & chair mats, tables, office furnishings, telephone & communication, computer peripherals, storage and organization, appliances, paper, bookcases, binders & binder accessories, etc.
- The small business customer with the highest sales is Dennis Kane.
- Adam Hart is the corporate customer that placed the most number of orders.
- The most profitable consumer customer was Emily Phan.
- About 872 customers returned items and these customers span across the various customer base of the company.
- I think the company appropriately spent shipping costs based on the order priority because for items that have critical and high order priority which needs to be delivered quickly to the customer, it still took the same average number of days (1 day) to deliver with express air as would the delivery truck. It was more economical for the company to use delivery trucks for items with critical and high order priority (as it would save shipping cost) since it would take the same average number of days if they were to be delivered by express air which is fast but more expensive.

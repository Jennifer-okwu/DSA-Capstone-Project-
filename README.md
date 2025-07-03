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


# Superstore Data Analysis Project

## Introduction
This project demonstrates the end-to-end process of analyzing the Superstore dataset using AWS services. The workflow includes AWS Glue, Crawlers, and Data Catalog for organizing and preparing data, Athena for querying, and QuickSight for visualization.

---

## Tech Stack
- AWS S3: Data storage for raw and transformed datasets.
- AWS Glue: Data preparation, ETL jobs, and cataloging.
- AWS Glue Crawlers: Automated schema inference and table creation.
- AWS Glue Data Catalog: Centralized metadata repository.
- AWS Athena: Serverless SQL queries for data analysis.
- AWS QuickSight: Data visualization and dashboarding.

---

## Project Workflow

1. **Data Upload to S3**  
   Upload the Superstore dataset (CSV format) to an S3 bucket (e.g., `s3://your-bucket-name/superstore/`).

2. **AWS Glue Crawler**  
   Create a Glue Crawler to scan the dataset in S3 and infer its schema. Configure the Crawler to update the Glue Data Catalog with a new table.

3. **AWS Glue Data Catalog**  
   The Crawler creates a metadata table in the Glue Data Catalog, which Athena can query.

4. **Query with AWS Athena**  
   Use Athena to query the Superstore data directly from the Glue Data Catalog. Perform various SQL operations for data analysis (e.g., sales by region, profit analysis).

5. **Visualize with AWS QuickSight**  
   Connect QuickSight to Athena to create interactive dashboards. Visualize metrics like sales trends, category performance, and regional breakdowns.

---

## Setup Instructions

### Step 1: Prepare S3 Bucket
- Create an S3 bucket in your AWS account (e.g., `superstore-data-analysis`).
- Upload the Superstore dataset (e.g., `superstore.csv`) to a designated folder (e.g., `s3://superstore-data-analysis/raw-data/`).

### Step 2: Configure AWS Glue Crawler
1. Navigate to the AWS Glue Console.
2. Create a new Crawler:
   - Name: `superstore-crawler`
   - Data Source: S3 path (`s3://superstore-data-analysis/raw-data/`)
   - IAM Role: An IAM role with S3 read access and Glue permissions.
3. Run the Crawler to populate the Glue Data Catalog.

### Step 3: Query Data with Athena
1. Open the Athena Console.
2. Select the Glue database created by the Crawler.
3. Write SQL queries to analyze the Superstore dataset. Examples:
   ```sql
   -- Total sales by region
   SELECT region, SUM(sales) AS total_sales
   FROM superstore_table
   GROUP BY region;

   -- Top 5 profitable products
   SELECT product_name, SUM(profit) AS total_profit
   FROM superstore_table
   GROUP BY product_name
   ORDER BY total_profit DESC
   LIMIT 5;
### Step 4: Visualize Data in QuickSight
1.Navigate to the AWS QuickSight Console.
2.Connect QuickSight to Athena and create a dataset from your Athena table.
3.Build dashboards with visualizations like bar charts, line graphs, and heatmaps.
### Sample Queries
```sql
 --Sales by Region:
 SELECT region, SUM(sales) AS total_sales
 FROM superstore_table
 GROUP BY region;
 --Top 10 Customers by Sales:

SELECT customer_name, SUM(sales) AS total_sales
FROM superstore_table
GROUP BY customer_name
ORDER BY total_sales DESC
LIMIT 10;
 --Monthly Sales Trend:

 SELECT EXTRACT(YEAR FROM order_date) AS year, 
       EXTRACT(MONTH FROM order_date) AS month, 
       SUM(sales) AS monthly_sales
 FROM superstore_table
 GROUP BY year, month
 ORDER BY year, month;
### Folder Structure
```kotlin
superstore-data-analysis/
├── data/
│   └── superstore.csv
├── notebooks/
│   └── AthenaQueries.sql
├── dashboards/
│   └── QuickSightScreenshots.png
├── README.md

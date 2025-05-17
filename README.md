# Amazon-Product-Analysis-using-AWS-Redshift
This project focuses on performing data analysis on Amazon India product listings using AWS 
services, primarily Amazon Redshift and AWS Glue. A cleaned dataset containing detailed product 
information such as title, price, rating, and bestseller status was loaded into Redshift from an S3 
bucket. Various SQL queries were executed to gain insights into product trends, including filtering 
products based on ratings, identifying bestsellers, and analyzing price distributions. Visualizations 
were created using Redshift’s built-in charting tools to interpret results more effectively. This 
project demonstrates practical use of ETL workflows and cloud-based data warehousing for large
scale e-commerce data analysis.

## Dataset : 
We used the Amazon India Products 2023 dataset, which includes product-level information 
from various categories listed on Amazon.in. The dataset was uploaded to Amazon S3 and later 
loaded, cleaned, and transformed using AWS Glue. The dataset contains details such as: 

![image](https://github.com/user-attachments/assets/052bd14c-c5a9-481e-b66b-0cb9949c1ece)

## Objectives : 
After transforming the data, we loaded it into Amazon Redshift Serverless to perform the 
following analyses: 
1. Filter by Ratings: Focused on products with stars > 1 to ensure quality feedback. 
2. Premium Product Analysis: Identified high-rated products priced above average to find 
valuable premium items. 
3. Bestseller Insights: Analyzed products marked as bestsellers to understand popular trends.

## Queries: 
1. Creating an external schema named amazon_india_schema_cleaned1 in Amazon Redshift, which links Redshift to your Glue Data Catalog so that Redshift can query external tables.
   
   ###QUERY### 

   CREATE EXTERNAL SCHEMA amazon_india_schema_cleaned1 
   FROM DATA CATALOG 
   DATABASE 'amazon_products_clean_db' 
   IAM_ROLE 'arn:aws:iam::841162699551:role/RedshiftS3AccessRole' 
   CREATE EXTERNAL DATABASE IF NOT EXISTS; 


2. Retrieving the first 10 rows from the external table amazon_products_clean_tableamazon_products_cleaned1 in the external schema amazon_india_schema_cleaned1.
   
   ###QUERY###
   
   SELECT * FROM 
   amazon_india_schema_cleaned1."amazon_products_clean_tableamazon_products_clean
   ed1" LIMIT 10;
   
   ![image](https://github.com/user-attachments/assets/b98ad691-ca02-4ef9-8eed-15d7d992b1df)


3. Creating a local Redshift table named amazon_products_local_redshift_cleaned1 by copying all the data from the external table in the schema amazon_india_schema_cleaned1. It loads the cleaned external table into Redshift's local storage for faster querying and analysis.
   
   ###QUERY###
   
   LOCAL TABLE CREATED ON REDSHIFT 
   (amazon_products_local_redshift_cleaned1) 
   CREATE TABLE amazon_products_local_redshift_cleaned1 AS 
   SELECT * FROM 
   amazon_india_schema_cleaned1."amazon_products_clean_tableamazon_products_clean
   ed1";


4. Displaying the first 20 rows from the local Redshift table.
   
   ###QUERY###
   
   SELECT * FROM amazon_products_local_redshift_cleaned1 LIMIT 20;

   ![image](https://github.com/user-attachments/assets/4a453efe-4911-4860-917d-4952dc24347d)


5. Filtering external table records where stars rating is more than 1.
   
   ###QUERY###
   
   SELECT * FROM  amazon_india_schema_cleaned1."amazon_products_clean_tableamazon_products_cleaned1" where stars>1;

   ![image](https://github.com/user-attachments/assets/a4e67e2e-0e98-46e6-bf1f-83cab4e717c2)


6. Filtering local Redshift table records with stars > 1.
   
   ###QUERY###
   
   SELECT * FROM amazon_products_local_redshift_cleaned1 where stars>1;

    ![image](https://github.com/user-attachments/assets/d841de4d-7e20-4055-9fbd-7917df618313)


7. Fetching products with a listprice above the average and stars > 1.
   
   ###QUERY###
   
   SELECT * FROM amazon_products_local_redshift_cleaned1 where listprice>(select avg(listprice) from amazon_products_local_redshift_cleaned1) and stars>1;

   ![image](https://github.com/user-attachments/assets/36d1645c-6534-4989-ae00-784fd3f23c0a)



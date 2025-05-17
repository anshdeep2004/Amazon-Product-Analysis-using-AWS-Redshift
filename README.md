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


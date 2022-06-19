# Amazon_Vine_Analysis

## Overview 

The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Some companies pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.

This project’s purpose was to analyze Amazon reviews written by members of the paid Amazon Vine program. For this purpose, we had access to approximately 50 Amazon product review datasets, each dataset contains reviews of a specific product. [Amazon Review datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt)

Among this dataset, the **"toy product"** reviews dataset was picked and PySpark was used to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. 

After those steps, PySpark was used to determine if there is any bias toward favorable reviews from Vine members in your dataset and a summary of the analysis was presented. 

## Result 

### 1.Perform ETL on Amazon Product Reviews

Using the cloud ETL process, an AWS RDS database with tables in pgAdmin was created and from the Amazon Review datasets **[toy product dataset](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Toys_v1_00.tsv.gz)** was picked.

The dataset was extracted into a DataFrame, and transformed into four separate DataFrames that match the table schema in pgAdmin. After, that transformed data was uploaded into the appropriate tables. The queries in pgAdmin were run to confirm that the data has been uploaded.

* A new database with Amazon RDS and in pgAdmin was created. 
* In pgAdmin, a new query to create the tables for the new database was run by using the code from the challenge_schema.sql file. After running the query, four tables in the database were created: “customers_table”, ” products_table”,  “review_id_table”, and “vine_table”.
* One of the review datasets was extracted and then a new DataFrame was created. [Amazon_Reviews_ETL.ipynb](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb)
* The dataset was transformed into four DataFrames that will match the schema in the pgAdmin tables:

    * [customers_table.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_1_images/customers_table.png)
    * [products_table.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_1_images/products_table.png)
    * [review_id_table.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_1_images/review_id_table.png)
    * [vine_table.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_1_images/vine_table.png)

### Load the DataFrames into pgAdmin
* The connection to the AWS RDS instance. was made. 
* The DataFrames that correspond to tables in pgAdmin were loaded. 
* In pgAdmin, a query was run to check that the tables have been populated.

   * [customers_table_pgAdmin.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_1_images/customers_table_pgAdmin.png)
   * [products_table_pgAdmin.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_1_images/products_table_pgAdmin.png)
   * [review_id_table_pgAdmin.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_1_images/review_id_table_pgAdmin.png)
   * [vine_table_pgAdmin.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_1_images/vine_table_pgAdmin.png)

### 2.Determine Bias of Vine Reviews 



## Summary 





## Resources

**Data Sources** 
* [Amazon Review datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt)
* [SQL table schema](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/challenge_schema%20(2).sql)
* [Amazon ETL starter code](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL_starter_code%20(2).ipynb)

**Database Management** 
* PostgreSQL
* AWS S3 and RDS
* Google Colab (to run PySpark)
* VS Code 

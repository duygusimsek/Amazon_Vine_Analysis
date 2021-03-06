# Amazon_Vine_Analysis

## Overview 

The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Some companies pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.

This project’s purpose was to analyze Amazon reviews written by members of the paid Amazon Vine program. For this purpose, we had access to approximately 50 Amazon product review datasets, each dataset contains reviews of a specific product. [Amazon Review datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt)

Among this dataset, the **"toy product"** reviews dataset was picked and PySpark was used to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. 

After those steps, PySpark was used to determine if there is any bias toward favorable reviews from Vine members in the dataset and a summary of the analysis was presented. 

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

Using the PySpark, we determined if there is any bias towards reviews that were written as part of the Vine program. For this analysis, if having a paid Vine review makes a difference in the percentage of 5-star reviews was analyzed. 

* The data was filtered and a new DataFrame was created to retrieve all the rows where the total_votes count is equal to or greater than 20. This helped to pick reviews that are more likely to be helpful and to avoid having division by zero errors later on.

   * [totalvotes_df.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_2_images/totalvotes_df.png)
* The new DataFrame that was created previously was filtered to find the helpful reviews. A new DataFrame that shows helpful reviews was formed and retrieved all the rows where the number of helpful_votes divided by total_votes is equal to or greater than 50%.

   * [helpful_votes50_df.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_2_images/helpful_votes50_df.png)
* The previous DataFrame (helpful_votes50) was filtered to display the reviews that were written as part of the Vine program (paid), vine == 'Y'. 

   * [vine_review_paid_df.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_2_images/vine_review_paid_df.png)
* To retrieve all the rows where the review was NOT part of the Vine program (unpaid), vine == ’N’ the same process was repeated. 

   * [vine_review_unpaid_df.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_2_images/vine_review_unpaid_df.png)
* Finally, the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid) were analyzed. 

   * [total_numbers.png](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Deliverable_2_images/total_numbers.png)
* The  Vine_Review_Analysis Google Colab Notebook was exported as an ipynb file. [Vine_Review_Analysis.ipynb](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Vine_Review_Analysis.ipynb)

**1. How many Vine reviews and non-Vine reviews were there?**

As the analysis shows there are **4,864,249** total reviews of toy products.  **63,294** of the total reviews are found helpful. When we examine the helpful reviews, numbers **1,266** are the total vine reviews (paid) that are written by Amazon Vine members and **62,028** are the total number of NON-PAID  reviews. 

**2. How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?**

The analysis displays that there are a total of 3,076,917 all 5-star reviews and **30,414** the “helpful 5-star” toy product reviews. The number of **432** reviews are “helpful vine (paid) 5-star”; the number of **29,982** reviews are “helpful non-vine (non-paid) 5-star“ reviews. 

**3. What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?**

While the percentage of 5-star Toy PAID (vine) and 'helpful' reviews is **0.341232** (34.12%), the percentage of 5-star Toy NON-PAID and 'helpful' reviews: is **0.483362** (48.33%). 

## Summary 

* The majority of reviews for Toys products are almost nothing or lower results from  Amazon vine participants. 
* Comparing the helpful 5-star toy products review for vine and non-vine, the number of the vine reviews are not notable. 
* As can be seen, there were not many helpful reviews, comparing the total reviews. 
* Even though the percentages may be misleading as the volume of reviews in the vine and non-vine programs vary so much, this itself is a sign that the vine program is not very popular in this category. 
* This shows that customers (Amazon vine members) don't feel a positivity bias for leaving good reviews in the paid program as there are so few and not so many well-rated.
* For recommendation,  to have a better understanding of the data, there could be more analysis of Vine members’ star rating scale to see if the Vine program serves its purpose. 




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

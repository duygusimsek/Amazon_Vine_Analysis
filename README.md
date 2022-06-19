# Amazon_Vine_Analysis

## Overview 

The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Some companies pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.

This project’s purpose was to analyze Amazon reviews written by members of the paid Amazon Vine program. For this purpose, we had access to approximately 50 Amazon product review datasets, each dataset contains reviews of a specific product. [Amazon Review datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt)

Among this dataset, the **"toy product"** reviews dataset was picked and PySpark was used to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. 

After those steps, PySpark was used to determine if there is any bias toward favorable reviews from Vine members in your dataset and a summary of the analysis was presented. 

## Result 



## Summary 





## Sources

**Data Sources** 
* [Amazon Review datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt)
* [SQL table schema](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/challenge_schema%20(2).sql)
* [Amazon ETL starter code](https://github.com/duygusimsek/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL_starter_code%20(2).ipynb)

**Database Management** 
* PostgreSQL
* AWS S3 and RDS
* Google Colab (to run PySpark)
* VS Code 

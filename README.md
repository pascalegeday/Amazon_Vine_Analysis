# Amazon Vine Analysis
# Overview
Analyzing Amazon reviews written by members of the paid Amazon Vine program, using use PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. Additionally, I'll be using PySpark to determine if there is any bias toward favorable reviews from Vine members in the 50 datasets that I was asked to analyze.

# Resources
* Google Colab, Pyspark, Amazon Web Services (AWS) - Relational Database Service (RDS), pgAdmin
* Amazon Review Dataset: https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Music_v1_00.tsv.gz

# Results

# Part 1: ETL
Using PySpark I performed the ETL process to extract the dataset relating to the product category of "US Music" 
I created four separate tables of the data to be able to be able to match the schema and then loaded the tables relative to the ones I created in pgAdmin. 

## Review by ID Table
<img width="1267" alt="Screen Shot 2022-03-16 at 3 02 26 PM" src="https://user-images.githubusercontent.com/94571150/158704826-ca349e2b-a8c9-4786-90fc-d82581200168.png">

## Vine Table
<img width="1058" alt="Screen Shot 2022-03-16 at 3 02 35 PM" src="https://user-images.githubusercontent.com/94571150/158704831-be12c2d7-fb6c-42b7-888a-28843a5a0310.png">

## Products Table
<img width="900" alt="Screen Shot 2022-03-16 at 3 02 20 PM" src="https://user-images.githubusercontent.com/94571150/158704834-f0dd6710-5f48-45a6-9bd1-1d088952fbea.png">

## Customers Table
<img width="1155" alt="Screen Shot 2022-03-16 at 3 02 16 PM" src="https://user-images.githubusercontent.com/94571150/158704839-d794f6d3-741d-4ebb-aa5d-5c123d92bab9.png">

# Part 2: Vine Program Bias
Next, using Pyspark I was able to determine whether or not there was any bias toward favorable reviews (in this case five star reviews) from Vine members. I focused on the Vine Table in order to more easily analyze through meaningful data. 
![Screen Shot 2022-03-16 at 3 45 57 PM](https://user-images.githubusercontent.com/94571150/158705844-0b47de88-c302-48a0-8126-c7913a1fe822.png)

## ETL for More Meaningful Analysis
First, I needed to filter the data and create a new DataFrame or table to retrieve all the rows where the total_votes count is equal to or greater than 20 to pick reviews that are more likely to be helpful and to avoid having division by zero errors later on. 

![Screen Shot 2022-03-16 at 3 46 04 PM](https://user-images.githubusercontent.com/94571150/158705691-e4889639-cb1f-4c45-8239-09846ebf40ad.png)

-------------------------------------------------------------------------

Additionally, I needed to filter the new DataFrame or table created in previously and create a new DataFrame or table to retrieve all the rows where the number of helpful_votes divided by total_votes is equal to or greater than 50%.

![Screen Shot 2022-03-16 at 3 46 12 PM](https://user-images.githubusercontent.com/94571150/158705683-8fbb0a2c-1f01-4726-83f7-ba9ebfdd7aec.png)

-------------------------------------------------------------------------
Then, I created to separated DataFrames or Tables to show the reviews from users who were part of the Vine program and those who were not. 
## Vine Program Users
![Screen Shot 2022-03-16 at 3 46 18 PM](https://user-images.githubusercontent.com/94571150/158705757-4c5d3996-7a50-4da6-919f-e84ffe54ad56.png)

-------------------------------------------------------------------------

## Non-Vine Program Users
![Screen Shot 2022-03-16 at 3 46 24 PM](https://user-images.githubusercontent.com/94571150/158705782-8afa4856-e94a-43a1-af79-6c19b5b6ebc7.png)

-------------------------------------------------------------------------

Finally, in order to determine if there was any bias towards favorable reviews from vine members I determined the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid).


## Total Number of Vine Program Reviews
![Screen Shot 2022-03-16 at 3 46 36 PM](https://user-images.githubusercontent.com/94571150/158706193-35074708-0424-4d6c-836c-c14c1ecdd07f.png)

-------------------------------------------------------------------------

## Total Number of Non-Vine Program Reviews
![Screen Shot 2022-03-16 at 3 46 40 PM](https://user-images.githubusercontent.com/94571150/158706164-1df183bb-a7de-4807-b9f4-361acac9b9e0.png)

-------------------------------------------------------------------------


## Vine Program - Total Number of Five Star Reviews
![Screen Shot 2022-03-16 at 3 46 51 PM](https://user-images.githubusercontent.com/94571150/158706044-dbd6f722-ce46-4f60-a530-28b7c568ce08.png)

-------------------------------------------------------------------------

## Non-Vine Program - Total Number of Five Star Reviews
![Screen Shot 2022-03-16 at 3 46 56 PM](https://user-images.githubusercontent.com/94571150/158705974-2c54b960-f068-404e-bc27-01aa24aaaa5c.png)

## Result Analysis
* There were a total of 7 Vine reviews and 105,979 Non-Vine reviews.
* There were 0 Vine reviews that were 5 stars and 67,580 Non-Vine reviews that were 5 stars.
* 0% percent of Vine reviews were 5 stars and  63% percent of Non-Vine reviews were 5 stars.

# Summary
It is evident that there is no positivity bias for reviews in the Vine program since there were no five star reviews from users who were part of the vine program. We could also retrieve more information about the non-vine program users by analyzing their average star rating. However, there would be no sense in further analyzing the vine program total since there were none. 


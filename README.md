# Customer Profiling & Consumer Value Analysis

---

### Objective

This dataset (mimic of real time data) was shared by an startup (that primarily sell internet proxies) who doesn't have a dedicated analytics practice to get a general sense of the generic inferences one could make with regard to their consumer analytics

![19209](https://user-images.githubusercontent.com/60640107/107474174-7f6aa180-6b37-11eb-9bd4-80a8acf6551f.jpg)

### Table of Contents
You're sections headers will be used to reference location of destination.

- Dataset Description
- Exploratory Data Analysis and Data Visualization
- Customer Segmentation
- Churn Prediction
- Future Work

### Dataset Description

Cancel Table:
1. userid - Fake userids and made them email addresses for this one.
2. orderid - Unique order # for a given purchase. One customer may have many orders.
3. customer_since - Date on which the customer first became a paying customer.
4. country - Home country of the customer.
5. amount - Order amount, which is typically monthly recurring revenue (MRR).
6. Client Status - Current state of customer account. There are three potential values:  Active, Inactive, and Closed.  The latter two are treated the same for this.
7. Order Status - Current state of order. 
8. billingcycle - Indicates whether this is monthly, quarterly, semi-annual, or annual payments.  As noted above on the Amount field, the vast majority of customers pay monthly.
9. product - We have a variety of product types, and I simply made this fake data by converting each to a numeric value. 
10. cancel_date - Self explanatory
11. Cancel Count (45 Days) - Count of an individual customer's orders that were cancelled in the last 45 days.
12. Active Order Count - Quantity of open orders for a single customer.
13. Recurring Amt - A summation of all active order $ amounts for a given customer. It is worth noting that this particular dataset may not have all orders for a customer, so if you sum up the values in the Amount field they are likely not going to total to the Recurring Amt field.
14. Customer Type - Indicates whether this customer ever actually paid us any money.  Many sign up for trials and then do not convert (which is one of the things I am hoping we can dive into deeper to understand why) and these are marked as 'Trial', whereas all those marked as 'Paying' either converted from trials or directly signed up and skipped the trial process.

Package Table:
1. Customer - This correlates to the customer ID in the Cancel table, although you would need to extract it from the email address.
2. Name - See note below. In short, this field has confused me for a while so you can likely disregard much of it. 
3. Category - We sell three types of proxies:  Dedicated (meaning a single customer has use), Semi-dedicated (meaning that multiple customers use the same one, but they get to pay a cheaper price as a result), and Rotating (meaning that they pay a set $ amount, and on a periodic basis that is usually around 10 minutes, they rotate amongst a pool of proxies).
4. Country - Our proxies IP addresses are in data centers throughout the world, so this is the location of that IP address.
5. Type - I'm actually not sure why this field sometimes has a combination of country and category, and usually just says standard.
6. Category - These should have been labeled better.  The first Category field above is from a proxy packages table, and this one in the far right column is from the history table. So for cancellations, this one is going to be the better to use.

[Back To The Top](#Objective)

#### Assumptions:
1. Assuming Terminated and Cancelled status to be the same due to lack of context on dataset to consider them as individual entities.
2. Assuming Closed and Inactive status to be the same due to lack of context on dataset to consider them as individual entities.

### Exploratory Data Analysis and Data Visualization

> Constasting volume of orders and number of customers year on year
![1](https://user-images.githubusercontent.com/60640107/107475896-7af3b800-6b3a-11eb-8316-ed954251d9e2.png)

> Geographic distribution of customers
![Untitled-2](https://user-images.githubusercontent.com/60640107/107475775-47b12900-6b3a-11eb-86ea-104ddfee3c08.png)

> Churn rate of US (Largest consumer base) vs Non US customers
![2](https://user-images.githubusercontent.com/60640107/107476115-d9209b00-6b3a-11eb-9f94-8405d96eb7e9.png)

> Histogram for most popular products
![3](https://user-images.githubusercontent.com/60640107/107476221-053c1c00-6b3b-11eb-996e-0a63de4d677f.png)

> Customer retention of top 10 products
![4](https://user-images.githubusercontent.com/60640107/107476313-36b4e780-6b3b-11eb-8a14-75c9a84c1c6d.png)

> Most popular proxy category
![5](https://user-images.githubusercontent.com/60640107/107476399-606e0e80-6b3b-11eb-8043-69a219be84b8.png)

> Which data centers handle most of the traffic?
![6](https://user-images.githubusercontent.com/60640107/107476561-b2af2f80-6b3b-11eb-8969-cfaee1e727ad.png)

[Back To The Top](#Objective)

### Customer Segmentation

The idea of segmenting customers is to guage the value of the exsisting customers; they were segmented based on the following key attributes:
- Tenure: How long the customer has been with the organization
- Frequency: Number of orders made by a particular customer
- Revenue: The revenue generated by each customer

K-means clustering was used along with the elbow plot to establish the right number of clusters for each of the attributes

![cluysters](https://user-images.githubusercontent.com/60640107/107477810-0fabe500-6b3e-11eb-87a5-9adb89ab04a0.png)

#### Generating an overall score to value customers as High/Medium/Low Value

Each of the attributes were given an equal weightage to calculate a score for "customer value". Ideally, it would be better to take a weighted estimate of each cluster. The scoring may be influenced by a biad or due to insufficiency of data which is causing irregualr clusters in terms of revenue.

![image](https://user-images.githubusercontent.com/60640107/107478153-9f519380-6b3e-11eb-81ea-f735e8795322.png)

![segmentds](https://user-images.githubusercontent.com/60640107/107478422-0ff8b000-6b3f-11eb-98aa-5483a872b67d.png)

[Back To The Top](#Objective)

### Churn Prediction

The objective here is to create a model to classify the Status of a client (Active/Inactive) so that it could be utizlized in the future to assess if an Active customer will potentially become an Inactive one.

Model Used: CatBoost Classifier
Test Score Achieved: 91.5%

> Classification Report

![image](https://user-images.githubusercontent.com/60640107/107478668-7a115500-6b3f-11eb-8c54-a491a5b66c5c.png)

We have a significant number of false positive predictions. We can resolve this by builing models that factor in the imabalance in the data set (by using Cost Sensitive, Data Sampling and Probability Calibration based models) to optimize the classification.

[Back To The Top](#Objective)

### Future Work

1. Conversion rate from trial to paying : Establishing a conversion rate was attempted but only found one order converted. With better and more accurate data, we can determine which products have a high conversion rate.

2. Working with a join on cancel table and package table to identify trends between cancelled orders with respect to package purchases.

*NOTE: Open the .html file to view the plotly visualizations.* 

[Back To The Top](#Objective)

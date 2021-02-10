# Customer Analytics Case Study

---

### Objective

This dataset (mimic of real time data) was shared by an startup (that primarily sell internet proxies) who doesn't have a dedicated analytics practice to get a general sense of the generic inferences one could make with regard to their consumer analytics

![19209](https://user-images.githubusercontent.com/60640107/107474174-7f6aa180-6b37-11eb-9bd4-80a8acf6551f.jpg)

### Table of Contents
You're sections headers will be used to reference location of destination.

- [Dataset Description](#description)
- [Exploratory Data Analysis and Data Visualization](#how-to-use)
- [References](#references)
- [License](#license)
- [Author Info](#author-info)

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
6. Category - Sorry, I should have labeled these better.  The first Category field above is from a proxy packages table, and this one in the far right column is from the history table. So for cancellations, this one is going to be the better to use.

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


*NOTE: Open the .html file to view the plotly visualizations.* 

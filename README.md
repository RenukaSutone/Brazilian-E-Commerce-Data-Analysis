
# Brazilian-E-Commerce-Data-Analysis

In this project, we will analyze customer orders placed between 2016-2018 from sellers on the Brazilian eCommerce platform Olist Store. From this data, we will first determine the number of customers by geographic region (looking at zip code prefix, city, and state), most popular products, number of repeat customers and purchases, and total purchases by date. After data cleaning and initial analysis, we will use machine learning to make predictions on customer behavior, providing sellers on Olist the opportunity to increase sales and customer base.

## Data Source

We chose the Brazilian-eCommerce dataset from Kaggle for our analysis. This dataset contains approximately 100,000 customer orders, along with corresponding files on product information and English translations of product categories originally in Portuguese. Seller names in this dataset were anonymized and replaced with Game of Thrones House names. Nine files from the original Kaggle dataset were chosen for further analysis: olist_geolocation_dataset, olist_customers_dataset, olist_sellers_dataset, olist_product_dataset, olist_order_items_dataset, olist_orders_dataset, olist_order_payments_dataset, olist_order_reviews_dataset and product_category_name_translation.

Data Source: https://www.kaggle.com/olistbr/brazilian-ecommerce
## Data Model
The Entity Relationship Diagram(ERD) below shows the connectivity between the 9 data tables used in our analysis.

![Data Model](https://github.com/user-attachments/assets/faf35492-6039-4802-be6f-cd8004523455)

**The description of these tables is as follows:**
1. **olist_orders_dataset**: This table is connected to 4 other tables. It is used to connect all the details related to an order.
2. **olist_order_items_dataset**: It contains the details of an item that had been purchased such as shipping date, price and so on.
3. **olist_order_reviews_dataset**: It contains details related to any reviews posted by the customer on a particular product that he had purchased.
4. **olist_products_dataset**: It contains related to a product such as the ID, category name and measurements.
5. **olist_order_payments_dataset**: The information contained in this table is related to the payment details associated with a particular order.
6. **olist_customers_dataset**: Details the customer base information of this firm.
7. **olist_geolocation_dataset**: It contains geographical information related to both the sellers and customers.
8. **olist_sellers_dataset**: This table contains the information related to all the sellers who have registered with this firm.
9. **olist_product_category_name_translation**: This table is connected to products database.
## Approach

Success criteria for this analysis stage is to answer the above questions with the available data and information. To archive this the following steps and techniques are applied:
1. Data import and wrangling
2. Exploratory data analysis
3. Time series visualization
4. Linear regression.

**Analysis software and libraries:**
* Python
* NumPy
* Pandas
* Matplotlib
* Plotly
* Seaborn
* scikit-learn
* datetime
* apyori
* re
* waffle
* surprise
## Data preparation
The notebook "olist_analysis" contains a complete procedure of data checks and cleaning. Applied verification methods:

* Missing data check: 3% missing data were substituted with forward fill, 0.05% of missing SKU dimensions were substitured with mean
* Duplicate records: No duplicates found
* Data formats: Date columns were converted to datetime format
## Modelling
For the predictive analysis part linear regression was applied. The date variable was the only input in this analysis. The output (the predicted value) was the total daily order volume (sold units). The predictions were made for a time range from 2017 to 2020. The date format needed to be translated to a numberical format to satisfy the underlying math. The predictions were added as a new column to the data table and visualized in the same time series chart as the original data. R2-scores calculated the accuracy of the model. To increase the prediction accuracy ourliers were removed from the data.
## Exploratory Data Analysis
Goal: getting insights around order composition and customer buying habits.

1. **Top customers**:There are a few customers which come back to place orders again but given the large range of customers overall and average user is only placing a small amount or orders.

2. **Top categories**:There are 73 product categories in which the first third represent the majority of the order volume.

  **Matrix factorization to find category similarities**
  Matrix factorization is used in a small function with the goal to calculate distance (similarity) between categories. The method is based on 
  comparing all ordered product categories in an order to all other orders. The greater the overlap between the orders the greater the similarity. 
  This method is also used in recommender functions to identify similar customers based on the shopping history.

3. **Order profile**:The orders are generally small, as expected for e-commerce. Very few orders have more than one SKU. 79% SIO (single-item-orders), 93% SLO (single-line-orders).

4. **Pareto chart**:The pareto chart shows almost the typically expected 80/20 profile. That means, there is a good distinction between the product's velocities. Under under circumstances this would be a base for a clever product allocation to different pick methods and technologies in a warehouse.

5. **SKU classification**:The ABC classes explain how frequently an item was picked in the observed time period. It shows that that there is no SKU ranked as X-mover and only some very few as Y. This is an extreme instance and shows that the SKUs are in general very infrequently picked.

6. **Customers resident location**:Customers live in 4,119 unique cities in 27 unique states.
The imbalanced distribution accross cities and states need to be kept in mind when drawing conclusions of statistical nature.There are 14,994 unique zip code prefixes.

7. **Customers joining date**:The date of the first order is assumed to be the user sign-up date.
Many new cutomers appeared on Black Friday. It is interesting to see that the impact is not very pronounced when looking at the cumulative customer count for the total time span. Overall, the increase of customers has an upward trend. The trendline is slightly exponential, which means that the growth is accelerating slowly.



## Recommendation System
**Problem:** 
* A well-known customer success law, the Pareto principle says that repeat customers generate revenue that is nearly 16 times more efficient than one-time customers. The potency of 80/20 is that 20 percent of a group is responsible for 80 percent of the sales. It also can be 85 / 20 or 66 / 10. In other words, the majority of the results (or outputs) are almost always caused by only a few inputs.
* A stunningly similar trend outlining a shift from selling a few hits in huge volumes toward selling numerous niche items, each of them in relatively small amounts.
* Though digital shelf space is unlimited, consumers’ time and attention remain finite, so creators have to spend more and more resources to try to stand out.

**Objective:**
Build recommendation system to increase sales by give suggestion products with purposes to reduce browsing time and make the customer purchase faster.

**Solution:**
* Customers demand personalization: Modern customers are becoming more interested in products and services that seem unique and fit their individual needs and tastes, creating more demand for a greater number of more unique items.
* The astounding thing is that if one has enough user-to-product data (ratings, purchases, etc…), then no other information is necessary to make decent recommendations. This is quite different than regression and classification problems where one must explore various features in order to boost a model’s predictive powers.

Hence, by implementing a recommendation system that maintain customer retention and encourages repeat purchases, the likelihood of generating higher revenue increases significantly.
## Conclusion
The analysis reveals three key problems for the Olist. Firstly, a significant 80% of transaction value is generated from only 17 categories of products (20%), indicating there’s still potential products in the remaining 55 categories. Secondly, there is a urgent issue with bad ratings in the top 17 categories, which may lead to customer dissatisfaction and impact customer retention. Thirdly, there’re still 78% first-time customer that bought 1 product instead of repeat customer that bought 2–3 products

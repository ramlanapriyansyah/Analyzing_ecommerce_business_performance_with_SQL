# Overview
Measuring business performance is crucial to track, monitor, and evaluate business processes in a company. In this paper, we will analyze the business performance of an e-commerce company by analyzing several business metrics such as customer growth, product quality, and payment type.

# Tools dan Dataset
Dataset can be seen here: [dataset](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/tree/main/dataset) </br>
Tools: PostgreSQL through DBeaver

# Data Preparation
The things done in the Data Preparation stage are as follows:
1. **Import Dataset**. Importing data from customers, geolocation, order_items, order_payments, order_reviews, orders, products, and sellers tables into RDBMS.
2. **Add Constraint**. Adding Primary Key and Foreign Key to create Entity Relationship Diagram (ERD) below.
![ERD (1)](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/assets/135192484/1c7c2192-e884-4634-92d8-749b31e442ef)

The syntax of queries to add Primary Key and Foreign Key can be seen here: [data_preparation.md](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/blob/main/data_preparation.md)

# Annual Customer Activity Growth Analysis
In this step, we conduct an analysis of annual customer activity by creating a master table that consists of these features: 
- Monthly_active_user: Average of total monthly active users per year.
- New_customer: Total new customers per year.
- Customer_with_repeat_order: Total customers who order more than once for each year.
- Average_order: Average of total orders per customer per year.
  
![customer_activity_table](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/assets/135192484/a6ca84da-30a0-491e-a1b9-371595ad049e)

The Annual Customer Activity Growth table is a result of extraction from several tables through these queries: [annual_customer_activity_growth.md](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/blob/main/annual_customer_activity_growth.md)
### Findings
1. The average number of monthly active users has increased from year to year. Starting from 109 customers in 2016, it increased rapidly to 3,758 in 2017, then continued to increase to a total of 5,401 customers in 2018.
2. The number of customers has grown significantly. The total of new customers increased rapidly from just 329 in 2016 to 45,101 in 2017. And continued to increase to 54,011 new customers in 2018.
3. The total number of customers who repeat orders increased from 3 customers in 2016 to 1,256 customers in 2017. Then it slightly decreased in 2018 to 1,167 customers. 
4. In general, the average number of orders every year was quite stagnant. It can be seen that the average order placed by a customer is never more than 1 order from year to year.

# Annual Product Category Quality Analysis
At this stage, the quality of the annual product category is analyzed through the creation of a master table with the following information:
  Total_revenue: The company’s total revenue per year.
  Cancel_order: Total canceled orders per year.
  Top_product_category: Product category with the highest revenue per year.
  Most_cancel_order_category: Product category with the highest canceled orders.

  ![product_category_table](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/assets/135192484/a52726a2-0ade-4c22-b12e-6d75970e5a5e)

The Annual Product Category Quality table above is generated with the query as attached in this file: [annual_product_category_analysis.md](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/blob/main/annual_product_category_analysis.md)
### Findings
1. The company's total revenue increased sharply, from just under 1 million in 2016 to 6.92 million in 2017, and continued to increase to 8.45 million in 2018.
2. On the one hand, the total canceled orders experienced by the company also continued to increase every year. From 26 canceled orders in 2016, to 265 in 2017, and increased again to 334 in 2018.
3. In 2016, the product category with the highest revenue was furniture_decor with a total revenue of 6,899. In 2017, the highest revenue was owned by the bed_bath_table category, with a total revenue of 580,946. And in 2018 the highest revenue is owned by the health_beuaty category, with a total revenue of 866,812.
4. In 2016, the toys category had the highest number of canceled orders, totaling 3. In 2017, the sport_leisure category took the lead with 25 canceled orders. By 2018, the health_beauty category topped the list with 27 canceled orders.

# Analysis of Annual Payment Type Usage
At this stage, a table is created that contains information about the use of payment types for each year as shown in the following table:

![annual_payment_type_usage_table](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/assets/135192484/edd6d16c-8cf5-4925-902b-1c6409e92240)


The queries can be seen here: [annual_payment_type_usage.md](https://github.com/ramlanapriyansyah/Analyzing_ecommerce_business_performance_with_SQL/blob/main/annual_payment_type_usage.md)

### Findings
1. The all-time favorite payment type is credit_card payment, with 76,800; followed by boleto with 19,800; voucher with 5,800; and debit_card with 1,500. The other payment types are just under 100.
2. The credit_card payment type itself has an average installment of 3-4 times in each year.







# E-commerce Data Analysis

## Project Overview

This project analyzes the **Brazilian E-Commerce Public Dataset by Olist** to extract insights on customer behavior, top products, company performance, delivery efficiency, and customer satisfaction.

## Dataset

The dataset contains multiple tables:

* **Orders** – information about customer orders and timestamps.
* **Order Reviews** – customer feedback on orders.
* **Products** – product details and categories.
* **Sellers** – seller information.
* **Customers** – customer demographics.
* **Items Ordered** – individual items in each order.

## Analysis Questions

The project aims to answer the following key questions:

1. **Customer-Seller Analysis**

   * Who are the **highest-spending customers** and which sellers do they prefer?

2. **Company-Category Analysis**

   * What is the **most frequently purchased product category in 2018** for the top companies?
   * Which **products are top-selling** for the highest-value customers?

3. **Revenue Analysis**

   * Which **product category generated the highest revenue each year**?

4. **Delivery Time Analysis**

   * Which **product categories have the fastest delivery times** and how does this vary annually?

5. **Review & Satisfaction Analysis**

   * Which **product categories are most rated each month**?
   * Is there a correlation between **delivery times and review scores**?
   * How do review scores reflect **overall customer satisfaction**?

---

## Analysis Steps

1. **Customer Analysis**

   * Identify top customers by total purchase value.
   * Visualize customer-company interactions using scatter plots or cross-tabulations.

2. **Company and Product Analysis**

   * Determine top companies by sales per year.
   * Analyze top-selling products for each company.
   * Identify the most purchased product categories per top company.
   * Visualize sales distribution using bar charts and scatter plots.

3. **Delivery Analysis**

   * Calculate delivery times in days.
   * Group data by purchase month and category to calculate mean review score and mean delivery time.
   * Identify the most rated categories each month.
   * Visualize trends using line plots or dual-axis charts.

4. **Category Performance**

   * Aggregate total sales by product category and year.
   * Highlight top revenue-generating categories.
   * Visualize trends using stacked bar charts.

5. **Review Analysis**

   * Measure mean review score per product or category to evaluate customer satisfaction.
   * Correlate review scores with delivery times.
   * Identify top-rated products and trends in customer feedback over time.

---

## Visualizations

* Scatter plots for customer-company interactions.
* Stacked bar charts for top customers by category.
* Bar charts for fastest delivery categories.
* Line plots for review score and delivery time trends per month.
* Dual-axis charts for comparing review score vs delivery speed.

## Tools & Libraries

* Python 3
* Pandas, NumPy
* Matplotlib, Seaborn
* Google Colab

## Key Insights

* Top customers and their preferred sellers.
* Companies generating the highest sales per year.
* Most frequently purchased categories per top company in 2018.
* Product categories with the fastest delivery times per year.
* Top-rated products and categories each month, including trends in customer satisfaction.
* Correlation between delivery times and review scores.

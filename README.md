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

### Analysis Question 
1. d
* Steps

### Code
* ```

## Questions
1. Who are the **highest-spending customers** and which sellers do they prefer?
  *Merge the tables to create a unified dataset for all analyses.
  *Identify the top customers by grouping data by customer_name, aggregating total sales per customer, 
    and sorting in descending order to select the top 10.
  *Filter the merged dataset to retain only records corresponding to the top customers.
  *Group the filtered data by customer name to account for multiple orders from the same company, 
   ensuring a clear view of customer-company relationships.
  *Visualize the relationships using a cross-tabulation to show which customers are associated with which companies.
  *Use a scatter plot to present the customer-company interactions in a clear and quickly understandable way.
- The code

```
merged_data = (
        orders_df.merge(items_order_df,on="order_id",suffixes=["_order","_items"])
        .merge(sellers_df,on="seller_id",suffixes=["_orders_merge","_sellers"])
        .merge(products_df,on="product_id",suffixes=["","_products"])
        .merge(customers_df,on="customer_id",suffixes=["","_customers"])
        .merge(product_english_name_df,on="product_category_name",suffixes=["","_naming"])
)

top_customers = (

                merged_data
                .groupby(["customer_unique_id"])["price"]
                .sum()
                .sort_values(ascending=False)
                .head(10)
                .index
)
top_companies_customers = (
      merged_data.loc[merged_data["customer_unique_id"].isin(top_customers)]\
     [["customer_unique_id","company_name","customer_name"]]\
     .groupby("customer_name",as_index=False)["company_name"]\
     .unique()
)

top_companies_customers["company_name"] = top_companies_customers["company_name"].apply(lambda x: ", ".join(x))
top_companies_customers

merged_data.head(1)

# Visualize the data using a cross-tabulation to highlight the 
# relationships between customers and companies.
pd.crosstab(
    top_companies_customers["company_name"],
    top_companies_customers["customer_name"]
    )

# Visualize the customer-company relationships using a scatter plot 
# for a clear and intuitive representation.
sns.scatterplot(data=top_companies_customers,x="company_name",y="customer_name",s=100,hue="company_name")
plt.title("Number of Top Customers per Company")
plt.legend().set_visible(False)
plt.ylabel("Number of Customers")
plt.xlabel("Company")
plt.xticks(rotation=45)
plt.show()

 ```
![companies per top customers](/images/companies_per_top _customers.PNG
)

### Insights 
Brent Jackson and Johnny Lee appear twice, meaning these companies serve multiple top customers. 
✅ Insight: Some companies have higher engagement with top customers — could be key accounts.

Most other customers are linked to a single company. 
✅ Insight: Many top customers stick to one company, suggesting loyalty or strong preference.

Companies that serve multiple top customers (Brent Jackson, Johnny Lee) may be important revenue sources.

🎯 Strategy: Focus on these companies for retention, upselling, or special offers.

### 2. What is the **most frequently purchased product category in 2018** for the top companies?
* Steps
   * Identify the top companies for 2018:
   * Filter the dataset to include only purchases from the year 2018.
   * Group the data by company_name and aggregate by counting order_id to determine total sales per company.
   * Sort the results in descending order to rank companies by sales and select the top 5 companies.
   * Save the result in top_company_2018.
   * Analyze top products for these companies:
   * Filter the merged dataset to include only records corresponding to the top 5 companies.
   * Group the data by company_name and sort by total sales in descending order.
   * For each company, select the top-selling product to identify the key product driving sales.
 #### Code
 ```  
 top_company_2018 = (
                     merged_data[merged_data["purchase_year"]==2018]
                    .groupby("company_name")["order_id"]
                    .count()
                    .sort_values(ascending=False)
                    .head(5)
)
most_purchased_category_2018 = (
                    merged_data[merged_data["company_name"].isin(top_company_2018.index)]
                    .groupby(["company_name","product_category_name_english"])
                    .agg(orders_count= ("order_id","count"))
                    .sort_values("orders_count",ascending=False)
)
most_purchased_category_2018.groupby("company_name").head(1)

# Visualize the  Top Products Fpr Top Customers 
most_purchased_category_2018=(
    most_purchased_category_2018.
    groupby("company_name")
    .head(1)
)

sns.barplot(
    most_purchased_category_2018,
    x="company_name",
    y="orders_count",
    hue="product_category_name_english"
)

plt.ylabel("Number of Orders per Category")
plt.xlabel("Company Name")
plt.xticks(rotation=45,ha="right")
plt.title("Top products for Top Companies")
plt.legend(title="Category",loc="upper right")
plt.show()
```
![companies per top customers](C:\Users\Mousa\Documents\_Data_Analysis_Projects\brzilian ecommerce\photo analysis\Top Products for Top Companies)
#### Insights 
* Each top company appears to focus on a different product category, showing clear specialization. Benjamin Jordan → watches_gifts        Dorothy Luna → bed_bath_table Shawn Riley → furniture_decor
* Companies can optimize inventory and marketing based on their strongest category.
* Identifies opportunities for cross-promotion if a company wants to expand into categories where competitors lead.
* Each company’s most purchased category reflects what consumers prioritize per brand, useful for trend analysis.
  











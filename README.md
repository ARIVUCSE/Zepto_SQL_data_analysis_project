🛒 Zepto Data Analysis using PostgreSQL

📌 Project Overview

This project is based on analyzing **Zepto product data** using **PostgreSQL**.
It focuses on **data exploration, cleaning, and extracting business insights** from an e-commerce dataset

📂 Dataset Details

The dataset was sourced from Kaggle and was originally scraped from Zepto’s official product listings. It mimics what you’d typically encounter in a real-world e-commerce inventory system.

Each row represents a unique SKU (Stock Keeping Unit) for a product. Duplicate product names exist because the same product may appear multiple times in different package sizes, weights, discounts, or categories to improve visibility – exactly how real catalog data looks.

The dataset contains product-level information such as:

* SKU ID
* Category
* Product Name
* MRP (Maximum Retail Price)
* Discount Percentage
* Available Quantity
* Discounted Selling Price
* Weight (in grams)
* Stock Availability

🛠️ Technologies Used

* PostgreSQL
* SQL (DDL, DML, Aggregations, Case Statements)

⚙️ Database Setup

Step 1: Create Table

    
    create table zepto (
    sku_id SERIAL PRIMARY KEY,
    category varchar(120),
    name varchar(150) NOT NULL,
    mrp numeric(8,2),
    discountPercent numeric(5,2),
    availableQuantity integer,
    discountedSellingPrice numeric(8,2),
    weightInGms integer,
    outOfStock boolean,
    quantity integer
    );

🔍 Data Exploration

* Count total records
* View sample data
* Check null values
* Identify unique product categories
* Analyze stock availability

 🧹 Data Cleaning

* Removed invalid records where MRP = 0
* Converted price from **paise to rupees**

```sql
update zepto 
set mrp = mrp/100.0,
    discountedSellingPrice = discountedSellingPrice/100.0;
```

📊 Key Analysis & Insights

🔹 Top Discounted Products

    * Identified products with highest discount percentages

🔹 High Value Out-of-Stock Products

    * Found expensive products that are unavailable

🔹 Revenue Estimation

```sql
select category,
sum(discountedSellingPrice * availableQuantity) as total_revenue
from zepto
group by category;
```
🔹 Best Value Products

    * Calculated **price per gram** to find cost-effective items

🔹 Category-wise Discount Analysis

    * Found top categories offering highest average discounts

🔹 Product Weight Classification

Products are categorized as:

* Low (< 1000g)
* Medium (< 5000g)
* Bulk (> 5000g)

📈 Business Insights

* Categories with highest revenue potential
* Products offering best value for money
* Stock availability trends
* Discount patterns across categories

🚀 How to Run

1. Open PostgreSQL / pgAdmin
2. Run the SQL script
3. Execute queries step by step
4. Analyze results







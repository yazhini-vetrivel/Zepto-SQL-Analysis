# Zepto-SQL-Analysis

## 🛠️ Project Execution Flow

### 1. Database Setup

Initialized the project by designing and creating the main SQL table with suitable column types for storing product-related information.

```sql
CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);
```

---

### 2. Dataset Import & Configuration

Imported the CSV dataset into PostgreSQL using pgAdmin’s import utility.

For environments where direct import was unavailable, the dataset was loaded using the following command:

```sql
\copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv'
WITH (
    FORMAT csv,
    HEADER true,
    DELIMITER ',',
    QUOTE '"',
    ENCODING 'UTF8'
);
```

During the import process, UTF-8 encoding conflicts were encountered and resolved by re-saving the dataset in **CSV UTF-8** format.

---

### 3. Initial Dataset Analysis

Performed exploratory analysis to better understand the structure and quality of the dataset:

* Calculated the total number of product entries
* Previewed sample records for schema understanding
* Inspected columns for missing or null values
* Extracted unique product categories
* Evaluated stock availability distribution
* Identified duplicate product names associated with different SKUs

---

### 4. Data Preprocessing

Cleaned and standardized the dataset to improve analysis accuracy:

* Removed records containing zero values in MRP or selling price
* Converted price-related columns from paise to rupees for consistency
* Ensured cleaner and more readable pricing data

---

### 5. Analytical Insights & Reporting

Executed multiple business-focused SQL analyses to generate meaningful insights:

* Retrieved top discounted products based on savings percentage
* Detected premium products currently marked as out of stock
* Estimated category-wise potential revenue
* Filtered high-priced products with low discount margins
* Ranked categories offering the highest average discounts
* Computed price-per-gram metrics for value comparison
* Segmented products into weight-based groups (Low, Medium, Bulk)
* Measured overall inventory weight across categories

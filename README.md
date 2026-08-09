# RUSH Sales Data Analysis and Predictive Modeling

## Project Overview
This project analyzes sales data for **RUSH**—a global sportswear and footwear brand known for innovative designs—to identify key sales trends, actionable insights, and opportunities for business growth. The workflow spans data cleaning, exploratory data analysis (EDA), visualization, feature engineering, and preparation for predictive modeling.

---

## Data Sources
The analysis utilizes three main relational datasets:
* `TABLE_PRODUCTS_885.csv`: Product catalog and details.
* `TABLE_RETAILER_885.csv`: Retailer profiles and metadata.
* `TABLE_SALES_885.csv`: Transactional sales records.

---

## Methodology

### 1. Data Loading & Merging
* All three datasets were loaded into Pandas DataFrames and merged into a consolidated dataset (`rush_sales_dt`) using primary key identifiers (`RETAILER_ID` and `PRODUCT_ID`).

### 2. Data Cleaning & Preprocessing
* **Column Cleanup**: Removed redundant ID columns (`RETAILER_ID`, `PRODUCT_ID`) after merging.
* **Data Type Conversion**: Converted `INVOICE_DATE` to standard `datetime` objects and coerced `UNITS_SOLD` into numeric types.
* **Missing Value Imputation**: Imputed missing `PRICE_PER_UNIT` values using the mode grouped by `PRODUCT_NAME`. Remaining rows with missing essential fields (`UNITS_SOLD`, `RETAILER`, `REGION`, `STATE`, `CITY`) were dropped.
* **Outlier & Anomaly Removal**: Filtered out invalid transactions where `UNITS_SOLD` equaled `0`. Handled numerical outliers via Winsorization (clipping values at the 5th and 95th percentiles).
* **Feature Calculation**: Engineered a direct `SALES` feature using:
  $$\text{SALES} = \text{UNITS\_SOLD} \times \text{PRICE\_PER\_UNIT}$$

### 3. Exploratory Data Analysis (EDA)
Summary statistics and correlation matrices were generated to uncover key business insights:
* **Highest Sales Product Category (2021)**: *Men's Street Footwear* ($23,283,356.00)
* **Top State for Women's Product Sales (2021)**: *Maine* ($2,176,301.00)
* **Top State for Men's Product Sales (2021)**: *Maine* ($4,393,491.00)
* **Retailers with Most Units Purchased**: 
  * **2021**: *Foot Locker* (1,097,410 units)
  * **2020**: *Amazon* (317,930 units)

### 4. Data Visualization
* **Sales Distribution**: Histograms visualizing total revenue and unit sales distribution.
* **Geospatial Analysis**: Choropleth maps highlighting 2021 product performance across U.S. states using state abbreviations.
* **Comparative Retailer Analysis**: Grouped bar charts contrasting year-over-year retailer volume (2020 vs. 2021).


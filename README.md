# **E-Commerce Sales and Delivery Performance Analysis Using Power BI**

**Team Members:**

* Arlen Ngahu - Power Query Data Preparation and Transformation
* Brad Ochola - DAX Measures and Calculations
* Andy Hadulo - Dashboard Design and Visualisations
* Nicholas Kinyanjui - Dashboard Design and Visualisations
* Nathan Omenge - Data Modelling
* Allan Mutugi - README & Documentation

**Class:** Business Organisation and Data Visualisation Course - DSA3050A
**Semester:** Spring 2026


## Project Overview

In this project, we analyzed an e-commerce dataset to understand sales performance, customer distribution, and delivery efficiency. The goal of the analysis was to transform raw transactional data into meaningful insights that can support business decision-making.

Using Microsoft Power BI, we cleaned and prepared the dataset, built a structured data model, and created interactive dashboards that highlight key business metrics such as revenue trends, regional sales performance, product category demand, and delivery timelines.

The project workflow consisted of several major stages:

1. **Data Preparation (Power Query)** – Cleaning, merging, and transforming the raw data.
2. **Data Modeling** – Establishing relationships between tables to support analysis.
3. **Feature Engineering** – Creating calculated columns and measures for key metrics.
4. **Data Visualization** – Building dashboards that communicate insights effectively.

Through this process, the project demonstrates how **business intelligence tools can be used to convert raw data into actionable insights** for monitoring operational performance and identifying opportunities for improvement.


## Tools Used

* **Microsoft Power BI**
* **Power Query**
* **DAX (Data Analysis Expressions)**


## Dataset Description

The dataset used in this project contains transactional information from an e-commerce platform.The data comes from the **Brazilian E-commerce Public Dataset by Olist**, available at: [Brazilian E-commerce Dataset - Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) 
It includes multiple related tables covering:

* Customer information
* Orders
* Order items
* Product details
* Payment information
* Delivery timestamps
* Geographic data

These tables were merged and transformed during the **Power Query data preparation stage** to create a structured dataset suitable for analysis.


## Project Sections

| Team Member | Objectives | Deliverables |
|---|---|---|
| Arlen Ngahu | Power Query Data Preparation and Transformation | Cleaned and transformed raw CSV datasets; merged multiple relational tables; standardized data types; created derived columns for delivery metrics and regional groupings; prepared dataset for analysis |
| Brad Ochola | DAX Measures and Calculations | Created DAX measures for total payments by payment type; developed calculated columns for product volume; built aggregated measures for total volume per product; enabled complex business logic calculations |
| Andy Hadulo & Nicholas Kinyanjui| Dashboard Design and Visualizations | Designed interactive Power BI dashboards; created visual representations of key metrics; built user-friendly reports for stakeholders; implemented drill-down capabilities for detailed analysis |
| Nathan Omenge | Data Modeling | Established relationships between tables; designed star schema structure; optimized data model for performance; ensured data integrity across all dimensions and fact tables |
| Allan Mutugi | README & Documentation | Created comprehensive project documentation; documented all transformation steps; provided detailed explanations of methodology; ensured project clarity for stakeholders |


---
## Power Query Data Preparation and Transformation
Arlen Ngahu - 667855


In this stage of the project, I used **Power Query in Microsoft Power BI** to clean, transform, and prepare the raw e-commerce dataset for analysis. Although the dataset was relatively structured, I still performed several transformations to ensure that the data model was consistent, reliable, and suitable for analytical reporting. Each transformation step is documented below.



## 1. Loading the Raw Dataset

I started by importing the raw CSV datasets into Power BI. These included the core transaction dataset and the related tables used to enrich it.

After loading the files, I opened **Power Query Editor** and inspected the structure of each table to understand the available columns, data types, and potential issues such as missing values or inconsistent formats.

![alt text](Screenshots/image-2.png) ## Loading the data
![alt text](Screenshots/image.png) ## Kaggle Dataset
![alt text](Screenshots/image-1.png) ## How it looks in Power BI
![alt text](Screenshots/image-3.png) ## Loading the data


## 2. Data Cleaning and Standardization

Before proceeding with further transformations, I performed several basic data cleaning steps to ensure the dataset was consistent and free from formatting issues.

First, I applied **Trim** and **Clean** transformations to relevant text columns. The **Trim** function removed any leading or trailing spaces that could cause inconsistencies when grouping or filtering data, while the **Clean** function removed non-printable characters that sometimes appear in imported datasets.

Next, I standardized text formatting by applying **Capitalization** (using the *Capitalize Each Word* option) to selected columns such as product categories and other descriptive fields. I decided to do this to ensure that the text values appear consistent and professional when used in reports and visualizations.

Finally, I reviewed all columns in the merged dataset and removed any **unnecessary or redundant columns** that were not required for analysis. This helped simplify the dataset, reduce model size, and improve overall performance when building the Power BI report.

These cleaning steps ensured that the dataset was well-structured, consistent, and ready for further transformation and analysis.

![alt text](Screenshots/image-27.png) ## Cleaning
![alt text](Screenshots/image-28.png) ## Trimming
![alt text](Screenshots/image-29.png) ## Capitalizing each word

![alt text](Screenshots/image-32.png) ## Removing unnecessary columns


## 3. Merging Related Tables

Because the original data was stored across several relational tables, I decided to merge them into a single enriched analytical table. I used **Merge Queries** in Power Query to join the tables using their key fields.

I began with the **order items table** as the base table because it represents the most granular transaction level (each row corresponds to a product in an order).

I then merged the following tables:

* Orders table (joined using `order_id`)
* Products table (joined using `product_id`)
* Customers table (joined using `customer_id`)
* Payments table (joined using `order_id`)

For each merge operation, I used a **Left Outer Join** so that all records from the base table were preserved.

After performing the joins, I expanded only the columns necessary for analysis, such as order timestamps, product categories, customer location information, and payment details.

![alt text](Screenshots/image-4.png) ## Olist_order_items merged with Olist_orders
![alt text](Screenshots/image-5.png) ## Olist_order_items merged with Olist_products 
![alt text](Screenshots/image-6.png) ## Olist_order_items merged with Olist_customers
![alt text](Screenshots/image-9.png) ## Olist_order_items merged with Olist_order_payments

![alt text](Screenshots/image-7.png) ## expanding olist_orders
![alt text](Screenshots/image-8.png) ## expanding olist_products
![alt text](Screenshots/image-10.png) ## expanding olist_customers
![alt text](Screenshots/image-11.png) ## expanding olist_order_payments


## 4. Renaming Columns for Clarity

After merging the tables, I noticed that several column names were long or not immediately intuitive for analysis. I decided to rename them to improve clarity and readability.

Examples of renaming include:

* `order_purchase_timestamp` → `Order_Date`
* `product_category_name` → `Product_Category`
* `payment_value` → `Payment_Amount`

This step ensures that the dataset is easier to understand when building visualizations and writing DAX measures later in the project.

![alt text](Screenshots/image-12.png) ## renamed to order_date


## 5. Correcting Data Types

Next, I verified and corrected the data types of all columns to ensure consistency.

For example:

* Date columns were converted to **Date/Time**
* Price and payment columns were converted to **Decimal Number**
* Categorical attributes such as product category and customer state were set to **Text**

Correct data types are important because they allow Power BI to perform calculations correctly and avoid errors during analysis.

![alt text](Screenshots/image-13.png) ## changed from Date/Time to Date
![alt text](Screenshots/image-34.png) ## changed from any to text


## 6. Removing Duplicate Records

To maintain data integrity, I checked for duplicate rows in the dataset.

I removed duplicates using the combination of:

`order_id + order_item_id`

This ensured that each row in the dataset represents a unique item within an order.

Removing duplicates prevents inaccurate calculations in measures such as total sales or total orders.

![alt text](Screenshots/image-14.png) ## removing duplicate records


## 7. Handling Missing Values

During inspection, I noticed that some delivery-related fields contained missing values.

Instead of replacing these values arbitrarily, I decided to create a **Shipping Status** indicator column. This column classifies each order based on whether a delivery date exists.

The logic used was:

* If the delivery date is null → "Not Delivered"
* Otherwise → "Delivered"

This approach preserves the original data while still enabling meaningful analysis of delivery performance.

![alt text](Screenshots/image-16.png) ## Creating the conditional column
![alt text](Screenshots/image-15.png) ## Shipping_Status column


## 8. Creating Delivery Time Metrics

To enable delivery performance analysis, I created a custom column to calculate the number of days between the order purchase date and the actual delivery date.

This column calculates the **delivery duration in days**, which will later be used in dashboard visuals and KPI calculations.

![alt text](Screenshots/image-17.png) ## Creating the custom column
![alt text](Screenshots/image-18.png) ## Delivery_days column


## 9. Extracting Date Components

To support time-based analysis, I extracted several components from the order purchase date.

The following columns were created:

* Year
* Month Number
* Month Name
* Quarter
* Day Name

These fields allow the dashboard to analyze trends such as monthly sales patterns and quarterly performance.

![alt text](Screenshots/image-21.png) ## Inserted year
![alt text](Screenshots/image-22.png) ## Year column
![alt text](Screenshots/image-23.png) ## Inserted month column
![alt text](Screenshots/image-24.png) ## Inserted month name
![alt text](Screenshots/image-25.png) ## Inserted quarter
![alt text](Screenshots/image-26.png) ## Inserted day


## 10. Creating Regional Groupings

The dataset included customer locations at the **state level**, which can be too granular for some business insights. To simplify geographic analysis, I created a new **Region** column that groups states into Brazil’s major geographic regions.

For example:

* SP, RJ, MG, ES → Southeast
* PR, RS, SC → South
* BA, PE, CE, etc. → Northeast

This transformation enables higher-level geographic comparisons such as **sales by region** and **delivery performance by region**.

![alt text](Screenshots/image-20.png) ## Creating the conditional column
![alt text](Screenshots/image-19.png) ## Region column


## 11. Creating Additional Analytical Columns

Finally, I created additional derived columns that help support business metrics used later in the dashboard.

Examples include:

* **Order Total** (product price + freight value)

These calculated columns enhance the dataset by introducing metrics that directly relate to operational and financial performance.

![alt text](Screenshots/image-30.png) ## Custom column creation
![alt text](Screenshots/image-31.png) ## Order_total column


## Summary of Power Query Transformations

Through the Power Query process, I completed several key data preparation steps:

* Merged multiple relational tables
* Renamed columns for clarity
* Corrected data types
* Removed duplicate records
* Handled missing values
* Created delivery performance metrics
* Extracted date components
* Grouped customer states into regions
* Generated additional analytical columns

These transformations ensured that the dataset was clean, structured, and ready for **data modeling, DAX calculations, and dashboard development** in the subsequent stages of the project.

## This photos basically follow a trend, we are going through the columns and swiping down on the query settings to show the work done.

![alt text](Screenshots/image-33.png)
![alt text](Screenshots/image-35.png)
![alt text](Screenshots/image-36.png)
![alt text](Screenshots/image-37.png)
![alt text](Screenshots/image-38.png)
![alt text](Screenshots/image-39.png)

---

## Data Modelling
Nathan Omenge - 670637

**Overview**
The modeling stage transforms the cleaned Power Query output into a structured star schema suitable for DAX calculations and dashboard development in Power BI.


## 2. Star Schema Design Rationale

The model follows a standard star schema pattern with one central fact table surrounded by six dimension tables. This design was chosen because it:

1. Optimises query performance in Power BI
2. Enables clean DAX measure writing without ambiguous filter paths
3. Supports time intelligence functions through a dedicated date dimension
4. Meets the project rubric requirement for star schema implementation


## Relationship Configuration

All ambiguous auto-detected relationships through the olist_orders_dataset raw table were deleted. Six clean active relationships were then created following the standard star schema pattern of many-to-one (*:1) with single cross-filter direction from dimension to fact:

| From (Fact) | Column | To (Dimension) | Cardinality | Status |
|-------------|--------|----------------|-------------|--------|
| FactTable | customer_id | DimCustomers | Many to one | Active |
| FactTable | Order_Date | DimDate | Many to one | Active |
| FactTable | order_id | DimPayments | Many to one | Active |
| FactTable | product_id | DimProducts | Many to one | Active |
| FactTable | review_id | DimReviews | Many to one | Active |
| FactTable | seller_id | DimSellers | Many to one | Active |

**Note:** DimReviews required duplicate removal on the review_id column in Power Query before the relationship could be established, as Power BI requires unique values on the one side of a many-to-one relationship.


## Foreign Key Column Management

Foreign key columns in both the FactTable and dimension tables were hidden from report view. These columns are used only for joining tables and should not appear in the Fields pane for report builders.

**Hidden in FactTable:** customer_id, product_id, seller_id, order_id, review_id

**Hidden in Dim tables:** The corresponding primary key column in each dimension table was also hidden.


## Model Validation Checklist

The completed star schema model meets all rubric requirements for the data modeling stage:

1. Star schema implementation with FactTable at the center
2. One fact table (FactTable) and six dimension tables
3. Dedicated Date dimension (DimDate) created using DAX
4. Clean relationship design with correct many-to-one cardinality
5. Single cross-filter direction on all relationships
6. DimDate marked as the official Date Table for time intelligence
7. Foreign key columns hidden from report view
8. Model view arranged in a professional star schema layout
9. Unused raw tables hidden from report view


## Tools and Techniques Used

1. Microsoft Power BI Desktop
2. Power Query Editor (for DimPayments aggregation, DimSellers rename, DimProducts merge, DimReviews deduplication)
3. DAX (for DimDate creation using ADDCOLUMNS and CALENDAR functions)
4. Model View (for relationship building and layout arrangement)
5. Table Tools (for marking DimDate as official Date Table)


## Table Summary

| Table | Type | Row Count | Primary Key | Joins To |
|-------|------|-----------|-------------|----------|
| FactTable | Fact | 95,122 | - | All Dims |
| DimCustomers | Dimension | 99,441 | customer_id | FactTable |
| DimProducts | Dimension | 999+ | product_id | FactTable |
| DimSellers | Dimension | 999+ | seller_id | FactTable |
| DimPayments | Dimension | 999+ | order_id | FactTable |
| DimReviews | Dimension | 999+ | review_id | FactTable |
| DimDate | Dimension | 1,096 | Date | FactTable |


## Key Transformations and Resolutions

### Step 1 - DimPayments Aggregation

**Issue identified:** The raw DimPayments table contained multiple rows per order because some customers paid using more than one payment method (e.g. part credit card, part voucher). Retaining this structure would have created a many-to-many relationship with the FactTable, causing incorrect DAX calculations.

**Resolution:** A Group By transformation was applied in Power Query Editor using the Advanced mode with the following aggregations:

1. Group by: order_id
2. Total_Payment = Sum of payment_value
3. Payment_Type = Min of payment_type
4. Payment_Installments = Max of payment_installments

**Result:** DimPayments now contains one row per order_id, enabling a clean one-to-many relationship with the FactTable.

### Step 2 - DimSellers Created

The raw olist_sellers_dataset table was renamed to DimSellers in Power Query Editor. No additional transformations were required as the table was already clean with 100% valid data across all four columns.

**Columns in DimSellers:**
1. seller_id (primary key)
2. seller_zip_code_prefix
3. seller_city
4. seller_state

### Step 3 - DimProducts Category Translation

**Issue identified:** The product_category_name column in DimProducts contained Portuguese category names, which would appear in dashboard visuals and reduce professional quality.

**Resolution:** The product_category_name_translation lookup table was merged into DimProducts using Merge Queries in Power Query with the following settings:

1. Join type: Left Outer Join
2. Join key: product_category_name (DimProducts) matched to Column1 (translation table)
3. Expanded column: Column2 (English names only)
4. Renamed to: Product_Category_English

**Result:** DimProducts now contains 10 columns including Product_Category_English with English category names visible across all dashboard visuals.


## Unused Raw Tables Hidden

Three raw source tables were hidden from the report view to keep the Fields pane clean and prevent accidental use by report builders:

1. olist_geolocation_dataset - geographic coordinates, not used in analysis
2. olist_orders_dataset - all required columns already merged into FactTable
3. product_category_name_translation - English names already merged into DimProducts

These tables remain in the model for data lineage purposes but are not visible in the report-building interface.


## Date Table Configuration

DimDate was marked as the official Date Table using the Table Tools ribbon in Data view. The Date column was selected as the date column and validated successfully.

This setting is required to unlock Power BI time intelligence functions including TOTALYTD, TOTALMTD, SAMEPERIODLASTYEAR, and DATEADD which are used in the DAX measures stage.

---

## DAX measures & columns 
Brad Ochola - 670346

#### From the DimPayments dataset we calculate the total payments per Payment type 

<img width="1337" height="672" alt="image" src="https://github.com/user-attachments/assets/118e6128-bafb-4bd8-b79e-9d3fd984df4f" />

This measure calculates the aggregated payment amount grouped by payment type from the DimPayments dataset. The query uses the SUMX function to iterate through each payment type and sum the corresponding payment amounts. This enables analysis of revenue distribution across different payment methods (e.g., credit card, debit card, voucher, etc.).

#### New column for volume of products using DAX 

<img width="1301" height="640" alt="image" src="https://github.com/user-attachments/assets/1b9a4754-0e84-4045-94f2-0fd4a0a84f7b" />

This calculated column computes the volume of products by calculating the total quantity of items ordered. The column uses DAX to aggregate order quantities at the product level. This metric is essential for understanding product demand and inventory movement.

#### measure of total volume per product using dax 

<img width="1314" height="648" alt="image" src="https://github.com/user-attachments/assets/921f386e-6a1b-4913-ad5e-4eb7454c3e98" />

This measure calculates the total volume aggregated by product category. It sums the product volumes across all orders, grouped by product category, enabling high-level analysis of category performance. The measure uses SUMX in combination with category grouping to provide insights into which product categories have the highest sales volumes.

**Technical Details:**
- The measure iterates through unique product categories
- For each category, it sums the individual product volumes
- Results are sorted by volume in descending order to highlight top-performing categories
- This enables drill-down analysis from category level to individual products

---

## Power BI Data Modeling Steps
Nathan Omenge - 670637

This document outlines the complete, step-by-step process for transforming, modeling, and optimizing the Power BI dataset based on the Olist e-commerce data.

## 1. DimPayments - Group By Aggregation
The `DimPayments` table originally contained multiple rows per order (one per payment method). To resolve the many-to-many relationship risk, a **Group By** transformation was applied in Power Query. 

Orders were grouped by `order_id` with three aggregations:
- `Sum` of `payment_value` → renamed `TotalPayment`
- `Min` of `payment_type` → renamed `Payment_Type`
- `Max` of `payment_installments` → renamed `Payment_Installments`

This ensures a clean **one-to-many** relationship between `DimPayments` and `FactTable`.

## 2. DimSellers - Created from `olist_sellers_dataset`
The raw `olist_sellers_dataset` table was renamed to `DimSellers` to serve as the seller dimension in the star schema. The table contains 4 columns:
- `seller_id` (primary key)
- `seller_zip_code_prefix`
- `seller_city`
- `seller_state`

All columns showed 100% valid data with no errors or empty values. Basic cleaning steps including **Trim**, **Clean**, and **Capitalize Each Word** had already been applied to text columns.

## 3. DimProducts - English Category Names Merged
The `product_category_name_translation` table was merged into `DimProducts` using a **Left Outer Join** on the `product_category_name` column. The join retrieved the English equivalent category names from `Column2` of the translation table. The resulting column was renamed `Product_Category_English`. 

This ensures product categories are displayed in English across all dashboard visuals. `DimProducts` now contains 10 columns including the new English category column.

## 4. Hidden Unused Tables
Three raw source tables were hidden from the report view to keep the model clean and prevent accidental use by report builders:
- `olist_geolocation_dataset`
- `olist_orders_dataset`
- `product_category_name_translation`

These tables served as data sources during the Power Query stage but are not required in the final analytical model.

## 5. DimDate - Created using DAX `ADDCOLUMNS`
A dedicated Date dimension table was created using DAX. The `CALENDAR` function generates a continuous date range from **1 January 2016** to **31 December 2018**, covering the full Olist dataset period. `ADDCOLUMNS` was used to derive 6 additional columns:
- `Year`
- `Month Number`
- `Month Name`
- `Quarter`
- `Day Name`
- `Week Number`

This table is required to enable time intelligence DAX measures such as YTD, MTD, and YoY calculations.

**DAX Code:**
```dax
DimDate = 
ADDCOLUMNS(
    CALENDAR(DATE(2016,1,1), DATE(2018,12,31)),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month Name", FORMAT([Date],"MMMM"),
    "Quarter", "Q" & QUARTER([Date]),
    "Day Name", FORMAT([Date],"DDDD"),
    "Week Number", WEEKNUM([Date])
)
```

## 6. DimDate - Marked as Official Date Table
`DimDate` was marked as the official Date Table in Power BI using the **Table Tools** ribbon. The `Date` column was selected as the date column and validated successfully. This setting enables Power BI to use `DimDate` for all time intelligence calculations including YTD, MTD, QTD, and YoY measures in DAX.

## 7. Relationships Built - Star Schema
Six active relationships were established, all **many-to-one (*:1)** with single cross-filter direction from dimension to fact table:

- `FactTable[customer_id]` → `DimCustomers[customer_id]`
- `FactTable[Order_Date]` → `DimDate[Date]`
- `FactTable[order_id]` → `DimPayments[order_id]`
- `FactTable[product_id]` → `DimProducts[product_id]`
- `FactTable[review_id]` → `DimReviews[review_id]`
- `FactTable[seller_id]` → `DimSellers[seller_id]`

All ambiguous relationships through `olist_orders_dataset` were removed. `DimReviews` duplicates were removed in Power Query before the relationship could be established.

## 8. Hidden Foreign Key Columns
Foreign key columns were hidden from the report view in both the `FactTable` and all dimension tables to prevent report builders from accidentally using join columns in visuals and to keep the Fields pane clean and professional.

**Hidden in `FactTable`:**
- `customer_id`
- `product_id`
- `seller_id`
- `order_id`
- `review_id`

The corresponding primary key columns were also hidden in each dimension table.

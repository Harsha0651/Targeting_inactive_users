# 🧵 Microsoft Fabric Data Engineering Project: Targeting Inactive Users
<img width="1512" alt="Image" src="https://github.com/user-attachments/assets/28191292-3ecf-472e-b234-07d0731f192f" />

## Project Overview

This project showcases an end-to-end Microsoft Fabric Data Engineering solution to identify inactive website users based on enquiry, social media, and web activity data. The pipeline empowers marketing teams with insights via Power BI dashboards.

## 🚀 Objective

Build an end-to-end pipeline using **Microsoft Fabric** to:
- Ingest and unify user activity data (enquiry, social, web)
- Identify **inactive website users** still engaged on other platforms
- Empower marketing teams via **Power BI insights** for retargeting

## 🧰 Tools & Technologies

- **Microsoft Fabric**
  - Data Factory
  - Lakehouse (Bronze, Silver, Gold)
  - OneLake Storage
  - Notebooks (PySpark)
- **Power BI**
- **SQL (T-SQL-like syntax)**
- **PYSPARK**
- **Python**

## 📘 Database Schema
The project uses six main tables:

1. **tbl_account**: Contains user account details.
 - `user_id`: Unique identifier for each user.
 - `first_name`: First name of the user.
 - `last_name`: Last name of the user.
 - `email`: Email address of the user.
 - `created_datetime_date`: Date the account was created.

2. **tbl_assets**: Holds information about digital or physical assets.
- `asset_id`: Unique identifier for each asset.
- `asset_name`: Name of the asset.
- `asset_description`: Description of the asset.
- `created_datetime_date`: Date the asset record was created.

3. **tbl_demand**: Tracks product demand or user purchase intent.
- `user_id`: References the user who placed the demand.
- `name`: Full name of the user.
- `product_id`: References the requested product.
- `status`: Status of the demand (e.g., completed, cancelled).
- `product_name`: Name of the product.
- `created_datetime_date`: Date the demand was created.

4. **tbl_product**: Contains detailed product information.
- `product_id`: Unique identifier for each product.
- `product_name`: Name of the product.
- `category`: Category of the product (e.g., Phones, Electronics).
- `location`: Location related to the product (e.g., store or region).
- `linked_courses_id`: Identifier linking to a related course (if applicable).

5. **tbl_social_media**: Captures user activity on social media platforms.
- `user_id`: References the user performing the action.
- `platform_name`: Name of the social platform (e.g., LinkedIn, Twitter).
- `device`: Device used for the interaction (e.g., Mobile, Desktop).
- `interaction_type`: Type of interaction (e.g., like, comment, share).
- `interaction_datetime_date`: Date of the interaction.
- `interaction_datetime_time`: Time of the interaction.

6. tbl_web_activity: Records user interactions on the website.
- `user_id`: References the user visiting the website.
- `web_id`: Unique identifier for each web activity session.
- `email`: Email address associated with the visit.
- `visit_datetime_date`: Date of the website visit.
- `visit_datetime_time`: Time of the website visit.

## 🔄 End-to-End Architecture

### 1. Ingest Raw Data (API to Bronze)
- Loop through 6 API-based files using `Lookup + ForEach` activity
- Store raw files in **Bronze Lakehouse** for traceability
![Image](https://github.com/user-attachments/assets/653d4186-3daa-435e-8577-4d3fb5ffd37b)

### 2. Bronze ➡️ Silver: Unified Table Creation
- Use **PySpark** to:
  - Merge all files into one table
  - Align schemas
  - Type cast & clean nulls/duplicates
- Save as a consolidated table in **Silver Lakehouse**
![Image](https://github.com/user-attachments/assets/9a0dd884-02f5-4a7b-aa11-a76439cdce75)

### 3. Silver ➡️ Gold: Data Modelling 
- Design a **Star Schema** using PySpark
- Create:
  - `fact_user_engagement`
  - `dim_user`, `dim_product`, `dim_platform`, `dim_date`
- Optimize for Power BI consumption
- Store model in **Gold Lakehouse**
![Image](https://github.com/user-attachments/assets/ea6831ff-851c-4187-b6df-4fffd6528361)

### Star Schema(Data Model)
![Image](https://github.com/user-attachments/assets/04711da8-7a22-4626-8c77-313cbeb15231)

### 🧪 Inactive User Identification

## 🔍 SQL Logic to Identify Inactive Users

```sql
SELECT DISTINCT f.user_key
FROM fact_user_engagement f
WHERE 
(
  f.demand_date IS NOT NULL OR 
  f.social_date IS NOT NULL
)
AND (
  f.web_visit_date IS NULL OR 
  f.web_visit_date < DATEADD(month, -6, GETDATE())
)
```
- 🔍 Detects users active on social or enquiry channels but not active on the website for 6+ months.
- 🎯 These users are ideal candidates for re-engagement campaigns.

## 📈 Power BI Integration
- Power BI is directly connected to the Gold Lakehouse SQL endpoint
- Marketing users can explore:
  - Correlations between enquiries and visits
  - Drop-off trends post-engagement
  - Channel-wise performance analysis
 
## ✅ Key Outcomes
- 🛠️ Built an end-to-end ETL pipeline using Microsoft Fabric
- 🔄 Integrated raw data from APIs into Bronze Lakehouse
- 🧹 Cleaned and merged into a unified Silver table
- 🏗️ Modelled star schema in Gold Lakehouse
- 📊 Enabled self-service analytics with Power BI
- 🎯 Delivered actionable insights to marketing teams for user retargeting


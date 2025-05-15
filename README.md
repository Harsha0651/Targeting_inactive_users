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
 - *user_id*: Unique identifier for each user.
 - *first_name*: First name of the user.
 - *last_name*: Last name of the user.
 - *email*: Email address of the user.
- *created_datetime_date*: Date the account was created.

2. **tbl_assets**: Holds information about digital or physical assets.
- *asset_id*: Unique identifier for each asset.
- *asset_name*: Name of the asset.
- *asset_description*: Description of the asset.
- *created_datetime_date*: Date the asset record was created.

3. **tbl_demand**: Tracks product demand or user purchase intent.
- *user_id*: References the user who placed the demand.
- *name*: Full name of the user.
- *product_id*: References the requested product.
- *status*: Status of the demand (e.g., completed, cancelled).
- *product_name*: Name of the product.
- *created_datetime_date*: Date the demand was created.

4. **tbl_product**: Contains detailed product information.
- *product_id*: Unique identifier for each product.
- *product_name*: Name of the product.
- *category*: Category of the product (e.g., Phones, Electronics).
- *location*: Location related to the product (e.g., store or region).
- *linked_courses_id*: Identifier linking to a related course (if applicable).

5. **tbl_social_media**: Captures user activity on social media platforms.
- *user_id*: References the user performing the action.
- *platform_name*: Name of the social platform (e.g., LinkedIn, Twitter).
- *device*: Device used for the interaction (e.g., Mobile, Desktop).
- *interaction_type*: Type of interaction (e.g., like, comment, share).
- *interaction_datetime_date*: Date of the interaction.
- *interaction_datetime_time*: Time of the interaction.

6. tbl_web_activity: Records user interactions on the website.
- *user_id*: References the user visiting the website.
- *web_id*: Unique identifier for each web activity session.
- *email*: Email address associated with the visit.
- *visit_datetime_date*: Date of the website visit.
- *visit_datetime_time*: Time of the website visit.




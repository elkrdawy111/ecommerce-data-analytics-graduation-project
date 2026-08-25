<div align="center">
# ✦ AURA ✦
### E-Commerce Data Analytics — Graduation Project
<a href="Database(create%20data%20by%20sql)/">
  <img src="https://img.shields.io/badge/-SQL%20Server-d5ad5d?style=for-the-badge&logo=microsoftsqlserver&logoColor=white&labelColor=17100a" alt="SQL Server" />
</a>
<a href="Python/">
  <img src="https://img.shields.io/badge/-Python-b88a3b?style=for-the-badge&logo=python&logoColor=white&labelColor=17100a" alt="Python" />
</a>
<a href="E_COMMERCE.xlsx">
  <img src="https://img.shields.io/badge/-Excel-8c672d?style=for-the-badge&logo=microsoftexcel&logoColor=white&labelColor=17100a" alt="Excel" />
</a>
<a href="e-commerce%20clothing.pbix">
  <img src="https://img.shields.io/badge/-Power%20BI-d5ad5d?style=for-the-badge&logo=powerbi&logoColor=white&labelColor=17100a" alt="Power BI" />
</a>
<br>
<img src="https://img.shields.io/badge/Status-Completed-b88a3b?style=flat-square&labelColor=0b0805" />
<img src="https://img.shields.io/badge/Tables-14-d5ad5d?style=flat-square&labelColor=0b0805" />
<img src="https://img.shields.io/badge/License-Educational-8c672d?style=flat-square&labelColor=0b0805" />
</div>

## ✦ &nbsp; About the Project

**AURA** is a fictional e-commerce platform selling clothing, shoes, bags, and accessories.
This project simulates a complete, real-world data analytics pipeline built entirely from scratch —
from database design to a fully interactive Power BI dashboard.

The dataset was **custom-designed and generated** for this graduation project (not sourced from Kaggle
or any public dataset), simulating realistic customer behavior, orders, payments, shipping, and
product reviews across the period **2024 – 2026**.

<br>

## ✦ &nbsp; Tech Stack

| Layer | Tools Used |
|---|---|
| **Database Design** | SQL Server (T-SQL) — 14 normalized tables, Views, Computed Columns |
| **Data Generation** | Python (`Faker`, `pandas`) |
| **Data Analysis** | Python (`pandas`, `matplotlib`, `seaborn`) via SQL connection (`pyodbc`) |
| **Reporting** | Microsoft Excel — Pivot Tables, Slicers, Charts |
| **Visualization** | Power BI — 5-page interactive dashboard, DAX measures |

<br>

## ✦ &nbsp; Entity Relationship Diagram

The database consists of **14 relational tables** covering the full e-commerce lifecycle:
Customers, Products, Categories, Brands, Suppliers, Orders, Order Items, Payments, Shipping,
Promotions, and Reviews — with dedicated lookup tables for statuses (Order, Payment, Shipping)
to keep the schema normalized.

```mermaid
erDiagram
    CUSTOMER ||--o{ ORDERS : places
    CUSTOMER ||--o{ REVIEW : writes
    PRODUCT ||--o{ REVIEW : receives
    CATEGORY ||--o{ PRODUCT : contains
    BRAND ||--o{ PRODUCT : manufactures
    SUPPLIER ||--o{ PRODUCT : supplies
    PROMOTION ||--o{ ORDERS : applied_to
    PROMOTION_TYPE ||--o{ PROMOTION : defines
    ORDER_STATUS ||--o{ ORDERS : tracks
    ORDERS ||--o{ ORDER_ITEMS : contains
    PRODUCT ||--o{ ORDER_ITEMS : included_in
    ORDERS ||--o| PAYMENT : processed_via
    PAYMENT_STATUS ||--o{ PAYMENT : updates
    ORDERS ||--o| SHIPPING : fulfilled_by
    SHIPPING_STATUS ||--o{ SHIPPING : reflects

    CUSTOMER {
        int CUSTOMER_ID PK
        varchar FULLNAME
        varchar EMAIL
        varchar GENDER
        date DATE_OF_BIRTH
        varchar CITY
        varchar COUNTRY
        varchar SIGNUP_CHANNEL
        date SIGNUP_DATE
    }
    CATEGORY {
        int CATEGORY_ID PK
        varchar CATEGORY_NAME
        varchar URL_IMG
    }
    BRAND {
        int BRAND_ID PK
        varchar BRAND_NAME
    }
    SUPPLIER {
        int SUPPLIER_ID PK
        varchar SUPPLIER_NAME
        varchar COUNTRY
    }
    PRODUCT {
        int PRODUCT_ID PK
        varchar PRODUCT_NAME
        varchar TARGET_GENDER
        decimal PRICE
        decimal COST
        int STOCK_QUANTITY
        date CREATE_DATE
        int CATEGORY_ID FK
        int BRAND_ID FK
        int SUPPLIER_ID FK
        varchar SIZE
    }
    PROMOTION_TYPE {
        int PROMO_TYPE_ID PK
        varchar TYPE_NAME
    }
    PROMOTION {
        int PROMO_ID PK
        varchar CODE
        decimal DISCOUNT_PERCENTAGE
        date START_DATE
        date END_DATE
        int PROMO_TYPE_ID FK
    }
    ORDER_STATUS {
        int ORDER_STATUS_ID PK
        varchar STATUS_NAME
    }
    ORDERS {
        int ORDER_ID PK
        int CUSTOMER_ID FK
        int PROMO_ID FK
        int ORDER_STATUS_ID FK
        date ORDER_DATE
        decimal TOTAL_PRICE
    }
    ORDER_ITEMS {
        int ORDER_ITEMS_ID PK
        int ORDER_ID FK
        int PRODUCT_ID FK
        int QUANTITY
        decimal UNIT_PRICE
        decimal Total_Price
    }
    PAYMENT_STATUS {
        int PAYMENT_STATUS_ID PK
        varchar STATUS_NAME
    }
    PAYMENT {
        int PAYMENT_ID PK
        int ORDER_ID FK
        int PAYMENT_STATUS_ID FK
        decimal AMOUNT
        varchar METHOD
    }
    SHIPPING_STATUS {
        int SHIPPING_STATUS_ID PK
        varchar STATUS_NAME
    }
    SHIPPING {
        int SHIPPING_ID PK
        int ORDER_ID FK
        int SHIPPING_STATUS_ID FK
        date SHIPPING_DATE
        date DELIVERY_DATE
        varchar CARRIER
        decimal SHIPPING_COST
    }
    REVIEW {
        int REVIEW_ID PK
        int CUSTOMER_ID FK
        int PRODUCT_ID FK
        int RATING
        varchar REVIEW_TEXT
        date REVIEW_DATE
    }
```

### Table reference

| Table | Purpose | Key Relationships |
|---|---|---|
| `CUSTOMER` | Stores customer demographics, location, and signup info | Referenced by `ORDERS`, `REVIEW` |
| `CATEGORY` | Product categories (Clothing, Shoes, Bags, Kids Wear, etc.) | Referenced by `PRODUCT` |
| `BRAND` | Product manufacturing brands (Pulse, Urbanix, Northline, etc.) | Referenced by `PRODUCT` |
| `SUPPLIER` | Vendors supplying the products across regions | Referenced by `PRODUCT` |
| `PRODUCT` | Product catalog containing pricing, cost, size, and stock | → `CATEGORY`, `BRAND`, `SUPPLIER` <br> Referenced by `ORDER_ITEMS`, `REVIEW` |
| `PROMOTION_TYPE`| Defines campaign types for promotions | Referenced by `PROMOTION` |
| `PROMOTION` | Discount codes, discount percentages, and active periods | → `PROMOTION_TYPE` <br> Referenced by `ORDERS` |
| `ORDER_STATUS`| Lookup table for order progression (e.g., Processing, Shipped) | Referenced by `ORDERS` |
| `ORDERS` | High-level customer order transactions and total prices | → `CUSTOMER`, `PROMOTION`, `ORDER_STATUS` <br> Referenced by `ORDER_ITEMS`, `PAYMENT`, `SHIPPING` |
| `ORDER_ITEMS` | Granular line items detailing specific products and quantities per order | → `ORDERS`, `PRODUCT` |
| `PAYMENT_STATUS`| Lookup table for payment outcomes (e.g., Paid, Failed) | Referenced by `PAYMENT` |
| `PAYMENT` | Financial transaction records tracking payment methods and amounts | → `ORDERS`, `PAYMENT_STATUS` |
| `SHIPPING_STATUS`| Lookup table for delivery progression (e.g., Delivered, Returned) | Referenced by `SHIPPING` |
| `SHIPPING` | Logistical details, delivery timelines, carriers, and shipping costs | → `ORDERS`, `SHIPPING_STATUS` |
| `REVIEW` | Post-purchase customer feedback and quantitative ratings | → `CUSTOMER`, `PRODUCT` |

<br>

## ✦ &nbsp; Power BI Dashboard

The dashboard is organized into **5 pages**, each answering a different business question. The visual identity utilizes a custom dark-gold UI (`#0b0805` background, `#d5ad5d` gold highlights) for premium branding and readability.

| Page | Focus |
|---|---|
| 🏠 **Home** | Landing page / brand identity |
| 📊 **Sales Overview** | High-level KPIs — revenue, orders, average order value, geographic breakdown |
| 👤 **Customer Analytics** | Demographics, signup channels, customer age distributions |
| 📦 **Product & Profit** | Profitability, brand comparison, price vs. rating analysis |
| 🚚 **Shipping & Payments** | Delivery performance by carrier, returned/cancelled rates, payment methods |

### Dashboard Previews

<div align="center">
  <a href="https://github.com/elkrdawy111/ecommerce-data-analytics-graduation-project/blob/main/Photo&Icon/POWERBI-DASHBOARD-1.png?raw=true">
    <img src="https://github.com/elkrdawy111/ecommerce-data-analytics-graduation-project/blob/main/Photo&Icon/POWERBI-DASHBOARD-1.png?raw=true" alt="Home Page" width="24%" style="margin: 2px;"/>
  </a>
  <a href="https://github.com/elkrdawy111/ecommerce-data-analytics-graduation-project/blob/main/Photo&Icon/POWERBI-DASHBOARD-2.png?raw=true">
    <img src="https://github.com/elkrdawy111/ecommerce-data-analytics-graduation-project/blob/main/Photo&Icon/POWERBI-DASHBOARD-2.png?raw=true" alt="Sales Overview" width="24%" style="margin: 2px;"/>
  </a>
  <a href="https://github.com/elkrdawy111/ecommerce-data-analytics-graduation-project/blob/main/Photo&Icon/POWERBI-DASHBOARD-3.png?raw=true">
    <img src="https://github.com/elkrdawy111/ecommerce-data-analytics-graduation-project/blob/main/Photo&Icon/POWERBI-DASHBOARD-3.png?raw=true" alt="Customer Analytics" width="24%" style="margin: 2px;"/>
  </a>
  <a href="https://github.com/elkrdawy111/ecommerce-data-analytics-graduation-project/blob/main/Photo&Icon/POWERBI-DASHBOARD-4.png?raw=true">
    <img src="https://github.com/elkrdawy111/ecommerce-data-analytics-graduation-project/blob/main/Photo&Icon/POWERBI-DASHBOARD-4.png?raw=true" alt="Product Profitability" width="24%" style="margin: 2px;"/>
  </a>
</div>


<br>

## ✦ &nbsp; Excel Dashboard

Complementing the Power BI suite is an interactive **Excel Dashboard**, allowing stakeholders to filter and review sales volumes and demographic summaries natively through Slicers and Pivot Tables.

<div align="center">
  <img src="https://github.com/elkrdawy111/ecommerce-data-analytics-graduation-project/blob/main/Photo&Icon/EXCEL-DASHBOARD.png?raw=true" alt="Excel Dashboard Overview" width="800"/>
</div>

<br>

## ✦ &nbsp; Key Insights

- 📈 Total Revenue: **$720.97K** across 180 orders
- 💰 Profit Margin: **~44%** overall
- 🚫 Cancelled/Returned Rate: **18.33%**
- ⭐ Average Product Rating: **4.26 / 5**
- 🛍️ **Customer Behavior**: Specific age brackets heavily dominate the active customer base, validating targeted marketing campaigns (e.g., Google Ads).
- 🚚 **Logistics Friction**: Variations in Average Delivery Time exist between carriers, directly correlating with the percentage of Returned Orders.

<br>

## ✦ &nbsp; Repository Structure

```
AURA-ecommerce-analytics/
│
├── README.md
├── Database(create data by sql)/
│   ├── E_COMMERCE_DB_DDL (Create database).sql.sql  # DDL — table definitions
│   ├── E_COMMERCE_DB_DATA (fil data).sql            # Generated INSERT statements
│   └── E_COMMERCE_QUERIERS.sql                      # Analysis-ready SQL views
│
├── Python/
│   ├── ecommerce-project.ipynb                      # EDA, data loading & profiling
│   └── VW_DASHBOARD_DATA.xlsx                       # Exported analytical dataset
│
├── E_COMMERCE.xlsx                                  # Pivot tables, charts, KPIs
├── e-commerce clothing.pbix                         # 5-page interactive dashboard
│
├── Dashboard/                                       # Power BI Screenshots
└── Photo/                                           # Icons, Backgrounds & Excel Screenshots

```

<br>

## ✦ &nbsp; How to Run This Project

1. **Database**: Run `Database(create data by sql)/E_COMMERCE_DB_DDL (Create database).sql.sql` on SQL Server to create `E_COMMERCE_DB`, then run `E_COMMERCE_DB_DATA (fil data).sql` to populate it. Create the views using `E_COMMERCE_QUERIERS.sql`.
2. **Python Analysis**: Open `Python/ecommerce-project.ipynb` in Jupyter Notebook, ensure the SQL Server name matches your local instance (`DESKTOP-UFA9267\SQLEXPRESS` by default), and run all cells.
3. **Excel**: Open `E_COMMERCE.xlsx` to interact with the Pivot Tables and Dashboard.
4. **Power BI**: Open `e-commerce clothing.pbix` in Power BI Desktop and refresh the data source to fetch live updates from your SQL Server.

<br>

## ✦ &nbsp; Author

**Mohamed Amir Elkrdawy**  
Graduation Project — Data Creation, Analysis & Visualization
<div align="center">
  <a href="https://www.linkedin.com/in/mohamed-amiir11/">
    <img src="https://img.shields.io/badge/LinkedIn-Connect-d5ad5d?style=for-the-badge&logo=linkedin&labelColor=17100a" alt="LinkedIn" />
  </a>
  <a href="https://www.kaggle.com/mohamedamiralkrdawy">
    <img src="https://img.shields.io/badge/Kaggle-Profile-b88a3b?style=for-the-badge&logo=kaggle&labelColor=17100a" alt="Kaggle" />
  </a>
  <a href="mailto:m.ekrdawy@gmail.com">
    <img src="https://img.shields.io/badge/Email-Contact-8c672d?style=for-the-badge&logo=gmail&labelColor=17100a" alt="Email" />

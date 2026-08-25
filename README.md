<div align="center">

# ✦ AURA ✦
### E-Commerce Data Analytics — Graduation Project

<img src="https://img.shields.io/badge/SQL_Server-Database-d5ad5d?style=for-the-badge&labelColor=17100a" />
<img src="https://img.shields.io/badge/Python-Analysis-b88a3b?style=for-the-badge&labelColor=17100a" />
<img src="https://img.shields.io/badge/Excel-Reports-8c672d?style=for-the-badge&labelColor=17100a" />
<img src="https://img.shields.io/badge/Power_BI-Dashboard-d5ad5d?style=for-the-badge&labelColor=17100a" />

<br>

<img src="https://img.shields.io/badge/Status-Completed-b88a3b?style=flat-square&labelColor=0b0805" />
<img src="https://img.shields.io/badge/Tables-14-d5ad5d?style=flat-square&labelColor=0b0805" />
<img src="https://img.shields.io/badge/License-Educational-8c672d?style=flat-square&labelColor=0b0805" />

</div>

<br>

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
| **Data Analysis** | Python (`pandas`, `matplotlib`) via SQL connection (`pyodbc`) |
| **Reporting** | Microsoft Excel — Pivot Tables, Slicers, Charts |
| **Visualization** | Power BI — 5-page interactive dashboard, DAX measures |

<br>

## ✦ &nbsp; Entity Relationship Diagram

<div align="center">
<img src="docs/erd_diagram.png" alt="AURA ERD" width="800"/>
</div>

The database consists of **14 relational tables** covering the full e-commerce lifecycle:
Customers, Products, Categories, Brands, Suppliers, Orders, Order Items, Payments, Shipping,
Promotions, and Reviews — with dedicated lookup tables for statuses (Order, Payment, Shipping)
to keep the schema normalized.

<br>

## ✦ &nbsp; Power BI Dashboard

The dashboard is organized into **5 pages**, each answering a different business question:

| Page | Focus |
|---|---|
| 🏠 **Home** | Landing page / brand identity |
| 📊 **Data Overview** | High-level KPIs — revenue, orders, profit, category breakdown |
| 👤 **Customer** | Demographics, signup channels, customer lifetime value |
| 📦 **Product** | Profitability, brand comparison, price vs. rating analysis |
| 🚚 **Shipping & Payments** | Delivery performance, cancellation rate, payment methods |

<div align="center">
<img src="docs/dashboard_overview.png" alt="Dashboard Preview" width="800"/>
</div>

<br>

## ✦ &nbsp; Key Insights

> Replace these with your own findings once your analysis is complete.

- 📈 Total Revenue: **$720.97K** across 180 orders
- 💰 Profit Margin: **~44%** overall
- 🚫 Cancelled/Returned Rate: **18.33%**
- ⭐ Average Product Rating: **4.26 / 5**

<br>

## ✦ &nbsp; Repository Structure

```
AURA-ecommerce-analytics/
│
├── README.md
├── database/
│   ├── schema.sql              # DDL — table definitions
│   ├── sample_data.sql         # Generated INSERT statements
│   └── views.sql                # Analysis-ready SQL views
│
├── python/
│   ├── generate_data.py        # Faker-based data generation script
│   └── analysis.ipynb          # EDA & analysis notebook
│
├── excel/
│   └── AURA_dashboard.xlsx     # Pivot tables, charts, KPIs
│
├── powerbi/
│   └── AURA_dashboard.pbix     # 5-page interactive dashboard
│
└── docs/
    ├── erd_diagram.png
    ├── dashboard_overview.png
    └── documentation.pdf        # 2-4 page project write-up
```

<br>

## ✦ &nbsp; How to Run This Project

1. **Database**: Run `database/schema.sql` on SQL Server to create `E_COMMERCE_DB`, then run `sample_data.sql` to populate it.
2. **Python Analysis**: Open `python/analysis.ipynb` in Jupyter, update the connection string in the first cell, and run all cells.
3. **Excel**: Open `excel/AURA_dashboard.xlsx` — it connects live to the SQL views if the database is running locally.
4. **Power BI**: Open `powerbi/AURA_dashboard.pbix` in Power BI Desktop and refresh the data source.

<br>

## ✦ &nbsp; Author

**[Your Name]**
Graduation Project — Data Creation, Analysis & Visualization

<div align="center"><a href="https://www.linkedin.com/in/mohamed-amiir11/" target="_blank">
  <img src="https://img.shields.io/badge/LinkedIn-Connect-d5ad5d?style=for-the-badge&labelColor=17100a" />
</a>
<img src="https://img.shields.io/badge/Email-Contact-b88a3b?style=for-the-badge&labelColor=17100a" />
</div>

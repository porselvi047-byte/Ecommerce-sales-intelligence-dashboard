 📊 Real-Time E-Commerce Analytics Dashboard


A production-grade business intelligence system that tracks *sales performance, **customer behavior, **profit trends, **product demand, and **regional revenue insights* across a full e-commerce dataset. Built end-to-end using Python, SQL, Power BI/Tableau, and Excel.


🖼️ Dashboard Preview



| Executive Overview | Regional Insights |

| Customer channel analysis | Customer Behavior |

|Time intelligence|

## 🎯 Project Objectives

- Track and visualize *monthly/quarterly revenue and profit trends*
- Perform *RFM segmentation* to classify customers into behavioral cohorts
- Analyze *product demand* by category, region, and time period
- Build *cohort retention tables* to measure customer loyalty over time
- Generate *automated Excel BI reports* for business stakeholders
- Deliver *interactive dashboards* for real-time decision-making

🗂️ Project Structure


ecommerce-analytics-dashboard/

─ data/   raw/                    
Original unprocessed dataset
     ── ecommerce_raw.csv
     ── cleaned/                Cleaned and feature-engineered data
     ── ecommerce_cleaned.csv
     ── ecommerce_cleaned.xlsx
── notebooks/
 ── 01_data_generation.ipynb        Synthetic data generation (optional)
   ── 02_eda_and_cleaning.ipynb      Exploratory analysis & data cleaning
 ── 03_feature_engineering.ipynb    New feature creation (RFM, cohorts)
 ── 04_visualizations.ipynb        Plotly charts and Python analysis
│
─ sql/
 ── schema.sql                     Star schema DDL (CREATE TABLE statements)
  ── load_data.py                   Python script to load data into SQLite
  └── queries/
   ── 01_monthly_revenue.sql
   ── 02_top_products.sql
   ── 03_revenue_by_region.sql
      04_profit_margin_by_category.sql
   ── 05_customer_order_frequency.sql
   ── 06_cohort_retention.sql
   ── 07_avg_order_value.sql
   ── 08_order_status_breakdown.sql
   ── 09_day_of_week_sales.sql
   ── 10_qoq_growth.sql
   ── dashboards/
   ── ecommerce_dashboard.pbix       Power BI dashboard file
  └── ecommerce_dashboard.twbx       Tableau packaged workbook

── reports/
─ revenue_trend.html             Interactive Plotly chart
  ─ Monthly_BI_Report.xlsx         Auto-generated Excel report
   Business_Intelligence_Report.pdf

─ screenshots/                       Dashboard screenshots for README

── generate_report.py                  Script to auto-generate Excel report
── requirements.txt
── .gitignore
── README.md

 Tech Stack

| Layer | Tool | Purpose |
|---|---|---|
| Data Generation | Python (Faker, NumPy) | Synthetic dataset creation |
| Data Cleaning | Python (Pandas) | EDA, missing values, outliers, type fixes |
| Feature Engineering | Python (Pandas) | RFM scores, cohorts, time features |
| Database | SQL (SQLite / PostgreSQL) | Star schema, business queries |
| Python Visualization | Plotly, Seaborn, Matplotlib | Interactive charts and analysis |
| BI Dashboard | Power BI / Tableau | Executive dashboards (5 pages) |
| Reporting | Excel (openpyxl) + Python | Automated stakeholder reports |

📐 Database Schema (Star Schema)


          ┌─────────────┐
          │  dim_date   │
          └──────┬──────┘
                 │
┌──────────────┐ │ ┌──────────────────┐
│ dim_customers│─┤─│   fact_orders    │─── dim_products
└──────────────┘ │ └──────────────────┘
                 │
          (order_id, customer_id, product_id,
           date_key, quantity, revenue, profit,
           order_status)


 📊 Dashboard Pages

Page 1 — Executive Overview
KPI cards for Total Revenue, Gross Profit, Total Orders, and Average Order Value. Line chart for monthly revenue trend. Donut chart for order status split. Bar chart for top 5 product categories.

Page 2 — Customer & channel analysis
Area chart for daily revenue (last 90 days). Column chart for revenue by day of week. Month-over-month growth percentage line. Quarterly waterfall profit chart.

Page 3 — Time intelligence
Filled map with revenue by region. Bar chart of profit margin by region. Matrix table showing region × category revenue breakdown. Gauge chart for regional target vs. actual.

🚀 Getting Started

1. Clone the repository

bash
git clone https://github.com/YOUR_USERNAME/ecommerce-analytics-dashboard.git
cd ecommerce-analytics-dashboard


2. Set up the Python environment

bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt


3. Generate or load the dataset

bash
Option A: Generate a synthetic dataset
jupyter notebook notebooks/01_data_generation.ipynb

Option B: Place your own CSV at data/raw/ecommerce_raw.csv


4. Run data cleaning and feature engineering

bash
jupyter notebook notebooks/02_eda_and_cleaning.ipynb
jupyter notebook notebooks/03_feature_engineering.ipynb


5. Load data into the SQL database

bash
python sql/load_data.py


6. Run Python visualizations

bash
jupyter notebook notebooks/04_visualizations.ipynb


7. Generate the Excel report

bash
python generate_report.py
# Output: reports/Monthly_BI_Report.xlsx


 8. Open the dashboard

- **Power BI:** Open `dashboards/ecommerce_dashboard.pbix` in Power BI Desktop

📦 Requirements

pandas>=2.0.0
numpy>=1.24.0
matplotlib>=3.7.0
seaborn>=0.12.0
plotly>=5.14.0
sqlalchemy>=2.0.0
scikit-learn>=1.2.0
statsmodels>=0.14.0
faker>=18.0.0
openpyxl>=3.1.0
xlsxwriter>=3.1.0
jupyter>=1.0.0
ipywidgets>=8.0.0


Install all at once:
bash
pip install -r requirements.txt

 📈 Key KPIs Tracked

| KPI | Description |
|---|---|
| Total Revenue | Sum of all completed order revenues |
| Gross Profit | Revenue minus cost of goods sold |
| Profit Margin % | (Profit / Revenue) × 100 |
| Average Order Value (AOV) | Mean revenue per order |
| Customer Lifetime Value (CLV) | Total spend per unique customer |
| MoM Revenue Growth | Month-over-month percentage change |
| RFM Segments | Champion / Loyal / At Risk / Lost |
| Cohort Retention Rate | % of customers returning each month |
| Product Demand Index | Units sold per product per time period |
| Regional Revenue Share | % of total revenue per geographic region |

---

🔍 Sample SQL Query — Monthly Revenue Trend

sql
SELECT
    d.year,
    d.month,
    SUM(f.revenue)          AS total_revenue,
    SUM(f.profit)           AS total_profit,
    COUNT(f.order_id)       AS total_orders,
    AVG(f.revenue)          AS avg_order_value,
    ROUND(SUM(f.profit) / SUM(f.revenue) * 100, 2) AS profit_margin_pct
FROM fact_orders f
JOIN dim_date d ON f.date_key = d.date_key
WHERE f.order_status = 'Completed'
GROUP BY d.year, d.month
ORDER BY d.year, d.month;

 🧠 Business Insights Generated

- *Peak sales months* identified — enabling targeted promotions and inventory planning
- *Top 20% of products* generate ~65% of total revenue (Pareto principle confirmed)
- *Champion customers* (top RFM segment) have 4× higher average order value than Lost segment
- *Regional disparities* revealed — East region outperforms by 23% in profit margin
- *Cohort analysis* shows Month 3 is the critical churn point — retention drops sharply after 90 days


## 📁 Data Sources

| Source | Description | Link |
|---|---|---|
| Olist Brazilian E-Commerce | 100k real orders, 2016–2018 | [Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) |
| Online Retail II (UCI) | UK transactions, 500k+ rows | [UCI ML Repository](https://archive.ics.uci.edu/ml/datasets/Online+Retail+II) |
| Synthetic (this repo) | Generated via Python Faker | notebooks/01_data_generation.ipynb |

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome. Feel free to open a pull request or file an issue.

1. Fork the repository
2. Create your feature branch (git checkout -b feature/add-forecasting)
3. Commit your changes (git commit -m 'Add revenue forecasting module')
4. Push to the branch (git push origin feature/add-forecasting)
5. Open a Pull Request

## 👤 Author

D.Porselvi
- Github: https://github.com/porselvi047-byte)
- LinkedIn: https://www.linkedin.com/in/porselvianalyst

Built as a portfolio project demonstrating end-to-end business intelligence skills across Python, SQL, Power BI, Tableau, and Excel.

# Customer Churn and Retention Analysis

<div align="center">
  <img src="./online_store.webp" alt="Customer Churn and Retention Analysis Banner" width="100%">
</div>

<br>

**Author:** Dinh Thi Thanh Hang

---

## 📌 Project Contents (Click on each section to expand)

<details>
  <summary><b>📖 1. Project Overview & Business Objectives</b></summary>
  <br>

  ### Project Overview
  This project analyzes customer purchasing behavior and churn patterns using over 500,000 transaction records from a UK-based B2B online retailer specializing in gifts, decorations, and home accessories.

  Using **PySpark** and **Python**, the project explores customer purchasing trends, identifies churn drivers, segments customers based on behavioral patterns, and develops a churn prediction framework to support retention strategies.

  ### Business Objectives
  * Analyze revenue growth and sales performance.
  * Understand customer purchasing behavior.
  * Detect and profile churned customers.
  * Discover key drivers of customer churn.
  * Build a customer churn prediction model.
  * Recommend actionable retention strategies.
</details>

<details>
  <summary><b>🛠️ 2. Tech Stack</b></summary>
  <br>

  ### Data Processing
  * ![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=flat-square&logo=apachespark&logoColor=white)
  * ![Spark SQL](https://img.shields.io/badge/Spark_SQL-E25A1C?style=flat-square&logo=apachespark&logoColor=white)
  * ![Window Functions](https://img.shields.io/badge/Window_Functions-FF6F00?style=flat-square)
  * ![RDDs](https://img.shields.io/badge/RDDs-FF6F00?style=flat-square)

  ### Data Analysis
  * ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
  * ![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)

  ### Data Visualization
  * ![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat-square)
  * ![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=flat-square)

  ### Machine Learning
  * ![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
  * ![XGBoost](https://img.shields.io/badge/XGBoost-EC6B23?style=flat-square)
  * ![LightGBM](https://img.shields.io/badge/LightGBM-02569B?style=flat-square)

  ### Development Environment
  * ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
  * ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)
  * ![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
</details>

<details>
  <summary><b>📊 3. Dataset Overview</b></summary>
  <br>

  The dataset contains transactional records from a UK-based online retailer.

  ### Dataset Characteristics
  | Metric | Value |
  | :--- | :--- |
  | **Transactions** | 500,000+ |
  | **Country Coverage** | Primarily United Kingdom |
  | **Business Type** | B2B Online Retail |
  | **Product Categories** | Gifts, Decorations, Home Accessories |
  | **Observation Period** | Dec 2010 – Dec 2011 |

  ### Key Fields
  | Column | Description |
  | :--- | :--- |
  | `InvoiceNo` | Transaction identifier |
  | `StockCode` | Product identifier |
  | `Description` | Product description |
  | `Quantity` | Number of units purchased |
  | `InvoiceDate` | Transaction timestamp |
  | `UnitPrice` | Product unit price |
  | `CustomerID` | Customer identifier |
  | `Country` | Customer location |
</details>

<details>
  <summary><b>📈 4. Executive Summary</b></summary>
  <br>

  ### Revenue Growth
  * Revenue experienced substantial growth from 2010 to 2011, increasing by **XX% YoY**.
  * November 2011 recorded the highest monthly revenue, reaching **£XX**, representing **XX% MoM growth**.

  ### Key Growth Drivers
  The strong sales performance in 2011 was primarily driven by:
  * Expansion of the active customer base (+20% MoM).
  * Higher average order values.
  * Increased purchases from high-value customer segments.
  * Customer preference shifts toward higher-priced products.

  ### Customer Behavior
  * A relatively small group of customers generated a disproportionately large share of total revenue.
  * High-spending customers exhibited significantly higher purchase frequency and retention rates.
  * Churned customers generally showed both low purchasing frequency and long inactivity periods.
</details>

<details>
  <summary><b>⚙️ 5. Methodology</b></summary>
  <br>

  ### 5.1 Data Preparation & Cleaning
  To ensure data quality and reliable customer analytics, the following preprocessing steps were performed:

  * **Data Type Validation:**
    - Verified schema and column data types.
    - Converted `InvoiceDate` from string to timestamp format.
  * **Missing Value Handling:**
    - Audited missing values across all columns.
    - Removed **1,454** records with missing product descriptions.
    - Replaced missing `CustomerID` values (**135,080 rows**) with `"Unknown"`.
  * **Duplicate Removal:**
    - Identified and removed duplicate transaction records.
  * **Invalid Transaction Filtering:**
    - Removed cancelled invoices (`InvoiceNo` beginning with `"C"`).
    - Removed negative quantities and negative unit prices.
    - Retained only valid purchase transactions.
  * **Non-Product Transaction Removal:** Excluded operational or non-commercial records such as:
    - `POST`, `DOT`, `M` (Manual), `BANK CHARGES`, `AMAZONFEE`, Gift Voucher Entries, and Administrative Adjustment Codes.
  * **Revenue Feature Creation:**
    - Created transaction-level revenue metric:  
      $$\text{TotalPrice} = \text{Quantity} \times \text{UnitPrice}$$
    - Used for revenue analysis, customer value measurement, and RFM calculations.

  > ⚠️ **Important Note:** Transactions with `InvoiceNo` starting with **"C"** indicate cancelled orders and were excluded from subsequent analysis.

  ---

  ### 5.2 Outlier Detection
  Customer-level outliers were investigated before segmentation and churn modeling.

  * **Distribution Analysis:** Analyzed the distribution of Customer Spending, Purchase Frequency, and Transaction Value.
  * **Methods Applied:** Utilized boxplot analysis, percentile analysis, and distribution visualization.
  * **Decision:** Retained extreme customer values where appropriate, treating high-value customers as genuine business behavior rather than data errors.

  ---

  ### 5.3 Feature Engineering & Churn Definition
  Customer-level features were created to support segmentation and churn prediction.

  #### 🕒 RFM Feature Construction:
  * **Recency (R):** Days since most recent purchase.
  * **Frequency (F):** Number of unique orders.
  * **Monetary (M):** Total customer spending.

  #### 🔴 Churn Label Creation:
  Since the dataset does not contain an explicit churn indicator, a rule-based churn definition was developed.
  * **Rules:** `Recency` > 108 days (70th percentile) AND `Frequency` $\le$ 4 orders (70th percentile).

  | Label | Rule |
  | :--- | :--- |
  | **🔴 Churn = 1** | `Recency` > 108 **AND** `Frequency` $\le$ 4 |
  | **🟢 Churn = 0** | Otherwise |

  ---

  ### 5.4 Exploratory Data Analysis (EDA)
  *(Analysis of customer behavioral structures, trends, and purchasing patterns).*
</details>

<details>
  <summary><b>🤖 6. Churn Prediction</b></summary>
  <br>

  ### 6.1 Problem Statement
  Develop a classification model capable of predicting whether a customer is likely to churn based on historical purchasing behavior.

  ---

  ### 6.2 Feature Selection
  *(Selection and evaluation of feature importance for RFM and secondary behavioral metrics to train predictive models).*

  ---

  ### 6.3 Model Development
  The model development process followed a standardized workflow to ensure a fair comparison across all algorithms:

  ```mermaid
  flowchart LR
      A["📂 Train-Test Split"] --> B["⚙️ Feature Scaling"]
      B --> C["🤖 Model Training"]
      C --> D["🔍 Hyperparameter Tuning"]
      D --> E["✅ Cross Validation"]

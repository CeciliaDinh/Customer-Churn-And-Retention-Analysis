# Customer Growth and Retention Analysis

<div align="center">
  <img src="./images/churn_prediction.png" alt="Customer Growth and Retention Analysis Banner" width="100%">
</div>

**Author:** Dinh Thi Thanh Hang

<details open>
<summary><strong>1. Project Overview</strong></summary>

This project analyzes customer purchasing behavior, revenue performance, and churn risk using 500,000+ transaction records from a UK-based online retailer.

The analysis combines PySpark-based data processing, customer segmentation, behavioral analysis, and machine learning to identify growth opportunities and support data-driven customer retention strategies.

</details>

<details>
<summary><strong>2. Business Objectives</strong></summary>

- Evaluate revenue growth and purchasing performance.
- Identify high-value customer segments and their purchasing patterns.
- Understand customer retention and churn behavior.
- Identify behavioral signals associated with customer disengagement.
- Develop a churn prediction model to prioritize at-risk customers.
- Translate analytical findings into actionable growth and retention strategies.

</details>

<details>
<summary><strong>3. Dataset Overview</strong></summary>

The dataset contains transactional records from a UK-based online retailer between December 2010 and December 2011.

| Metric | Description |
|---|---|
| Transaction Records | 500,000+ |
| Observation Period | Dec 2010 – Dec 2011 |
| Business Context | Online Retail |
| Geographic Coverage | Primarily United Kingdom |
| Identified Customers | 4,334 |

**Key Fields**

| Field | Description |
|---|---|
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
<summary><strong>4. Key Business Metrics & Definitions</strong></summary>

| Metric | Definition |
|---|---|
| Revenue | `Quantity × UnitPrice` for valid purchase transactions |
| Total Orders | Number of distinct successful purchase invoices |
| Active Customers | Identified customers with successful purchases during the period |
| Average Order Value (AOV) | Total Revenue / Total Orders |
| Purchase Frequency | Number of successful purchase invoices per customer |
| Recency | Days since the customer's most recent successful purchase |
| Monetary Value | Total historical purchase value per customer |
| Cancellation Rate | Cancelled invoices relative to total purchase and cancellation activity |
| Churn | Customer inactivity and purchasing frequency-based behavioral proxy |

**Operational Churn Definition**

```text
Churn = 1 if Recency > 108 days AND Frequency <= 4
Churn = 0 otherwise
```

The dataset does not contain an explicit churn label. This rule-based definition is an operational proxy rather than directly observed customer attrition.

</details>

<details>
<summary><strong> <details>
<summary><strong>5. Analytical Approach</strong></summary>

The analysis follows a growth-oriented framework, combining business performance diagnosis, the 3Ps analytical dimensions, and customer lifecycle analysis to identify opportunities for sustainable revenue growth.

### **5.1 Growth Diagnosis**

- Analyze revenue, customer, and order trends over time.
- Decompose revenue growth into customer base, purchase frequency, and average order value (AOV).
- Identify key growth drivers, performance changes, and seasonal patterns.

### **5.2 3Ps Analysis**

**Product**

- Analyze revenue and sales contribution by product, category, and subcategory.
- Identify top-performing products and customer product preferences.
- Examine product affinity and cross-selling opportunities.

**Place**

- Analyze revenue, order, and customer distribution across geographic markets.
- Compare purchasing patterns and customer value across locations.
- Identify high-potential markets and geographic growth opportunities.

**People**

- Segment customers based on purchasing behavior and monetary value.
- Identify high-value, low-engagement, and at-risk customer segments.
- Compare purchasing patterns and product preferences across customer groups.

### **5.3 Customer Lifecycle Analysis**

**Acquire**

- Analyze new customer trends and first-purchase behavior.
- Identify customer acquisition patterns across products and locations.
- Examine early repeat-purchase signals.

**Engage & Develop**

- Analyze repeat-purchase behavior, purchase frequency, and spending patterns.
- Identify opportunities to increase customer value through basket expansion and cross-selling.
- Examine differences in purchasing behavior across customer segments.

**Retain**

- Analyze cohort retention, customer inactivity, and churn patterns.
- Identify behavioral signals associated with customer disengagement.
- Evaluate customer segments with elevated churn risk.

### **5.4 Churn Prediction**

- Construct customer-level RFM and cancellation-related features.
- Define churn using a behavioral rule based on recency and frequency.
- Benchmark Logistic Regression, Random Forest, and LightGBM.
- Apply Out-of-Time validation to evaluate performance on unseen periods.
- Use SHAP to interpret important churn predictors.

</details>

<details open>
<summary><strong>6. Key Findings & Business Recommendations</strong></summary>

### 6.1 Revenue Growth & Performance Drivers

# 📈 Revenue Growth & Performance Drivers

> **Executive Summary:** Revenue demonstrated a two-phase trajectory throughout 2011: a stable baseline across H1 followed by a massive late-year inflection. Top-line expansion was overwhelmingly driven by **Customer Base Acquisition** and **late-year purchase frequency**, successfully offsetting compressed basket sizes during holiday promotions.

---

### **1. Top-Line Trajectory: Mid-Year Plateau to Q4 Inflexion**

* **Record Revenue Peak:** Monthly revenue climbed from **$562.7K (Jan)** to break the million-dollar barrier in October ($1.002M) before peaking at **$1.137M in November (+13.4% MoM)**.
* **Q4 Growth Acceleration:** After range-bound performance between Feb–Aug ($442K–$659K), sales surged starting September ($938.8K), driven by seasonal holiday demand.

![Chart 3: Monthly Revenue Trend, January–November 2011](images/chart_3_monthly_revenue_trend.png)

---

### **2. Revenue Driver Decomposition: What Powered the Surge?**

$$\text{Revenue} = \text{Active Customers} \times \text{Order Frequency} \times \text{Average Order Value (AOV)}$$

#### **Primary Driver: Customer Acquisition Expansion (+125% YTD)**
* The customer base served as the core growth engine, expanding consistently from **739 active accounts in January to 1,660 in November (+124.6%)**.
* Massive customer influx began in September (+34.9% MoM jump to 1,259 accounts), sustaining momentum through October (1,361) and November (1,660).

![Chart 5: Monthly Active Customers, January–November 2011](images/chart_5_monthly_active_customers.png)

#### **Secondary Driver: Late-Year Order Velocity & Purchase Frequency**
* Purchase frequency reached an annual high of **1.59 orders/customer in November (+13.8% MoM)**.
* Total order volume surged to **2,642 orders in November (+38.8% MoM)**, driving transaction velocity to record levels.

#### **Commercial Trade-off: Volume Elasticity vs. Basket Size (AOV)**
* Despite record top-line revenue in November, **AOV contracted sharply to $430.18 (-18.3% MoM)**.
* *Business Insight:* High-velocity seasonal discounting (e.g., Black Friday) compressed individual basket sizes, but explosive order volume and repeat purchases easily outweighed the discount impact, maximizing total revenue.

![Chart 4: Monthly AOV, Order Volume and Order Frequency with MoM Growth, January–November 2011](images/chart_4_monthly_aov_order_volume_frequency.png)

---

### 6.3 Customer Retention & Churn Behavior

- Customers with no repeat purchase within 30 days showed approximately 3× higher churn risk.
- Customers purchasing only one product had a churn rate of approximately 71%.
- Broader product engagement was associated with lower churn risk.

*Business Implications:*
- Prioritize early re-engagement before customers become inactive.
- Encourage product discovery and cross-selling.
- Monitor customers with limited purchasing history as an early-warning segment.

---

### 6.4 Product Affinity & Cross-Selling

- FP-Growth identified product associations with co-purchase strength exceeding 60%.

*Business Implications:*
- Use frequently co-purchased products to design bundles and cross-selling recommendations.
- Promote complementary products to increase product engagement and repeat purchasing.

---

### 6.5 Churn Prediction Performance

- LightGBM achieved an ROC-AUC of **0.77** using Out-of-Time validation.
- The model achieved **1.35× Lift@20%**.
- SHAP analysis highlighted cancellations, product diversity, and customer tenure among the important churn-related features.

*Business Implications:*
- Use model scores to prioritize retention outreach.
- Investigate cancellation behavior and declining product engagement.
- Combine predictive scores with customer value when allocating retention resources.

</details>

</details>

<details>
<summary><strong>7. Proposed Retention Strategy Framework</strong></summary>

| Customer Segment | Observed Behavior | Proposed Strategy |
|---|---|---|
| New Customers | Disengagement after 1–2 purchases | Onboarding and second-purchase incentives |
| Early At-Risk Customers | No repeat purchase within 30 days | Timely reminders and personalized recommendations |
| Single-Product Customers | Limited product engagement | Cross-selling and complementary product offers |
| High-Value Customers | High historical monetary contribution | Personalized offers and loyalty initiatives |
| High Churn-Risk Customers | Elevated model-predicted churn risk | Prioritized retention outreach |

The proposed framework is intended to guide future retention experiments. Its actual business impact would need to be measured through controlled campaign evaluation.

</details>

<details>
<summary><strong>8. Limitations & Further Analysis</strong></summary>

**Limitations**

- The dataset covers approximately one year, limiting the ability to assess long-term customer lifetime behavior.
- Churn is defined using a behavioral proxy rather than an explicitly observed customer attrition label.
- Customer-level analysis excludes transactions without a `CustomerID`.
- Predictive performance reflects the operational churn definition and does not necessarily represent confirmed customer attrition.
- Historical transaction data does not capture the impact of actual retention interventions.

**Further Analysis**

- Validate the churn definition using longer observation periods.
- Evaluate retention strategies through controlled experiments.
- Develop customer lifetime value (CLV) estimates.
- Monitor model performance and churn patterns over time.
- Assess the incremental revenue and retention impact of targeted interventions.

</details>

<details>
<summary><strong>9. Tools & Technologies</strong></summary>

**Data Processing**

![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![Spark SQL](https://img.shields.io/badge/Spark_SQL-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)

**Data Analysis**

![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)

**Data Visualization**

![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=for-the-badge)

**Machine Learning**

![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-EC6B23?style=for-the-badge)
![LightGBM](https://img.shields.io/badge/LightGBM-02569B?style=for-the-badge)

**Development Environment**

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

</details>

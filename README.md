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
<summary><strong>5. Analytical Approach</strong></summary>

The analysis follows three stages, moving from business performance to customer behavior and churn prediction.

**5.1 Revenue & Purchasing Performance**

- Analyze revenue and order trends over time.
- Examine changes in customer activity and average order value.
- Identify periods of strong growth and potential changes in purchasing behavior.

**5.2 Customer Behavior & Segmentation**

- Segment customers based on purchasing value and behavioral patterns.
- Analyze customer cohorts and repeat-purchase behavior.
- Compare purchasing patterns between retained and churned customers.
- Examine product preferences, purchase frequency, and cancellation behavior.
- Identify early signs of customer disengagement.

**5.3 Churn Prediction**

- Construct customer-level RFM and cancellation-related features.
- Define churn using a behavioral rule based on recency and frequency.
- Benchmark Logistic Regression, Random Forest, and LightGBM.
- Apply Out-of-Time validation to evaluate performance on unseen periods.
- Use SHAP to interpret important churn predictors.

</details>

<details>
<summary><strong>6. Key Findings & Business Recommendations</strong></summary>

**Customer Acquisition & Early Engagement**

- Approximately 30% of customers disengaged after only one or two purchases.
- Around 20% of new customers showed a preference for premium home décor products in Q3.

*Business implications:*
- Strengthen onboarding and post-purchase engagement.
- Encourage second purchases through relevant product recommendations.
- Explore targeted acquisition based on promising customer and product profiles.

**Customer Retention & Churn Behavior**

- Customers with no repeat purchase within 30 days showed approximately 3× higher churn risk.
- Customers purchasing only one product had a churn rate of approximately 71%.
- Broader product engagement was associated with lower churn risk.

*Business implications:*
- Prioritize early re-engagement before customers become inactive.
- Encourage product discovery and cross-selling.
- Monitor customers with limited purchasing history as an early-warning segment.

**Product Affinity & Cross-Selling**

- FP-Growth identified product associations with co-purchase strength exceeding 60%.

*Business implications:*
- Use frequently co-purchased products to design bundles and cross-selling recommendations.
- Promote complementary products to increase product engagement and repeat purchasing.

**Churn Prediction Performance**

- LightGBM achieved an ROC-AUC of **0.77** using Out-of-Time validation.
- The model achieved **1.35× Lift@20%**.
- SHAP analysis highlighted cancellations, product diversity, and customer tenure among the important churn-related features.

*Business implications:*
- Use model scores to prioritize retention outreach.
- Investigate cancellation behavior and declining product engagement.
- Combine predictive scores with customer value when allocating retention resources.

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

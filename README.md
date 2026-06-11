# Customer Churn and Retention Analysis

<div align="center">
  <img src="./online_store.webp" alt="Customer Churn and Retention Analysis Banner" width="100%">
</div>

<br>

**Author:** Dinh Thi Thanh Hang

## Project Overview

This project analyzes customer purchasing behavior and churn patterns using over 500,000 transaction records from a UK-based B2B online retailer specializing in gifts, decorations, and home accessories.

Using PySpark and Python, the project explores customer purchasing trends, identifies churn drivers, segments customers based on behavioral patterns, and develops a churn prediction framework to support retention strategies.

### Business Objectives

* Analyze revenue growth and sales performance
* Understand customer purchasing behavior
* Identify customer segments through RFM analysis
* Detect and profile churned customers
* Discover key drivers of customer churn
* Build a customer churn prediction model
* Recommend actionable retention strategies

---

## Tech Stack

### Data Processing

* PySpark

  * Spark SQL
  * Window Functions
  * RDDs

### Data Analysis

* Pandas
* NumPy

### Data Visualization

* Matplotlib
* Seaborn

### Machine Learning

* Scikit-learn

---

## Dataset Overview

The dataset contains transactional records from a UK-based online retailer.

### Dataset Characteristics

| Metric             | Value                                |
| ------------------ | ------------------------------------ |
| Transactions       | 500,000+                             |
| Country Coverage   | Primarily United Kingdom             |
| Business Type      | B2B Online Retail                    |
| Product Categories | Gifts, Decorations, Home Accessories |
| Observation Period | Dec 2010 – Dec 2011                  |

### Key Fields

| Column      | Description               |
| ----------- | ------------------------- |
| InvoiceNo   | Transaction identifier    |
| StockCode   | Product identifier        |
| Description | Product description       |
| Quantity    | Number of units purchased |
| InvoiceDate | Transaction timestamp     |
| UnitPrice   | Product unit price        |
| CustomerID  | Customer identifier       |
| Country     | Customer location         |

---

# Executive Summary

### Revenue Growth

* Revenue experienced substantial growth from 2010 to 2011, increasing by **XX% YoY**.
* November 2011 recorded the highest monthly revenue, reaching **£XX**, representing **XX% MoM growth**.

### Key Growth Drivers

The strong sales performance in 2011 was primarily driven by:

* Expansion of the active customer base (+20% MoM)
* Higher average order values
* Increased purchases from high-value customer segments
* Customer preference shifts toward higher-priced products

### Customer Behavior

* A relatively small group of customers generated a disproportionately large share of total revenue.
* High-spending customers exhibited significantly higher purchase frequency and retention rates.
* Churned customers generally showed both low purchasing frequency and long inactivity periods.

---

# Methodology

## 1. Data Preparation

### 1.1 Data Cleaning

To ensure data quality and reliable customer analytics, the following preprocessing steps were performed.

#### Data Type Validation

* Verified schema and column data types.
* Converted `InvoiceDate` from string to timestamp format.

#### Missing Value Handling

* Audited missing values across all columns.
* Removed 1,454 records with missing product descriptions.
* Replaced missing `CustomerID` values (135,080 rows) with `"Unknown"`.

#### Duplicate Removal

* Identified and removed duplicate transaction records.

#### Invalid Transaction Filtering

Removed:

* Cancelled invoices (`InvoiceNo` beginning with `"C"`)
* Negative quantities
* Negative unit prices

Only valid purchases were retained for analysis.

#### Non-Product Transaction Removal

Excluded operational records including:

* POST
* DOT
* M
* BANK CHARGES
* AMAZONFEE
* Gift voucher entries
* Administrative adjustment codes

#### Revenue Feature Creation

Created a transaction-level metric:

```python
TotalPrice = Quantity * UnitPrice
```

This metric was used for revenue, customer value, and RFM calculations.

---

### 1.2 Outlier Detection

Outliers were analyzed across:

* Customer spending
* Purchase frequency
* Transaction values

Methods used:

* Boxplots
* Percentile analysis
* Distribution visualization

Extreme customer values were retained where appropriate, as they represent genuine high-value customers rather than data errors.

---

### 1.3 Feature Engineering

Customer-level features were created to support segmentation and churn prediction.

#### RFM Metrics

| Feature   | Definition                      |
| --------- | ------------------------------- |
| Recency   | Days since most recent purchase |
| Frequency | Number of unique orders         |
| Monetary  | Total customer spending         |

### Churn Label Creation

Because the dataset does not contain an explicit churn indicator, a rule-based churn definition was created.

A customer is classified as churned when:

* Recency > 108 days (70th percentile)
* Frequency ≤ 4 orders (70th percentile)

| Churn Status | Condition                       |
| ------------ | ------------------------------- |
| Churn = 1    | Recency > 108 AND Frequency ≤ 4 |
| Churn = 0    | Otherwise                       |

This churn label serves as the target variable for predictive modeling.

---

## 2. Exploratory Data Analysis

### 2.1 Analytical Framework

The following business metrics were evaluated:

* Revenue
* Active Customers
* Average Order Value (AOV)
* Purchase Frequency
* Customer Lifetime Value (CLV)
* Customer Retention Rate
* Customer Churn Rate

---

### 2.2 Revenue Analysis

Key questions:

* How has revenue evolved over time?
* Are there seasonal purchasing patterns?
* Which product categories drive revenue growth?
* What factors contributed to peak sales periods?

#### Key Findings

* Revenue increased significantly throughout 2011.
* Strong seasonal effects were observed during Q4.
* November 2011 generated the highest monthly sales.
* High-priced product categories contributed the majority of revenue.

---

### 2.3 Customer Segmentation Analysis

Customers were segmented using RFM analysis.

Segments identified:

* Champions
* Loyal Customers
* Potential Loyalists
* At Risk
* Hibernating Customers
* Lost Customers

#### Key Findings

* A small proportion of customers generated the majority of revenue.
* Loyal customers exhibited significantly higher order frequency.
* Churn risk was concentrated among low-frequency purchasers.

---

### 2.4 Retention and Churn Analysis

Objectives:

* Quantify churn rate
* Understand churn behavior
* Identify risk indicators

#### Key Findings

* Churned customers displayed substantially longer inactivity periods.
* Purchase frequency strongly influenced retention.
* Monetary value alone was insufficient to predict churn.

---

## 3. Churn Prediction

### 3.1 Problem Statement

Develop a classification model capable of predicting whether a customer is likely to churn based on historical purchasing behavior.

---

### 3.2 Feature Selection

Candidate features included:

* Recency
* Frequency
* Monetary
* Average Order Value
* Purchase Interval
* Customer Lifetime Metrics

---

### 3.3 Model Development

Workflow:

1. Train-test split
2. Feature scaling
3. Model training
4. Hyperparameter tuning
5. Cross-validation

Models evaluated:

* Logistic Regression
* Random Forest
* XGBoost (Optional)

---

### 3.4 Model Evaluation

Evaluation metrics:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC

Model performance was compared to identify the best balance between identifying churned customers and minimizing false positives.

---

# Key Business Insights

### Revenue Drivers

* Growth in active customers was the primary contributor to revenue expansion.
* Higher-value product categories generated a disproportionate share of revenue.

### Customer Behavior

* Repeat customers contributed the majority of revenue.
* Customer retention strongly correlated with purchase frequency.

### Churn Indicators

Strong indicators of churn included:

* Long inactivity periods
* Low order frequency
* Low customer engagement

---

# Recommendations

### Customer Retention

* Launch reactivation campaigns targeting inactive customers.
* Offer personalized promotions to at-risk segments.
* Implement loyalty and rewards programs.

### Revenue Growth

* Prioritize acquisition of high-value customer segments.
* Cross-sell complementary products to existing customers.
* Promote high-margin product categories.

### Predictive Analytics

* Deploy churn monitoring dashboards.
* Integrate churn prediction into CRM workflows.
* Trigger retention campaigns automatically for high-risk customers.

---

# Future Improvements

* Incorporate marketing campaign data.
* Include customer demographics.
* Develop real-time churn prediction pipelines.
* Build an interactive dashboard using Power BI or Tableau.

---

# Repository Structure

```text
Customer-Churn-And-Retention-Analysis/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   ├── Data_Cleaning.ipynb
│   ├── EDA.ipynb
│   └── Churn_Modeling.ipynb
│
├── images/
│   ├── online_store.webp
│   ├── revenue_trend.png
│   ├── churn_distribution.png
│   └── rfm_segmentation.png
│
├── src/
│
├── README.md
│
└── requirements.txt
```

---

## Contact

**Dinh Thi Thanh Hang**

* LinkedIn: *Your LinkedIn URL*
* Email: *Your Email Address*
* GitHub: *Your GitHub Profile*

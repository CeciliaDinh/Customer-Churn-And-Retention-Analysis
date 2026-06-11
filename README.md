
# Customer Churn And Retention Analysis 
**Author:** Dinh Thi Thanh Hang
- In this project, I leveraged PySpark (Window Functions, SparkSQL, Rdds) and Python (Pandas, NumPy, Seaborn) to clean and analyze 500K+ rows of transactions from an B2B online store based in the UK, which sells mostly gifts, decorations.
### Executive Summary 
- Revenue witnessed significant growth from XX in 2010 to XX to 2011 (+XX YoY). Worth noticing is that November 2011, showed the highest sales peak ever with revenue reaching XX (+XX MoM)
- The main revenue drivers for such significant growth in 2011, are the the significant increase in customer base (+20% MoM) and slightly higher average order value (+XX MoM) with customers preferences shifting towards products with higher prices.
### I. Project Overview & Key Objectives: 
- This project aims to identify and validate key sales trend, and profile customers based purchasing behaviors, to grow new customers, engage existing customers, and reduce churn rate by uncovering key root causes of churn. 
#### Dataset Overview 

### III. Methodology 
#### 1. Data Cleaning 
## 1.1 Data Preprocessing Checklist

To ensure data quality and reliable customer analytics, the following preprocessing steps were performed:

### ✅ Data Type Validation & Correction

* Inspected the dataset schema and verified column data types.
* Converted `InvoiceDate` from string format to timestamp format to enable time-series analysis and customer lifecycle tracking.

### ✅ Missing Value Handling

* Audited missing values across all columns.
* Removed records with missing `Description` values (1,454 rows), as product information could not be reliably inferred.
* Replaced missing `CustomerID` values (135,080 rows) with `"Unknown"` to preserve transaction records while distinguishing anonymous customers.

### ✅ Duplicate Record Removal

* Identified duplicate transactions in the dataset.
* Removed duplicate rows to prevent inflation of sales, customer counts, and transaction-based metrics.

### ✅ Cancellation & Invalid Transaction Filtering

* Identified cancelled orders using invoice numbers beginning with `"C"`.
* Removed:

  * Cancelled transactions
  * Records with negative quantities
  * Records with negative unit prices
* Retained only valid purchase transactions for customer behavior analysis.

### ✅ Non-Product Transaction Removal

* Identified abnormal `StockCode` values representing operational charges rather than actual products, including:

  * `POST` (Postage fees)
  * `DOT` (Discount adjustments)
  * `M` (Manual adjustments)
  * `BANK CHARGES`
  * `AMAZONFEE`
  * Gift voucher codes and other administrative entries
* Excluded these records to ensure product-level analyses reflected genuine customer purchases.

### ✅ Revenue Feature Creation

* Created a new transaction-level metric:

> **TotalPrice = Quantity × UnitPrice**

* Used this metric as the foundation for revenue, customer value, and RFM calculations.

### ✅ Customer-Level Aggregation

* Aggregated transaction-level data into customer-level metrics to support customer segmentation, churn analysis, and predictive modeling.

---

## 1.2 Feature Engineering

To profile customer purchasing behavior and support churn prediction, Recency, Frequency, and Monetary (RFM) features were constructed.

### RFM Metrics

| Feature       | Definition                                               |
| ------------- | -------------------------------------------------------- |
| **Recency**   | Number of days since the customer's most recent purchase |
| **Frequency** | Number of distinct orders placed by the customer         |
| **Monetary**  | Total amount spent by the customer across all purchases  |

### Churn Label Creation

Because the dataset does not contain an explicit churn indicator, a rule-based churn definition was created using customer purchasing behavior.

Customers were classified as **churned** when:

* **Recency > 108 days** (70th percentile)
* **Frequency ≤ 4 orders** (70th percentile)

This approach identifies customers who have not purchased for an extended period and have historically exhibited low purchasing activity.

| Churn Status  | Condition                       |
| ------------- | ------------------------------- |
| **Churn = 1** | Recency > 108 AND Frequency ≤ 4 |
| **Churn = 0** | Otherwise                       |

The resulting churn label was used as the target variable for subsequent customer retention analysis and churn prediction modeling.


#### 1.1. Data Preprocessing Checklist 
#### 1.2. Outliers Detection 

#### 1.3. Feature Engineering 
#### 2. Data Analysis 
#### 2.1. Approach & Key Metrics Definition 
#### 2.2. Detailed Analysis 
#### 3. Churn Prediction 
#### 3.1. Problem Statement
#### 3.2. Feature And Model Selection
#### 3.3. Model Building 
#### 3.4. Model Evaluation & Tuning 



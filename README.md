
# 🧠 Customer 360 Analytics
### Cohort Retention, FP-Growth & RFM Analysis using Python & PySpark
**Author:** Dinh Thi Thanh Hang

---

## 🚀 Project Overview

This project leverages **Python and PySpark** to perform full-scale customer analytics on a retail transactional dataset (500K+ records). The objective is to translate raw data into actionable business strategies that optimize revenue, retention, and geographic expansion. 

The analysis is structured using the **3P-G Framework**:
> **Product – People – Place – Growth**

---

## 🧩 Problem Statement

Despite healthy topline revenue, the business faces critical bottlenecks that threaten long-term profitability:
* ⚠️ **High Churn Risk (~32%)** driven by a "leaky bucket" of one-time buyers.
* 🇬🇧 **Geographic Over-reliance** on the UK market.
* 🎯 **Weak Post-Purchase Retention** failing to convert first-time buyers into loyalists.
* 📉 **Revenue Volatility** heavily dependent on seasonal spikes.

---

## 🛠️ Tech Stack

* **Data Processing & ML:** PySpark (Window Functions, MLlib for FP-Growth)
* **Exploratory Analytics:** Python (Pandas, NumPy)
* **Algorithms:** FP-Growth (Market Basket Analysis), K-Means Clustering
* **Analytics Framework:** RFM (Recency, Frequency, Monetary), Cohort Analysis
* **Visualization:** Matplotlib, Seaborn

---

# 📖 The Data Story: Diagnosing the "Leaky Bucket"

To solve the high churn rate, I connected three distinct analytical approaches—Cohort Analysis, Product Correlation, and Market Basket Analysis—to find the root cause and the optimal solution.

### Part 1: The Symptom - When do we lose customers?
![Customer Cohort Retention Heatmap](images/cohort_heatmap.png)

* **Insight:** The Cohort Retention Heatmap reveals a drastic drop-off immediately after the first month. For instance, the Jan 2011 cohort drops from 100% down to just 22% by Month 1.
* **Conclusion:** The business does not have an acquisition problem; it has a **post-purchase experience problem**. The critical window to retain a customer is within the first 30 days.

### Part 2: The Root Cause - Why are they leaving?
To understand *why*, I analyzed the specific items present in the baskets of churned customers.

![Top Products Purchased by Churn Customers](images/churn_products.png)

* **Insight:** Churned users heavily over-index on specific items: *White Hanging Heart T-Light Holder, Regency Cakestand 3 Tier, and Party Bunting.*
* **Strategic Diagnosis (2 Hypotheses):**
  1. **The Event-Driven Churn:** These are highly specific event items (Weddings, Tea Parties). Customers buy them for a one-off life event, meaning churn is a natural product characteristic.
  2. **The Fragility Risk:** Cakestands and T-Light holders are fragile. If inadequate packaging leads to shipping damage, it destroys the customer experience immediately.

### Part 3: The Solution - Maximizing Value Upfront (FP-Growth)
If customers are naturally prone to leaving after one event-driven purchase, the strategy must pivot from *long-term retention* to **maximizing Average Order Value (AOV) upfront**. I applied the **FP-Growth algorithm** to discover high-affinity cross-sell opportunities.

![Market Basket Analysis - FP Growth](images/fp_growth_table.png)

* **Insight:** The ML model yielded incredibly strong association rules:
  * **The Christmas Set:** `Wooden Heart` & `Wooden Star` (Lift: **26.54**, Confidence: 81%).
  * **The Regency Set:** `Pink Regency Teacup` & `Green/Roses Regency Teacup` (Lift: **18.81 - 19.17**, Confidence: 71-91%).
* **Actionable Solution:** Notice that the *Regency Cakestand* drives churn, but *Regency Teacups* are highly co-purchased. We must create a **"Complete Regency Tea Party Bundle"** (Teacups + Cakestand) at a slight premium. This extracts maximum value in the *first* transaction before the customer potentially churns.

---

# 👥 Deeper Analytics: People & Place

## 1. Customer Behavior (Average RFM per User)

| Metric (Per User Avg) | Active Loyalists | Churned Customers |
|-----------------------|----------------|-----------------|
| **Recency** | 16 days | 197 days |
| **Frequency** | ~12.4 purchases | ~1.2 purchases |
| **Monetary (CLV)** | High Value | Low Value |

💡 **Takeaway:** Churned users typically abandon the brand after just **1 to 2 purchases**. Converting a user to their 3rd purchase is the statistical tipping point for long-term loyalty.

## 2. Customer Segmentation (K-Means Clustering)
Using K-Means and behavioral features, I identified 4 actionable customer personas:

* 🟡 **One-Time Buyers (High Flight Risk):** Need immediate automated onboarding & reactivation campaigns within 14 days of purchase.
* 🟢 **Loyal Core:** High frequency, top revenue drivers. Ripe for VIP perks, early-access, and referral programs.
* 🔵 **Discount Hunters:** High price sensitivity. Limit their discount abuse; leverage flash sales only to clear old inventory.
* 🟣 **New High-Potential:** Recent activity, full-price buyers. Require premium "Welcome Kits" to secure the crucial second purchase.

## 3. Geographic Expansion & Churn Risk
* **United Kingdom:** The main revenue engine (~3,900 users) but suffers a massive **~33% churn rate**. Needs urgent retention focus.
* **Emerging Markets (Australia, EU):** Exhibiting strong baseline growth. A clear path to diversify revenue away from UK dependence. A localized, market-specific retention strategy is required.

---

# 🚀 Executive Recommendations

1. **Deploy Dynamic Bundling:** Integrate the FP-Growth association rules directly into the e-commerce recommendation engine ("Frequently Bought Together").
2. **Audit Quality Assurance (Urgent):** Immediately review the supply chain, packaging, and shipping damage rates for the top 5 fragile items bought by churned users to stop product-driven churn.
3. **Launch a 30-Day Reactivation Sequence:** Since cohorts drop sharply at Month 1, deploy automated retention workflows targeting the "One-Time Buyer" segment at Day 14 and Day 28.
4. **Scale High-Growth Markets:** Aggressively allocate acquisition budget to hyper-growth regions (e.g., Australia) to reduce geographic reliance on the UK.

---

# 📌 Key Takeaway

> The most profitable business opportunity is not top-of-funnel acquisition —  
> **it’s plugging the leaky bucket, maximizing initial basket size via ML bundling, and converting one-time buyers into lifelong loyalists.**

---

## 📬 Contact
**Dinh Thi Thanh Hang**  
Reach out for collaboration or discussion!

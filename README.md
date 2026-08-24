# 📊 Customer Churn & Retention Analysis (Power BI)

An end-to-end analysis of **3.15M+ transaction records across 48,723 customers**, built using Python and Power BI to identify customer churn, current retention risk, customer value, and actionable retention opportunities.

---

## 📌 Project Overview

Customer transaction data can reveal important patterns about engagement, customer value, and potential churn. This project transforms raw transaction records into a customer-level analytical dataset and an interactive Power BI dashboard designed to help businesses understand **who is at risk and where retention efforts should be focused**.

The analysis uses **Python/Pandas** for data cleaning, feature engineering, churn analysis, and customer segmentation, followed by **Power BI** for interactive visualization and business insights.

**Dataset:** Transaction-level customer data  
**Transactions:** 3,159,157  
**Unique Customers:** 48,723  
**Period:** January 2023 – December 2023  
**Dashboard:** 2-page interactive Power BI report

---

## 🗂️ Dataset Description

Each row represents a single customer transaction.

| Category | Columns |
|---|---|
| Customer | `customer_id` |
| Transaction | `date`, `amount` |
| Transaction Type | `type` |

### Key Statistics

- **3,159,157** total transactions
- **48,723** unique customers
- **0** missing values in the final transaction dataset
- **0** duplicate customer IDs in the customer-level dataset
- Transaction period: **January 2023 – December 2023**

---

## 🔄 Analysis Workflow


Raw Transaction Data
        ↓
Data Cleaning
        ↓
Customer-Level Feature Engineering
        ↓
Historical Churn Analysis
        ↓
Recency / Frequency / Value Segmentation
        ↓
Retention Prioritization
        ↓
Power BI Dashboard
        ↓
Business Insights & Recommendations
##### 🔥 Churn Definition
The project uses two separate customer-status concepts.
Historical Churn
A customer is classified as historically churned if they had transaction activity before 30 September 2023, but had no transaction from 1 October through 29 December 2023.
Historical Results:
Metric	Value
Total Customers	48,723
Historical Churned	780
Retained	47,943
Churn Rate	1.60%
Retention Rate	98.40%


Current Customer Status
Current activity is measured using recency as of 29 December 2023.
Recency	Status	Customers
0–30 days	Active	39,378
31–60 days	At Risk	6,696
61–90 days	High Risk	1,896
90+ days	Inactive	753


Customers requiring attention: 9,345
Historical churn and 90+ days inactivity are intentionally treated as separate metrics.

#### 👥 Customer Segmentation
Customers were analyzed across three key behavioral dimensions:
Recency
Measures how recently a customer made a transaction.
Frequency
Measures how frequently a customer transacts.
Frequency Segment	Customers
Low Frequency	24,712
Regular Frequency	12,065
High Frequency	7,132
Very High Frequency	4,814


Value
Customers were segmented based on total customer spend:
- Low Value
- Regular Value
- High Value
- Very High Value
These dimensions were combined to identify customer groups and prioritize retention efforts.
#### 🚨 Retention Prioritization
Customer retention priority was determined using recency, frequency, and customer value.
Key retention groups identified:
Retention Group	Customers
Customers Requiring Attention	9,345
High-Value At Risk	2,294
High-Value High Risk	580
High-Value 90+ Days Inactive	216


This helps move the analysis from simply measuring churn to identifying actionable retention opportunities.
##### 📊 Power BI Dashboard
The Power BI report contains 2 interactive pages:
1. Executive Overview
Provides a high-level view of overall customer and transaction health.
Includes:
- Total Customers
- Total Transactions
- Total Customer Spend
- Historical Churned Customers
- Retained Customers
- 90+ Days Inactive Customers
- Churn Rate
- Retention Rate
- Customer Segment Distribution
- Current Customer Health
- Monthly Transaction Trend
- Monthly Customer Spend Trend
2. Churn & Retention Analysis
Focuses on identifying customers who require retention attention.
Includes:
- Customers Needing Attention
- High-Value At Risk
- High-Value High Risk
- High-Value Inactive
- Retention Priority Distribution
- Retention Priority by Customer Value
- Retention Priority by Customer Frequency
- Historical Churn by Customer Value
- Historical Churn by Customer Frequency
- Customer Retention Action List
The dashboard includes interactive slicers for:
- Recency
- Customer Value
- Customer Frequency
#### 🔍 Key Insights
- The historical churn rate was 1.60%, with a 98.40% retention rate.
- 9,345 customers currently show some level of inactivity or retention risk.
- 6,696 customers are currently At Risk and represent the largest immediate retention opportunity.
- 2,294 high/very-high-value customers are currently At Risk and should receive higher retention priority.
- 580 high/very-high-value customers are in the High-Risk stage and require urgent intervention.
- 753 customers are currently inactive for 90+ days, including 216 high/very-high-value customers who represent important win-back opportunities.
####💡 Business Recommendations
Customer Situation	Recommended Action
Active + Valuable	Maintain & nurture
At Risk + High Value	Re-engagement campaign
High Risk + High Value	Urgent intervention
90+ Days Inactive + High Value	Win-back campaign
At Risk + Low Value	Standard re-engagement
Active + Low Value	Maintain / nurture


The analysis supports a targeted retention strategy instead of treating all customers equally.
#### 🛠️ Tools & Techniques
- Python – Data analysis and feature engineering
- Pandas / NumPy – Data cleaning and transformation
- Jupyter Notebook – Exploratory analysis
- Power BI Desktop – Dashboard development
- DAX – KPI and analytical measures
- Power Query – Data transformation
- Data Visualization – Interactive charts, slicers, KPI cards, and tables


## 👤 Author

**Prashant Solanki**
B.Tech Computer Science, GLA University
[GitHub](https://github.com/Prashant963478)

##Screenshot


<img width="1345" height="742" alt="image" src="https://github.com/Prashant963478/Customer-Churn-Analysis/blob/main/Executive%20Overview.png" />
<img width="1345" height="742" alt="image" src="https://github.com/Prashant963478/Customer-Churn-Analysis/blob/main/Churn%20Retention%20%26%20Analysis.png" />

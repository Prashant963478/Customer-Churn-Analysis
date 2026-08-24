# Customer Churn & Retention Analysis

An end-to-end customer retention analysis using **3,159,157 transaction records** across **48,723 customers**. The project converts transaction-level activity into customer-level recency, frequency, value, and retention-priority insights, with an interactive two-page Power BI dashboard.

> **Important terminology:** this project keeps **Historical Churn** and **Current 90+ Days Inactive** as separate measures. They answer different questions and must not be used interchangeably.

## Business Objective

This project answers practical customer-retention questions:

- How many customers were historically observed to churn during a defined observation window?
- Which customers are currently active, at risk, high risk, or inactive?
- Which high-value customers should be prioritized for retention or win-back efforts?
- How can recency, transaction frequency, and customer value support targeted action?
- How can these insights be explored interactively in Power BI?

The analysis identifies behavioral patterns and prioritization opportunities. It does **not** establish causal reasons for churn or inactivity.

---

## Dataset

The source is transaction-level customer data covering **4 January 2023 to 29 December 2023**.

| Metric | Value |
|---|---:|
| Transaction records | 3,159,157 |
| Unique customers | 48,723 |
| Transaction-level columns | 4 |

### Transaction-Level Columns

| Column | Description |
|---|---|
| `customer_id` | Unique customer identifier |
| `date` | Transaction date |
| `amount` | Transaction amount |
| `type` | Transaction type |

---

## Data Preparation

Python and Pandas were used to create an analysis-ready transaction dataset.

- Converted `date` to datetime format.
- Checked missing values and duplicate transaction records.
- Validated customer identifiers, data types, transaction dates, and transaction amounts.
- Created a clean transaction dataset for customer-level aggregation.

The final transaction-level dataset contains **3,159,157 rows** and the four fields above, with no missing values reported in the cleaned dataset.

---

## Customer-Level Feature Engineering

Transactions were aggregated so that each row represents one customer. The resulting customer-level dataset contains **48,723 unique customers**, with no duplicate customer IDs or missing values.

| Feature | Description |
|---|---|
| `first_tx` | First transaction date |
| `last_tx` | Most recent transaction date |
| `transaction_count` | Total transactions by the customer |
| `customer_tenure_days` | Days between first and last transaction |
| `avg_days_between_transactions` | Average interval between transactions |
| `recency_days` | Days since the most recent transaction as of 29 Dec 2023 |
| `recency_band` | Current activity/risk band based on recency |
| `frequency_segment` | Transaction-frequency group |
| `total_spend` | Customer's cumulative transaction amount |
| `avg_transaction_value` | Average amount per transaction |
| `value_segment` | Customer value group based on total spend |
| `retention_priority` | Recommended retention-action priority |
| `customer_segment` | Combined behavioral segment |
| `churned` | Historical churn label |

---

## Churn and Current-Status Definitions

### 1. Historical Churn — Observed Outcome

Historical churn uses a fixed observation window. A customer is classified as **historically churned** when they had transaction activity before **30 September 2023** but no transaction between **1 October and 29 December 2023**.

| Metric | Value |
|---|---:|
| Total customers | 48,723 |
| Historical churned customers | 780 |
| Retained customers | 47,943 |
| Historical churn rate | 1.60% |
| Retention rate | 98.40% |

This measure answers:

> “How many customers were observed to churn in the historical observation window?”

### 2. Current Status — Recency as of 29 December 2023

Current activity is evaluated separately using:

```text
recency_days = 29 Dec 2023 − customer last_tx
Recency Band	Definition	Customers	Share of Customers
Active	0–30 days since last transaction	39,378	80.82%
At Risk	31–60 days	6,696	13.74%
High Risk	61–90 days	1,896	3.89%
90+ Days Inactive	More than 90 days	753	1.55%
Customers Needing Attention	At Risk + High Risk + 90+ Days Inactive	9,345	19.18%


90+ Days Inactive (753) is a current recency status; it is not the historical churn label. The difference from the historical churn count (780) is expected because the measures apply different business logic.
Segmentation and Retention Priorities
Recency
Recency shows how recently customers transacted and supports early intervention:
Active → At Risk → High Risk → 90+ Days Inactive
Frequency
Frequency Segment	Customers
Low Frequency	24,712
Regular Frequency	12,065
High Frequency	7,132
Very High Frequency	4,814


Value
Customers are grouped by total_spend into:
- Low Value
- Regular Value
- High Value
- Very High Value
The value groups are quartile-based and therefore approximately equal in customer count.
Retention Priority Framework
Recency, frequency, and value are combined to support action-oriented segments.
Customer Situation	Suggested Priority / Action
Active, valuable customer	Healthy / Maintain
At Risk, high or very high value	Re-engagement
High Risk, high or very high value	Urgent re-engagement
90+ Days Inactive, high or very high value	Win-back
At Risk, lower value	Standard re-engagement


Priority is a decision-support framework based on observed customer characteristics. It does not imply that any individual characteristic causes churn.
Power BI Dashboard
The dashboard contains two interactive pages.
Page 1 — Executive Overview
This page answers:
“What is happening with the customer base?”

Key components include:
- Total customers, transactions, and customer spend
- Historical churned and retained customers
- Historical churn rate and retention rate
- 90+ Days Inactive customers
- Current customer-health distribution
- Customer-segment distribution
- Monthly transaction trend
- Monthly customer-spend trend
Page 2 — Churn & Retention Analysis
This page answers:
“Who needs attention and where should retention focus?”

Key components include:
- Customers needing attention
- High-value At Risk, High Risk, and 90+ Days Inactive customers
- Retention-priority distribution
- Retention priority by customer value and frequency
- Historical churn by value and frequency
- Customer-level retention action list
Dynamic Slicers and Interactions
The report uses interactive filtering and slicers to explore results by:
- Current risk / recency band
- Customer value segment
- Customer frequency segment
- Transaction type
Key Findings
1. Historical churn was low: 780 customers were historically observed as churned, resulting in a 1.60% churn rate and a 98.40% retention rate.
2. The immediate retention opportunity is broader than observed historical churn: 9,345 customers (19.18%) were currently in an At Risk, High Risk, or 90+ Days Inactive status.
3. At Risk is the largest intervention group: 6,696 customers had not transacted for 31–60 days, making this the main early-intervention population.
4. High-value customers deserve focused action: 2,294 high/very-high-value customers were At Risk, and 580 were High Risk.
5. Win-back is a defined opportunity: 753 customers were currently 90+ days inactive, including 216 high/very-high-value customers.
6. Frequency should be interpreted alongside value and recency: Low Frequency is the largest frequency group with 24,712 customers, but frequency alone does not determine customer value or future churn behavior.
These are descriptive findings and prioritization signals, not evidence of causal relationships.
Recommendations
Target Group	Recommended Action
Active, high-value customers	Maintain engagement through loyalty, personalized communication, and relevant cross-sell or upsell offers.
At Risk, high-value customers	Run timely personalized re-engagement campaigns before customers move into a higher-risk band.
High Risk, high-value customers	Use urgent, stronger, and more targeted outreach; monitor response.
90+ Days Inactive, high-value customers	Use tailored win-back campaigns and evaluate reactivation response.
At Risk, lower-value customers	Use scalable standard re-engagement messaging and offers.


Campaign outcomes should be tracked with controlled testing where possible before attributing retention improvements to a specific intervention.
Tools & Technologies
Data Analysis
- Python
- Pandas
- NumPy
- Jupyter Notebook
Business Intelligence
- Microsoft Power BI
- Power Query
- DAX
Concepts Applied
- Data Cleaning
- Feature Engineering
- Customer Segmentation
- Exploratory Data Analysis
- Churn Analysis
- Retention Analysis
- KPI Development
- Business Intelligence
Project Structure
Customer_Churn_Retention_Analysis/
├── 01_Raw_Data/
│   └── transaction_data.csv
├── 02_Cleaned_Data/
│   ├── transaction_data_clean.csv
│   └── customer_data_clean.csv
├── 03_Analysis/
│   └── customer_churn_analysis.ipynb
├── 04_Python/
│   └── analysis notebooks and scripts
├── 05_PowerBI/
│   └── Customer_Churn_Retention_Analysis.pbix
├── 06_Exports/
│   └── dashboard exports
├── 07_Documentation/
│   └── project documentation
└── README.md
Metrics Glossary
Metric	Definition
Historical Churn Rate	Historical churned customers divided by total customers, using the Sep 30 observation cutoff and Oct 1–Dec 29 inactivity window.
Retention Rate	Retained customers divided by total customers under the historical churn definition.
Recency Days	Days between a customer's last transaction and 29 Dec 2023.
Customers Needing Attention	Customers in At Risk, High Risk, or 90+ Days Inactive recency bands.
Total Spend	Sum of transaction amounts for a customer.
Average Transaction Value	Total spend divided by transaction count.


Interview Summary
I analyzed 3.16 million transaction records across 48,723 customers using Python, Pandas, and Power BI. After cleaning and validating the transaction data, I created a customer-level dataset with recency, frequency, tenure, and customer-value measures. For historical churn, I identified customers with activity before 30 September 2023 but no transactions from 1 October through 29 December, resulting in 780 observed churned customers and a 1.60% churn rate. Separately, I used recency as of 29 December to classify current customer status and identified 9,345 customers needing attention. I combined recency, frequency, and value to prioritize retention and win-back opportunities, then built a two-page interactive Power BI dashboard to communicate the findings.

Limitations
- The analysis is based on transaction behavior and does not include customer demographics, acquisition channel, product attributes, service interactions, campaign exposure, or stated reasons for inactivity.
- The historical churn definition is an operational observation-window rule rather than permanent proof of customer loss.
- Recency bands are business rules; their thresholds should be validated against the organization’s transaction cycle and retention goals.
- Results identify associations and priority groups, not causal drivers of churn.
Future Enhancements
- Add customer demographics, channel, product, support, and campaign-response data.
- Compare churn and retention metrics across cohorts, acquisition periods, and transaction types.
- Measure campaign uplift with holdout groups or experiments.
- Add customer lifetime value and margin-based prioritization.
- Build a churn-propensity model after defining a validated outcome label and prediction horizon.
- Schedule automated data refreshes and monitoring alerts for changes in risk segments.

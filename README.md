# Credit Card Financial & Customer Analysis Dashboard 📊💳

An end-to-end Power BI business intelligence project designed to analyze credit card transaction data and customer demographics. This project provides actionable insights into revenue streams, transaction volumes, card usage behaviors, and customer segments, enabling financial institutions to make data-driven decisions.

---

## 📂 Project Structure & Files

The repository contains the following datasets and core Power BI files:

### 1. Power BI Reports
* `Credit_Card_Report.pbix` / `Credit_Card_Transaction_Report.pbix`: The master Power BI files containing the data model, DAX measures, and interactive dashboards.

### 2. Transaction Datasets
* **`credit_card.csv`**: The baseline transaction database containing records from early-to-mid 2023.
* **`cc_add.csv`**: Incremental transaction data used to simulate automated data updates or batch loads (e.g., Week-53 / Q4 data).

### 3. Customer Datasets
* **`customer.csv`**: Baseline customer demographic records matching the baseline transaction data.
* **`cust_add.csv`**: Incremental customer data updates corresponding to new account acquisitions.

---

## 📊 Data Dictionary

### Transaction Tables (`credit_card.csv` & `cc_add.csv`)
| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| **Client_Num** | Integer | Unique identifier for each customer/account. |
| **Card_Category** | String | Tier of credit card (**Blue**, **Silver**, **Gold**, **Platinum**). |
| **Annual_Fees** | Integer | Annual subscription fee charged for the card tier. |
| **Activation_30_Days** | Binary (0/1) | Indicates if the card was activated within 30 days of issuance. |
| **Customer_Acq_Cost** | Integer | The cost incurred to acquire the customer (CAC). |
| **Week_Start_Date** | Date | Starting date of the reporting week. |
| **Week_Num** | String | The specific week identifier (e.g., `Week-01` to `Week-53`). |
| **Qtr** | String | Fiscal Quarter (**Q1**, **Q2**, **Q3**, **Q4**). |
| **Credit_Limit** | Integer | Maximum spending limit allocated to the card. |
| **Total_Revolving_Bal** | Integer | Rollover unpaid balance subject to interest. |
| **Total_Trans_Amt** | Integer | Total expenditure/transaction monetary value. |
| **Total_Trans_Ct / Vol** | Integer | Count of transactions made by the user. |
| **Avg_Utilization_Ratio**| Decimal | Percentage of credit limit utilized by the user. |
| **Use_Chip / Use Chip**| String | Transaction channel method used (**Chip**, **Swipe**, **Online**). |
| **Exp_Type / Exp Type** | String | Spending category (**Bills**, **Entertainment**, **Fuel**, **Food**, **Grocery**, **Travel**). |
| **Interest_Earned** | Decimal | Interest revenue generated from revolving balances. |
| **Delinquent_Acc** | Binary (0/1) | Flag for accounts defaulting on payments. |

### Customer Tables (`customer.csv` & `cust_add.csv`)
| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| **Client_Num** | Integer | Unique identifier (Foreign key linked to transactions). |
| **Customer_Age** | Integer | Age of the cardholder. |
| **Gender** | String | Gender of the customer (**M** / **F**). |
| **Dependent_Count** | Integer | Number of dependents tied to the account holder. |
| **Education_Level** | String | High School, Graduate, Uneducated, Doctorate, etc. |
| **Marital_Status** | String | Single, Married, Divorced, or Unknown. |
| **state_cd** | String | US State Code location of the user (e.g., TX, NY, CA, FL, NJ). |
| **Zipcode** | Integer | Direct resident zip code. |
| **Car_Owner** | String | Vehicle ownership status (`yes` / `no`). |
| **House_Owner** | String | Property ownership status (`yes` / `no`). |
| **Personal_loan** | String | Active personal loan status (`yes` / `no`). |
| **contact** | String | Preferred communication method (**cellular**, **telephone**, **unknown**). |
| **Customer_Job** | String | Occupation group (Blue-collar, Govt, White-collar, Selfemployed, etc.). |
| **Income** | Integer | Annual gross income of the client. |
| **Cust_Satisfaction_Score**| Integer | Feedback rating scored between 1 and 5. |

---

## 📈 Key DAX Measures Calculated

To extract deep financial insights, custom **DAX (Data Analysis Expressions)** measures were built into the Power BI report:

* **Total Revenue Generation:** Calculates total earnings factoring in interest income and recurring annual fees.
    ```dax
    Revenue = SUM(credit_card[Total_Trans_Amt]) + SUM(credit_card[Interest_Earned]) + SUM(credit_card[Annual_Fees])
    ```
* **Total Transaction Volume:**
    ```dax
    Total_Transactions = SUM(credit_card[Total_Trans_Ct])
    ```
* **Delinquency Rate Tracking:** Monitors risk exposure by counting high-risk accounts.
    ```dax
    Delinquent_Accounts_Count = CALCULATE(COUNT(credit_card[Client_Num]), credit_card[Delinquent_Acc] = 1)
    ```

---

## 💡 Core Insights & Features

1. **Transaction Method Trends:** Deep-dive analysis comparing user safety/preference across **Swipe**, **Chip**, and **Online** payments.
2. **Expense Breakdown:** Identify what categories (such as *Grocery*, *Bills*, or *Travel*) drive the highest transactional value.
3. **Customer Segmentation Matrix:** Review KPIs filtered across demographic factors like **Age Groups**, **Income Levels**, **Education Tiers**, and **Job Roles**.
4. **Geographical Distribution:** Visual map distribution highlighting active transaction metrics across states like **Texas (TX)**, **California (CA)**, and **New York (NY)**.

---

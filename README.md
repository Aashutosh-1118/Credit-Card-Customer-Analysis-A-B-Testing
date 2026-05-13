# 🏦 AtliQo Bank — Credit Card Launch Analysis

> **End-to-end data analytics project** covering customer profiling, data cleaning, EDA, and a statistically validated A/B test to identify and target an untapped market segment for a new credit card product.

---

## 📌 Project Overview

AtliQo Bank wants to launch a new credit card and needs to identify the right customer segment to target. This project analyzes customer demographics, credit profiles, and transaction behavior to:

1. **Clean and explore** raw data from 3 MySQL tables
2. **Identify** the 18–25 age group as an untapped segment with low credit card usage
3. **Design and validate** an A/B test to measure the impact of a targeted credit card campaign

---

## 📁 Project Structure
AtliQo-Bank-Credit-Card-Analysis/
│
├── 01_EDA_Data_Cleaning.ipynb       # Phase 1: Data wrangling, EDA & visualization
├── 02_AB_Testing.ipynb              # Phase 2: Sample size calculation & hypothesis testing
│
├── data/
│   └── avg_transactions_after_campaign.csv   # Post-campaign A/B test data
│
├── .env.example                     # Environment variable template
├── .gitignore                       # Ignores .env and cache files
├── requirements.txt                 # Python dependencies
└── README.md                        # Project documentation
---

## 📊 Notebooks Summary

### Phase 1 — `01_EDA_Data_Cleaning.ipynb`
| Step | Details |
|------|---------|
| **Data Source** | MySQL database (`customers`, `transactions`, `credit_profiles`) |
| **Missing Values** | Group-based median imputation (by occupation) for `annual_income` and `age` |
| **Outlier Treatment** | IQR method for transaction amounts; business-logic-based caps for `outstanding_debt` |
| **Duplicate Handling** | Removed duplicate `cust_id` entries in credit profiles |
| **Feature Engineering** | Created `age_group` bins (18–25, 26–48, 49–65) |
| **Key Finding** | Age group 18–25 shows significantly lower credit card usage vs other groups |

### Phase 2 — `02_AB_Testing.ipynb`
| Step | Details |
|------|---------|
| **Sample Size Calculation** | Used statistical power analysis (power=0.8, α=0.05, effect size=0.4) → 100 customers |
| **Test Group** | 40 customers who adopted the new credit card |
| **Control Group** | 40 customers using existing card (mutually exclusive) |
| **Campaign Duration** | 2 months (09-Oct-23 to 11-Oct-23) |
| **Statistical Test** | Two-sample Z-test (right-tailed) |
| **Result** | Rejected null hypothesis — new card significantly increased avg transaction amounts |

---

## 🔍 Key Insights

- The **18–25 age group** represents ~25% of the customer base but has the **lowest credit card adoption**
- This segment earns **< ₹50K average annual income** and has limited credit history
- Top spending categories for 18–25: **Electronics, Fashion & Apparel, Beauty & Personal Care**
- Top platforms used: **Amazon, Flipkart, Alibaba**
- After the campaign, the test group showed **statistically higher average transaction amounts** (p < 0.05)

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| **Language** | Python, SQL |
| **Database** | MySQL |
| **Data Manipulation** | Pandas, NumPy |
| **Visualization** | Matplotlib, Seaborn |
| **Statistics** | SciPy, Statsmodels |
| **DB Connection** | mysql-connector-python |
| **Environment** | Jupyter Notebook, Anaconda |

---

## ⚙️ How to Run

### 1. Clone the repository
```bash
git clone https://github.com/Aashutosh-1118/Credit-Card-Customer-Analysis-A-B-Testing.git
cd Credit-Card-Customer-Analysis-A-B-Testing
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Set up environment variables
```bash
cp .env.example .env
# Open .env and add your MySQL password
```

### 4. Set up MySQL database
- Import the `e_master_card` database with tables: `customers`, `transactions`, `credit_profiles`
- Update `host` and `user` in the notebook if different from defaults

### 5. Run the notebooks in order

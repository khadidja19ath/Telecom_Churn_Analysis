# 📉 Telco Customer Churn — Exploratory Data Analysis

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Pandas](https://img.shields.io/badge/Pandas-EDA-green)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

> Identifying the key drivers of customer churn in a telecom company to support data-driven retention strategies.

---

## 📌 Overview

Customer churn is one of the most costly problems in the telecom industry. Acquiring a new customer costs 5–7× more than retaining an existing one. This project performs a full **Exploratory Data Analysis** on the IBM Telco Customer Churn dataset to uncover behavioral patterns and risk factors associated with customers who leave.

This is a **data analysis project** — the focus is on understanding the data deeply and extracting actionable business insights, not on modeling.

---

## 📂 Dataset

| Property | Value |
|---|---|
| Source | [IBM Sample Dataset — Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) |
| Size | 7,043 customers × 21 features |
| Target variable | `Churn` (1 = left, 0 = stayed) |
| Churn rate | 26.5% |

**Feature categories:**
- **Demographics:** gender, SeniorCitizen, Partner, Dependents
- **Services:** PhoneService, InternetService, OnlineSecurity, TechSupport, StreamingTV...
- **Account info:** Contract, PaymentMethod, PaperlessBilling, MonthlyCharges, TotalCharges, tenure

---

## 🔍 Analysis Pipeline

| Step | Description |
|---|---|
| 1. Load Data | Read CSV, configure display options |
| 2. Global Overview | Shape, dtypes, null values |
| 3. Format Correction | Fix `SeniorCitizen` (int→object), `TotalCharges` (object→float), `Churn` (Yes/No→1/0) |
| 4. Column Classification | Separate numerical and categorical features |
| 5. Categorical Analysis | Value counts + ratio + distribution plots for all 17 categorical columns |
| 6. Numerical Analysis | Descriptive stats + quantile distribution + histograms |
| 7. Missing Value Treatment | 11 null values in `TotalCharges` — filled using `MonthlyCharges` (new customers with tenure = 0 left before end of first month) |
| 8. Outlier Detection | IQR-based detection with boxplots — 0 outliers found in all numerical columns |
| 9. Correlation Analysis | Pearson heatmap for numerical features + Cramér's V matrix for the 7 most important categorical features |
| 10. Target Relationship | All features analyzed against `Churn` to identify key predictors |

---

## 📊 Key Findings

### 🔴 High-Risk Customer Profile

**Contract Type** — strongest predictor

| Contract | Churn Rate |
|---|---|
| Month-to-month | **42.7%** |
| One year | 11.3% |
| Two year | 2.8% |

**Internet Service**

| Service | Churn Rate |
|---|---|
| Fiber optic | **41.9%** |
| DSL | 19.0% |
| No internet | 7.4% |

**Payment Method**

| Method | Churn Rate |
|---|---|
| Electronic check | **45.3%** |
| Mailed check | 19.1% |
| Bank transfer | 16.7% |
| Credit card | 15.2% |

**Other risk factors:**
- Short tenure — churned customers stayed an average of **17.9 months** vs 37.6 for retained customers
- Higher monthly charges — churned customers paid **74.4$/month** vs 61.3$
- No OnlineSecurity → 41.8% churn vs 14.6% with OnlineSecurity
- No TechSupport → 41.6% churn vs 15.2% with TechSupport
- Senior citizens churn at **41.7%** vs 23.6% for non-seniors

### 🟢 Retention Factors
- Long-term contracts (1 or 2 years)
- Bundled services: OnlineSecurity, TechSupport, OnlineBackup, DeviceProtection
- Having a partner or dependents
- Automatic payment methods (bank transfer or credit card)

### 🔗 Feature Relationships (Cramér's V)
Strong associations between `InternetService` and its add-ons — customers without internet cannot subscribe to these services. This multicollinearity should be handled before modeling.

`TotalCharges` and `tenure` are highly correlated (r = 0.83) — one may be dropped before modeling.

---

## 💼 Business Recommendations

| Priority | Action | Expected Impact |
|---|---|---|
| 🔴 High | Target month-to-month customers with contract upgrade offers | Highest churn segment (42.7%) |
| 🔴 High | Focus retention on the first 3–6 months of tenure | Highest churn window |
| 🟡 Medium | Bundle security and support services with fiber optic plans | Fiber churn is 41.9% without add-ons |
| 🟡 Medium | Investigate why electronic check users churn more (45.3%) | Possible friction in payment experience |
| 🟢 Low | Design senior citizen loyalty programs | 41.7% churn rate in this segment |

---

## 🛠️ Tools & Libraries

```
Python 3 | Pandas | NumPy | Matplotlib | Seaborn | SciPy | Missingno | Plotly
```

---

## 📁 Repository Structure

```
telco-churn-analysis/
│
├── teleco-churn.ipynb      # Full EDA notebook
├── README.md               # Project documentation
└── data/
    └── WA_Fn-UseC_-Telco-Customer-Churn.csv
```

---

## ▶️ How to Run

```bash
git clone https://github.com/your-username/telco-churn-analysis.git
cd telco-churn-analysis
pip install pandas numpy matplotlib seaborn scipy missingno plotly
jupyter notebook teleco-churn.ipynb
```

---

## 🔮 Next Steps

Features identified as strong predictors — `Contract`, `tenure`, `MonthlyCharges`, `InternetService`, `OnlineSecurity`, `TechSupport`, `PaymentMethod` — are strong candidates for a prediction model.

- Feature engineering (encode categoricals, handle multicollinearity)
- Build classification models: Logistic Regression, Random Forest, XGBoost
- Evaluate with ROC-AUC and Precision-Recall (imbalanced target: 26.5% churn)

---

## 👩‍💻 Author

**Khadidja Aithoici**
AI Engineering Student — ENSTA Algiers (2024–2028)
[LinkedIn](#) · [GitHub](#)

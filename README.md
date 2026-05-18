# Customer_churn_prediction_engine
 End-to-end churn prediction engine | XGBoost · K-Means · Kaplan-Meier · Power BI
# Customer Churn Prediction & Revenue Recovery Engine

**End-to-end ML pipeline for telecom customer attrition analysis**

*Ashik Mu Asharaf · Data Science Professional  ·MSc AI & Data Science (Distinction)*  
[LinkedIn](https://linkedin.com/in/ashik-muhammad-asharaf-ai-data-scientist) · ashikmasharaf@outlook.com

---

## Business Problem

A telecom company is losing 400–500 customers every month.  
Each customer is worth ₹850/month on average.  
**That is ₹4.25 lakh walking out the door — every single month.**

This project builds a system that identifies which customers are about to leave, quantifies the revenue at risk, and models the ROI of retaining them before they go.

---

## Project Architecture

```
customer-churn-prediction-engine/
├── notebooks/
│   ├── 01_EDA_Business_Framing.ipynb         # Revenue at risk · churn drivers · loyalty curve
│   ├── 02_Customer_Segmentation.ipynb        # K-Means · 4 customer personas · priority matrix
│   ├── 03_Churn_Prediction_Models.ipynb      # Logistic Regression · Random Forest · Gradient Boosting
│   ├── 04_Revenue_Impact_Quantification.ipynb # ₹ ROI · 3 retention scenarios · CFO summary
│   ├── 05_Survival_Analysis.ipynb            # Kaplan-Meier · intervention calendar · log-rank test
│   └── 06_Executive_Summary.ipynb            # Full narrative · all outputs in one place
├── models/
│   ├── logistic_regression.pkl
│   ├── random_forest.pkl
│   ├── gradient_boosting.pkl
│   └── model_config.json
├── outputs/
│   ├── retention_scenarios.csv
│   ├── segment_revenue_impact.csv
│   ├── intervention_calendar.csv
│   └── km_*.csv                              # Kaplan-Meier curves by segment
├── data/
│   └── telco_churn.csv                       # IBM Telco dataset (place here before running)
├── requirements.txt
└── README.md
```

---

## Methodology

### Phase 01 — Exploratory Data Analysis & Business Framing
Baseline churn rate established at **26.5%**. Revenue at risk quantified at **₹4.25 lakh/month** (₹51 lakh/year). Identified the critical dropout window between **Month 12 and Month 18** of customer tenure.

### Phase 02 — Customer Segmentation (K-Means)
K-Means clustering (K=4, validated by Elbow + Silhouette) identified four business personas:

| Code | Persona | Churn Rate | Priority |
|---|---|---|---|
| ST_M2M | High-Risk New Customers | ~43% | CRITICAL |
| DIG_STRM | Price-Sensitive Churners | ~28% | HIGH |
| DISC_SAV | Engaged Mid-Tier | ~8% | MEDIUM |
| LT_BUND | Loyal High-Value | <5% | PROTECT |

### Phase 03 — Churn Prediction Models
Three classification models trained and evaluated with **recall on the churned class** as the primary metric — not accuracy.

| Model | Recall (Churn) | AUC-ROC |
|---|---|---|
| Logistic Regression | 78.4% | 0.832 |
| Random Forest | 81.1% | 0.854 |
| **Gradient Boosting** ✓ | **85.2%** | **0.881** |

Decision threshold optimised from 0.50 → 0.38 to maximise recall while maintaining precision.

### Phase 04 — Revenue Impact Quantification
Model predictions converted to rupees across three retention scenarios:

| Scenario | Retention Rate | Monthly Saving | Annual ROI |
|---|---|---|---|
| Conservative (outreach) | 20% | ₹36,200 | ~340% |
| **Moderate (₹150 discount)** ✓ | **40%** | **₹72,400** | **~520%** |
| Aggressive (upgrade offer) | 60% | ₹1.27 lakh | ~680% |

### Phase 05 — Survival Analysis (Kaplan-Meier)
Implemented from first principles (equivalent to `lifelines.KaplanMeierFitter`).  
Log-rank test confirms survival curves differ significantly by contract type (p < 0.001).

**Key finding:** Month-to-month contracts exhibit their steepest survival decline between **Month 12 and Month 18**.  
**Action:** Deploy retention campaigns at **Month 10** — before the decision to leave is made.

---

## Key Results

- **₹4.25 lakh** monthly revenue at risk identified
- **85.2% recall** on churned class (Gradient Boosting, threshold=0.38)
- **4 customer personas** with distinct churn trajectories and intervention strategies
- **Month 10** established as the universal pre-emptive intervention window
- **₹72,400/month** recoverable under moderate retention scenario (₹8.69 lakh/year)
- Top 3 churn drivers: tenure, contract type, internet service tier

---

## Technical Stack

| Tool | Purpose |
|---|---|
| Python · Pandas · NumPy | Data pipeline |
| Scikit-Learn | Logistic Regression, Random Forest, Gradient Boosting, K-Means |
| SciPy | Kaplan-Meier survival estimator (manual implementation) |
| Matplotlib · Seaborn | 19 production-grade visualisations |
| Power BI Desktop | 4-view executive dashboard (.pbix) |
| Jupyter Notebooks | 6 structured analysis notebooks |
| GitHub | Version control · public portfolio |

---

## Dataset

IBM Telco Customer Churn — [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)  
7,043 customer records · 21 features · No missing values after preprocessing

Place the downloaded CSV at `data/telco_churn.csv` before running notebooks.

---

## Running the Project

```bash
git clone https://github.com/Ashik-AI-DataScientist/customer-churn-prediction-engine.git
cd customer-churn-prediction-engine
pip install -r requirements.txt
# Place telco_churn.csv in data/
jupyter notebook notebooks/01_EDA_Business_Framing.ipynb
```

Run notebooks in order (01 → 05). Each saves outputs used by the next.

---


---

*Report: Available as pdf in report Customer_Churn_Project_IBM/Project Report/Telecom_Churn_Upgraded_Enterprise_Report.pdf

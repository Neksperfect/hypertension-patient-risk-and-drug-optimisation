# Predicting Blood Pressure Control Failure & Optimising Drug Selection in Hypertensive Patients

> **Zion Tech Hub Data Challenge — May 2026**
> **Author:** Muoneke Donmoen Nwamba | [LinkedIn](https://www.linkedin.com/in/muoneke-nwamba) | [GitHub](https://github.com/Neksperfect)

---

## Project Overview

Out of 350 patients treated at a hypertension cardiology centre, only **33 had their blood pressure under control after 3 months** — fewer than 1 in every 10. For the remaining 317, blood pressure remained dangerously high, putting them at ongoing risk of stroke, heart attack, and kidney damage.

This project addresses two clinical questions:

1. **Who is at risk of BP control failure?** — Can we identify high-risk patients early enough to intervene, using only information available at the point of prescription?
2. **Which medication works best for each patient type?** — Given different comorbidities (diabetes, kidney disease, obesity, dyslipidemia), which drug class produces the best outcomes?

---

## Repository Structure

```
├── report_final.pdf                                     # Analytical report with findings & recommendations
├── README.md                                            # You are here
└── Zion_Tech_Hub_Data_Challenge_Final.ipynb             # Full analysis notebook
```

---

## Dataset

| Property | Detail |
|---|---|
| Source | Hypertension Cardiology Center (Challenge Dataset) |
| Patients | 350 |
| Features | 16 (demographics, comorbidities, drug class, adherence, BP readings) |
| Target | BP controlled after 3 months (Yes / No) |
| Missing values | None |
| Class imbalance | 317 uncontrolled (90.6%) vs 33 controlled (9.4%) |

---

## Key Findings

### Exploratory Data Analysis

- **Combination therapy** outperformed every single-drug treatment — achieving a ~20% control rate vs 3–11% for monotherapy
- **Medication adherence** made a dramatic difference: patients with good adherence had a **15% control rate** vs less than **2%** for poor adherence
- **Chronic kidney disease** was the only comorbidity that meaningfully reduced BP control rates
- **Age** showed no consistent relationship with outcomes — it is not a reliable risk predictor
- **Baseline BP on day one** was the single strongest predictor of failure — patients who started higher had a much harder road to control

### Machine Learning — BP Control Failure Prediction

Two models were trained and compared:

| Model | Recall (at-risk patients caught) | Overall Accuracy |
|---|---|---|
| Logistic Regression | **86% → 100%*** | 98% |
| Random Forest | 43% | 99% |

*Recall improved to **100%** after threshold tuning from 0.5 → 0.3*

**Logistic Regression was selected** — not because it scored highest on every metric, but because it performed best on the metric that matters most clinically: **catching every at-risk patient before the 3-month review.**

#### Threshold Tuning Results

| Threshold | Patients Caught | Patients Missed | False Alarms | Recall |
|---|---|---|---|---|
| 0.5 (default) | 6 of 7 | 1 | 5 | 86% |
| **0.3 (recommended)** | **7 of 7** | **0** | **8** | **100%** |

> In a clinical setting, 8 unnecessary follow-up calls is a small and manageable price to pay for catching every high-risk patient.

#### Top Predictors of Failure
1. **Baseline systolic blood pressure** — the single most powerful signal
2. **Medication adherence** — poor adherence nearly guaranteed failure
3. **Drug class** — treatment choice was significantly associated with outcomes

---

### Drug Performance by Comorbidity Profile

| Patient Profile | Best Drug Class | Control Rate | Avg BP Drop | Second Best |
|---|---|---|---|---|
| Hypertension + Diabetes | Combination Therapy | 25.0% | 22.7 mmHg | Thiazide Diuretic |
| Hypertension + CKD | **Thiazide Diuretic** | 17.6% | 12.9 mmHg | Combination Therapy |
| Hypertension + Dyslipidemia | Combination Therapy | 25.9% | 22.5 mmHg | Thiazide Diuretic |
| Hypertension + Obesity | Combination Therapy | 18.4% | 21.6 mmHg | ARB |

### The ACE Inhibitor Finding

Across **every single patient group** — diabetes, CKD, dyslipidemia, and obesity — **not one patient on ACE inhibitors achieved blood pressure control.** This finding was consistent across 45 patients and warrants a serious clinical review of ACE inhibitors as standalone treatment for significantly hypertensive patients.

---

## Clinical Recommendations

1. **Start high-risk patients on combination therapy from day one** — single drugs rarely achieve control when baseline BP is significantly elevated
2. **Schedule every patient for an early follow-up within 2–4 weeks** — don't wait for the 3-month review to find out a treatment isn't working
3. **Prioritise adherence support early** — patients on poor adherence had a <2% control rate; early intervention can change this
4. **Review ACE inhibitors as standalone treatment** — consistent 0% control rate across all patient groups is a red flag
5. **Apply different treatment logic for CKD patients** — thiazide diuretics outperformed combination therapy in this group specifically
6. **Deploy the predictive model at first follow-up** — run it once adherence can be observed, use output to prioritise intensive support

---

## 🛠️ Tools & Technologies

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=flat)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)

- **Data Analysis:** Pandas, NumPy
- **Visualisation:** Matplotlib, Seaborn
- **Machine Learning:** Scikit-learn (Logistic Regression, Random Forest, SMOTE for class imbalance)
- **Reporting:** Full analytical report with EDA, modelling methodology, limitations, and recommendations

---

## ⚙️ How to Run

```bash
# 1. Clone the repository
git clone https://github.com/Neksperfect/<repo-name>.git
cd <repo-name>

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn jupyter

# 3. Launch the notebook
jupyter notebook Zion_Tech_Hub_Data_Challenge_Final.ipynb
```

---

## 📄 Full Report

The complete analytical report — including detailed EDA, model methodology, threshold tuning rationale, limitations, and clinical recommendations — is available in [`report_final.docx`](./report_final.docx)

---

## 👤 About the Author

**Muoneke Donmoen Nwamba** is a Healthcare & Clinical Data Analyst with a background in Molecular Genetics. He combines hands-on clinical diagnostics experience with data analytics, machine learning, and business intelligence — bringing domain knowledge that most data analysts don't have.

- 🔗 [LinkedIn](https://www.linkedin.com/in/muoneke-nwamba)
- 💻 [GitHub](https://github.com/Neksperfect)
- 📧 donmoen.devdas@yahoo.com

---

*This project was completed as part of the Zion Tech Hub Data Challenge, May 2026.*


# 🏥 Health Dataset Cleaning & Preprocessing

A complete data cleaning and preprocessing pipeline for a synthetic healthcare dataset.
This project focuses entirely on preparing raw, messy health data into a clean,
ML-ready format — the most critical step in any data science workflow.

---

> ⚠️ **Note:** The primary focus of this project is **data cleaning and preprocessing**.
> Simple baseline models are included only to confirm the dataset is properly prepared —
> not to achieve high accuracy.

---

## 📌 Project Overview

Real-world health datasets are messy. They contain missing values, invalid entries,
and logical inconsistencies that can completely break any analysis or model.
This project demonstrates a professional, step-by-step approach to handling all of
these issues on a synthetic healthcare dataset of 1,000 patients.

---

## 📊 Dataset

- **File:** raw_synthetic_health_dataset.xlsx
- **Rows:** 1,000 patients
- **Columns:** 15 features
- **Target Variable:** Illness (Yes / No)

### Feature Categories

| Category | Features |
|---|---|
| Demographics | Gender, Age |
| Lifestyle | Smoking, Alcohol Consumption, Exercise Frequency |
| Clinical Measurements | Blood Pressure, Cholesterol Level, BMI, Heart Rate, Blood Sugar Level, Sleep Hours |
| Health Outcomes | Illness, Family History, Medication Use |

---

## 🗂️ Project Structure
```
health-dataset-cleaning/
│
├── Data/
│   ├── raw_synthetic_health_dataset.xlsx    # Original raw dataset
│   ├── health_cleaned.csv                   # After cleaning
│   └── data_preprocessed.csv               # After preprocessing (ML-ready)
│
├── Notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_data_preprocessing.ipynb
│   └── 03_a_simple_model.ipynb
│
└── README.md
````
---

## ⚙️ What I Did — Step by Step

### Step 1 — Data Cleaning (`01_data_cleaning.ipynb`)

#### Missing Value Analysis

<!-- ADD IMAGE: missing value count bar chart here -->

| Column | Missing Values | Strategy Used |
|---|---|---|
| Alcohol_Consumption | 351 (35.1%) | Created missing flag → filled with 'Unknown' |
| Medication_Use | 345 (34.5%) | Created missing flag → filled with 'Unknown' |
| Gender, Smoking, Exercise_Frequency etc. | 5–12 | Mode imputation |
| Age, BMI, Heart_Rate, Sleep_Hours, Blood_Sugar_Level | 3–8 | Median imputation |
| Illness | 0 | No action needed |

#### Why These Strategies?
- **Mode imputation** for categorical columns — mean/median doesn't apply to text
- **Median imputation** for numerical columns — robust to outliers unlike mean
- **'Unknown' category** for high-missing columns — preserves original missing pattern for bias analysis
- **Missing flags** created for Alcohol and Medication — tracks where data was missing

#### Logical Inconsistency Fixes

Real-world data has impossible combinations. I identified and fixed:

- ❌ **Age = 0** → replaced with median age
- ❌ **Minors (age < 16) marked as Smokers** → changed to 'Unknown'
- ❌ **Minors (age < 16) marked as Heavy Drinkers** → changed to 'Unknown'
- Created `minor_smoking_flag` and `minor_alcohol_flag` columns to track these corrections

<!-- ADD IMAGE: boxplots of numerical features after cleaning here -->

#### Result After Cleaning
- ✅ 0 missing values remaining
- ✅ Logical inconsistencies corrected
- ✅ 4 new flag columns added for tracking
- ✅ Exported as `health_cleaned.csv`

---

### Step 2 — Feature Engineering & Preprocessing (`02_data_preprocessing.ipynb`)

Transformed the cleaned dataset from text format into fully numerical ML-ready format.

#### Encoding Strategy

| Encoding Type | Applied To | Reason |
|---|---|---|
| One-Hot Encoding | Gender, Smoking, Medication Use, Alcohol Consumption, Cholesterol Level | No natural order (nominal) |
| Ordinal Encoding | Exercise Frequency, Blood Pressure, Stress Level | Has natural order |
| Binary Encoding | Family History, Illness | Simple Yes/No variables |

#### Ordinal Mappings
- **Exercise Frequency:** Never=1, Rarely=2, Often=3, Daily=4
- **Blood Pressure:** Low=1, Normal=2, High=3
- **Stress Level:** Low=1, Medium=2, High=3

#### Before vs After

| | Before | After |
|---|---|---|
| Total Columns | 15 | 22 |
| Data Types | Mixed (object, float, int) | All numerical (int64, float64) |
| Missing Values | 784 total | 0 |
| ML Ready | ❌ No | ✅ Yes |

---

### Step 3 — Simple Baseline Models (`03_a_simple_model.ipynb`)

Two simple models were built to confirm the dataset is properly cleaned and formatted.

| Model | Train Score | Test Score |
|---|---|---|
| Random Forest | 79.75% | 45.5% |
| Logistic Regression | 57.25% | 46.5% |

#### Why Such Low Accuracy? (Expected)
- Dataset only has 1,000 samples — too small for complex health prediction
- Health/illness prediction requires much richer clinical data
- Simple features alone are not sufficient for this domain
- No single feature had strong correlation with Illness

> This is **completely normal and expected** for this type of dataset.
> The purpose was not accuracy — it was to prove the data is clean and ready.

<!-- ADD IMAGE: Random Forest confusion matrix here -->

<!-- ADD IMAGE: Logistic Regression confusion matrix here -->

<!-- ADD IMAGE: feature correlation with Illness bar chart here -->

---

## 🛠️ Tools & Libraries

| Category | Tools |
|---|---|
| Language | Python |
| Data Manipulation | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Machine Learning | Scikit-learn |
| Environment | Jupyter Notebook |

---

## 🚀 How to Run

```bash
# 1. Clone the repository
git clone https://github.com/Md-Maruf-1727/health-dataset-cleaning.git

# 2. Install required libraries
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl

# 3. Open Jupyter Notebook
jupyter notebook

# 4. Run notebooks in order:
# 01 → 02 → 03
```

---

## 📈 Key Takeaways

- Missing values are not always equal — high-missing columns need different strategies than low-missing ones
- Logical inconsistencies in data are just as dangerous as missing values
- Creating missing flags preserves information that would otherwise be lost
- Proper encoding of categorical variables is essential before any modeling
- A clean dataset with low accuracy is better than a dirty dataset with misleading accuracy

---

## 👤 Author

**Md. Maruf**
GitHub: [github.com/Md-Maruf-1727](https://github.com/Md-Maruf-1727)

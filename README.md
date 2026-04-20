# Student Addiction Risk Prediction

Exploratory data analysis and machine learning baseline for predicting 
cannabis addiction risk in university students. This repository contains 
all data processing, EDA, and modelling notebooks for the COMP3931 
Individual Project at the University of Leeds.

## Repository Structure

student-addiction-risk-prediction/
│
├── data/
│   ├── raw/
│   │   ├── drug_consumption.data           ← UCI raw dataset
│   │   ├── student_addiction_dataset_train.csv  ← Original Kaggle (deprecated)
│   │   └── student_addiction_dataset_test.csv   ← Original Kaggle (deprecated)
│   │
│   └── processed/
│       ├── uci_drug_clean.csv              ← Cleaned UCI dataset
│       ├── uci_cannabis_train.csv          ← UCI train split (80%)
│       ├── uci_cannabis_test.csv           ← UCI test split (20%)
│       ├── cleaned_student_addiction_dataset_train_cleaned.csv
│       ├── cleaned_student_addiction_dataset_test_cleaned.csv
│       ├── encoded_student_addiction_dataset_train.csv
│       └── encoded_student_addiction_dataset_test.csv
│
├── notebooks/
│   ├── cleaning.ipynb              ← UCI data cleaning + target binarisation
│   ├── encoding.ipynb              ← Feature encoding pipeline
│   ├── EDA.ipynb                   ← Exploratory analysis (raw data)
│   ├── EDA_encoded.ipynb           ← Exploratory analysis (encoded data)
│   ├── model_baseline.ipynb        ← LR baseline + RF comparison + threshold tuning
│   └── random_forest_model.ipynb   ← Final RF model + joblib export
│
├── ml_artifacts/
│   ├── rf_cannabis_model.joblib    ← Serialised Random Forest (gitignored)
│   └── model_metadata.json        ← Model version and feature metadata
│
├── confusion_matrices.png          ← LR vs RF confusion matrix comparison
├── rf_model_comparison.png         ← ROC curves + feature importance chart
├── .gitignore
├── requirements.txt
└── README.md

## Dataset

**Primary:** UCI Drug Consumption (Quantified) — Fehrman et al. (2015)  
1,885 real participants. 12 features: Big Five personality traits 
(NEO-PI-R), impulsivity (BIS-11), sensation-seeking (SSS-V), and 
5 demographic variables. Cannabis usage frequency binarised into 
Non-Risk (CL0–CL1) and At-Risk (CL2–CL6).

Available at: https://archive.ics.uci.edu/dataset/373/drug+consumption+quantified

**Note:** The `data/raw/` folder also contains the original Kaggle 
"Student Drugs Addiction Dataset 2024" used in early project stages. 
This dataset was abandoned after diagnostic analysis revealed zero 
mutual information between all features and the target variable, 
indicating the labels were synthetically assigned. See 
`model_baseline.ipynb` for the full diagnostic findings.

## Notebook Workflow

Run notebooks in this order:

| Step | Notebook | Description |
|---|---|---|
| 1 | `cleaning.ipynb` | Load UCI raw data, binarise cannabis target, train/test split |
| 2 | `encoding.ipynb` | Encode features, verify null counts, save processed CSVs |
| 3 | `EDA.ipynb` | Summary statistics, class balance, feature distributions |
| 4 | `EDA_encoded.ipynb` | Correlation matrix, feature means by class |
| 5 | `model_baseline.ipynb` | LR baseline, C sweep, RF comparison, threshold tuning |
| 6 | `random_forest_model.ipynb` | Final RF training, feature importance, joblib export |

## Model Results

| Model | Threshold | Accuracy | Recall (At-Risk) | F1 (At-Risk) | AUC-ROC |
|---|---|---|---|---|---|
| Logistic Regression | 0.495 | 0.78 | 0.77 | 0.83 | 0.862 |
| **Random Forest ★** | **0.45** | **0.79** | **0.88** | **0.85** | **0.855** |

Random Forest selected as primary model on the basis of superior 
recall for the At-Risk class. Serialised model is loaded by the 
Django web application in the companion repository.

## Companion Repository

The trained model is deployed via a Django web application:  
https://github.com/TerrenceGwati/addiction-risk-api

## Setup

```bash
git clone https://github.com/TerrenceGwati/student-addiction-risk-prediction.git
cd student-addiction-risk-prediction
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

## Academic Context

COMP3931 Individual Project — University of Leeds — 2025/26  
Dataset: Fehrman, E. et al. (2015). The Five Factor Model of 
personality and evaluation of drug consumption risk. arXiv:1506.06297.
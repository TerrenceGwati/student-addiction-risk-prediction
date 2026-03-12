# student-addiction-risk-prediction

This project explores the use of machine learning to predict student drug addiction risk using academic, behavioral, and social indicators.

## Project Structure


student-addiction-risk-prediction/
│
├── data/
│   ├── raw/
│   │   ├── student_addiction_dataset_train.csv
│   │   └── student_addiction_dataset_test.csv
│   └── processed/
│       ├── cleaned_student_addiction_dataset_train_cleaned.csv
│       ├── cleaned_student_addiction_dataset_test_cleaned.csv
│       ├── encoded_student_addiction_dataset_train.csv
│       └── encoded_student_addiction_dataset_test.csv
│
├── notebooks/
│   ├── cleaning.ipynb
│   ├── encoding.ipynb
│   ├── EDA.ipynb
│   ├── EDA_encoded.ipynb
│   └── model_baseline.ipynb
├── reports/
├── src/
├── .gitignore
├── requirements.txt
└── README.md


## Data

- **data/raw/**: Contains original train and test datasets.
- **data/processed/**: Contains cleaned and encoded datasets for modeling.

## Workflow Progress

- **Cleaning and Imputation**: Missing categorical features (≤5%) imputed using mode and saved as cleaned CSV files in `data/processed/`.
- **Encoding**: All categorical features encoded (Yes/No → 1/0) in `encoding.ipynb`, with outputs saved to `data/processed/`.
- **EDA**: Both the raw and encoded datasets analyzed in `EDA.ipynb` and `EDA_encoded.ipynb` — including summary statistics, group means, feature distributions, and correlation analysis.
- **Baseline Modeling**: Logistic regression implemented in `model_baseline.ipynb` with class weighting to handle imbalance, and performance evaluated using accuracy, precision, recall, and F1 score.
- **Model Results**: Achieved recall and F1-score that demonstrate discrimination of minority class, with plans for further tuning and feature/model experimentation.

## Usage

- Place any raw data in `data/raw/`.
- Execute cleaning, encoding, EDA, and modeling in notebooks under `notebooks/`.
- Review outputs and figures for analysis and evaluation in `reports/`.

## Current Status

- [x] Project and folder structure established.
- [x] Raw and processed data files created.
- [x] Cleaning and encoding completed.
- [x] Exploratory and statistical analysis performed on both raw and encoded data.
- [x] Baseline logistic regression trained and evaluated.
- [ ] Model tuning, feature selection, and alternative models planned for next session.

## Next Steps

- Hyperparameter tuning and additional model evaluation.
- Experiment with sampling methods and alternative classification algorithms.
- Documentation and visualization of further findings.

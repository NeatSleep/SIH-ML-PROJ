# SIH-ML-PROJ
EWS for GLOFs (Glacier  Lake Outburst Floods)
# GLOF Early Warning System (EWS) – Baseline ML Prototype

This repository contains a Jupyter Notebook implementing a **baseline Early Warning System (EWS)** for **Glacial Lake Outburst Floods (GLOFs)** using time-series meteorological data and classical machine learning.

This is a research prototype, not a production system. It demonstrates a verifiable pipeline:  
**data ingestion → preprocessing → exploratory analysis → time-aware model training → quantitative evaluation → risk categorization.**  
Every step is directly traceable in the notebook and can be cross-checked.

---

## What the Notebook Does

1. **Loads tabular climate data**
```python
file_path = "/content/new data 01.csv"
data = pd.read_csv(file_path)
The dataset is assumed to contain:

A datetime column (#NAME?)

Meteorological features:

Temperature(℃)

Rainfall (mm)

Relative Humidity(%)

hour, day, month, year

Target variable: Risk_Factor

Parses time and validates continuity

python
Copy code
data['#NAME?'] = pd.to_datetime(data['#NAME?'], format='mixed')
Time-series plots are generated to confirm temporal structure.

Explores data quality

Missing value counts and percentages

Distribution plots and box plots for numerical features

Defines the learning problem

Inputs:

python
Copy code
X = data[['hour', 'day', 'month', 'year',
          'Temperature(℃)', 'Rainfall (mm)',
          'Relative Humidity(%)']]
Target:

python
Copy code
y = data['Risk_Factor']
The model predicts a continuous risk score related to GLOF-prone conditions.

Uses time-aware cross-validation

python
Copy code
tscv = TimeSeriesSplit(n_splits=5)
This preserves temporal order and prevents future data leakage.

Trains a regression model

python
Copy code
model = LinearRegression()
model.fit(X_train, y_train)
Evaluates with standard metrics

For each fold:

RMSE (Root Mean Squared Error)

MAE (Mean Absolute Error)

R² Score

Averages across folds are computed.

Maps metrics to a risk label

python
Copy code
def categorize_risk_based_on_metrics(rmse, mae, r2):
    if rmse > rmse_threshold_high and mae > mae_threshold_high and r2 < r2_threshold_low:
        return "High"
    elif rmse < rmse_threshold_low and mae < mae_threshold_low and r2 > r2_threshold_high:
        return "Low"
    else:
        return "Medium"
Final output:

Average RMSE

Average MAE

Average R²

GLOF Risk Category (High, Medium, Low)

What This Is — and Is Not
This is:

A baseline ML pipeline for GLOF risk modeling

Time-series safe

Fully auditable

Suitable as a research foundation

This is not:

A physically validated hydrological model

A real-time deployment system

An operational disaster warning tool

It is a scaffold on which:

Stronger models (Random Forest, XGBoost, LSTM, Transformers)

Remote sensing features (lake area, DEM slope, snowmelt indices)

Real-time ingestion pipelines

can be built.

Requirements
Python 3.x

pandas

numpy

matplotlib

seaborn

scipy

statsmodels

scikit-learn

How to Use
Place your dataset in CSV format.

Update:

python
Copy code
file_path = "your_dataset.csv"
Run the notebook end-to-end.

Inspect:

Time plots

Missing value diagnostics

Cross-validated metrics

Final GLOF risk category

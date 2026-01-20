# SIH-ML-PROJ
EWS for GLOFs (Glacier  Lake Outburst Floods)
# GLOF Early Warning System (EWS) – Baseline ML Prototype

This repository contains a Jupyter Notebook implementing a **baseline Early Warning System (EWS)** for **Glacial Lake Outburst Floods (GLOFs)** using time-series meteorological data and classical machine learning.

This is a research prototype, not a production system. It demonstrates a verifiable pipeline:  
**data ingestion → preprocessing → exploratory analysis → time-aware model training → quantitative evaluation → risk categorization.**  

* **The dataset is assumed to contain:**
  * A datetime column (#NAME?)
  * Meteorological features:
  * Temperature(℃)
  * Rainfall (mm)
  * Relative Humidity(%)
  * hour, day, month, year
  * Target variable: Risk_Factor


* Parses time and validates continuity
  * Time-series plots are generated to confirm temporal structure.


* Explores data quality
  * Missing value counts and percentages
  * Distribution plots and box plots for numerical features


* Defines the learning problem
  * The model predicts a continuous risk score related to GLOF-prone conditions.


* Uses time-aware cross-validation
  * This preserves temporal order and prevents future data leakage.


* Trains a regression model

* Evaluates with standard metrics
  * For each fold:
    * RMSE (Root Mean Squared Error)
    * MAE (Mean Absolute Error)
    * R² Score
    * Averages across folds are computed.


* Maps metrics to a risk label
* **Final output:**

  * Average RMSE
  * Average MAE
  * Average R²
  * GLOF Risk Category (High, Medium, Low)

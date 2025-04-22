# Predictive Maintenance for IoT Sensor Devices

## Objective

The goal of this project is to develop a machine learning model that predicts failures in IoT sensor devices using structured time-series data. The pipeline addresses the challenges of imbalanced data and leverages feature engineering to extract meaningful patterns for predictive modeling.

---

## 1. Data Overview

The dataset contains the following:

- **Sensor Features**: Voltage_Fluctuation, Signal_Strength, Runtime_Hours, Temperature, Vibration, etc.
- **Timestamp**: Time of sensor reading
- **Target Variable**: `Error_Code`
  - `0` → Normal Operation
  - `1` → Failure

---

## 2. Exploratory Data Analysis (EDA)

- Checked data types and missing values
- Found high class imbalance (very few failure cases)
- Correlation analysis revealed:
  - Only `Voltage_Fluctuation`, `Signal_Strength`, and `Runtime_Hours` show weak correlation with the target
  - No features clearly separate classes
- Conclusion: Feature interactions may be non-linear; simple models may not perform well without engineering

---

## 3. Model 1 – Logistic Regression (Baseline)

- Applied Logistic Regression without feature engineering
- High accuracy due to class imbalance
- Poor performance for class `1` (minority):
  - Low recall and F1-score
  - Model biased toward predicting `0`

---

## 4. Handling Class Imbalance – SMOTE

- Applied **SMOTE** to oversample class `1` in the training set
- Results:
  - Class `1` recall and F1-score improved
  - Overall accuracy dropped slightly
  - Model now better recognizes failure cases

---

## 5. Feature Engineering

Created features to enhance model learning:

- **Time-based Features**:
  - `Hour`, `DayOfWeek`, `IsWeekend` derived from timestamp
- **Rolling Statistics**:
  - 3-point rolling mean for `Temperature`, `Vibration`, and `Signal_Strength`
- **Interaction Features**:
  - `Temp_x_Vibration` = Temperature × Vibration
  - `Signal_per_Runtime` = Signal_Strength ÷ Runtime_Hours

Feature engineering improved model interpretability and performance with SMOTE.

---

## 6. Model 2 – Random Forest (Non-Linear)

- Used to capture complex non-linear interactions missed by Logistic Regression
- Initial model gave average accuracy
- Poor metrics for class `1`

---

## 7. Hyperparameter Tuning

- Applied **GridSearchCV** to optimize Random Forest
- Some improvement in class `1` metrics, but still underwhelming
- Logistic Regression with feature engineering and SMOTE outperformed it

---

## 8. Final Model Comparison

| Model                           | Accuracy | Class 1 Recall | Class 1 F1-Score |
|--------------------------------|----------|----------------|------------------|
| Logistic Regression (Base)     | High     | Low            | Low              |
| Logistic + SMOTE               | Moderate | Slightly Better| Improved         |
| Logistic + FE + SMOTE          | Higher    | Improved       | Better           |
| Random Forest (Default)        | Average  | Poor           | Poor             |
| Random Forest + GridSearchCV   | Moderate | Improved       | Still Low        |

---

## Conclusion

- The best performing setup was **Logistic Regression** with **feature engineering and SMOTE**.
- Despite its simplicity, the linear model performed better than Random Forest for the given data.
- Feature engineering and proper class balancing had a greater impact than model complexity.
- Future work could explore more complex feature transformations or time-aware models.

---

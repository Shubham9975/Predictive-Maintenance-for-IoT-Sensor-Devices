Project Title: Predictive Maintenance for IoT Sensor Devices
Objective: To build a machine learning model that predicts failure in IoT sensor devices using tabular time-series data, with special focus on class imbalance and feature engineering.

1. Understanding the Data
The dataset consists of time-stamped IoT sensor readings capturing:

Sensor Metrics: Temperature, Vibration, Signal_Strength, Runtime, etc.

Time Feature: Timestamp

Target Variable: Error_Code, where 1 indicates failure and 0 indicates normal operation.

2. Exploratory Data Analysis (EDA)
A thorough EDA was performed to understand data characteristics:

Checked for missing values and data types.

Analyzed class distribution — observed high class imbalance (very few positive failure cases).

Visualized correlations and distributions:

No strong linear correlation found between numeric features.

Feature distributions were visualized to understand spread and identify skewness.

3. Handling Class Imbalance
Due to the rarity of failure events (Error_Code = 1), SMOTE (Synthetic Minority Oversampling Technique) was employed to oversample the minority class in the training data. This ensures the model doesn't become biased toward the majority class.

4. Feature Engineering
To enhance model learning, domain-relevant features were created:

Time-based Features:

Hour, DayOfWeek, IsWeekend derived from the timestamp.

Rolling Statistics:

3-point rolling means for Temperature, Vibration, and Signal_Strength.

Interaction Features:

Temp_x_Vibration: captures combined effect of two key metrics.

Signal_per_Runtime: signal normalized by operational time.

All features were selected to reflect real-world sensor behavior and potential early signs of failure.

5. Model Building
Two classification models were used and compared:

Logistic Regression:

Trained both with and without SMOTE + Feature Engineering.

Performance compared using accuracy, recall, and F1-score.

Random Forest Classifier:

Trained on original (imbalanced) data.

Hyperparameters tuned using GridSearchCV.

Best model evaluated on the test set using classification metrics.

6. Model Evaluation
The final evaluation was conducted using:

Confusion Matrix

Classification Report (Precision, Recall, F1-score for both classes)

Accuracy Score

This ensured that the model’s performance was validated from multiple perspectives, especially for the minority failure class.

Conclusion
The pipeline demonstrates a complete and systematic approach to predictive maintenance using machine learning on IoT data. The work includes:

Robust preprocessing and exploration

Handling of imbalanced classification using SMOTE

Domain-specific feature engineering

Comparison of linear and tree-based classifiers

Hyperparameter tuning for performance optimization

This approach ensures reliable early detection of device failure, supporting proactive maintenance strategies in IoT-enabled environments.

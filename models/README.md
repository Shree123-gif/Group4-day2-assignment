# Model Card — Residential Gas Consumption Prediction

## 1. Model Overview

This project predicts annual residential gas consumption using building characteristics and historical gas consumption data.

* **Model type:** Random Forest Regressor
* **Task:** Regression
* **Target variable:** `Gcons2024`
* **Saved model:** `model.joblib`
* **Framework:** Scikit-learn

## 2. Intended Use

The model is intended for educational and experimental use to explore machine learning methods for predicting residential gas consumption.

It should not be treated as a substitute for measured consumption or used as the sole basis for important decisions.

## 3. Input Features

The model uses the following features:

* `PROP_TYPE`
* `PROP_AGE_BAND`
* `FLOOR_AREA_BAND`
* `COUNCIL_TAX_BAND`
* `REGION`
* `MAIN_HEAT_FUEL`
* `Gcons2023`
* `Gcons2022`
* `Gcons2021`

The target-year flag `GasValFlag2024` is excluded from the inputs.

## 4. Preprocessing

The saved pipeline includes preprocessing for numerical and categorical features.

* Numerical features: median imputation and standardisation.
* Categorical features: most-frequent imputation and one-hot encoding.

## 5. Model Configuration

The selected Random Forest configuration uses:

* `max_depth=10`
* `n_estimators=100`

Hyperparameter tuning was performed using GridSearchCV with three-fold cross-validation.

## 6. Evaluation Results

The reported held-out test results are:

| Metric |       Result |
| ------ | -----------: |
| MAE    | 1,777.18 kWh |
| RMSE   | 3,129.35 kWh |
| R²     |       0.7811 |

Lower MAE and RMSE indicate smaller prediction errors. Higher R² indicates a better fit relative to a mean-prediction baseline.

## 7. Limitations

* Historical gas consumption is the dominant predictor.
* Prediction errors vary between properties.
* A previous-year baseline achieved a lower MAE than the Random Forest on the evaluated subset.
* Feature importance does not establish causation.
* The model's performance may change on different datasets or future years.
* The test set has already been used for evaluation and baseline comparisons.

## 8. Data and Reproducibility

The raw dataset is not included in the repository. Reproducing the experiments requires access to the dataset and the dependencies listed in the project's `requirements.txt`.

The model was trained on an anonymised residential gas consumption dataset.

## 9. Ethical Considerations

Predictions may be inaccurate for individual properties. Results should be interpreted cautiously and should not be used to make consequential decisions about individual households without further validation.

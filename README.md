# Residential Gas Consumption Prediction

## Project Overview

This project develops and evaluates machine learning models to predict annual residential gas consumption using building characteristics and historical gas consumption data.

The project compares multiple regression models, applies cross-validation and hyperparameter tuning, and evaluates the selected model using a held-out test set.

## Objectives

* Explore the relationship between building characteristics and annual gas consumption.
* Establish a baseline for regression performance.
* Train and compare multiple machine learning models.
* Tune model hyperparameters using cross-validation.
* Evaluate predictions using MAE, RMSE, and R².
* Analyse prediction errors and feature importance.
* Save the trained model pipeline for reuse.

## Dataset

The project uses an anonymised dataset containing building characteristics and annual gas consumption measurements.

The input features include:

* Property type
* Property age band
* Floor area band
* Council tax band
* Region
* Main heating fuel
* Historical gas consumption for 2021, 2022, and 2023

**Target:** `Gcons2024`

The target-year flag `GasValFlag2024` is excluded from the input features to avoid potential target leakage.

The raw dataset is not included in the repository.

## Methodology

### 1. Data preparation

The dataset is separated into training and test sets using an 80/20 split with `random_state=42`.

### 2. Preprocessing

A preprocessing pipeline handles missing values and prepares the input features:

* Numerical features: median imputation and standardisation.
* Categorical features: most-frequent imputation and one-hot encoding.

### 3. Model comparison

The models explored include:

* Dummy Regressor baseline
* Linear Regression
* Ridge Regression
* Decision Tree Regressor
* Random Forest Regressor
* Gradient Boosting Regressor

Five-fold cross-validation is used for model comparison, with Mean Absolute Error (MAE) as the main metric. Lower MAE indicates better predictive performance.

### 4. Hyperparameter tuning

GridSearchCV is used to tune the Random Forest model.

The selected Random Forest configuration uses:

* `max_depth=10`
* `n_estimators=100`

The tuning process uses three-fold cross-validation. The selected model is also evaluated using five-fold cross-validation.

### 5. Evaluation

The selected Random Forest's held-out test results are:

| Metric |       Result |
| ------ | -----------: |
| MAE    | 1,777.18 kWh |
| RMSE   | 3,129.35 kWh |
| R²     |       0.7811 |

The MAE represents the average absolute prediction error. RMSE gives greater weight to larger errors, while R² measures the proportion of target variation explained relative to a mean-prediction baseline.

## Results and Interpretation

The tuned Random Forest achieved a test MAE of 1,777.18 kWh and an R² of 0.7811.

Feature importance analysis identified `Gcons2023` as the dominant predictor, followed by `Gcons2022` and `Gcons2021`.

This indicates that historical gas consumption provides the strongest predictive signal in the selected model.

A previous-year baseline comparison was also explored. On the evaluated subset, the simple baseline achieved a lower MAE than the Random Forest, while the Random Forest achieved a lower RMSE. Therefore, the more complex model did not outperform the simple baseline on every metric.

## Visualisations

The project includes visualisations for:

* Actual versus predicted gas consumption
* Residuals versus predicted gas consumption
* Correlations between historical consumption and the target
* Random Forest feature importance

See the `figures/` directory for the generated plots.

## Project Structure

```text
.
├── data/                       
├── figures/                    
├── models/                     
├── notebooks/
│   └── 02_model_training.ipynb
├── .gitignore
├── README.md
└── requirements.txt
```

## How to Run

1. Clone the repository.
2. Create and activate a Python virtual environment.
3. Install the dependencies listed in `requirements.txt`.
4. Obtain the dataset separately and place it in the expected `data/` location.
5. Open `notebooks/02_model_training.ipynb`.
6. Run the notebook cells in order.

The dataset is not distributed with this repository, so the notebook cannot run from beginning to end without access to the required data.

## Limitations

* Historical gas consumption dominates the model's feature importance.
* Some properties have substantially larger prediction errors than others.
* The test set has already been used for model evaluation and baseline comparisons; it is not a completely untouched final benchmark.
* The previous-year baseline performs better on MAE for the evaluated subset.
* Feature importance describes the model's reliance on input features and does not establish causation.
* Results may differ on other datasets, regions, or future years.

## AI Use Disclosure

AI tools were used to support aspects of coding, debugging, explanation, and documentation. 

## Authors

IAAC AI Methods — Group 4

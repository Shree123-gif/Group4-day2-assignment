# Group4-day2-assignment
# Building Energy Consumption Prediction — Model Training

## 1. Objective

The objective is to train a machine-learning model that predicts annual gas consumption for residential properties using building characteristics and historical gas consumption.

**Target variable:** `Gcons2024`

**Input features:**

* Building characteristics, including property type, age band, floor-area band, council tax band, region and main heating fuel.
* Historical gas consumption from 2021, 2022 and 2023.

## 2. Modelling Workflow

1. Load the prepared dataset and define the input features and target.
2. Split the data into training and test sets.
3. Build a preprocessing pipeline for numerical and categorical features.
4. Establish a baseline model.
5. Train and compare multiple regression models.
6. Evaluate model performance using cross-validation and Mean Absolute Error (MAE).
7. Evaluate the selected model on the test set.
8. Save the final model for deployment.

## 3. Evaluation Metric

We will use **Mean Absolute Error (MAE)** as the primary metric. It measures the average absolute difference between predicted and actual annual gas consumption in kWh. Lower MAE indicates better predictive accuracy.

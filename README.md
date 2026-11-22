# Flight Fare Prediction️

This project demonstrates data auditing, exploratory analysis, feature engineering, leakage-aware validation, model selection, error analysis, and inference. All executable project code and its explanations are contained in Jupyter notebook

## Results

- The best model is selected based on the lowest average MAE from **5 group-aware cross-validation splits** using only the training data.
- **Random Forest** achieved the lowest average MAE and was selected as the best model.  It is then trained again using the full training set and evaluated once on the unseen holdout test set.
  

| Final holdout metric | Result |
| --- | ---: |
| **MAE** | **601.0060 INR** |
| **RMSE** | **1,630.2024 INR** |
| **R²** | **0.8787** |
| Holdout rows | 2,123 |
| Training rows | 8,560 |

## Model Comparison Results

The following models were evaluated using **5 group-aware cross-validation splits**.

| Model | CV MAE (INR) ↓ | MAE SD | CV R² ↑ |
|---|---:|---:|---:|
| **Random Forest** | **647.614** | **9.833** | 0.891 |
| XGBoost | 656.159 | 14.264 | **0.916** |
| Decision Tree | 817.343 | 40.583 | 0.836 |
| Ridge Regression | 1,593.261 | 35.518 | 0.718 |
| Median Baseline | 3,620.397 | 41.558 | -0.027 |

- **Random Forest** achieved the lowest average MAE (647.614 INR) and was selected as the best model.
- **XGBoost** achieved the highest R² (0.916), but its MAE was slightly higher than Random Forest.
- **Random Forest** also had the lowest MAE standard deviation, showing more consistent results across the validation splits.


## Repository structure

```text
flight_price_portfolio/
├── flight_price_prediction.ipynb   # All code, analysis, charts, results, and explanations
├── README.md                       # Project overview 
├── requirements.txt                # Python dependencies
└── data/
    ├── Data_Train.xlsx             # 10,683 rows with the Price label
    └── Test_set.xlsx               # 2,671 rows without the Price label
```


## Data and task

- **Objective:** predict a fare in **Indian rupees (INR)** from airline, route, journey date, scheduled departure/arrival times, journey duration, number of stops, and additional flight information.
- **Labeled data:** `data/Data_Train.xlsx`, 10,683 observations and 10 input features plus `Price`.
- **Unlabeled data:** `data/Test_set.xlsx`, 2,671 observations and 10 input features. **It has no `Price` column**, so test scores cannot be computed from it.
- **Time period:** journey dates in **March–June 2019**. Ticket purchase or booking dates are not supplied.
- **Data anomalies:** one missing `Route`, one missing `Total_Stops`, 220 exact duplicate labeled rows, and 419 duplicated sets of input features (ignoring target). Some arrival date strings are inconsistent; the notebook uses the arrival *clock time* but does not interpret embedded arrival dates.

A commonly cited public listing for this dataset is [Kaggle: Flight Fare Prediction MH](https://www.kaggle.com/datasets/nikhilmittal/flight-fare-prediction-mh). 

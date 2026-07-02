# Bike Sharing Demand Prediction with AutoGluon

Predicting hourly bike rental demand using AutoGluon's automated machine learning framework, completed as part of the **AWS Machine Learning Fundamentals Nanodegree (Udacity)**. The project follows an iterative improvement approach: baseline model → feature engineering → hyperparameter tuning, with real Kaggle competition submissions at each stage.

## Results

| Stage | Kaggle RMSE Score | Improvement |
|---|---|---|
| Initial (raw features) | 1.80342 | Baseline |
| + Feature Engineering | 0.56030 | 69% reduction |
| + Hyperparameter Tuning | **0.50686** | **72% total reduction** |

The single biggest improvement came from **feature engineering** — extracting `hour`, `day`, and `month` from the raw datetime column reduced RMSE from 1.80 to 0.56. This makes intuitive sense: bike demand is strongly time-of-day dependent, and AutoGluon could not extract this signal from a raw datetime object.

## Dataset

- **Source:** Kaggle Bike Sharing Demand Competition
- **Size:** 10,886 training rows, 6,493 test rows
- **Features:** datetime, season, holiday, workingday, weather, temp, atemp, humidity, windspeed
- **Target:** `count` (total hourly bike rentals)

## Approach

### Stage 1: Baseline Model
- Loaded raw data and dropped `casual` and `registered` columns (not present in test set)
- Trained AutoGluon `TabularPredictor` with `best_quality` preset, 10-minute time limit, RMSE metric
- Best model: WeightedEnsemble_L3 (val RMSE: 53.13)
- **Kaggle Score: 1.80342**

### Stage 2: Feature Engineering
- Extracted `hour`, `day`, and `month` from the `datetime` column
- Converted categorical columns (`season`, `weather`, `holiday`, `workingday`) from int to `category` dtype so AutoGluon treats them correctly
- Retrained with same AutoGluon settings on the enriched feature set
- **Kaggle Score: 0.56030** — largest single improvement of the project

### Stage 3: Hyperparameter Tuning
- Configured custom hyperparameters for Random Forest, Extra Trees, LightGBM, CatBoost, and XGBoost
- Added `hyperparameter_tune_kwargs` with `num_trials` and `scheduler` settings
- Tuned `num_bag_folds` and `num_stack_levels` for better ensemble stacking
- **Kaggle Score: 0.50686**

## Individual Model Comparison (standalone, non-AutoGluon)

| Model | RMSE |
|---|---|
| XGBoost | 149.60 |
| Random Forest | 154.40 |
| Linear Regression | 156.51 |
| KNN | 160.95 |

## Key Insights

- **Hour of day is the most important feature** — datetime decomposition drove the largest improvement by far, confirming that bike demand follows strong time-of-day patterns (commute hours, weekends)
- **AutoML (AutoGluon) outperforms individual models significantly** — best standalone model (XGBoost RMSE: 149.60) was far outperformed by AutoGluon's ensemble (val RMSE: ~50)
- **Feature engineering > hyperparameter tuning** for this dataset — the 69% improvement from feature engineering dwarfed the additional 3% from HPO

## Tools & Libraries

Python, AutoGluon, Pandas, Matplotlib, Seaborn, Scikit-learn, XGBoost, Kaggle API

## Notes

This was a guided project completed as part of the AWS Machine Learning Fundamentals Nanodegree. The iterative submission structure (baseline → features → HPO) and final report are required deliverables of the nanodegree curriculum.

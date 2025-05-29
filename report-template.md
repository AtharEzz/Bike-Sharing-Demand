# Report: Predict Bike Sharing Demand with AutoGluon Solution
Athar Ezzeldin

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
Initially, I focused on reading and preprocessing the training and test datasets correctly, ensuring proper parsing of the datetime column and handling any missing values.
I dropped two columns from the training dataset to ensure that the number of features matched between the training and test sets for prediction.
### What was the top ranked model that performed?
WeightedEnsemble

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
I extracted the year, month, day, hour, minute, and second from the datetime column. After exploration, I realized that:

The year column only had two unique values.

Minute and second did not provide useful information.

Therefore, I decided to include only the month, day, and hour features. The hour feature, in particular, turned out to be one of the most important and required further analysis and preprocessing.

I also noticed that some columns like season, workingday, and holiday were represented as numerical values. I converted them into categorical data types.

### How much better did your model preform after adding additional features and why do you think that is?
The model's performance improved significantly. The testing score changed from approximately 1.8 to 0.54.
I believe this improvement is due to:

The removal of noise from irrelevant or redundant features.

The simplification and transformation of features into more meaningful formats.

Converting numerical columns into categorical types helped the model interpret those features better.

Extracting and including hour, day, and month enabled the model to recognize clearer temporal patterns in the data.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
The model's performance improved further after tuning the hyperparameters. The testing score decreased from 0.54 to 0.50, indicating better predictive accuracy.
To enhance performance, I introduced custom hyperparameters for the RandomForest (RF) and ExtraTrees (XT) models, and used Bayesian optimization for more effective tuning.
I then used this setup in the final training step
These enhancements allowed for more robust model validation (via increased bagging and stacking depth) and improved predictive performance through more diverse model ensembles and smarter hyperparameter exploration.

### If you were given more time with this dataset, where do you think you would spend more time?

If given more time, I would focus on advanced feature creation, tuning ensemble weights, and experimenting with alternative model architectures for better improvements.
### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|?|?|?|?|
|add_features|?|?|?|?|
|hpo|?|?|?|?|


### Create a line plot showing the top model score for the three (or more) training runs during the project.

TODO: Replace the image below with your own.

![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

TODO: Replace the image below with your own.

![model_test_score.png](img/model_test_score.png)

## Summary
This project demonstrated how AutoGluon can be used to rapidly develop and improve a regression model for predicting bike-sharing demand. Through a series of iterative enhancements—starting with baseline model training, then applying feature engineering, and finally hyperparameter tuning—I significantly reduced the test RMSE from 1.80 to 0.50.
With feature engineering made the biggest impact on performance,and converting numeric variables to categorical helped the model learn more meaningful splits.
Hyperparameter tuning using Bayesian optimization and custom model definitions provided further but smaller improvements.While Stacked ensembling and bagging improved generalization and robustness.
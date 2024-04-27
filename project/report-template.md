# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### DIYA KHAJURIA

NOTE: Initially tried to train locally, many dependency conflicts occured in the conda environment that was created. Wasn't completing running the training code cells. Switched to AWS Sagemaker, worked perfectly from there on out. Ran notebook twice due to different completion status on 2 days, thus double score submitted on kaggle.
Bill: 0.09 dollars

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
I realized that the predicions on the test data had to be > 0. Thus, changing the negative outputs of the predictor to a positive value was essential.  

### What was the top ranked model that performed?
As visulaized by the score_val VS model bar plots, it's apparent that the WeightedEnsemble_L3 is the top performing model.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
Upon visualizing the histogram for all features, I observed that the datetime histogram was too crowded to offer any discernible trend or conclusions.So, splittiong up the datetime into 4 additional features of year, month, day, hour.
Converting features such as season, weather into categorical types was done next. Visualizing of correlation between features was done using heatmap along with 3 line graph subplots of bike share demand by hour VS season,day, and user_type. 

### How much better did your model preform after adding additional features and why do you think that is?
The Kaggle score improved from 1.80055 to 0.63016. Autogluon was able to gather more information and discover patterns and trends in-depth, when we divided datetime into 4 additional features. Also, season and weather features were now known to it as being of categorical type.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
The kaggle score improved from 0.63016 to 0.48668. On the other hand though, the score_eval VS model barplot showed a decline in model performance from it's previous computations (same params as original, additional features).

### If you were given more time with this dataset, where do you think you would spend more time?
I would have spent my time on optimizing hyperparameters, trying for different architectures, and experimenting with different hyperparameter values and time_limits. Also, I would have liked to do a more thorough EDA along with trying out the rest of the additional suggestions that Udacity provided.  

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|time limit|num trials|hyperparams|score|
|--|--|--|--|--|
|initial|700|1|default|1.80055|
|add_features|700|1|default|0.63016|
|hpo|1200|6|XGB and GBM tuned|0.48668|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png]("C:\Users\Diya\OneDrive\Desktop\model_train_score.png")

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.


![model_test_score.png]("C:\Users\Diya\OneDrive\Desktop\model_test_score.png")

## Summary
Three models were built, yielding different training scores and kaggle scores.

Model 1:

* The baseline model
* Trained for 700 seconds, for a presets of best_quality
* Kaggle score is 1.80055

Model 2: we devised data and fed it to Model 1

* Feature engineered year, month, day, hour columns from datetime
* Trained for 700 seconds, for a presets of best_quality
* Set season, weather features to categorical type
* Kaggle score is 0.63016

Model 3: defined Hyperparameters, increased time
* Trained for 1200 seconds, for a presets of best_quality
* XGB and GBM Hyperparameters fed 
* Kaggle score is 0.48668

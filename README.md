The project was broken down into various stages, beginning with data pre-processing, where missing values were addressed, and multicollinearity was carefully examined to ensure the dataset's integrity. 

Data exploratory analysis was conducted to find the relevant predictors and to identify the correlation. Feature selection played a pivotal role, and the Best Subset Method was utilized to identify key variables, leading to the conclusion that time, creatinine, ejection fraction, and age were optimal features for predictive modeling. 
In model selection, we have taken logistic regression, decision tree, and random forest. For logistic regression, the model's accuracy was checked with and without outliers, and was found that the outliers were relevant in our case.

The models were trained and cross-validated using 5-fold cross-validation. Grid search was employed to find the hyperparameter for the decision tree and random forest and the stability of the models was checked using bootstrap methods with up to 5000 iterations. The final model was found to Random Forest with 81.33% accuracy.

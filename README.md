1. Objective: Determine sensitivity of CatBoost models to changing distribution of input features 

2. Industry Relevance: In real world classifications tasks like AD CTR, distributions of user variables will change drastically with time, so knowledge of robustness (or lack thereof) of a model to these shifts is essential

3. Application/Use: If we are able to identify the cases in which CatBoost is sensitive to distributional shifts, we can derive rules on when CatBoost models need to be retrained for optimal commercial use

What is CatBoost?
CatBoost is tree based model specifically designed to handle categorical features with high cardinality
Uses Sequential Target Encoding and then sequential boosting to train a forest
Model Advantages:
 - Ease of Use: CatBoost can handle high-cardinality categorical variables directly.
 - Efficiency: Faster training times compared to other gradient-boosting algorithms (symmetric decision trees).
 - Regularization: Built-in mechanisms to reduce overfitting, ideal for high-dimensional datasets.

Methodology: 
 - Train CatBoost model to predict AD CTR on train_data_ads.csv data set (split into training and testing) to get baseline measurement of Testing AUC
 - Average CatBoost Testing AUCs over models trained on random subsets of training data (comprising 70%) to get new baseline AUC
 - Iterate through each feature and drop 30% of the rows in a way that simulates shifting the distribution of the feature and record the AUC
 - Analyze relationship between feature importance metric for each feature and change in Testing AUC to see under which distribution shifts CatBoost models might need to be retrained

Evaluation Metric: Area Under the Curve (AUC)
Selected as a robust metric for distinguishing between clicks and non-clicks.
Cross-Validation Results:
5-Fold Cross-Validation AUC Scores:
Scores: [0.8115, 0.8123, 0.8132, 0.8113, 0.8118], Mean = 0.8120, SD = 0.00066
AUC Score on test set: 0.8103

Results: 
Analysis
The radical shifts in feature distributions did not seem to have a substantial impact on the testing AUC
Shifting the most important feature did not have the most radical impact on AUC
Thus, for this data set, CatBoost proved to be a resilient and reliant model that is not sensitive to shifting distributions

Implications
This data set is not a representative sample of all AD CTR data sets, so we cannot conclusively make the assertion that CatBoost models will not need retraining in commercial applications; however the results seem promising
Repetition on other similar and dissimilar AD CTR data sets is needed and a logical next step to further test the sensitivity of the CatBoost Algorithm in AD CTR prediction. 

Conclusion
For AD CTR Prediction on the Huawei Data set, the CatBoost model proved to be resilient to simulations of distributional shifts of features, managing to maintain a commercially acceptable AUC of 0.8
Further study can be conducted by synthesizing AD CTR data sets and running the same procedures

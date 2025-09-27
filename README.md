## Recipe Site Traffic Prediction

### Problem Description
This project aims to predict whether a recipe will have "High" or "Low" traffic on a recipe website based on its nutritional information and category. The dataset contains missing values and an imbalanced target variable, which needs to be addressed for effective model training.

### Methodology
The approach involves:
Data loading and initial exploration.
Handling missing values using KNN imputation for numerical features.
Feature engineering by one-hot encoding categorical features.
Addressing the imbalanced target variable using a Self-Training Classifier.
Training a model (RandomForestClassifier) on the combined labeled and pseudo-labeled data.
Evaluating the model's performance.
Predicting traffic for unlabeled data.

### Data Cleaning
Missing values in 'calories', 'carbohydrate', 'sugar', and 'protein' were imputed using KNNImputer.
Missing values in the target variable 'high_traffic' were identified for semi-supervised learning.
Semantically similar values in the 'servings' column were reconciled.
Outliers in numerical columns were removed from the unlabeled data to improve model robustness.

### Feature Engineering
Categorical features ('category' and 'servings') were one-hot encoded to convert them into a numerical format suitable for machine learning models.
The original 'category' and 'servings' columns were dropped after one-hot encoding.

### Visualization
A histogram of the 'calories' feature was plotted to visualize its distribution.

### Addressing Imbalance
A Self-Training Classifier was used to leverage the unlabeled data. The model trained on the labeled data predicted pseudo-labels for the unlabeled data with high confidence. This pseudo-labeled data was then combined with the original labeled data to retrain the model, helping to address the class imbalance.

### Modeling
A RandomForestClassifier was initially trained on the labeled data.
A SelfTrainingClassifier with a RandomForestClassifier as the base estimator was used to train on the combined labeled and pseudo-labeled data.
A Logistic Regression model was also trained and evaluated for comparison.

### Evaluation
The models were evaluated using accuracy and classification reports on the labeled test set.
The SelfTrainingClassifier achieved perfect accuracy on the labeled test set.
The Logistic Regression model also showed good accuracy, but with warnings related to convergence and ill-defined metrics due to the imbalance in the test set.

### Prediction
The trained SelfTrainingClassifier was used to predict the 'high_traffic' for the remaining unlabeled data.
Recipes predicted to have high traffic were identified and displayed.

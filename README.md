# Finding-Donors-for-CharityML

## Introduction

This project shows how we can use supervised learning to solve a business problem. Charity ML is an imaginary non-profit which survives from donations. In particular, past experience has shown that people making more than $50,000 a year were much more likely to donate. As a result, our goal is to use publicly available data (from Census information) to build a model to predict someone's income, thus allowing CharityML to focus its outreach efforts on people most likely to donate.

The dataset for this project originates from the UCI Machine Learning Repository. It was donated by Ron Kohavi and Barry Becker, after being published in the article "Scaling Up the Accuracy of Naive-Bayes Classifiers: A Decision-Tree Hybrid". We can find the article by Ron Kohavi online. The data we investigate here consists of small changes to the original dataset, such as removing the 'fnlwgt' feature and records with missing or ill-formatted entries.

Our approach will consist in building several models on this data. We will then select the best candidate algorithm and tune it further. We use a supervised learning approach since we have a target variable (binary, whether an individual makes more than $50,000) which we want to model.

## Repository

In order to run this project, you can simply clone this repository. In particular, visuals.py contains helper functions to help us visualize our data and the model outputs. The census data is included in census.csv.

The analysis is contained in finding_donors.ipynb, which an HTML version in finding donors.html. In order to run the notebook, you will need the following libraries:

numpy
pandas
Ipython.display
time
sklearn

## Analysis
We built a robust model CharityML can use to identify potential donors.

### Preprocessing
Given its source, our dataset is already clean, but we do need to perform some preprocessing:

- transform skewed features by applying a logarithmic transformation
- normalize features through a MinMaxScaler
- encode categorical features through one-hot encoding
- encode the categorical target variable by a numeric binary variable

### Modeling
We build four models:

- a naive predictor, that always predicts an individual makes more than $50,000. This serves as a benchmark the other model have to improve upon
- Gaussian NB
- Support Vector Machines
- Adaboost Classifier

In order to choose between these three models, we rely both on accuracy and F0.5 score to have a good balance between precision and recall (placing a bit more emphasis on precision thanks to the beta parameter). Based on these criteria, AdaBoost trains fast and gives higher score. We further tune its hyperparameters through grid search:

- number of weak learners used (n_estimators): 100, 200, 500
- learning rate (learning_rate): 0.5, 1, 2

After tuning, we see improvement in performance, both for the F0.5 score and the accuracy compared to the original model. It is also an approximately 3x increase compared to our naive predictor, which was our original benchmark.

### Feature Selection
The 5 most important features in the model are *capital_gain, capital_loss,hours_per_week, education_num and age*. With that in mind, we can fit a model with only these most important features, at very little cost in accuracy and F0.5 score. As a result, if speed is of the essence for the training of this model, I would recommend focusing on these features.

## Acknowledgments
This project was part of Udacity's Data Scientist nanodegree. They provided the data, as well as the original instructions for this project. All of the code is my own unless specified otherwise.

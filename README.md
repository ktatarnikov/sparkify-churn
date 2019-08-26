# The Churn Classification Using Apache Spark

  This repo contain the set of notebooks addressing the improvement of the fictitious online music service.
  The issue the company is trying to solve is to reduce customer churn.

  The approach is to determine the target group - the customers that are in a risky category and potentially willing to unsubscribe from the service and then to give them an incentive to stay, e.g. in a form of discounts or special offers.

  In order to determine the customers under risk user activity features are extracted from the service access log and model is trained that can predict if the user is likely to unsubscribe soon.

# Problem statement

  The full dataset is big to fit single workstation therefore I split the pipeline into two parts: the goal of the first part is to do model selection - it operates on a small subset of the data and allows fast iteration during data wrangling and features engineering, the goal of the second part is testing and tuning the final model on the full dataset where I use the distributed spark cluster.

  The small dataset pipeline performs the following steps:

  - Loading the dataset
  - Preprocessing the data: Cleaning the data from NaNs and convert types if necessary
  - Extracting possible features and verifying if they can explain churn
  - Feature Engineering: checking feature distributions, assembling the classification dataset
  - Model selection among three candidates: Decision Tree, Random Forest, Gradient Boosting Tree

  The big dataset pipeline continues where the previous pipeline left off:

  - Executes the code that does feature engineering from the first pipeline and assemble features on the big dataset
  - Perform model tuning using the best model from the first pipeline
  - Execute final testing on the big dataset

# Datasets

  - Small dataset is available in the repository
  - Full dataset (12Gb) available from [Udacity](https://www.udacity.com/course/data-scientist-nanodegree--nd025)

# Feature Engineering

  Based on exploratory analysis the following features are included in the final dataset:
  - user_city
  - user_state
  - user_os
  - items_in_session: min and max item in sessions
  - sessions_per_week: min and avg sessions per week
  - total length of all listened songs
  - minimum page views per day for pages: Add friend, Add to Playlist, Next Song, Roll Advert, Thumbs Down, Thumbs Up
  - maximum page views per day for pages: About, Add friend, Next Song, Thumbs Down

# Classification Model Selection

  Model selection is done among three algorithms: Decision Tree, Random Forest, Gradient Boosting Tree.

  The results of model selections are the following:

    | Classifier             | f1score |
    | Decision Tree          | 0.76    |
    | Random Forest          | 0.82    |
    | Gradient Boosting Tree | 0.71    |

  The selected model is Random Forest

# Test Results

  The results of the evaluation on the final dataset are given below:
  - f1score: 0.81
  - precision: 0.82
  - recall: 0.83
  - accuracy: 0.83

# Setup

  The notebooks can be run in the AWS Spark EMR Cluster (EMR 5.20).

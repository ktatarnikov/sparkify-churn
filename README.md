# The Churn Classification Using Apache Spark

  This repo contain the set of notebooks addressing the improvement of the fictitious online music service.
  The issue the company is trying to solve is to reduce customer churn.

  The approach is to determine the target group - the customers that are in a risky category and potentially willing to unsubscribe from the service and then to give them an incentive to stay, e.g. in a form of discounts or special offers.

  In order to determine the customers under risk user activity features are extracted from the service access log and model is trained that can predict if the user is likely to unsubscribe soon.

# Problem statement

  For the classification task I take the user activity log and extract a number of relevant features so they potentially can explain the risky category:
  Further the binary classifier is trained using the extracted features. Three candidate algorithms are evaluated: Decision tree, Random forest and Gradient boosting.

  The full dataset contains 12Gb of data and it is too big to wrangle locally, therefore model selection is done on a small subset and then the best model
  is being evaluated on the full dataset where the final parameter tuning and testing is done.

# Datasets

  - Small dataset is available in the repository (mini_sparkify_event_data.json.zip)
  - Full dataset (12Gb) available in s3 bucket (s3n://udacity-dsnd/sparkify/sparkify_event_data.json)

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

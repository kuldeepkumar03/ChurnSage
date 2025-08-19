# ChurnSage: Customer Churn Prediction with PySpark on AWS

## Project Overview

This project implements an end-to-end machine learning pipeline to predict customer churn for a music streaming service. The entire workflow is built on a scalable, cloud-based architecture using Apache Spark and AWS. The goal was to process a large dataset, perform feature engineering, compare several classification models, and create a final model capable of identifying users at high risk of churning.

## Technology Stack

* **Cloud Platform**: AWS (Amazon Web Services)
    * **Storage**: S3 (Simple Storage Service) for the data lake.
    * **Compute**: EC2 (Elastic Compute Cloud) for the Spark cluster.
* **Big Data Framework**: Apache Spark (using the PySpark API).
* **Machine Learning**: Spark MLlib.
* **Reporting**: Power BI.

## The Pipeline

1.  **Environment Setup**: A Linux EC2 instance was configured with Java, Python, and Spark. An IAM role was attached to grant secure access to the S3 data lake.
2.  **Data Engineering**: Loaded and joined three large datasets (members, transactions, user logs) from S3 into Spark DataFrames.
3.  **Feature Engineering**: Aggregated user transaction and listening data to create powerful predictive features, such as `transaction_count`, `total_songs_played`, and `total_unique_songs`.
4.  **Data Preprocessing**: Cleaned the data by handling null values and converted categorical features (like gender) into a numerical format using `StringIndexer` and `OneHotEncoder`.
5.  **Model Training**: Assembled all features into a single vector and trained three different classification models:
    * Logistic Regression
    * Decision Tree
    * Random Forest
6.  **Model Evaluation**: Evaluated the models on a test set using the Area Under ROC Curve (AUC) metric. The Random Forest model was selected as the best performer.
7.  **Outcome**: Saved the trained Random Forest model and the final predictions back to S3 for reporting.

## Final Model Performance

| Model                 | Accuracy (AUC) |
| --------------------- | -------------- |
| Logistic Regression   | 0.643          |
| Decision Tree         | 0.271          |
| **Random Forest** | **0.843** |

The Random Forest model was the clear winner, demonstrating its ability to handle complex interactions in the data and avoid the overfitting seen in the single Decision Tree.

## Business Impact

The final predictions can be loaded into a BI tool like Power BI to create a dashboard that identifies high-risk customers. This allows a customer retention team to proactively engage these users with targeted offers and prevent churn.



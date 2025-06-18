# From Engagement to Exit: Scalable Churn Prediction Engine for Recruitment Platforms

## Overview
In this project, I built a machine learning-based churn prediction engine simulating a recruitment platform’s customer base. 

The goal: to identify customers likely to churn (i.e., stop using the platform) based on historical activity and engagement patterns.

This project mirrors a real-world SaaS recruitment platform, simulating customer behavior to explore churn dynamics. Using a synthetic dataset, I built and deployed a churn prediction engine — integrating data simulation, feature engineering, modeling, and real-time Streamlit app deployment..

## Folder Structure 

```kotlin
churn-prediction-engine/
├── data/
├── notebooks/
│   └── churn_exploration.ipynb
├── src/
│   ├── churn_pipeline.py
│   └── utils.py
├── streamlit_app.py
├── run.py
├── requirements.txt
└── README.md
```

##  Dataset Description
This is a synthetic dataset created using Python's `Faker` library to reflect customer behavior on a B2B recruitment platform (like JobStreet or SEEK). Each row represents a customer record.While synthetic, the data was carefully modeled to reflect plausible engagement behaviors using controlled randomness and business heuristics.

| Column                  | Description                                |
| ----------------------- | ------------------------------------------ |
| `customer_id`           | Unique identifier for each customer        |
| `signup_date`           | Date the customer registered               |
| `last_login_date`       | Date of most recent platform login         |
| `job_posts`             | Number of job postings created             |
| `applications_received` | Total applications received from job posts |
| `support_tickets`       | Number of support requests submitted       |
| `plan_type`             | Subscription type (e.g., Free, Basic, Pro) |
| `is_churned`            | Target label: 1 = churned, 0 = retained    |

## Project Pipeline
The project follows an end-to-end ML workflow, designed to be modular, interpretable, and ready for deployment. Here's how it's structured:

### 1. Data Simulation
Used Faker to generate ~1000 customer records.

Applied logic-based probabilities to simulate churn (e.g., low job posts + long inactivity → higher churn chance).

### 2. Data Preprocessing
Converted dates to datetime objects.

Engineered features such as:

days_since_signup

days_since_last_login

Encoded plan_type as categorical (ordinal values).

Handled feature scaling where needed.

### 3. Exploratory Data Analysis
Visualized feature distributions and class imbalance.

Found correlations: 
churn was higher among:

- Free plan users

- Inactive customers (long days_since_last_login)

- Low activity users (fewer job posts & applications)

### 4. Modeling
Models tested:

Logistic Regression (baseline)

Random Forest Classifier (best performer)

Evaluation metrics:

Accuracy, Precision, Recall, F1-score

Confusion matrix

ROC-AUC score

Best model (Random Forest) achieved:

F1-score: 0.86

ROC-AUC: 0.91

### 5. Model Insights
The model highlighted key predictors of churn, including:

- Long periods of inactivity (days since last login)

- Free-tier usage

- Low engagement (few job posts and applications)

These insights align with typical SaaS churn patterns, validating the logic behind the data simulation.

## Streamlit App (Deployed Demo)
The model is deployed via a Streamlit app, allowing users to:

Upload new customer data (CSV)

View churn predictions in real time

Highlight customers at risk of churning

🔗 [ Link to app]

## Key Insights & Business Value
- The platform can proactively detect churn risks by tracking inactivity and engagement metrics.

- Free-tier users and those with low usage patterns are more likely to churn — suggesting upsell, onboarding, or reactivation campaigns.

- Churn prediction enables data-driven customer retention strategies to reduce revenue loss.

## Potential Improvements
- Use real-world anonymized or public datasets (e.g., from Kaggle or HuggingFace) to validate performance in realistic environments.
  
- Introduce more behavior metrics like login frequency, session duration, or email engagement.

- Add time-series features (e.g., monthly job post trend).

- Use SHAP for deeper model interpretability.

- Build a dashboard with Power BI for executive reporting.

## Sample Usage (in Streamlit)
Upload a file like:
```csv
customer_id,signup_date,last_login_date,job_posts,applications_received,support_tickets,plan_type
CUS1234,2023-01-02,2024-03-15,10,120,1,Pro
CUS5678,2022-07-10,2023-12-01,1,10,3,Free
```
And the app will return:

`is_churned = 1` → likely to churn

`is_churned = 0` → likely to stay

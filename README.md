# Customer Retention Strategy for Model Fitness: Predictive Churn Analysis

## 1. Problem

Model Fitness, a gym chain, faces the challenge of customer churn, where clients decide to terminate their memberships. This churn directly impacts the economic health and growth of the business. This project aims to develop a data-driven customer retention strategy by identifying at-risk clients and the key factors driving their decisions, allowing for the implementation of proactive and personalized actions.

## 2. Data

The `gym_churn_us.csv` dataset provides detailed information about Model Fitness clients. It consists of 4000 rows and 14 columns, with no missing values, indicating high data quality.

**Key Data Characteristics:**
*   **Gender, Near_Location, Partner, Promo_friends, Phone, Group_visits, Churn:** Binary (0/1) indicators.
*   **Contract_period, Month_to_end_contract, Lifetime, Age:** Integer values related to membership duration and demographics.
*   **Avg_additional_charges_total, Avg_class_frequency_total, Avg_class_frequency_current_month:** Float values representing spending and attendance frequency.

**Initial Observations:**
*   An overall churn rate of **26.5%** was observed.
*   The average age of clients is around 29, indicating a young-to-middle-aged client base.
*   84.5% of clients live near the gym.

## 3. Method

### 3.1. Exploratory Data Analysis (EDA)

*   **Data Loading & Initial Inspection:** Loaded `gym_churn_us.csv` and performed initial checks for size, types, and null values.
*   **Descriptive Statistics:** Summarized numerical features.
*   **Churn-based Analysis:** Calculated mean feature values for churned (Churn=1) and retained (Churn=0) customers.
*   **Distribution Visualization:** Used histograms to compare feature distributions across churn groups.
*   **Correlation Matrix:** Generated a heatmap to visualize correlations between all variables, particularly with `Churn`.

**Key EDA Findings:**
*   **Commitment Factors:** Contract duration (1-month contracts, nearing end of contract), customer `Lifetime`, and `Avg_class_frequency_current_month` are strong churn predictors.
*   **Financial Engagement:** Higher `Avg_additional_charges_total` correlates with lower churn.
*   **Social Connection:** `Promo_friends` and `Group_visits` positively influence retention.
*   **Onboarding Vulnerability:** Most churn occurs in the early stages of membership.

### 3.2. Predictive Modeling for Churn

*   **Objective:** To predict future churn to proactively identify at-risk clients.
*   **Data Preprocessing:**
    *   Split data into features (X) and target (y = `Churn`).
    *   Divided into training (75%) and testing (25%) sets (`random_state=42`).
    *   Scaled features using `StandardScaler`.
*   **Models Trained:**
    *   **Logistic Regression:** Chosen for binary classification and interpretability.
    *   **Random Forest Classifier:** Selected for robustness and ability to handle non-linear relationships.
*   **Evaluation Metrics:** Accuracy, Precision, and Recall were used to assess model performance.

### 3.3. Customer Segmentation (Clustering)

*   **Objective:** Group customers with similar characteristics for personalized retention strategies.
*   **Data Preparation:** Removed `Churn` column and standardized remaining features.
*   **Optimal Cluster Estimation:** A dendrogram was used to visually determine an optimal number of 5 clusters for K-Means.
*   **K-Means Clustering:** Applied K-Means with 5 clusters to segment the customers.
*   **Profile Analysis:** Calculated mean characteristics for each cluster and analyzed their specific churn rates to create detailed user profiles.
*   **Visualization:** Generated density plots to visualize feature distributions per cluster.

## 4. Results/KPIs

### 4.1. Predictive Model Performance

| Metric    | Logistic Regression | Random Forest |
|-----------|---------------------|---------------|
| **Accuracy**| 0.9260              | 0.9150        |
| **Precision**| 0.8841              | 0.8621        |
| **Recall**  | 0.8142              | 0.7905        |

**Conclusion:** The **Logistic Regression** model outperformed Random Forest across all metrics, particularly in **Recall (0.8142)**. This makes it the preferred model for churn prediction, as it is better at identifying a larger proportion of actual churning customers (minimizing false negatives), which is critical for effective retention efforts.

### 4.2. Customer Cluster Profiles and Churn Rates

Five distinct customer clusters were identified:

*   **Cluster 0: Low Commitment & Distant Customers**
    *   **Churn:** 0.450 (high)
    *   **Profile:** Live far from the gym, short contracts, low lifetime, moderate-low visit frequency. High churn risk.
*   **Cluster 1: Loyal, Long-Term Customers**
    *   **Churn:** 0.022 (very low)
    *   **Profile:** Very long contracts, high remaining contract time, good lifetime, high additional spending. Most valuable and loyal.
*   **Cluster 2: Active Customers with Social Connections**
    *   **Churn:** 0.246 (moderate)
    *   **Profile:** Referred by friends or corporate partners, medium contract duration, moderate visit frequency. Churn risk near average.
*   **Cluster 3: New, Low Commitment Customers**
    *   **Churn:** 0.527 (highest)
    *   **Profile:** Very low lifetime, very short contracts, few months left on contract, very low visit frequency. Highest churn risk.
*   **Cluster 4: Highly Active & Senior Customers**
    *   **Churn:** 0.069 (low)
    *   **Profile:** Very high class frequency, highest lifetime, slightly older age. Highly active and committed.

**Impact on Retention Strategy:** This segmentation allows for tailored interventions:
*   **Prioritize Clusters 0 & 3:** Focus intensive efforts on these high-risk groups (proactive contact, longer contract offers, improved onboarding, attendance monitoring).
*   **Foster Loyalty in Clusters 1 & 4:** Maintain satisfaction for loyal customers (loyalty programs, recognition, exclusive services).
*   **Strengthen Social Ties in Cluster 2:** Enhance community events and incentivize referrals to boost engagement and extend contracts.

## 5. How to Run

1.  **Environment:** Ensure you have a Python environment with `pandas`, `scikit-learn`, `matplotlib`, `seaborn`, and `scipy` installed.
2.  **Data:** Download `gym_churn_us.csv` and place it in a directory you know and update the `pd.read_csv()` path in the notebook.
3.  **Execution:** Run the Jupyter Notebook (`.ipynb`) cells sequentially from top to bottom.

## 6. Demo

The notebook provides a comprehensive demonstration of the analysis. Upon execution, users will see:

*   **Data Overview:** Initial DataFrame head, info, and descriptive statistics.
*   **EDA Visualizations:** Histograms showing feature distributions by churn status, and a correlation heatmap.
*   **Model Evaluation:** Printed metrics (Accuracy, Precision, Recall) for both Logistic Regression and Random Forest models.
*   **Clustering Analysis:** A dendrogram for cluster estimation, a table of mean characteristics for each of the 5 K-Means clusters, and density plots visualizing feature distributions across these clusters.
*   **Churn Rate by Cluster:** A clear display of churn rates for each identified customer segment.

Throughout the notebook, markdown cells provide detailed observations, analyses, conclusions, and strategic recommendations, guiding you through the entire process from raw data to actionable business insights for Model Fitness.

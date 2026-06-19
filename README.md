<div align="center">
📊 Advanced Data Mining Dashboard

An end-to-end, GUI-driven data mining pipeline — upload a raw CSV and get cleaning, clustering, and classification with zero code.

Show Image
Show Image
Show Image
Show Image

Overview · Architecture · Project 1 · Project 2 · Setup

</div>

📌 Overview

The Advanced Data Mining Dashboard is an interactive Python application that takes raw, messy CSV data and turns it into analytical insight — without the user writing a single line of code. It handles data validation, cleaning, feature engineering, dimensionality reduction, clustering, and classification, all behind a simple Gradio web interface.

The system combines two independent analytical pipelines into one dashboard:

PipelineGoalTechniqueProject 1Customer segmentationData cleaning → PCA → K-Means clusteringProject 2Predictive modelingFeature engineering → Logistic Regression classification


🛠️ Tech Stack

LayerTechnologyLanguagePython 3GUIGradioData manipulationPandas · NumPyMachine learningscikit-learnVisualizationMatplotlib · Plotly


📁 Project Structure

data-mining-dashboard/
├── gui_app.py            # GUI layer — file upload, event binding, output rendering
├── project1_logic.py     # Data mining & unsupervised learning (cleaning, PCA, K-Means)
├── project2_logic.py     # Predictive modeling & supervised learning (Logistic Regression)
├── project1_unclean.csv  # Sample raw dataset for Project 1 (customer data)
├── project2_unclean.csv  # Sample raw dataset for Project 2 (transaction data)
└── README.md

The codebase follows a 3-layer modular design:


GUI layer (gui_app.py) — handles file upload, triggers pipelines, displays results
Unsupervised learning logic (project1_logic.py) — cleaning, PCA, clustering
Supervised learning logic (project2_logic.py) — feature engineering, classification


This separation keeps the UI free of analytical logic and makes each module independently testable.


🏗️ Architecture

User uploads CSV
      │
      ▼
 Gradio GUI (gui_app.py)
      │
      ▼
 Processing logic (project1_logic.py / project2_logic.py)
      │
      ├── Data validation & cleaning
      ├── Feature engineering
      ├── Model execution (PCA / K-Means / Logistic Regression)
      └── Logging at every stage
      │
      ▼
 Visualizations, logs & processed data → rendered back in GUI

Each processing stage is logged for transparency and traceability.


🧮 Project 1 — Cleaning, PCA & Clustering

Goal: Clean customer-related data, reduce dimensionality, and group similar customers using K-Means.

Data Validation & Preparation

StepWhat it doesMissing column handlingAdds any expected column as NaN if absent, to keep schema consistentType conversionCoerces values to numeric, converting invalid entries to NaNOutlier handlingFlags unrealistic values (e.g. Age <= 0 or Age > 90) as missingMissing value imputationFills missing numeric values with the column medianCategorical encodingMaps Gender (male/female) to 0/1

Dimensionality Reduction & Clustering


Standardization — StandardScaler ensures all features contribute equally
PCA — reduces features to 2 principal components while preserving variance
K-Means — groups records into 3 clusters based on feature similarity
Visualization — interactive PCA scatter plot (Plotly), colored by cluster



🎯 Project 2 — Predictive Modeling

Goal: Predict whether a transaction amount is above or below the median value (binary classification).

Feature Engineering


Item Count Extraction — converts the Items_Purchased text field into a numeric count (number of comma-separated items)


Model Pipeline

StepDetailTrain/test split75/25 split, stratified to preserve class balanceModelLogisticRegression(max_iter=1000)EvaluationConfusion matrix visualization (ConfusionMatrixDisplay)InterpretabilityFeature importance via model.coef_


🚀 Setup

Prerequisites


Python 3.9+


1 — Install dependencies

bashpip install gradio pandas numpy scikit-learn matplotlib plotly

2 — Run the dashboard

bashpython gui_app.py

3 — Use it


Open the local Gradio URL printed in the terminal
Upload a CSV file (e.g. project1_unclean.csv or project2_unclean.csv)
Click Run to trigger the analysis pipeline
View logs, plots, and the cleaned/processed dataset directly in the browser



📊 Sample Data

FileUsed byContentsproject1_unclean.csvProject 1Raw customer demographic data (age, gender, etc.) with missing/invalid valuesproject2_unclean.csvProject 2Raw transaction data (Transaction_ID, Items_Purchased, Date, Amount) with inconsistent formats and missing values


Both sample datasets are intentionally "dirty" — inconsistent date formats, missing values, and messy text fields — to demonstrate the dashboard's automated cleaning capabilities.




✅ Key Strengths


Modular, scalable architecture — clear separation between UI and analytical logic
Automated data cleaning & validation — handles missing columns, invalid types, and outliers without manual intervention
No-code analysis — non-technical users can run advanced ML pipelines through the GUI
Industry-standard libraries — built on scikit-learn, Pandas, and Plotly



🔭 Future Extensions


Support for additional datasets and file formats
Additional clustering/classification algorithms (e.g. DBSCAN, Random Forest)
Real-world business analytics use cases (churn prediction, market segmentation, etc.)

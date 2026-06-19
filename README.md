<div align="center">

# 📊 Advanced Data Mining Dashboard

**An end-to-end, GUI-driven data mining pipeline — upload a raw CSV and get cleaning, clustering, and classification with zero code.**

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Gradio](https://img.shields.io/badge/Gradio-UI-FF7C00?style=flat-square&logo=gradio&logoColor=white)](https://gradio.app)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)](https://scikit-learn.org)
[![Plotly](https://img.shields.io/badge/Plotly-Visualization-3F4F75?style=flat-square&logo=plotly&logoColor=white)](https://plotly.com)

[Overview](#-overview) · [Architecture](#-architecture) · [Project 1](#-project-1--cleaning-pca--clustering) · [Project 2](#-project-2--predictive-modeling) · [Setup](#-setup)

</div>

---

## 📌 Overview

The **Advanced Data Mining Dashboard** is an interactive Python application that takes raw, messy CSV data and turns it into analytical insight — without the user writing a single line of code. It handles data validation, cleaning, feature engineering, dimensionality reduction, clustering, and classification, all behind a simple **Gradio** web interface.

The system combines two independent analytical pipelines into one dashboard:

| Pipeline | Goal | Technique |
|---|---|---|
| **Project 1** | Customer segmentation | Data cleaning → PCA → K-Means clustering |
| **Project 2** | Predictive modeling | Feature engineering → Logistic Regression classification |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3 |
| GUI | Gradio |
| Data manipulation | Pandas · NumPy |
| Machine learning | scikit-learn |
| Visualization | Matplotlib · Plotly |

---

## 📁 Project Structure
data-mining-dashboard/

├── gui_app.py            # GUI layer — file upload, event binding, output rendering

├── project1_logic.py     # Data mining & unsupervised learning (cleaning, PCA, K-Means)

├── project2_logic.py     # Predictive modeling & supervised learning (Logistic Regression)

├── project1_unclean.csv  # Sample raw dataset for Project 1 (customer data)

├── project2_unclean.csv  # Sample raw dataset for Project 2 (transaction data)

└── README.md

The codebase follows a **3-layer modular design**:

1. **GUI layer** (`gui_app.py`) — handles file upload, triggers pipelines, displays results
2. **Unsupervised learning logic** (`project1_logic.py`) — cleaning, PCA, clustering
3. **Supervised learning logic** (`project2_logic.py`) — feature engineering, classification

This separation keeps the UI free of analytical logic and makes each module independently testable.

---

## 🏗️ Architecture
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

---

## 🧮 Project 1 — Cleaning, PCA & Clustering

**Goal:** Clean customer-related data, reduce dimensionality, and group similar customers using K-Means.

### Data Validation & Preparation

| Step | What it does |
|---|---|
| Missing column handling | Adds any expected column as `NaN` if absent, to keep schema consistent |
| Type conversion | Coerces values to numeric, converting invalid entries to `NaN` |
| Outlier handling | Flags unrealistic values (e.g. `Age <= 0` or `Age > 90`) as missing |
| Missing value imputation | Fills missing numeric values with the column **median** |
| Categorical encoding | Maps `Gender` (`male`/`female`) to `0`/`1` |

### Dimensionality Reduction & Clustering

1. **Standardization** — `StandardScaler` ensures all features contribute equally
2. **PCA** — reduces features to 2 principal components while preserving variance
3. **K-Means** — groups records into 3 clusters based on feature similarity
4. **Visualization** — interactive PCA scatter plot (Plotly), colored by cluster

---

## 🎯 Project 2 — Predictive Modeling

**Goal:** Predict whether a transaction amount is above or below the median value (binary classification).

### Feature Engineering

- **Item Count Extraction** — converts the `Items_Purchased` text field into a numeric count (number of comma-separated items)

### Model Pipeline

| Step | Detail |
|---|---|
| Train/test split | 75/25 split, **stratified** to preserve class balance |
| Model | `LogisticRegression(max_iter=1000)` |
| Evaluation | Confusion matrix visualization (`ConfusionMatrixDisplay`) |
| Interpretability | Feature importance via `model.coef_` |

---

## 🚀 Setup

### Prerequisites

- Python 3.9+

### 1 — Install dependencies

```bash
pip install gradio pandas numpy scikit-learn matplotlib plotly
```

### 2 — Run the dashboard

```bash
python gui_app.py
```

### 3 — Use it

1. Open the local Gradio URL printed in the terminal
2. Upload a CSV file (e.g. `project1_unclean.csv` or `project2_unclean.csv`)
3. Click **Run** to trigger the analysis pipeline
4. View logs, plots, and the cleaned/processed dataset directly in the browser

---

## 📊 Sample Data

| File | Used by | Contents |
|---|---|---|
| `project1_unclean.csv` | Project 1 | Raw customer demographic data (age, gender, etc.) with missing/invalid values |
| `project2_unclean.csv` | Project 2 | Raw transaction data (`Transaction_ID`, `Items_Purchased`, `Date`, `Amount`) with inconsistent formats and missing values |

> Both sample datasets are intentionally "dirty" — inconsistent date formats, missing values, and messy text fields — to demonstrate the dashboard's automated cleaning capabilities.

---

## ✅ Key Strengths

- **Modular, scalable architecture** — clear separation between UI and analytical logic
- **Automated data cleaning & validation** — handles missing columns, invalid types, and outliers without manual intervention
- **No-code analysis** — non-technical users can run advanced ML pipelines through the GUI
- **Industry-standard libraries** — built on scikit-learn, Pandas, and Plotly

---

## 🔭 Future Extensions

- Support for additional datasets and file formats
- Additional clustering/classification algorithms (e.g. DBSCAN, Random Forest)
- Real-world business analytics use cases (churn prediction, market segmentation, etc.)

---

## 📄 License

Built as a Data Mining course project.

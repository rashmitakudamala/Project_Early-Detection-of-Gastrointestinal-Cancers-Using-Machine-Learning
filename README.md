# Early Detection of Gastrointestinal Cancers Using Machine Learning

This repository contains the Jupyter notebook and presentation slides for a group project completed as part of **INFO-I 501: Introduction to Informatics, Indiana University**.
The project investigates whether **blood-based biomarkers**, supported by statistical analysis and machine learning, can assist in the **early detection of gastrointestinal (GI) cancers**, specifically gastric and colorectal cancers.

---

## Purpose and Motivation

Gastrointestinal cancers often remain undetected until advanced stages due to vague symptoms and reliance on invasive diagnostic methods. Early detection can significantly improve outcomes, yet current screening methods (endoscopy, imaging, biopsy) are costly and unsuitable for population-level use.

This project explores whether **patterns in routine blood biomarkers**, evaluated through data-driven techniques, can distinguish **cancer** from **normal** cases in a scalable, non-invasive manner.

---

## Project Objectives

1. Integrate, clean, and preprocess biomarker and demographic data from multiple source tables.
2. Apply clinical threshold–based feature engineering to enhance interpretability.
3. Perform statistical testing to identify biomarkers with significant differences between groups.
4. Address class imbalance using multiple resampling strategies.
5. Train and evaluate machine learning models to classify GI cancer vs. normal cases.
6. Identify high-impact biomarkers and assess their predictive relevance.
7. Demonstrate a reproducible, end-to-end analytical pipeline suitable for research or clinical prototyping.

---

## Tools and Technologies Used

### Programming & Data Analysis

* Python
* Pandas (data wrangling and transformation)
* NumPy (numerical operations)
* Scikit-learn (modeling, evaluation, and preprocessing)
* Imbalanced-learn (SMOTE, oversampling, undersampling, bootstrapping)
* Matplotlib and Seaborn (EDA, statistical plots, and model visualizations)

### Database Integration (SQL → Python Workflow)

A structured database workflow was used to ensure clean integration of biomarker and demographic records.

* **MySQL** for storing and managing extracted biomarker and metadata tables
* **phpMyAdmin** for uploading and organizing CancerSeek CSV files
* **mysql.connector** for SQL-to-Python connectivity
* **Pandas** for executing SQL queries and retrieving tables into Jupyter Notebook

**End-to-end extraction workflow:**

```
CancerSeek Supplementary CSV Files (Tables 1–6)
               |
               v
Upload to phpMyAdmin → Stored in MySQL
               |
               v
SQL connection in Jupyter Notebook (mysql.connector)
               |
               v
SQL queries to retrieve:
   - Biomarker matrix (SampleID + biomarker values)
   - Demographic / clinical metadata
               |
               v
Merge on SampleID (outer join)
               |
               v
Unified dataset imported into Python
```

This integration ensured consistency, reproducibility, and a reliable foundation for downstream statistical and machine learning analysis.

---

## Workflow Overview

### Data Cleaning and Preparation

```
Merged Dataset
    |
    |-- Remove non-numeric characters (*, ^, spaces)
    |-- Drop irrelevant metadata fields
    |-- Retain only gastric, colorectal, and normal cases
    |-- Standardize column names and data types
    |-- Convert cancer status to binary labels (1 = cancer, 0 = normal)
    |-- Remove rows with missing values (<10% of dataset)
    v
Cleaned dataset (1,255 records)
```

### Feature Engineering

```
Cleaned Dataset
    |
    |-- Apply clinical thresholds to biomarker values
    |-- Flag as normal (0) or elevated (1)
    |-- Preserve continuous values for biomarkers without standard thresholds
    v
Engineered Feature Set
```

### Statistical Analysis

* Independent t-tests for continuous biomarkers
* Mann–Whitney U tests for non-normally distributed biomarkers
* Chi-square tests for threshold-based categorical features
* Identification of biomarkers showing statistically significant differences between groups

### Machine Learning Pipeline

```
Train-Test Split (80/20)
         |
         |-- SMOTE
         |-- Oversampling
         |-- Undersampling
         |-- Bootstrapping
         v
Model Training:
   - Random Forest
   - Logistic Regression
         |
         v
Evaluation:
   - AUC
   - Precision
   - Recall
   - F1-score
   - Confusion matrices
```

---

## Key Findings

### Machine Learning Results

Random Forest consistently outperformed Logistic Regression across sampling strategies.
The best-performing configuration was:

**Random Forest + SMOTE**, achieving:

* High AUC (0.92)
* Balanced precision and recall
* Effective detection of cancer cases without overfitting

Undersampling also performed well, producing the highest F1-score for Random Forest.

### Biomarker Insights

Several biomarkers showed strong predictive value and significant differences between groups.
The most impactful included:

* IL-6
* TIMP-2
* CEA
* CD44
* Prolactin
* PAR
* sEGFR
* sPECAM-1

These biomarkers contributed substantially to classification and should be considered in future biomarker-based screening research.

### Demographic Findings

Age, sex, and race were weak predictors relative to biomarker patterns.
Biomarkers provided the primary discriminatory power in all modeling approaches.

---

## Novelty of the Project

1. **Hybrid Clinical-ML Approach**
   The integration of clinical cutoff thresholds with machine learning created a medically interpretable feature space.

2. **Comprehensive Resampling Comparison**
   Multiple imbalance-handling methods were evaluated systematically to identify the most reliable strategy.

3. **SQL-Based Data Integration**
   Few student projects utilize a full MySQL → Python data pipeline, demonstrating proficiency in database systems and reproducible workflows.

4. **Dual Representation of Biomarkers**
   Continuous and threshold-based representations provided deeper insights across statistical and ML analyses.

5. **End-to-End Reproducibility**
   The notebook reflects a complete workflow from raw data to final model evaluation, suitable for research extension.

---

## Future Continuation

This project can be extended in several impactful directions:

* Multi-class classification (e.g., distinguishing gastric vs. colorectal cancer)
* External dataset validation to test generalizability
* SHAP or LIME interpretability for clinical explainability
* Development of a lightweight risk prediction prototype
* Longitudinal biomarker trend analysis for early relapse detection
* Integration of additional clinical variables (e.g., lifestyle factors, comorbidities)

---

## Repository Contents

```
├── gi-cancer-early-detection.ipynb    # Complete analysis and machine learning workflow
└── presentation.pdf                   # Slide deck summarizing methods and findings
```

---

## Course Context

This project was completed as part of:

**INFO-I 501: Introduction to Informatics
Indiana University**

---

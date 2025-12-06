# Medicare-claim-variance-analysis
A Healthcare Revenue Cycle Analytics Project using PySpark & Machine Learning

This project builds an end-to-end Medicare claim denial prediction system designed to help healthcare providers understand why claims get denied and how to reduce denial rates using data-driven insights. It integrates multiple CMS datasets, performs large-scale preprocessing in PySpark, and applies machine learning to predict denial likelihood and highlight major contributing factors.

# Project Overview

In the U.S. healthcare reimbursement process, claim denials cause significant revenue loss and operational inefficiency. This project leverages Medicare inpatient, outpatient, and carrier claims to identify patterns behind denials and create a scalable model to support Root-Cause Analysis (RCA).

Key objectives:

- Clean and normalize raw Medicare claims (beneficiary, inpatient, outpatient, carrier)

- Join datasets with DRG tables for richer clinical and financial context

- Train ML models (Linear Regression, Random Forest) to predict payment variances and denials

- Visualize trends such as top denied DRGs, payment variance by MDC, and provider performance

# Data Sources

CMS De-SynPUF (2008–2010)

- Inpatient, Outpatient, and Carrier claims

- Beneficiary summary tables

MS-DRG Weight Tables (2008–2010) — from CMS Final Rule files (Table 5)

- Columns: DRG Code, Title, Weights, LOS (Geometric & Arithmetic)

DRG–MDC Mapping — used to link claim diagnosis with cost and length of stay

Custom Derived Features:

- dx_all, pr_all, dx_count, drg_weight, base_rate, payment_variance, etc.

# Data Engineering Pipeline

Built in PySpark for scalability and reproducibility:

1. Data Ingestion:

- Read and combine multiple years of Medicare datasets (2008–2010).

- Extract and clean MS-DRG tables (converted from PDF → CSV/Excel → Spark DataFrames).

2. Data Cleaning & Feature Engineering:

- Remove duplicates, handle nulls, and standardize column names.

- Merge inpatient/outpatient/carrier data into unified claim structure.

- Map DRG codes to weights, LOS, and MDC categories.

- Add derived features such as avg_payment, payment_to_weight_ratio, and variance_from_expected.

3. Categorical Encoding:

- Applied StringIndexer + OneHotEncoder for categorical variables like gender, exercise_frequency, diet_quality, us_state.

4. Model Development:

- Built predictive models for payment variance and denial probability using:

- Linear Regression

- Random Forest Regressor (optimized for limited memory)

- Evaluated using RMSE, MAE, and R² metrics.

5. Root-Cause Visualization:

- DRG vs. Average Payment

- MDC vs. LOS vs. Payment

- State-level payment variance heatmap

- Provider-type performance dashboards

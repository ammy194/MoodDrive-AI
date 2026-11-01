# MoodDrive AI — Dataset 1 Exploration

## 1. Dataset Information
- Source: Hugging Face
- Publisher: premswan
- Dataset: Engine Predictive Maintenance Data
- Format: CSV
- Total records: 19,535
- Total features: 6
- Target variable: Engine Condition
- Declared licence: MIT

## 2. Dataset Structure
The dataset contains six numerical engine measurements:
- Engine RPM
- Lub oil pressure
- Fuel pressure
- Coolant pressure
- Lub oil temperature
- Coolant temperature

The target variable is Engine Condition.

## 3. Target Distribution
- Class 1: 12,317 records (63.05%)
- Class 0: 7,218 records (36.95%)

The dataset has a moderately imbalanced binary target distribution.

## 4. Data Quality
- Missing values: 0
- Duplicate records: 0
- All columns contain 19,535 observations.
- All features are numerical.

## 5. Initial Observations
- The dataset is suitable for initial exploratory data analysis.
- Pressure and temperature measurements have different numerical scales.
- Some pressure measurements have very small minimum values and require further investigation.
- The original data collection methodology and independent ground-truth validation remain to be established.

## 6. Next Steps
1. Investigate feature distributions.
2. Identify potential outliers.
3. Analyse correlations between engine measurements.
4. Investigate target relationships.
5. Prepare data for baseline machine-learning experiments.
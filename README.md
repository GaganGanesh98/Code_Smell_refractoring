AI-Driven Code Refactoring & Technical Debt Reduction

An end-to-end machine learning pipeline for predicting code refactoring impact and optimizing technical debt reduction using XGBoost and statistical validation.

This project explores how AI can assist software developers in prioritizing refactoring decisions by predicting complexity reduction and comparing AI-driven selection strategies against traditional static-rule baselines.

⸻
 Project Overview

Modern software systems accumulate technical debt over time, leading to:
	•	Reduced maintainability
	•	Increased bug-proneness
	•	Higher long-term development cost

This project builds a data-driven AI system that:
	1.	Predicts refactoring benefit (delta_complexity)
	2.	Prioritizes files under a fixed refactoring budget
	3.	Compares AI vs rule-based vs random baselines
	4.	Validates results using bootstrap statistical testing
	5.	Interprets model decisions using SHAP

⸻

Research Goal

Can AI optimize refactoring prioritization better than traditional static rules?

We evaluate whether a machine learning model can identify files that yield higher complexity reduction compared to:
	•	Random selection
	•	Static threshold rules (LOC / Cyclomatic Complexity)
	•	Technical debt–based ranking

⸻

🗂 Dataset

Synthetic but structurally realistic dataset of:
	•	120,000 files
	•	15 code smell types
	•	Multiple programming languages
	•	Pre- and post-refactoring complexity metrics

Key Features

Feature	Description
lines_of_code	File size
cyclomatic_complexity	Structural complexity
num_methods	Method count
num_classes	Class count
technical_debt_minutes	Estimated technical debt
maintainability_index	Maintainability score
bug_prone_score	Bug likelihood
developer_experience_years	Developer expertise
pre_refactor_complexity	Before refactoring
post_refactor_complexity	After refactoring

Target variable:

delta_complexity = pre_refactor_complexity - post_refactor_complexity


⸻

Model Architecture

 Regression Model
	•	Model: XGBoost Regressor
	•	Objective: Predict delta_complexity
	•	Hyperparameter search + early stopping
	•	SHAP-based interpretability

 Classification Model
	•	Model: XGBoost Classifier
	•	15 smell classes
	•	Evaluated using macro-F1 and confusion matrix

⸻

Results

Regression Performance

Metric	Value
MAE	9.71
RMSE	11.23
R²	0.667

The model explains ~67% of variance in complexity reduction.

Feature importance shows:

pre_refactor_complexity → strongest predictor


⸻

Refactoring Budget Experiment

We simulate a fixed refactoring budget (Top 10% of files).

Comparison

Strategy	Avg Delta	% Positive Improvements
Random	~11.9	70%
Static Rule	~12.0	70%
Debt Ranking	~11.3	69%
AI (XGBoost)	37.17	100%
Oracle	45.23	100%


⸻

Bootstrap Validation

1000 bootstrap iterations:
	•	AI vs Debt baseline:
	•	Mean improvement: +25.9
	•	95% CI: [25.01, 26.84]
	•	AI wins in 100% of samples
	•	AI vs Static Rule:
	•	Mean improvement: +25.17
	•	AI wins in 100% of samples

Statistically significant superiority.

⸻

Interpretability (SHAP)

SHAP analysis confirms:
	•	pre_refactor_complexity is dominant driver
	•	Structural metrics provide secondary signals

This improves trust and explainability of the prioritization system.

⸻

Important Findings

1. Regression works well

AI can effectively prioritize refactoring candidates.

2. Smell classification is difficult

Predicting specific code smell types from coarse metrics yields near-random performance (~6.6% macro-F1 for 15 classes).

This highlights that:

Code smell detection requires richer structural/AST-level features.

⸻

Repository Structure

├── AI_Code_Refactoring.ipynb
├── xgb_reg_booster.json
├── xgb_preprocess.joblib
├── figures/
├── dataset/
├── README.md


⸻

 How to Run

1. Install dependencies

pip install -r requirements.txt

Or manually:

pip install pandas numpy scikit-learn xgboost shap matplotlib seaborn joblib

2. Open notebook

jupyter notebook AI_Code_Refactoring.ipynb

3. Run all cells

⸻

 Experimental Components
	•	Feature engineering
	•	Hyperparameter search
	•	Early stopping
	•	Confusion matrix visualization
	•	Bootstrap statistical testing
	•	Budget sensitivity analysis
	•	SHAP explainability

⸻

 Academic Context

This project aligns with:

“How Can AI Assist Software Developers in Automated Code Refactoring and Technical Debt Reduction?”

Relevant for:
	•	Software Engineering
	•	AI for DevOps
	•	Technical Debt Research
	•	Intelligent Code Analysis

⸻

 Technologies Used
	•	Python
	•	XGBoost
	•	Scikit-learn
	•	SHAP
	•	Pandas / NumPy
	•	Matplotlib / Seaborn

⸻

 Future Improvements
	•	AST-level structural features
	•	Graph-based code representations
	•	Real-world repository dataset
	•	Hierarchical smell classification
	•	Integration into CI/CD pipelines

⸻

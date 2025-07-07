# Statistical Learning for Robotic Manipulation

This repository contains code, data processing scripts, and results from a statistical learning project aimed at predicting robot task duration and classifying task completion speed. The study leverages real-world control data from the Franka Panda robot performing object stacking tasks on the *PhysicalAI-Robotics-Manipulation-SingleArm* platform.

## Project Overview

- **Dataset:** `panda-stack-platforms-texture` dataset from the *PhysicalAI-Robotics-Manipulation-SingleArm* collection. This dataset contains detailed frame-level control data, including joint movements, end-effector positions, object poses, and more.
- **Data Scope:**  
  The analysis is based on features engineered **only from the first 30 frames** of each robot task episode. This design choice captures early task dynamics while keeping the feature space manageable.  
  **Important:** The target variable — episode duration — is measured over the **entire episode** (from start to finish), not just the first 30 frames.
- **Tasks:**  
  - **Regression:** Predict the total duration of each robot task episode using features derived from early episode data.
  - **Classification:** Classify whether an episode represents a "fast" or "slow" task completion relative to the median duration.
- **Data Access:**  
  The dataset used in this project is not publicly available in this repository due to its size and licensing conditions.  
  If you are interested in accessing the data for academic or research purposes, please contact:  
  **Mendy Fishman** — [mendyfishman@gmail.com](mailto:mendyfishman@gmail.com)

## Methods

### Regression Models
- Forward Stepwise Regression (interpretable, linear model with feature selection)
- Lasso Regression (L1 regularization for feature selection and bias-variance tradeoff)
- CatBoost Gradient Boosting (non-linear model capturing complex relationships)

### Classification Models
- Bagging Classifier (ensemble of decision trees to reduce variance)
- Random Forest Classifier (bagging with feature randomness for stronger generalization)
- Support Vector Machine (SVM) (optimal margin classifier for separating fast/slow tasks)
- Gradient Boosting Classifier (iteratively reduces classification error with shallow trees)

## Results

- **Regression:**  
  - *Best model:* CatBoost  
  - *Test R²:* ≈ 0.63  
  - *Test MSE:* 0.0258  

- **Classification:**  
  - *Best model:* SVM  
  - *Test Accuracy:* ≈ 84.5%  
  - *Precision (Fast Class):* ≈ 87%  
  - *F1 Score (Fast Class):* ≈ 82%

## Key Engineered Features

- End-effector displacement and velocity statistics (mean, max, variance, std)
- Joint displacement norms (individual joints and total)
- Spatial distances between end-effector and objects
- Quaternion angular differences between robot and object orientations


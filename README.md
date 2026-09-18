# Breast Cancer Classification Analysis
                                                                                                    
## Overview
Breast cancer is one of the most commonly diagnosed cancers worldwide. Early and accurate detection is critical; the difference between a malignant and benign diagnosis can determine a patient's entire treatment path. This project uses machine learning to classify breast tumors as malignant or benign based on clinical measurements of cell nuclei. Using the Wisconsin Breast Cancer Dataset, I built and compared two classification models, Logistic Regression and Random Forest, to determine which clinical features most strongly predict a cancer diagnosis, and which model performs best in this context.

## Dataset
- **Source:** Wisconsin Breast Cancer Dataset (built into scikit-learn)
- **Size:** 569 patient records, 30 features
- **Target variable:** Malignant (0) vs Benign (1)
- **Class distribution:** 212 malignant, 357 benign
- **Features:** Clinical measurements of cell nuclei including radius, texture, perimeter, area, smoothness, compactness, concavity, symmetry, and fractal dimension — each measured as mean, standard error, and worst value

- ## Tools & Technologies
- **Python** — core programming language
- **pandas & numpy** — data manipulation and numerical analysis
- **scikit-learn** — machine learning models and evaluation metrics
- **matplotlib & seaborn** — data visualization
- **Jupyter Notebook** — development environment
- **Git/GitHub** — version control

## Project Workflow

### 1. Data Loading & Cleaning
Loaded the dataset directly from scikit-learn and converted it into 
a pandas DataFrame. Ran a full data quality check:
- No missing values across all 30 features
- No duplicate rows
- All features correctly typed as float64; target as int64
Clean data means trustworthy results — documenting this step is standard practice in any professional data analytics workflow.

### 2. Exploratory Data Analysis (EDA)
Before building any model, I explored the data visually to understand patterns and relationships:
- **Correlation Heatmap** : most features are highly correlated with each other, indicating multicollinearity. Features measuring size (radius, perimeter, area) cluster together strongly.
- **Class Balance** : 357 benign vs 212 malignant. Slight imbalance noted and considered in model evaluation.
- **Feature Distributions** : malignant tumors consistently show higher worst radius and mean concave points than benign tumors, with meaningful but imperfect separation.
- **Top Feature Correlations** : worst concave points (r=0.79), worst perimeter (r=0.78), and worst radius (r=0.78) showed the strongest correlation with diagnosis.
Key insight: no single feature perfectly separates malignant from benign, which is exactly why machine learning models are needed.

### 3. Logistic Regression Classifier
Logistic Regression is a foundational classification algorithm that models the probability of a binary outcome. It is widely used in medical settings because its results are interpretable, you can explain exactly why a prediction was made.
**Results:**
- Accuracy: **97%**
- Malignant recall: **95%** (caught 95% of actual cancer cases)
- AUC: **0.997**

### 4. Random Forest Classifier
Random Forest builds 100 decision trees and combines their votes for a final prediction. It handles complex, non-linear relationships well and is more robust to outliers than logistic regression.
**Results:**
- Accuracy: **96%**
- Malignant recall: **93%**
- AUC: **0.997**

### 5. Model Comparison
Both models were compared using ROC curves: a visualization of how well each model separates the two classes across different thresholds.
- Both achieved AUC = 0.997, indicating near-perfect discrimination
- Logistic Regression marginally outperformed Random Forest on accuracy (97% vs 96%) and malignant recall (95% vs 93%)
- Random Forest identified **worst area** as the most important feature; Logistic Regression weighted **worst texture** most heavily

## Key Findings

| Metric | Logistic Regression | Random Forest |
|--------|-------------------|---------------|
| Accuracy | 97% | 96% |
| Malignant Recall | 95% | 93% |
| AUC Score | 0.997 | 0.997 |
| Top Feature | Worst Texture | Worst Area |

## What This Means
Both models achieved near-perfect AUC scores of 0.997, meaning they are exceptionally good at distinguishing malignant from benign tumors. Logistic Regression marginally outperformed Random Forest: 97% vs 96% accuracy, and 95% vs 93% malignant recall.

In cancer detection, malignant recall is the most critical metric. Missing a malignant tumor (a false negative) has far greater consequences than a false positive. Logistic Regression's higher malignant recall makes it the preferred model here; not just because it performs better, but because it is also interpretable. In clinical settings, a model that can explain why it flagged a tumor as malignant is far more trustworthy and actionable than one that cannot.

The two models disagreed on which features matter most; Random Forest weighted worst area most heavily, while Logistic Regression prioritized worst texture. This tells us that tumor size and surface irregularity are both meaningful predictors, and that no single measurement tells the whole story. Machine learning adds value precisely because it weighs many features simultaneously in ways that single-variable analysis cannot.

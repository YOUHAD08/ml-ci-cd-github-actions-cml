# 🤖 ML CI/CD Pipeline with GitHub Actions & CML

[![churn-imbalanced-dataset](https://github.com/YOUHAD08/ml-ci-cd-github-actions-cml/actions/workflows/cml-churn.yaml/badge.svg)](https://github.com/YOUHAD08/ml-ci-cd-github-actions-cml/actions/workflows/cml-churn.yaml)

**Automated Machine Learning Training & Reporting Pipeline**

This project demonstrates a complete CI/CD workflow for Machine Learning using GitHub Actions and CML (Continuous Machine Learning). Every push automatically trains a churn prediction model and publishes performance metrics directly to GitHub.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)
- [How It Works](#how-it-works)
- [Setup & Installation](#setup--installation)
- [Results](#results)
- [Future Improvements](#future-improvements)

---

## 🎯 Overview

This project tackles the **customer churn prediction** problem using imbalanced dataset techniques and automated ML workflows. The pipeline:

- ✅ Automatically trains a RandomForest model on every `git push`
- ✅ Handles class imbalance using **SMOTE** and **class weights**
- ✅ Generates performance metrics (F1-score, precision, recall)
- ✅ Creates confusion matrices for visual evaluation
- ✅ Posts automated reports as GitHub comments via **CML**

**Goal:** Demonstrate MLOps best practices with continuous integration for machine learning.

---

## ✨ Features

### 🔄 Automated CI/CD Pipeline

- GitHub Actions workflow triggered on every push
- Python 3.11 environment setup
- Automatic dependency installation
- Model training execution

### 📊 Handling Imbalanced Data

The pipeline trains **3 models** with different strategies:

1. **Baseline** - Without imbalance handling
2. **Class Weights** - Weighted loss function
3. **SMOTE** - Synthetic oversampling

### 📈 Automated Reporting

- Generates `metrics.txt` with F1-scores
- Creates combined confusion matrix visualization
- Posts results as GitHub PR/commit comments using CML

### 🧪 Data Preprocessing

- Missing value imputation
- One-hot encoding for categorical features
- Standard scaling for numerical features
- Age-based filtering (outlier removal)

---

## 📁 Project Structure

```
ml-ci-cd-github-actions-cml/
│
├── dataset.csv                    # Customer churn dataset
├── script.py                      # ML training script
├── requirements.txt               # Python dependencies
│
├── .github/
│   └── workflows/
│       └── cml-churn.yaml        # GitHub Actions + CML pipeline
│
├── README.md                      # Project documentation
│
└── outputs/ (generated)
    ├── metrics.txt                # Model performance metrics
    └── conf_matrix.png            # Combined confusion matrices
```

---

## 🛠️ Technologies Used

### Machine Learning

- **scikit-learn** - Model training & evaluation
- **imbalanced-learn** - SMOTE oversampling
- **pandas** - Data manipulation
- **numpy** - Numerical operations

### Visualization

- **matplotlib** - Plot generation
- **seaborn** - Confusion matrix heatmaps

### MLOps & CI/CD

- **GitHub Actions** - Automation workflow
- **CML** (Continuous Machine Learning) - ML reporting
- **Python 3.11** - Runtime environment

---

## ⚙️ How It Works

### 1️⃣ Data Preparation

```python
- Load dataset.csv
- Drop unnecessary columns (RowNumber, CustomerId, Surname)
- Filter outliers (Age > 80)
- Split into train/test (80/20)
```

### 2️⃣ Feature Engineering

```python
- Numerical features: Age, CreditScore, Balance, EstimatedSalary
  → Median imputation + Standard scaling

- Categorical features: Gender, Geography
  → Most frequent imputation + One-hot encoding

- Ready features: NumOfProducts, HasCrCard, IsActiveMember, Tenure
  → Most frequent imputation
```

### 3️⃣ Model Training (3 Approaches)

| Approach      | Technique                   | Purpose                                        |
| ------------- | --------------------------- | ---------------------------------------------- |
| Baseline      | None                        | Measure performance without handling imbalance |
| Class Weights | `class_weight` parameter    | Penalize majority class                        |
| SMOTE         | Oversampling minority class | Balance dataset synthetically                  |

### 4️⃣ Evaluation & Reporting

- Calculate F1-score for train/test sets
- Generate confusion matrices
- Save metrics to `metrics.txt`
- Combine all matrices into `conf_matrix.png`

### 5️⃣ CI/CD Pipeline (GitHub Actions)

```yaml
on: [push] # Triggered on every push

steps: 1. Setup Python 3.11
  2. Install dependencies
  3. Execute script.py
  4. Generate CML report
  5. Post comment to GitHub
```

---

## 🚀 Setup & Installation

### Prerequisites

- Python 3.11+
- Git
- GitHub account

### Local Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/YOUHAD08/ml-ci-cd-github-actions-cml.git
   cd ml-ci-cd-github-actions-cml
   ```

2. **Create conda environment**

   ```bash
   conda create -n ci-cd-cml-env python=3.11 -y
   conda activate ci-cd-cml-env
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Run training locally**

   ```bash
   python script.py
   ```

   **Outputs:**
   - `metrics.txt` - Model performance metrics
   - `conf_matrix.png` - Confusion matrices visualization

### GitHub Actions Setup

The CI/CD pipeline is **automatically configured** and will run on every push. No manual setup required!

Just push your code:

```bash
git add .
git commit -m "feat: your feature description"
git push
```

Check the **Actions** tab on GitHub to see the pipeline running.

---

## 📊 Results

### Automated Report Example

After each push, the pipeline generates a comment like this:

```markdown
## Metrics

RandomForestClassifier without-imbalance
F1-score of Training is: 68.XX %
F1-Score of Validation is: 62.XX %

RandomForestClassifier with-class-weights
F1-score of Training is: 72.XX %
F1-Score of Validation is: 65.XX %

RandomForestClassifier with-SMOTE
F1-score of Training is: 75.XX %
F1-Score of Validation is: 68.XX %

## Confusion Matrix

![Confusion Matrix](./conf_matrix.png)
```

### Model Comparison

The combined confusion matrix shows side-by-side comparison of all three approaches:

- **Without Imbalance Handling**
- **With Class Weights**
- **With SMOTE Oversampling**

This allows quick visual assessment of which technique performs best for the churn prediction task.

## 📚 Workshop Context

This project is part of **Atelier 3: CI/CD for Machine Learning** taught by Prof. Soufiane HAMIDA (January 17, 2026).

**Learning Objectives:**

- ✅ Automate ML training with GitHub Actions
- ✅ Generate automated performance reports
- ✅ Implement continuous integration for data science
- ✅ Use CML for ML-specific CI/CD workflows

---

## 📄 License

This project is for educational purposes as part of ENSET ML/MLOps curriculum.

---

## 👤 Author

**Ayoub Youhad** ([@YOUHAD08](https://github.com/YOUHAD08))

---

## 🙏 Acknowledgments

- Prof. Soufiane HAMIDA for the workshop materials

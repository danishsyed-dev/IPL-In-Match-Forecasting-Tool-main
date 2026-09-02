# 🏏 IPL 2nd Innings Chase Success Probability Model

This repository contains a pre-processed dataset and machine learning script that predicts whether a team successfully **chases a target score** using Indian Premier League (IPL) matches across all seasons to 2025.  

The project uses a **Random Forest Classifier** with hyperparameter tuning and is evaluated on data from the **2025 IPL season** as a hold-out test set.  

---

## Dataset

The project uses a comprehensive historical IPL dataset (`win_viz_df.xlsx`) containing:
- Ball-by-ball match data from all IPL seasons through 2025
- Pre-engineered features capturing match context and game state
- Binary target variable: `chased_successfully` (successful chase = 1, failed = 0)

---

## Model Pipeline

The training workflow includes the following key steps:

1. **Data Loading & Preprocessing** — Imports pre-processed IPL historical data
2. **Baseline Establishment** — Evaluates baseline performance metrics (log loss, accuracy, F1 score)
3. **Hyperparameter Optimization** — Applies GridSearchCV with Stratified K-Fold cross-validation, optimizing log loss
4. **Random Forest Tuning** — Tunes key hyperparameters: `n_estimators`, `max_depth`, `min_samples_leaf`
5. **Model Evaluation** — Validates performance on held-out 2025 IPL season test set
6. **Artifacts Generation** — Produces:
   - Cross-validation results dataframe (log loss, accuracy, F1 scores)
   - Feature importance rankings
   - ROC curve with AUC metric
7. **Model Serialization** — Exports trained model via joblib for production deployment

---

## Repository Structure

```
.
├── win_viz_df.xlsx                # Input dataset with historical IPL data
├── ipl_win_viz_modelling.py      # Main training and evaluation script
├── requirements.txt               # Python dependencies
├── README.md                      # Project documentation
├── results.xlsx                   # (Generated) Cross-validation results
├── rf_model.pkl                   # (Generated) Serialized trained model
└── graphify-out/                  # (Generated) Model visualization artifacts
```

## Installation

### Prerequisites
- Python 3.8 or higher
- pip or conda package manager

### Setup Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/danishsyed-dev/IPL-In-Match-Forecasting-Tool-main
   cd IPL-In-Match-Forecasting-Tool-main
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

   **Core dependencies:**
   - pandas, numpy — Data manipulation and numerical computing
   - scikit-learn — Machine learning and model evaluation
   - matplotlib, seaborn — Visualization
   - joblib — Model serialization
   - scipy, openpyxl — Additional utilities

## Usage

### Quick Start

1. **Prepare Dataset** — Ensure `win_viz_df.xlsx` is located in the repository root

2. **Configure Paths** — Update file paths in `ipl_win_viz_modelling.py`:
   ```python
   # Input data
   df = pd.read_excel('path/to/win_viz_df.xlsx')
   
   # Output results
   results_df.to_excel('path/to/results.xlsx')
   
   # Serialized model
   joblib.dump(rf_best_model, 'path/to/rf_model.pkl')
   ```

3. **Execute Training Pipeline**:
   ```bash
   python ipl_win_viz_modelling.py
   ```

### Output Artifacts

After successful execution, the script generates:
- **results.xlsx** — GridSearchCV results with cross-validation metrics
- **rf_model.pkl** — Trained Random Forest model for production inference
- **Feature rankings & ROC curve** — Model diagnostics and performance visualization



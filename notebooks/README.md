# Notebooks Overview

This folder contains the Jupyter Notebooks used for the analysis in this project.

The notebooks are designed to be run **in order**, starting from exploratory data analysis and then moving to modeling.

---

## 1. `01_eda_country_overview.ipynb`

**Purpose:**  
High-level exploratory data analysis (EDA) of the Kickstarter dataset, with a focus on country-level patterns.

**Main steps:**

- Load the raw `kickstarter_projects.csv` dataset.
- Inspect data structure (`head`, `info`, dtypes).
- Explore the distribution of:
  - Campaign states (`State`)
  - Countries (`Country`)
- Filter to completed campaigns:
  - Keep only `State` in `{"Successful", "Failed"}`
  - Create binary label: `is_success` (1 = Successful, 0 = Failed)
- Compute and visualize:
  - Number of campaigns per state
  - Top countries by number of campaigns
  - Success rate per country (especially for high-volume countries)
- Create simple derived features for later use (e.g., `log_goal`, `duration_days`, `Year`).

**Outputs / Takeaways:**

- A clear picture of where most Kickstarter campaigns come from.
- Initial comparison of success rates across countries.
- Cleaned subset of the data and ideas for modeling features.

---

## 2. `02_country_success_analysis.ipynb`

**Purpose:**  
Build a simple, interpretable **logistic regression** model to predict campaign success and study country-level differences after controlling for other factors.

**Main steps:**

1. **Data preparation**
   - Start from campaigns labeled as `Successful` / `Failed`.
   - Reuse `is_success` as the target variable.
   - Engineer features:
     - `duration_days` from `Launched` and `Deadline`
     - Filter out `Goal <= 0` and create `log_goal = log10(Goal)`
     - `Year` from `Launched`
   - Optionally restrict to the **top N countries** by campaign count (e.g., top 5) to reduce sparsity.

2. **Feature matrix**
   - Input features:
     - `Country` (categorical)
     - `Category` (categorical)
     - `Year`
     - `log_goal`
     - `duration_days`
   - Target: `is_success` (0 = failed, 1 = successful)
   - Encode categorical variables using `pandas.get_dummies(drop_first=True)`.

3. **Model training**
   - Split data into train/test sets with `train_test_split`:
     - `test_size=0.2`
     - `stratify=y` to preserve class balance
   - Train a baseline logistic regression model:
     - `LogisticRegression(max_iter=1000)`

4. **Evaluation**
   - Use:
     - `classification_report` (precision, recall, f1-score, accuracy)
     - `confusion_matrix`
   - Analyze how well the model identifies:
     - Failed campaigns
     - Successful campaigns
   - Discuss limitations (e.g., missing text/marketing features).

5. **(Optional) Hyperparameter exploration**
   - Experiment with:
     - `C` (regularization strength)
     - `class_weight` (e.g. `"balanced"`)
   - Observe trade-offs between overall accuracy and recall/F1 for the successful class.

**Outputs / Takeaways:**

- A working end-to-end classification model on real-world data.
- Quantitative evaluation of how well simple features (country, category, goal, duration, year) explain success.
- A foundation for more advanced models or country-level comparison of predicted success probabilities.

---

## Usage Notes

- Run `01_eda_country_overview.ipynb` **before** `02_country_success_analysis.ipynb`.
- Make sure the dataset is available at: `../data/kickstarter_projects.csv` relative to this folder.
- The notebooks are written to be executed **top-to-bottom** without manual jumping between cells.

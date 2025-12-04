# Kickstarter Country-Level Success Rate Analysis

## Overview

This project analyzes **Kickstarter crowdfunding campaigns** from a country-level perspective.

The main goal is to understand how **campaign success rates differ across countries**, and how these differences relate to:

- Funding goals  
- Campaign duration  
- Project categories (e.g., Games, Music, Technology, etc.)

The analysis is implemented in **Python** using Jupyter Notebooks, with a focus on:

- Clear EDA (exploratory data analysis)  
- A simple but interpretable **logistic regression** model  
- Clean visualizations suitable for a data portfolio

---

## Dataset

- **Source**: Kaggle – `kickstarter_projects.csv`  
- **Rows**: ~375k campaigns  
- **Columns used** (original names):

  - `Category`, `Subcategory`  
  - `Country`  
  - `Launched`, `Deadline`  
  - `Goal`, `Pledged`, `Backers`  
  - `State` (e.g., `Successful`, `Failed`, `Canceled`, `Live`, `Suspended`)

For modeling, the project focuses on **completed campaigns** where:

- `State` is either `Successful` or `Failed`  

and defines a binary label:

- `is_success = 1` if `State == "Successful"`  
- `is_success = 0` if `State == "Failed"`

Additional engineered features:

- `Launched_dt`, `Deadline_dt` – parsed datetimes  
- `duration_days` – campaign duration in days  
- `log_goal` – `log10(Goal)` for `Goal > 0`  
- `Year` – launch year from `Launched_dt`

---

## Repository Structure

```text
kickstarter-country-success-analysis/
├── data/
│   └── kickstarter_projects.csv          # Raw Kaggle dataset (not committed to Git)
├── notebooks/
│   ├── 01_eda_country_overview.ipynb    # Exploratory data analysis (EDA)
│   └── 02_country_success_analysis.ipynb # Logistic regression & country-level modeling
├── .gitignore
└── README.md                             # This file
```

---

## Notebooks

- `notebooks/01_eda_country_overview.ipynb`  
  - Exploratory data analysis of the raw Kickstarter dataset  
  - Focus on state distribution, country distribution, and basic country-level success rates  

- `notebooks/02_country_success_analysis.ipynb`  
  - Logistic regression models to predict campaign success  
  - Compares a country-only model with a richer model including category, goal, backers, and duration  

---

## Conclusions

Using two logistic regression specifications, we see very different pictures of what drives Kickstarter success:

- A baseline model that includes **only country dummies** has a very low pseudo R² (~0.005), indicating that country alone explains almost none of the variation in success. Some countries (e.g., United States, United Kingdom, Hong Kong, Denmark, France) show higher success odds than the omitted baseline country, while others (e.g., Italy, Austria, Netherlands, Spain, Germany) show lower odds, but overall the model fits the data poorly.

- After adding **project category, log-transformed funding goal, number of backers, and campaign duration**, the pseudo R² jumps to ~0.75. In this richer model, the **strongest effects come from**:
  - `log_backers` (large positive coefficient): campaigns with more backers are much more likely to succeed.
  - `log_goal` (large negative coefficient): campaigns with higher funding goals are less likely to succeed.
  - Certain categories (e.g., Theater, Dance, Film & Video, Music) are associated with higher success probabilities, while others (e.g., Games, Technology, Comics) are associated with lower success probabilities.
  - Campaign duration has a small negative effect, suggesting that longer campaigns are slightly less likely to succeed.

- Once we control for these project-level factors, **most country coefficients shrink and many lose statistical significance**; a few countries (e.g., Hong Kong, Switzerland, Denmark, France) remain positively associated with success, but the differences are much smaller than in the country-only model. This suggests that **project characteristics and campaign design matter far more than country alone**.

- The second model also triggers a quasi-separation warning, meaning that a subset of campaigns is almost perfectly predicted by the included features. This reinforces that the model is very good at distinguishing “obviously successful” vs “obviously unsuccessful” projects, but some of the extreme coefficients should be interpreted with caution rather than as exact causal effects.


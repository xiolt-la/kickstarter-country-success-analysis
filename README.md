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

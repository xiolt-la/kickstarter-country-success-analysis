# Kickstarter Country-Level Success Rate Analysis

## Overview

This project analyzes **Kickstarter crowdfunding campaigns** from a country-level perspective.  
The goal is to understand how **campaign success rates differ across countries**, and how these differences relate to:

- Funding goals  
- Campaign duration  
- Project categories (e.g., Games, Music, Technology, etc.)

The analysis is implemented in **Python** using Jupyter Notebooks and focuses on clear, interpretable visualizations and practical insights.

> This project was inspired by a guided project from Dataquest, then rebuilt and extended as a personal project.

---

## Dataset

- **Source**: Kickstarter campaign dataset provided in a Dataquest course  
  - (Optionally, you can mention the original public source if available, e.g. a Kaggle dataset.)  
- **Rows**: ~`TODO: fill in` campaigns  
- **Time range**: `TODO: fill in`  
- **Key columns used in this project**:
  - `state` — final state of the campaign (e.g., `successful`, `failed`, `canceled`, etc.)  
  - `country` — country code of the project creator  
  - `main_category` — high-level project category  
  - `goal` — funding goal (in the project’s original currency)  
  - `launched`, `deadline` — timestamps for the campaign  
  - (Optionally) text fields such as `name`, `blurb` for simple text-based features

In this project, we focus on campaigns whose final state is **either `successful` or `failed`**, and we create a binary variable:

- `is_success = 1` if `state == "successful"`  
- `is_success = 0` otherwise (failed campaigns in our filtered subset)

---

## Objectives

The analysis is structured around the following questions:

1. **Which countries launch the most Kickstarter campaigns?**  
2. **How do campaign success rates differ across countries, especially for countries with a large number of projects?**  
3. **How do country-level success rates relate to:**
   - Typical funding goals  
   - Typical campaign duration  
4. **Within each major country, which project categories tend to perform best?**

These questions are relevant both for **campaign creators** (who want to increase their chances of success) and for understanding **geographic patterns** in crowdfunding.

---

## Project Structure

```text
kickstarter-country-success-analysis/
├── data/
│   └── README.md              # Notes on data source and fields (no raw data committed, optional)
├── notebooks/
│   ├── 01_eda_country_overview.ipynb
│   └── 02_country_category_and_features.ipynb
├── .gitignore
└── README.md                  # This file

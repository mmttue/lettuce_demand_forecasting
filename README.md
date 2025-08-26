# Demand Forecasting Project

This project implements an end-to-end pipeline for demand forecasting in a fast-food restaurant chain and was performed for a university lecture.
The focus is on forecasting daily demand for lettuce across four stores (two in California, two in New York), supporting inventory replenishment decisions.

The repo has been adapted into a clean, reproducible structure for public demonstration.

# Repository Structure

├── notebooks/
│ ├── 01_data_wrangling.ipynb # Extract & preprocess store-level lettuce demand
│ └── 02_forecasting.ipynb # Apply Holt-Winters, SARIMA, STL decomposition
│
├── data/
│ ├── sample/ # Small demo CSVs (included in repo)
│ └── processed/ # Generated outputs (ignored by git)
│
├── docs/
│ ├── Data_Description.pdf # Dataset description
│ ├── ERD.pdf # Entity-relationship diagram
│ └── FAQ.pdf # Frequently asked questions
│
├── requirements.txt # Python dependencies
├── .gitignore # Exclude venv, large data, cache files
└── README.md # Project documentation (you are here)

# Data Description

The dataset included:
- Transactions (pos_ordersale, menuitem)
- Menu hierarchy (menu_items, recipes, sub_recipes)
- Ingredients & units (ingredients, portion_uom_types)
- Store metadata (store_restaurant)

The focus was on IngredientId = 27 (Lettuce) and IngredientId = 291 (Lettuce - Metric), ensuring consistency in measurement (converted to pounds/ounces).

The ER diagram illustrates how transactions link through recipes and sub-recipes to ingredient usage.

# Methodology

1. Data Wrangling (01_data_wrangling.ipynb)
- Merged transactional and recipe tables into daily demand per store.
- Converted lettuce demand into a consistent unit.
- Exported aligned store-level time series to data/processed/final_demand.parquet.

2. Forecasting (02_forecasting.ipynb)
- Applied Holt-Winters exponential smoothing and SARIMA models.
- Used STL decomposition for exploratory analysis.
- Compared models via MAE, RMSE, MAPE, SMAPE.
- Exported combined two-week forecasts to data/processed/forecast_results.csv.

3. Model Insights
- Store 46673: Holt-Winters slightly outperformed SARIMA.
- Other stores: SARIMA handled seasonality better.
- Overall, hybrid usage of HW + SARIMA recommended

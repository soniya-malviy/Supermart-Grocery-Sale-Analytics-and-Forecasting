# Supermart Grocery Sales Analytics & Forecasting

This repository contains a comprehensive retail data science project focusing on **Exploratory Data Analysis (EDA)**, **Feature Engineering**, and **Time Series Forecasting** of grocery sales using transactional records spanning from 2015 to 2018.

Demo:

https://www.loom.com/share/8bf8b5b70e3a40f2ab576eee3458e08d
---

##  Key Project Insights

Through extensive exploratory analysis and statistical modeling of the transaction history, we discovered several critical drivers of sales volume and profitability:

### 1. Exploratory Data Analysis (EDA) Insights
*   **Sales Volume Leaders:** **Snacks** are the highest-selling product category by transaction volume, followed closely by **Beverages** (specifically *Health Drinks* and *Soft Drinks*).
*   **Seasonality Trends:** Sales exhibit a strong, recurring annual trend:
    *   **Peak Demand:** Sales peak dramatically in **November**, driven by year-end festival shopping and promotions.
    *   **Low Demand:** Sales hit their lowest valley in **February** as seasonal spending subsides.
*   **Profitability vs. Volume:** While Snacks and Beverages are highly profitable and command high volumes, other categories like **Oil & Masala** and **Chicken** represent the lowest sales volumes and lowest profit margins.
*   **High Discount Dependency:** Approximately **25%** of total supermarket revenue is spent on customer discounts. Statistical correlation analysis shows a high positive relationship between discount amounts and sales volume, indicating that promotions are a primary driver of transactions in this market.

### 2. Time Series Forecasting Performance
We trained and evaluated multiple forecasting models on monthly aggregated sales. The models were trained on data from **2015–2017** and evaluated on unseen test data from **2018** using **3-fold TimeSeriesSplit cross-validation**.

The final metrics comparison is summarized below:

| Forecasting Model | RMSE | MAE | MAPE | $R^2$ Score |
| :--- | :---: | :---: | :---: | :---: |
| **Prophet** | **64,625.21** | **47,992.60** | **10.35%** | **0.8605** |
| **Seasonal Naive (Baseline)** | 104,274.31 | 92,237.83 | 22.53% | 0.6369 |
| **ARIMA (5, 1, 2)** | 174,246.46 | 156,413.92 | 46.37% | -0.0139 |
| **XGBoost (Regularized)** | 201,463.95 | 146,356.05 | 33.25% | -0.3553 |
| **Naive (Baseline)** | 201,648.37 | 190,416.67 | 61.24% | -0.3578 |

*   **Best Performing Model:** **Prophet** significantly outperformed all other models, achieving a low **10.35% MAPE** and explaining **86.05%** of the variance in monthly sales.
*   **Model Analysis:** The strong performance of the *Seasonal Naive* baseline highlights the dominant annual seasonality of the dataset. More complex models like *ARIMA* and *XGBoost* struggled to generalize on the relatively small history size (48 monthly points), making Prophet's robust Bayesian curve fitting the ideal choice.

---

##  Strategic Business Recommendations

Based on these findings, we recommend the following three strategies to optimize supermarket operations:

1.  **Inventory Alignment with Seasonal Peaks:**
    *   Increase warehouse and shelf space capacity for high-selling categories (*Snacks*, *Health Drinks*, *Soft Drinks*) starting in **September/October** to prepare for the November peak.
    *   Scale down inventory levels in **January** to minimize carrying costs during the low-demand month of February.
2.  **Margin-Based Stock Optimization:**
    *   **Allocate More Resources:** Direct marketing budgets and premium shelf space towards *Health Drinks*, *Soft Drinks*, and *Cookies* (high volume + high margin).
    *   **Restructure Low-Performers:** Scale down stock levels for *Oil & Masala* and *Chicken* (low volume + low margin). Run bundled promotions (e.g., pairing Chicken with high-margin Beverages) to clear stock while protecting overall profitability.
3.  **Targeted Promotion Design:**
    *   Since store-wide discounts consume 25% of revenue, transition to targeted promotions. Direct discounts specifically towards sub-categories with high discount-to-sales sensitivity (*Beverages*) to maximize volume gains, while keeping standard margins on stable everyday staples.

---

##  Project Structure & Engineering Additions

The project Jupyter notebook [AIML_PROJECT.ipynb](file:///Users/soniyamalviya/Desktop/SME/AIML_PROJECT.ipynb) includes several advanced data science steps:
*   **Preprocessing:** Outlier handling using the IQR method (capped to preserve time series continuity), missing value matrix plots, and scaling via `MinMaxScaler` / `StandardScaler`.
*   **Feature Engineering:** Monthly lags (`lag_1`, `lag_3`, `lag_6`), rolling mean and standard deviation (7-day and 30-day windows), `profit_margin`, and sub-category-level `discount_impact` correlation mapping.
*   **Categorical Encoding:** Implementation of both Label Encoding and One-Hot Encoding with documentation of their use cases.
*   **Visualizations:** Multi-axis boxplots, YoY line plots, and actual vs. predicted forecast charts with **95% Confidence Intervals** shaded.

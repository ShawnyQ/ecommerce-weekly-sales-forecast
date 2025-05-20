# 🛒 E-Commerce Weekly Sales Forecasting

This project analyzes the weekly sales data of a UK-based online retailer. With rising inventory costs and customer demand for fast, reliable service, it's crucial to anticipate revenue fluctuations in advance.

By forecasting **weekly total sales**, this model helps the business:

- 📉 Minimize overstock and understock risks  
- 🚚 Improve inventory and fulfillment efficiency  
- 📊 Support strategic planning with data-driven insights  

---

## 📌 Problem Statement

Can we accurately forecast **weekly sales revenue** based on historical sales patterns, calendar seasonality, and recent performance trends?

---

## 🧠 Modeling Approach

We treat this as a **supervised regression problem**, using **XGBoost** to forecast weekly revenue. The model incorporates both short-term memory (lags, rolling means) and long-term seasonal indicators (month, week of year, spike-week flags).

---

## 🛠️ Workflow Overview

### 1. 🧹 Data Cleaning
- Filtered for valid UK transactions (removed cancellations and returns)
- Ensured accurate parsing of timestamps and numeric fields

### 2. 📊 Exploratory Analysis
- Ranked top products by quantity sold
- Analyzed category-level revenue and sales
- Identified and investigated a strong December spike in 2011

### 3. 📆 Feature Engineering
- Time-based fields: `Month`, `Quarter`, `WeekOfYear`
- Lag and rolling statistics: `Sales_Lag_1`, `Sales_Lag_4`, `RollingMean_4`, `RollingSTD_4`
- Seasonal flags: `IsDecember`, `IsQ4`, `IsSpikeWeek`
- Cyclical encodings: `Month_sin`, `Month_cos`

### 4. ⚙️ Modeling
- Trained `XGBoostRegressor` on weekly sales data
- Held out last 6 weeks for evaluation (time-aware split)

### 5. 📉 Evaluation
- **MAE**: £41,024  
- **RMSE**: £64,712  
- Captured the year-end spike trend, though slightly underestimated its magnitude

### 6. 🔍 Interpretation
- `WeekOfYear` was the most important feature
- Seasonal indicators provided useful signal
- Spike underprediction was attributed to unmodeled holiday events (e.g., promotions)

---

## 🔍 Visual Example

<p align="center">
</p><img width="738" alt="Screenshot 2025-05-20 at 10 55 25 AM" src="https://github.com/user-attachments/assets/8873c2bc-9a4a-4e05-906e-86d24f67a301" />


📉 The model captured trend and seasonality well, though it slightly underpredicted the final December spike.  
*Actual vs Predicted Weekly Sales (Final 6 Weeks)*

---

## ✅ Why XGBoost?

- Handles non-linear relationships and feature interactions
- Supports calendar-based features, lags, and rolling statistics
- Interpretable via feature importance

---

## 📂 Repository Contents

| File | Description |
|------|-------------|
| `E-Commerce Sales Forecast.ipynb` | Full modeling notebook |
| `train_df_ready.csv` / `test_df_ready.csv` | Cleaned datasets (linked externally if large) |
| `forecast_plot.png` | Visualization of model predictions |
| `README.md` | This file |

---

## 📦 Future Improvements

- Add holiday and promotion flags (e.g., Black Friday, Cyber Monday)
- Test alternative models like Prophet or hybrid LSTM
- Extend forecasting horizon beyond 6 weeks

---

## 👨‍💻 Author

**Shawn Waringu**  
Data Scientist & Analyst | Dubai  
[LinkedIn](https://www.linkedin.com/in/shawn-chege-856048312)  
[GitHub](https://github.com/ShawnyQ)

---

# 📘 Electricity Consumption Forecasting — Comparative Statistical & Deep Learning Study

This project is part of my **higher-studies application research work**.
It presents a comparative study of statistical, baseline, and deep learning models for **short-term hourly electricity consumption forecasting**, using the *Global Active Power* variable from the Household Power Consumption dataset.

The study evaluates:

* Naive Forecast (Baseline)
* Moving Average Models
* ARIMA
* SARIMA
* Prophet
* **LSTM (Deep Learning, 24-hour window)**

Experiments were implemented and executed in **Google Colab**.

---

## 📊 Project Motivation

Short-term load forecasting plays a critical role in:

* energy demand planning
* consumption analytics
* smart-grid load scheduling

While complex forecasting models are widely used, empirical results often show that:

> Simple persistence-based baselines may outperform sophisticated classical models for short-horizon load prediction.

This project investigates that hypothesis through a structured and reproducible model comparison.

---

## 📂 Dataset

**Household Electric Power Consumption Dataset**

Source (Kaggle mirror):
[https://www.kaggle.com/datasets/uciml/electric-power-consumption-data-set](https://www.kaggle.com/datasets/uciml/electric-power-consumption-data-set)

Target variable:

* `Global_active_power`

Preprocessing steps:

* combined Date + Time into timestamp
* sorted chronologically
* converted numeric fields
* resampled to **hourly mean consumption**
* interpolated missing hours
* applied time-aware 80/20 train–test split

Processed dataset is stored under:

```
data/processed/
```

---

## 🧮 Models Implemented

### 🟢 Baseline Models

* Naive Persistence Forecast
  *(next value = previous hour)*
* Moving Average

  * 3h, 6h, 12h, 24h windows

---

### 🟣 Statistical Models

* ARIMA
* SARIMA *(daily seasonal, m = 24)*

Models were tuned using compact parameter grids to ensure:

* reproducibility
* computational feasibility
* fair comparison across methods

---

### 🔵 Machine Learning Model

* Prophet *(trend-based time-series forecasting)*

---

### 🟠 Deep Learning Model

* **LSTM — 24-hour sliding window**

Pipeline:

* Min-Max scaling on training data
* supervised time-series sequence generation
* sequential next-hour prediction
* evaluation on unseen test set

---

## 🧾 Evaluation Metrics

All models were evaluated using:

* **MAE** — Mean Absolute Error
* **RMSE** — Root Mean Square Error
* **MAPE** — Mean Absolute Percentage Error
* **sMAPE** — Symmetric MAPE *(robust alternative for near-zero values)*

Metrics were computed on the **same hourly test partition** to ensure fair comparison.

---

## 🟣 Final Results — Summary

From the final experiment results:

| Model                 | MAE               | RMSE     | Notes                           |
| --------------------- | ----------------- | -------- | ------------------------------- |
| **LSTM (24h window)** | ⭐ Lowest          | ⭐ Lowest | Best overall                    |
| Naive Forecast        | 2nd Best          | 2nd Best | Strong persistence baseline     |
| Moving Average Models | Higher error      | —        | Oversmoothing effect            |
| SARIMA                | Better than ARIMA | —        | Limited seasonal benefit        |
| ARIMA                 | Poor              | —        | Lacks seasonality               |
| Prophet               | Highest error     | —        | Over-smooths noisy load pattern |

### 🎯 Key Findings

* **LSTM achieved the best accuracy** across MAE, RMSE and sMAPE
* Naive persistence remained a **strong and competitive baseline**
* Moving Average degraded performance due to loss of local variation
* SARIMA improved ARIMA by modeling daily recurrence
* Prophet struggled with **volatile, appliance-driven usage patterns**

> Deep learning captured nonlinear and intra-day dynamics
> that classical models could not learn — while results also confirm
> that persistence behavior is dominant in short-term household load forecasting.

This dual outcome strengthens the reliability of the comparative analysis.

---

## 🧪 Experimental Environment

* Platform → **Google Colab**
* Language → **Python**
* Libraries
  `pandas`, `numpy`, `matplotlib`,
  `scikit-learn`, `statsmodels`,
  `prophet`, `tensorflow`

A `requirements.txt` file is provided for reproducibility.

---

## 🗂 Repository Structure (Suggested)

```
notebooks/
   01_hourly_naive_forecast_energy_consumption.ipynb
   02_hourly_moving_average_forecast_energy_consumption.ipynb
   03_hourly_arima_forecast_energy_consumption.ipynb
   04_hourly_sarima_forecast_energy_consumption.ipynb
   05_hourly_prophet_forecast_energy_consumption.ipynb
   06_hourly_lstm_forecast_energy_consumption.ipynb

data/
   raw/
   processed/

results/
   metrics/
   figures/
   comparison_tables/
```

This organization keeps experiments **modular, transparent, and reproducible**.

---

## 🙋 Author

**Dhanvan Venkatesh S**

---

## 📌 Future Work

Potential extensions include:

* GRU-based recurrent model
* CNN-LSTM hybrid architecture
* multi-feature forecasting using:

  * sub-metering values
  * voltage & current fields
* probabilistic forecasting
* multi-step ahead load prediction

---

## 🙏 Acknowledgement

Dataset courtesy of **UCI Machine Learning Repository**
Kaggle dataset mirror used for accessibility convenience.

---

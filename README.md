# Cinema Audience Attendance Forecasting

## Project Overview
Predicting cinema attendance is a complex time-series challenge where digital intent meets physical reality. This project builds a forecasting model to predict daily audience counts by integrating data from two distinct ecosystems:
* **BookNow:** An online booking aggregator (advance reservations).
* **CinePOS:** A theater-side Point-of-Sale system (walk-in sales).

By blending these sources, the model accounts for the shifting dynamics between online convenience and traditional on-site ticket purchasing.

---

## Dataset Structure
The project utilizes 8 distinct data sources to capture the full picture of theater traffic:

| File Name | Description |
| :--- | :--- |
| `booknow_booking.csv` | Historical online booking transactions. |
| `cinePOS_booking.csv` | Historical on-site (POS) ticket sales. |
| `booknow_visits.csv` | **Target Variable:** Actual daily audience counts. |
| `date_info.csv` | Calendar metadata (holidays, weekends, day of week). |
| `movie_theater_id_relation.csv` | Mapping between BookNow and CinePOS IDs. |
| `booknow_theaters.csv` | Metadata for online-listed theaters. |
| `cinePOS_theaters.csv` | Metadata for physical theater locations. |
| `sample_submission.csv` | Format for forecasting future attendance. |

---

## Tech Stack
* **Language:** Python 3.11+
* **Data Analysis:** pandas, numpy
* **Visualization:** matplotlib, seaborn
* **Machine Learning:** scikit-learn, XGBoost, LightGBM
* **Optimization:** Optuna (Hyperparameter tuning)

---

## The Pipeline

### 1. Data Integration and Cleaning
* Merged fragmented CSVs into a unified Master DataFrame.
* Handled missing values resulting from theater closures or platform-specific downtime.
* Synchronized IDs using the movie_theater_id_relation mapping.

### 2. Feature Engineering
* **Temporal Features:** Extracted day of the week, month, and year.
* **Categorical Encoding:** Applied LabelEncoder for theater types and locations.
* **External Factors:** Integrated holiday flags and weekend markers to capture attendance spikes.

### 3. Advanced Modeling
A comparison of multiple regression architectures was conducted to find the best fit for the time-series data:
* **Random Forest Regressor** (Baseline)
* **XGBoost** (Handling non-linearities)
* **LightGBM** (Efficiency on tabular data)

### 4. Hyperparameter Tuning
Automated search for optimal model parameters was performed using Optuna, focusing on maximizing the R² score and minimizing prediction error.

### 5. Future Scope
Genre Analysis: Incorporating movie metadata to see if "Blockbuster" weekends behave differently than "Indie" weeks.
Weather Integration: Adding regional weather data to account for rainy-day attendance boosts.
Lag Features: Implementing rolling averages of the previous 7 days to better capture momentum.

---

## Results
The final model effectively captures the correlation between advance online bookings and final headcount. The integration of "Online + POS" features significantly outperformed models relying on a single data source.

---

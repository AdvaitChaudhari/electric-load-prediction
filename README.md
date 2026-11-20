# Electric load forecasting – office floor

Hour-ahead forecast of the total electric load of one office floor, using the CU-BEMS dataset
(Chulalongkorn University, Bangkok: 1-minute AC, lighting and plug-load readings per zone, 2019, floor 6).

**Approach**
- sum all kW channels into a total floor load and resample to hourly
- features available at forecast time only: load lags (1, 2, 3, 24, 168 h), 24 h rolling mean, previous-hour temperature, hour, weekday
- chronological 80/20 split
- XGBoost, compared against two naive baselines (previous hour, same hour last week)

> **Fix vs. my first version:** the original notebook had the target column inside the feature set,
> which produced an R² of 0.99 that meant nothing. The current version only uses past information.

**Results (test period)**

| Model | MAE [kW] | RMSE [kW] | R² |
|---|---|---|---|
| Previous hour (naive) | 9.32 | 19.54 | 0.60 |
| Same hour last week (naive) | 4.50 | 11.72 | 0.86 |
| **XGBoost** | **1.98** | **4.48** | **0.98** |

XGBoost cuts the error by more than half compared with the best naive baseline. The previous-hour
baseline does badly because the office switches on and off in steps at the start and end of the day.
The hour-of-day feature lets the model anticipate those steps.

Data isn't committed because of its size. Put `2019Floor6.csv` or the course zip (`GroupF_Electric_Load_Data*.zip`) next to the notebook.

*University group project (Group F), M.Sc. Smart Energy Systems.*

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

_Results will be added after the next run. The notebook prints XGBoost against both baselines (MAE, RMSE, R²)._

Data isn't committed because of its size. Put `2019Floor6.csv` (or the course zip) next to the notebook.

*University group project (Group F), M.Sc. Smart Energy Systems.*

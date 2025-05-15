# ENFIELD-Hackathon

Octavian Manea, Lidia Manea, Stefan Saraev, Vlad Florea

Solutions are evaluated on prediction with the main metric being MAPE
We have firtly done an EDA with data cleaning and visualization. After that we tried some baseline models:
1) Naive Hourly Average: Predicts each hour using the average consumption for that hour from the known 2 months.
2) Hourly + Weekend/Weekday Average: Improves baseline by splitting averages by hour and weekend/weekday.
3) Prophet: Time series forecasting with daily, weekly, and yearly seasonality, trained on the 2 months of the new building.
4) Transfer Learning / Cross-Building: Trains models on all buildings except the target, then fine-tunes or predicts for the new building using its 2 months of data.
5) MICN, TimesNet: Sequence models trained on multiple buildings, fine-tuned on the new building's 2 months. These models can be found in the Time-Series-Library at https://github.com/thuml/Time-Series-Library

Table for MAPE:

Model / Approach              	MAPE (%)	                         Complexity
Naive Hourly Average	            6.80	            Very low: Simple mean by hour, no dependencies, instant computation
XGBoost (cross-building)	        6.94	            Moderate: Requires feature engineering (calendar, weather), fast training
XGBoost Forecast	                2.69	              Moderate: Same as above, but with more granular aggregation
with 6h Aggregation		                               Moderate: Requires data resampling, similar to above	
XGBoost Forecast	                3.08	            Moderate: Same as above, but with different aggregation window
with 12h Aggregation		                               Moderate: Requires data resampling, similar to above
Prophet	                          12.73             	Low: Easy to use, handles seasonality, slower for large data
MICN*	                            0.04	       High: Deep learning, needs GPU, pretraining and fine-tuning, complex pipeline
TimesNet*                       	0.05	           High: SOTA deep learning, cross-building pretraining, GPUrecommended

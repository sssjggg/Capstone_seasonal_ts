# Analysis and forecast multiseasonal time series

Final project at the Data Science Bootcamp at neuefische. This project has been developed in 4 weeks.

# Introduction
Especially for bakeries, whose products usually have a very short sales period of only one day, it is essential to predict the daily sales figures as accurately as possible. This is the only way to avoid overproduction, which means nothing other than financial losses, as well as unnecessary food waste, and at the same time to guarantee sufficiently full shelves for the customers until closing time.

Whereas in the past, when a baker usually ran his own bakery, it might have been sufficient to estimate the figures based on his own experience, this is no longer sufficient in today's bakeries, which are usually part of large chain stores.  At this point, data science can make a difference by not only helping the companies, but also by contributing a little to the reduction of food waste.

It is undeniable that sales figures are always influenced by external factors, such as the weather, holidays or even a pandemic, and should be included in the calculation. It is also undeniable that the prediction of seasonal products, due to their special data characteristics, is additionally a special challenge.

 However, the use of exogenous data is not part of this project, the aim here is to find out if models can be improved in a classical way, by including multiple seasonalities subject to the main seasonality.
For this purpose, a quite extensive EDA was made in Python, its findings applied to three ML models in R and integrated into the fbProphet.
The project is based on data from three seasonal products kindly provided by Meteolytix:
.

# Repro organization

+ [```EDA```](https://github.com/sssjggg/Capstone_seasonal_ts_/blob/main/EDA.ipynb): Analysis and visualisation of data and their characteristics, including: Stationarity; determination of seasonalities
+ [```R-Modelle```](https://github.com/sssjggg/Capstone_seasonal_ts_/blob/main/R_models.ipynb): Seasonal naïve, ARIMA, TBATS; with ts, msts objects and dummy regressors.
+ [```Prophet```](https://github.com/sssjggg/Capstone_seasonal_ts_/blob/main/Prophet.ipynb): Standard model and model with multiple saiosonalities
+ [```Presentation```](https://github.com/sssjggg/Capstone_seasonal_ts/blob/main/Presentation.pdf)

# Environment set up

pyenv local 3.8.5
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements_.txt
# Summary of the characteristics found in the EDA 

Before choosing a model, it is advisable to summarise the characteristics of the ts, because many models make certain assumptions about their characteristics, i.e. not every model is suitable for all ts.

| characteristic | article one | article two | article three | |
| :--- | :--- | :--- | :--- | :---: |
| univariate | y | y | y | - |
| NaNs | n | n | n | - |
| duplicates | n | n | n | - |
| continuous | n | n | n | possible interpolation |
| intermittent | n | n | n | - |
| stationarity | n | y | y | article one: difference stationarity needs one differencing |
| trend | n | n | n | - |
| multisaisonality* | y | y | y | further decomposition |
| normally distributed | y | n | n | possible logarithmization |

*Seasonalities found article one: 
  + from the plots: 5 (monthly sales), 18 (weekly sales), 7 (weekdays), 365 (simple decomposition)
  + additionally periodogram: 100 (100.11; number of data points per year), 77, 43.5
  + additionally suspected: 53 (number of weeks per year)

![Title Image](https://github.com/sssjggg/Capstone_seasonal_ts_/blob/main/images/R_decompose_msts.png)
# Model results

![Title Image](https://github.com/sssjggg/Capstone_seasonal_ts_/blob/main/images/R_compare_all.png)

# Future work

+ Automate frequency search for seasonalities
+ Repeat for items 2 & 3
+ Hyperparameter search + cross-validation fbprophet

#### This project demonstrates time series forecasting on the classic AirPassengers dataset using both ARIMA and SARIMA models.

#### The dataset contains monthly totals of international airline passengers from 1949 to 1960. The project workflow includes:

- Data visualization and exploration

- Stationarity checks with ADF test

- Differencing to remove trend and seasonality

- Identification of ARIMA (p,d,q) and SARIMA (p,d,q)(P,D,Q,s) parameters using ACF and PACF

- Model fitting for both ARIMA and SARIMA

- Residual analysis to validate models

- Forecasting future passenger numbers

### Dataset

The project uses the AirPassengers dataset from the statsmodels library:

```
import statsmodels.api as sm
data = sm.datasets.get_rdataset("AirPassengers").data
```

-Columns:
-- time: Year (as float)
-- value: Number of passengers
-- Converted to a datetime index for time series operations.

### Methodology

#### 1. ARIMA Model
1. **Visualize the time series** to understand trends and patterns.  
2. **Check stationarity** using the Augmented Dickey-Fuller (ADF) test.  
3. **Apply non-seasonal differencing** (`d`) to remove trend and achieve stationarity.  
4. **Identify ARIMA parameters** `(p,d,q)` using ACF and PACF plots:
   - PACF spikes - AR order `p`  
   - ACF spikes - MA order `q`  
5. **Fit the ARIMA model** with the selected `(p,d,q)` parameters.  
6. **Analyze residuals** to ensure they behave like white noise.  
7. **Forecast future values** (e.g., next 24 months) and visualize predictions.  

#### 2. SARIMA Model
1. **Apply seasonal differencing** (`D`) with period `s` (12 months) to remove seasonality.  
2. **Check stationarity** after seasonal differencing; apply non-seasonal differencing (`d`) if needed.  
3. **Identify SARIMA parameters** `(P,D,Q)` for seasonal AR, differencing, and MA using ACF and PACF of the seasonally differenced series.  
4. **Fit the SARIMA model** `(p,d,q)(P,D,Q,s)` combining non-seasonal and seasonal components.  
5. **Analyze residuals** to ensure no remaining patterns exist.  
6. **Forecast future values** and plot predictions with confidence intervals.  

##### Notes
- SARIMA is especially useful for **seasonal datasets**, like monthly AirPassengers data.  
- ARIMA may work for **non-seasonal patterns**, but often underperforms when seasonality is strong.  

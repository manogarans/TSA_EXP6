# Ex.No: 6               HOLT WINTERS METHOD
### Date: 24.03.2026



### AIM
To implement the Holt-Winters (Triple Exponential Smoothing) Model in Python to perform time series decomposition, evaluate model performance using RMSE, and generate future stock price forecasts for the Apple dataset.

### ALGORITHM:
1. You import the necessary libraries
2. You load a CSV file containing daily sales data into a DataFrame, parse the 'date' column as
datetime, and perform some initial data exploration
3. You group the data by date and resample it to a monthly frequency (beginning of the month
4. You plot the time series data
5. You import the necessary 'statsmodels' libraries for time series analysis
6. You decompose the time series data into its additive components and plot them:
7. You calculate the root mean squared error (RMSE) to evaluate the model's performance
8. You calculate the mean and standard deviation of the entire sales dataset, then fit a Holt-
Winters model to the entire dataset and make future predictions
9. You plot the original sales data and the predictions
### PROGRAM:
## TEST_PREDICTION :
```
import pandas as pd
import matplotlib.pyplot as plt
import os

# Load Data
file_path = '/aapl_master_enriched.csv' if os.path.exists('/aapl_master_enriched.csv') else 'aapl_master_enriched.csv'
df = pd.read_csv(file_path)

# Parse 'date' and initial exploration
df['date'] = pd.to_datetime(df['date'])
df.set_index('date', inplace=True)

# Resample to monthly frequency (Month Begin)
monthly_data = df['close'].resample('MS').mean()

# Plot the time series
plt.figure(figsize=(12, 6))
plt.plot(monthly_data, label='Monthly Average Close Price', color='blue')
plt.title('Apple Stock Price: Monthly Time Series Data')
plt.xlabel('Date')
plt.ylabel('Price ($)')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()

print("Initial Monthly Data (First 5 Rows):")
print(monthly_data.head())
```
## FINAL_PREDICTION :
```
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
import os

# Load and Resample
file_path = '/aapl_master_enriched.csv' if os.path.exists('/aapl_master_enriched.csv') else 'aapl_master_enriched.csv'
df = pd.read_csv(file_path, index_col='date', parse_dates=True)
monthly_data = df['close'].resample('MS').mean()

# Decompose the time series (Additive model)
decomposition = seasonal_decompose(monthly_data, model='additive', period=12)

# Plot components
fig = decomposition.plot()
fig.set_size_inches(12, 8)
plt.suptitle('Apple Stock Price: Seasonal Decomposition (Trend, Seasonality, Residuals)', fontsize=14)
plt.tight_layout(rect=[0, 0.03, 1, 0.95])
plt.show()
```

### OUTPUT:
<img width="1099" height="743" alt="image" src="https://github.com/user-attachments/assets/caa3ad3e-da5a-40d4-a70c-fdb3679baed0" />
<img width="1289" height="828" alt="image" src="https://github.com/user-attachments/assets/8638a246-ecb4-40a1-97a9-77c940b34472" />


### RESULT:
Thus the program run successfully based on the Holt Winters Method model.

# DEVELOPED BY : SHALINI K
# REGISTER NUMBER : 212222240095

# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on bitcoin dataset
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```PY
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
%matplotlib inline

df = pd.read_csv("coin_Bitcoin.csv")
df['Date'] = pd.to_datetime(df['Date'])
df.set_index('Date', inplace=True)
print(df.head())

df['Close'].plot(title='Bitcoin Closing Price', figsize=(10, 6))
plt.show()
def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)

# Perform the ADF test on the 'Close' price
adf_test(df['Close'])

# First difference to remove trend
df['Close_diff'] = df['Close'] - df['Close'].shift(1)
df['Close_diff'].dropna().plot(title='Differenced Bitcoin Closing Price', figsize=(10, 6))
plt.show()

# Seasonal differencing (replace 'n' with the appropriate lag value)
n = 7  # Example: weekly seasonality
df['Close_seasonal_diff'] = df['Close'] - df['Close'].shift(n)
df['Close_seasonal_diff'].dropna().plot(title='Seasonally Differenced Bitcoin Closing Price', figsize=(10, 6))
plt.show()

# Log transformation
df['Close_log'] = np.log(df['Close'])
df['Close_log_diff'] = df['Close_log'] - df['Close_log'].shift(1)
df['Close_log_diff'].dropna().plot(title='Log Differenced Bitcoin Closing Price', figsize=(10, 6))
plt.show()

# Analyze the whole dataset, apply transformations, and visualize as needed
df['Close'].plot(title='Bitcoin Closing Price (Full Data)', figsize=(10, 6))
plt.show()

# Apply ADF test, differencing, and logging to other columns if necessary
# Example for 'High' column:
adf_test(df['High'])

df['High_diff'] = df['High'] - df['High'].shift(1)
df['High_diff'].dropna().plot(title='Differenced Bitcoin High Price', figsize=(10, 6))
plt.show()

df['High_log'] = np.log(df['High'])
df['High_log_diff'] = df['High_log'] - df['High_log'].shift(1)
df['High_log_diff'].dropna().plot(title='Log Differenced Bitcoin High Price', figsize=(10, 6))
plt.show()

```


### OUTPUT:


REGULAR DIFFERENCING:


SEASONAL ADJUSTMENT:


LOG TRANSFORMATION:



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.

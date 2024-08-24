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
```

# REGULAR DIFFERENCING:
```py
df['Close_diff'] = df['Close'] - df['Close'].shift(1)
df['Close_diff'].dropna().plot(title='Differenced Bitcoin Closing Price', figsize=(10, 6))
plt.show()
```
# SEASONAL ADJUSTMENT:
```py
# Define the lag for seasonal differencing (e.g., 1 for daily data)
n = 1  # Adjust as necessary for your data's seasonality
df['Close_seasonal_diff'] = df['Close'] - df['Close'].shift(n)
df['Close_seasonal_diff'].dropna().plot(title='Seasonally Differenced Bitcoin Closing Price', figsize=(10, 6))
plt.show()
```
# LOG TRANSFORMATION:
```py
# Apply log transformation
df['Close_log'] = np.log(df['Close'])
df['Close_log_diff'] = df['Close_log'] - df['Close_log'].shift(1)
df['Close_log_diff'].dropna().plot(title='Log Differenced Bitcoin Closing Price', figsize=(10, 6))
plt.show()
```

### OUTPUT:
<div><img height=20% width=30% src="https://github.com/user-attachments/assets/a388172b-de2b-4c09-9a19-93491e27ca23">
<img height=20% width=30% src="https://github.com/user-attachments/assets/426b00e1-02d2-4faf-b8b9-777129752b42">
<img height=20% width=30% src="https://github.com/user-attachments/assets/2df304d3-db49-4fdc-89b3-943b42f1007a"></div>


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on bitcoin dataset.

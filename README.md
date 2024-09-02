# NAME: SANTHANA LAKSHMI K
# REGISTER NO 212222240091

# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
   
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
%matplotlib inline

train = pd.read_csv("/content/powerconsumption.csv (2).zip")

train['Datetime'] = pd.to_datetime(train['Datetime'], format='%m/%d/%Y %H:%M')
train.set_index('Datetime', inplace=True)
train.head()
train['PowerConsumption_Zone1'].plot(title='Power Consumption - Zone 1')

def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)
adf_test(train['PowerConsumption_Zone1'])
```
# REGULAR DIFFERENCING:
```
train['PowerConsumption_Zone1_diff'] = train['PowerConsumption_Zone1'] - train['PowerConsumption_Zone1'].shift(1)
train['PowerConsumption_Zone1_diff'].dropna().plot(title='Differenced Power Consumption - Zone 1')

```
# SEASONAL ADJUSTMENT:
```
train['PowerConsumption_Zone1_seasonal_diff'] = train['PowerConsumption_Zone1'] - train['PowerConsumption_Zone1'].shift(n)
train['PowerConsumption_Zone1_seasonal_diff'].dropna().plot(title='Seasonally Differenced Power Consumption - Zone 1')

```
# LOG TRANSFORMATION:
```
train['PowerConsumption_Zone1_log'] = np.log(train['PowerConsumption_Zone1'])
train['PowerConsumption_Zone1_log_diff'] = train['PowerConsumption_Zone1_log'] - train['PowerConsumption_Zone1_log'].shift(1)
train['PowerConsumption_Zone1_log_diff'].dropna().plot(title='Log Differenced Power Consumption - Zone 1')

```
### OUTPUT:

![image](https://github.com/user-attachments/assets/9aa36e4c-ba39-4241-bf70-929fbfbe0410)

![image](https://github.com/user-attachments/assets/cb4bab01-e48f-4ab6-9273-554d67f3ffc4)

# REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/14f17d50-2849-4d93-a4c1-ee02efb5a2aa)

# SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/a0fe3e0f-f0b1-4510-8fc5-44f9831b15cd)


# LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/be6cf5b1-93b8-49b0-b83b-203115025e4b)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.

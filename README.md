# Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Developed by : Vedagiri Indu Sree
# Date:19/08/2025 

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

from statsmodels.tsa.seasonal import seasonal_decompose

data=pd.read_csv('AirPassengers.csv')

data.head()

data['Month']=pd.to_datetime(data['Month']) #data=pd.read_csv("/content/AirPassengers.csv",parse_dates=

data.set_index('Month', inplace=True)

data['passengers_diff']=data['#Passengers']-data['#Passengers'].shift(1)

result = seasonal_decompose(data['#Passengers'], model='additive', period=12)

data['passengers_sea_diff']=result.resid

data['passengers_log'] = np.log(data['#Passengers'])

data['passengers_log_diff']=data['passengers_log']-data['passengers_log'].shift(1)

result = seasonal_decompose (data['passengers_log_diff'].dropna(), model='additive', period=12)

data['passengers_log_seasonal_diff']=result.resid

plt.figure(figsize=(12, 20))

plt.subplot(6, 1, 1)

plt.plot(data['#Passengers'], label='Original')

plt.legend(loc='best')

plt.title('Original Data')

plt.xlabel('Year')

plt.ylabel('No of passengers')
```
```
import matplotlib.pyplot as plt

plt.figure(figsize=(12, 20))   

plt.subplot(6, 1, 2)
plt.plot(data['passengers_diff'], label='Regular Difference')

plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced No of passengers')

plt.show()
```
```
import matplotlib.pyplot as plt

plt.figure(figsize=(12, 18))   

plt.subplot(6, 1, 3)
plt.plot(data['passengers_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally adjusted No of passengers')
```
```
plt.figure(figsize=(12, 18)) 
plt.subplot(6, 1, 4)
plt.plot(data['passengers_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log (No of passengers)')
```
```
plt.figure(figsize=(12, 20)) 
plt.subplot(6, 1, 5)
plt.plot(data['passengers_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Log (No of passengers)')
```
```
plt.figure(figsize=(12, 20)) 
plt.subplot(6, 1, 6)
plt.plot(data['passengers_log_seasonal_diff'], 
         label='Log Transformation + Regular Differencing + Seasonal Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Regular & Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff (RDiff (Log (No of passengers)))')

plt.tight_layout()
plt.show()
```
### OUTPUT:

### ORIGINAL:
<img width="1248" height="433" alt="image" src="https://github.com/user-attachments/assets/db82cc7e-1f5a-490e-9707-435bc1a515dd" />

### REGULAR DIFFERENCING:
<img width="1266" height="382" alt="image" src="https://github.com/user-attachments/assets/ad9130e7-6536-4437-a270-289ce8e7c1af" />

### SEASONAL ADJUSTMENT:
<img width="1252" height="398" alt="image" src="https://github.com/user-attachments/assets/76dca096-5c4c-48ee-b2b6-085ca8d46c69" />

### LOG TRANSFORMATION:
<img width="1255" height="405" alt="image" src="https://github.com/user-attachments/assets/01cf9f32-2ca5-4fba-81a1-abb9cfaab4b4" />

### Log Transformation and Regular Differencing:
<img width="1247" height="422" alt="image" src="https://github.com/user-attachments/assets/d6e9cdc0-d83f-4d67-aed5-7b44c6a4377b" />

### Log Transformation + Regular & Seasonal Differencing:
<img width="1245" height="403" alt="image" src="https://github.com/user-attachments/assets/e5151dc1-4689-4d34-be29-b0448bfcbf9e" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.

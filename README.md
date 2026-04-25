# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 25/04/26

### AIM:
To perform regular differncing,seasonal adjustment and log transformation on international airline passenger data

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.


### PROGRAM:
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose



data = pd.read_csv('/content/AirPassengers.csv', parse_dates=['Month'])
data.set_index('Month', inplace=True)


data['passengers_diff'] = data['#Passengers'].diff()
data['passengers_log'] = np.log(data['#Passengers'])
data['passengers_log_diff'] = data['passengers_log'].diff()

data['passengers_sea_diff'] = seasonal_decompose(
    data['#Passengers'], model='additive', period=12
).resid

data['passengers_log_seasonal_diff'] = seasonal_decompose(
    data['passengers_log_diff'].dropna(), model='additive', period=12
).resid


plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 2)
plt.plot(data['passengers_diff'], label='Regular Difference')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced No of passengers')
plt.legend()

plt.subplot(6, 1, 3)
plt.plot(data['passengers_sea_diff'], label='Seasonal Adjustment')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally adjusted No of passengers')
plt.legend()

plt.subplot(6, 1, 4)
plt.plot(data['passengers_log'], label='Log Transformation')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(No of passengers)')
plt.legend()

plt.tight_layout()
plt.show()
```

### OUTPUT:


REGULAR DIFFERENCING:

<img width="824" height="142" alt="Screen Shot 2026-04-25 at 09 25 14" src="https://github.com/user-attachments/assets/dbe5b547-5480-4a13-8363-20132a6503d1" />



SEASONAL ADJUSTMENT:
<img width="819" height="147" alt="Screen Shot 2026-04-25 at 09 25 33" src="https://github.com/user-attachments/assets/ab1a5a58-a691-4038-bed2-588efe11bb8b" />

LOG TRANSFORMATION:

<img width="811" height="138" alt="Screen Shot 2026-04-25 at 09 25 52" src="https://github.com/user-attachments/assets/35829d6b-50df-4197-8405-d2924f3fb151" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.

# Temperature over time
<img width="max" alt="Screenshot 2023-12-22 at 0 59 13 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/56ccfa76-cf5c-4abb-af70-0b00215d4bc1">

```.py
import matplotlib.pyplot as plt
import pandas as pd

# Load the data from the CSV file
file_path = 'formatted_data.csv'
data = pd.read_csv(file_path)

data.columns = ['Date', 'Time', 'Room Humidity 1', 'Room Temperature 1',
                'Room Humidity 2', 'Room Temperature 2', 'Room Humidity 3', 'Room Temperature 3']

temperature_types = ['Room Temperature 1', 'Room Temperature 2', 'Room Temperature 3']

humidity_summary = data[['Room Humidity 1', 'Room Humidity 2', 'Room Humidity 3']].describe()

import matplotlib.dates as mdates

data['Datetime'] = pd.to_datetime(data['Date'] + ' ' + data['Time'])

plt.figure(figsize=(15, 6))

plt.plot(data['Datetime'], data['Room Temperature 1'], label='Room Temperature 1', color='orange')

plt.plot(data['Datetime'], data['Room Temperature 2'], label='Room Temperature 2', color='purple')

plt.plot(data['Datetime'], data['Room Temperature 3'], label='Room Temperature 3', color='brown')

plt.ylim(data[temperature_types].min().min(), data[temperature_types].max().max())

plt.xlabel('Date and Time')
plt.ylabel('Temperature (°C)')
plt.title('Temperature Over Time')
plt.legend()
plt.grid(True)

plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
plt.gcf().autofmt_xdate()

plt.show()
```

# Smoothed temperature
<img width="max" alt="Screenshot 2023-12-22 at 1 00 03 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/5ee074f8-dc18-4f24-8eb2-051e8d52b93e">

```.py
import matplotlib.pyplot as plt
import pandas as pd
import matplotlib.dates as mdates

# Load the data from the CSV file
file_path = 'formatted_data.csv'
data = pd.read_csv(file_path)

data.columns = ['Date', 'Time', 'Room Humidity 1', 'Room Temperature 1',
                'Room Humidity 2', 'Room Temperature 2', 'Room Humidity 3', 'Room Temperature 3']

temperature_types = ['Room Temperature 1', 'Room Temperature 2', 'Room Temperature 3']

data['Datetime'] = pd.to_datetime(data['Date'] + ' ' + data['Time'])

fig, ax = plt.subplots(figsize=(15, 6))

# Specify colors for each line
line_colors = ['orange', 'purple', 'brown']

for i, temperature_type in enumerate(temperature_types):
    # Smooth temperature using a rolling window with a mean
    smoothed_temperature = data[temperature_type].rolling(window=10, min_periods=1).mean()
    ax.plot(data['Datetime'], smoothed_temperature, label=temperature_type, color=line_colors[i])

ax.set_ylim(data[temperature_types].min().min(), data[temperature_types].max().max())
ax.set_xlabel('Date and Time')
ax.set_ylabel('Temperature (°C)')
ax.set_title('Smoothing temperature')
ax.legend()
ax.grid(True)

ax.xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
ax.xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

plt.show()
```

# Linear and temperature
<img width="max" alt="Screenshot 2023-12-22 at 1 01 27 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/51c92717-83e5-4a90-965c-e362d519f5a0">

```.py
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
import numpy as np
import matplotlib.dates as mdates

def linear_regression(x, y):
    n = len(x)
    slope = (n * np.sum(x * y) - np.sum(x) * np.sum(y)) / (n * np.sum(x**2) - (np.sum(x))**2)
    intercept = (np.sum(y) - slope * np.sum(x)) / n
    return slope, intercept

file_path = 'formatted_data.csv'
data = pd.read_csv(file_path)

data.columns = ['Date', 'Time', 'Room Humidity 1', 'Room Temperature 1',
                'Room Humidity 2', 'Room Temperature 2', 'Room Humidity 3', 'Room Temperature 3']

temperature_summary = data[['Room Temperature 1', 'Room Temperature 2', 'Room Temperature 3']].describe()

data['Datetime'] = pd.to_datetime(data['Date'] + ' ' + data['Time'])

temperature_types = ['Room Temperature 1', 'Room Temperature 2', 'Room Temperature 3']
colors = ['orange', 'purple', 'brown']

data['DatetimeNumeric'] = data['Datetime'].astype(int) / 10**9

plt.figure(figsize=(15, 6))

for temp_type, color in zip(temperature_types, colors):
    x = data['DatetimeNumeric'].values
    y = data[temp_type].values

    slope, intercept = linear_regression(x, y)

    y_pred = slope * x + intercept

    future_timestamps = np.arange(x[-1], x[-1] + 12 * 3600, 3600)
    future_y_pred = slope * future_timestamps + intercept

    sns.lineplot(x=data['Datetime'], y=data[temp_type], label=f'{temp_type}', color=color)
    plt.plot(data['Datetime'], y_pred, label=f'Linear Model {temp_type}', linestyle='--', color=color)
    plt.plot(pd.to_datetime(future_timestamps, unit='s'), future_y_pred, label=f'Future Prediction {temp_type}', linestyle=':', color=color)
    plt.ylim(data[temperature_types].min().min(), data[temperature_types].max().max())

plt.xlabel('Date and Time')
plt.ylabel('Temperature (°C)')
plt.title('Temperature and Linear Model Over Time with Future Prediction')
plt.legend(bbox_to_anchor=(0.7, 1), loc='upper center', ncol=2)
plt.grid(True)

plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
plt.gcf().autofmt_xdate()

plt.show()
```

# Quadratic and temperature
<img width="max" alt="Screenshot 2023-12-22 at 1 02 06 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/9e895ad9-08a5-495a-b839-565e47e071b4">

```.py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.dates as mdates
import datetime
from numpy.polynomial.polynomial import Polynomial

data = pd.read_csv('formatted_data.csv')

data.columns = ['Date', 'Time', 'Room Humidity 1', 'Room Temperature 1',
                'Room Humidity 2', 'Room Temperature 2', 'Room Humidity 3', 'Room Temperature 3']
data['Datetime'] = pd.to_datetime(data['Date'] + ' ' + data['Time'])
data['Timestamp'] = data['Datetime'].apply(lambda x: x.timestamp())

def fit_and_predict_quadratic(X, y):
    coefs = Polynomial.fit(X, y, 2).convert().coef
    predictions = coefs[0] + coefs[1] * X + coefs[2] * X ** 2
    return predictions, coefs

last_timestamp = data['Timestamp'].iloc[-1]
last_datetime = data['Datetime'].iloc[-1]
one_hour = 3600
future_timestamps = np.array([last_timestamp + (i * one_hour) for i in range(1, 13)])
future_datetimes = [last_datetime + datetime.timedelta(hours=i) for i in range(1, 13)]

plt.figure(figsize=(15, 6))
colors = ['orange', 'purple', 'brown']

for i, column in enumerate(['Room Temperature 1', 'Room Temperature 2', 'Room Temperature 3']):
    X = data['Timestamp']
    y = data[column]
    predictions, coefs = fit_and_predict_quadratic(X, y)
    plt.plot(y, label=f'Original {column}', color=colors[i])
    plt.plot(data['Datetime'], predictions, label=f'Quadratic Fit for {column}', linestyle='--', color=colors[i])
    future_predictions = coefs[0] + coefs[1] * future_timestamps + coefs[2] * future_timestamps ** 2
    plt.plot(future_datetimes, future_predictions, label=f'12h Prediction for {column}', linestyle=':', color=colors[i])

plt.gca().xaxis.set_major_locator(mdates.HourLocator(interval=6))
plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
plt.xlim(data['Datetime'].min(), future_datetimes[-1])
plt.xlabel('Date and Time')
plt.ylabel('Temperature (°C)')
plt.title('Temperature Over Time with Quadratic Fits and Consecutive 12-Hour Predictions')
plt.legend(bbox_to_anchor=(0.4,1), loc="upper left", ncol=2)
plt.grid(True)
plt.gcf().autofmt_xdate()
plt.show()
```

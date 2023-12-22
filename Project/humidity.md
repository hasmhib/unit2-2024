# Humidity over time
<img width="max" alt="Screenshot 2023-12-22 at 0 53 54 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/39783ac3-7ca3-4db5-bf83-56d346247f44">

```.py
import matplotlib.pyplot as plt
import pandas as pd

# Load the data from the CSV file
file_path = 'formatted_data.csv'
data = pd.read_csv(file_path)

data.columns = ['Date', 'Time', 'Room Humidity 1', 'Room Temperature 1',
                'Room Humidity 2', 'Room Temperature 2', 'Room Humidity 3', 'Room Temperature 3']

humidity_summary = data[['Room Humidity 1', 'Room Humidity 2', 'Room Humidity 3']].describe()

humidity_types = ['Room Humidity 1', 'Room Humidity 2', 'Room Humidity 3']
import matplotlib.dates as mdates

data['Datetime'] = pd.to_datetime(data['Date'] + ' ' + data['Time'])

plt.figure(figsize=(15, 6))

plt.plot(data['Datetime'], data['Room Humidity 1'], label='Room Humidity 1', color='blue')

plt.plot(data['Datetime'], data['Room Humidity 2'], label='Room Humidity 2', color='green')

plt.plot(data['Datetime'], data['Room Humidity 3'], label='Room Humidity 3', color='red')

plt.ylim(15, data[humidity_types].max().max())

plt.xlabel('Date and Time')
plt.ylabel('Humidity (%)')
plt.title('Humidity Over Time')
plt.legend()
plt.grid(True)

plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
plt.gcf().autofmt_xdate()

plt.show()
```

# Smoothed humidity
<img width="max" alt="Screenshot 2023-12-22 at 0 57 32 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/8b175df4-1642-4f95-aaac-7706bb8807f2">

```.py
import matplotlib.pyplot as plt
import pandas as pd
import matplotlib.dates as mdates

# Load the data from the CSV file
file_path = 'formatted_data.csv'
data = pd.read_csv(file_path)

data.columns = ['Date', 'Time', 'Room Humidity 1', 'Room Temperature 1',
                'Room Humidity 2', 'Room Temperature 2', 'Room Humidity 3', 'Room Temperature 3']

humidity_types = ['Room Humidity 1', 'Room Humidity 2', 'Room Humidity 3']

data['Datetime'] = pd.to_datetime(data['Date'] + ' ' + data['Time'])

fig, ax = plt.subplots(figsize=(15, 6))

# Specify colors for each line
line_colors = ['blue', 'green', 'red']

for i, humidity_type in enumerate(humidity_types):
    # Smooth temperature using a rolling window with a mean
    smoothed_humidity = data[humidity_type].rolling(window=10, min_periods=1).mean()
    ax.plot(data['Datetime'], smoothed_humidity, label=humidity_type, color=line_colors[i])

ax.set_ylim(data[humidity_types].min().min(), data[humidity_types].max().max())
ax.set_xlabel('Date and Time')
ax.set_ylabel('Humidity (°C)')
ax.set_title('Smoothed Humidity')
ax.legend()
ax.grid(True)

plt.ylim(15, data[humidity_types].max().max())
ax.xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
ax.xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

plt.show()
```

# Linear and humidity
<img width="max" alt="Screenshot 2023-12-22 at 0 55 11 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/cbfb056f-e0cf-4cf1-8a50-21c74f5e66d3">

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

humidity_types = ['Room Humidity 1', 'Room Humidity 2', 'Room Humidity 3']

data['Datetime'] = pd.to_datetime(data['Date'] + ' ' + data['Time'])

fig, ax = plt.subplots(figsize=(15, 6))

# Specify colors for each line
line_colors = ['blue', 'green', 'red']

for i, humidity_type in enumerate(humidity_types): # enumerate means
    smoothed_humidity = data[humidity_type].rolling(window=10, min_periods=1).mean()
    ax.plot(data['Datetime'], smoothed_humidity, label=humidity_type, color=line_colors[i])

ax.set_ylim(data[humidity_types].min().min(), data[humidity_types].max().max())
ax.set_xlabel('Date and Time')
ax.set_ylabel('Humidity (°C)')
ax.set_title('Smoothed Humidity')
ax.legend()
ax.grid(True)

plt.ylim(15, data[humidity_types].max().max())
ax.xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
ax.xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

plt.show()
colors_humidity = ['blue', 'green', 'red']

data['DatetimeNumeric'] = data['Datetime'].astype(int) / 10**9

plt.figure(figsize=(15, 6))

for temp_type, color in zip(humidity_types, colors_humidity):
    x = data['DatetimeNumeric'].values
    y = data[temp_type].values

    slope, intercept = linear_regression(x, y)

    y_pred = slope * x + intercept

    future_timestamps = np.arange(x[-1], x[-1] + 12 * 3600, 3600)
    future_y_pred = slope * future_timestamps + intercept

    sns.lineplot(x=data['Datetime'], y=data[temp_type], label=f'{temp_type}', color=color)
    plt.plot(data['Datetime'], y_pred, label=f'Linear Model {temp_type}', linestyle='--', color=color)
    plt.plot(pd.to_datetime(future_timestamps, unit='s'), future_y_pred, label=f'Future Prediction {temp_type}', linestyle=':', color=color)
    plt.ylim(15, data[humidity_types].max().max())

plt.xlabel('Date and Time')
plt.ylabel('Humidity (%)')
plt.title('Humidity and Linear Model Over Time with Future Prediction')
plt.legend()
plt.grid(True)

plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
plt.gcf().autofmt_xdate()

plt.show()
```

# Quadartic and humidity
<img width="max" alt="Screenshot 2023-12-22 at 0 56 28 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/6f29e6a9-5f46-45ba-84f5-dbb3d5145f22">

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

def fit_and_predict_quadratic(X, y, future_X):
    coefs = Polynomial.fit(X, y, 2).convert().coef
    predictions = coefs[0] + coefs[1] * X + coefs[2] * X ** 2
    future_predictions = coefs[0] + coefs[1] * future_X + coefs[2] * future_X ** 2
    return predictions, future_predictions

last_timestamp = data['Timestamp'].iloc[-1]
last_datetime = data['Datetime'].iloc[-1]
one_hour = 3600
future_timestamps = np.array([last_timestamp + (i * one_hour) for i in range(1, 13)])
future_datetimes = [last_datetime + datetime.timedelta(hours=i) for i in range(1, 13)]

plt.figure(figsize=(15, 6))
colors = ['blue', 'green', 'red']

for i, column in enumerate(['Room Humidity 1', 'Room Humidity 2', 'Room Humidity 3']):
    X = data['Timestamp']
    y = data[column]
    predictions, future_predictions = fit_and_predict_quadratic(X, y, future_timestamps)

    plt.plot(data['Datetime'], y, label=f'Original {column}', color=colors[i])
    plt.plot(data['Datetime'], predictions, label=f'Quadratic Fit for {column}', linestyle='--', color=colors[i])
    plt.plot(future_datetimes, future_predictions, label=f'12h Prediction for {column}', linestyle=':', color=colors[i])

plt.gca().xaxis.set_major_locator(mdates.HourLocator(interval=6))
plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))

plt.xlim(data['Datetime'].min(), future_datetimes[-1])
plt.xlabel('Date and Time')
plt.ylabel('Humidity (%)')
plt.title('Humidity Over Time with Quadratic Fits and Consecutive 12-Hour Predictions')
plt.legend(bbox_to_anchor=(0.7, 1), loc='upper center', ncol=2)
plt.grid(True)
plt.gcf().autofmt_xdate()
plt.show()
```

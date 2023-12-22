# Analysis of humidy and temperature over time
<img width="max" alt="Screenshot 2023-12-22 at 0 48 22 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/c79e2396-d023-4f5a-88d7-4b038131237f">

# Standard Deviation of humidity and temperature over time
<img width="max" alt="Screenshot 2023-12-22 at 0 48 55 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/fb3944df-3b4e-492b-8233-aaaf185eefea">

```.py
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.gridspec import GridSpec
import pandas as pd
import matplotlib.dates as mdates

file_path = 'formatted_data.csv'
data = pd.read_csv(file_path)

data.columns = ['Date', 'Time', 'Room Humidity 1', 'Room Temperature 1',
                'Room Humidity 2', 'Room Temperature 2', 'Room Humidity 3', 'Room Temperature 3']

humidity_types = ['Room Humidity 1', 'Room Humidity 2', 'Room Humidity 3']
temperature_types = ['Room Temperature 1', 'Room Temperature 2', 'Room Temperature 3']

x_values = np.arange(len(data['Room Humidity 1']))

data['Datetime'] = pd.to_datetime(data['Date'] + ' ' + data['Time'])
data['DatetimeNumeric'] = data['Datetime'].astype(int) / 10**9

# Create a figure with a grid layout
fig = plt.figure(figsize=(12, 10))
gs = GridSpec(2, 1, height_ratios=[1, 1], hspace=0.3)
plt.subplots_adjust(hspace=2)

# Subplot 1: Humidity
ax1 = fig.add_subplot(gs[0])
mean_values = data[humidity_types].mean(axis=1)
std_values = data[humidity_types].std(axis=1)
max_values = data[humidity_types].max(axis=1)
min_values = data[humidity_types].min(axis=1)
median_values = data[humidity_types].median(axis=1)

ax1.plot(data['Datetime'], mean_values, 'r-', label='Mean')
ax1.fill_between(data['Datetime'], min_values, max_values, color='lightblue', alpha=0.5, label='Range')
ax1.plot(data['Datetime'], max_values, 'blue', label='Maximum')
ax1.plot(data['Datetime'], min_values, 'yellow', label='Minimum')
ax1.plot(data['Datetime'], median_values, 'black', label='Median')
#ax1.errorbar(data['Datetime'], mean_values, std_values, fmt='o-', color='green', label='Standard Deviation', alpha=0.5)
ax1.set_ylim(0, data[humidity_types].max().max())
ax1.set_ylabel('Humidity (%)')
ax1.legend()
ax1.grid(True)
ax1.set_title('Analysis for Humidity over time')
ax1.xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
ax1.xaxis.set_major_locator(mdates.AutoDateLocator())
plt.setp(ax1.get_xticklabels(), rotation=30, ha='right')  # Adjust rotation for better readability

# Subplot 2: Temperature
ax2 = fig.add_subplot(gs[1])
mean_values_temp = data[temperature_types].mean(axis=1)
std_values_temp = data[temperature_types].std(axis=1)
max_values_temp = data[temperature_types].max(axis=1)
min_values_temp = data[temperature_types].min(axis=1)
median_values_temp = data[temperature_types].median(axis=1)

ax2.plot(data['Datetime'], mean_values_temp, 'r-', label='Mean')
ax2.fill_between(data['Datetime'], min_values_temp, max_values_temp, color='lightcoral', alpha=0.5, label='Range')
ax2.plot(data['Datetime'], max_values_temp, 'blue', label='Maximum')
ax2.plot(data['Datetime'], min_values_temp, 'yellow', label='Minimum')
ax2.plot(data['Datetime'], median_values_temp, 'black', label='Median')

#ax2.errorbar(data['Datetime'], mean_values_temp, std_values_temp, fmt='o-', color='green', label='Standard Deviation', alpha=0.5)
ax2.set_ylim(-10, data[temperature_types].max().max())
ax2.set_xlabel('Date and Time')
ax2.set_ylabel('Temperature (°C)')
ax2.legend()
ax2.grid(True)
ax2.set_title('Analysis for Temperature over time')
ax2.xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
ax2.xaxis.set_major_locator(mdates.AutoDateLocator())
plt.setp(ax2.get_xticklabels(), rotation=30, ha='right')  # Adjust rotation for better readability

plt.suptitle('Analysis for Humidity and Temperature over time.', y=0.95, x=0.5, color='black', horizontalalignment='center')
plt.show()
```

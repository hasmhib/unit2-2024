# Remote temperature analysis
<img width="max" alt="Screenshot 2023-12-12 at 11 45 58 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/b2818635-fca8-4832-aff3-dd5d1b7fb1be">

```.py
from matplotlib.gridspec import GridSpec
import numpy as np
from Quizzes.lib_api import get_sensors, smoothing, get_sensors_datetime
import matplotlib.pyplot as plt
import matplotlib.dates as mdates

ids = [0, 2, 4]
sensors = get_sensors(ids=ids)
datetime_list = get_sensors_datetime(ids=[2])
temp1 = sensors[2] + sensors[4]

mean_values = []
std_values = []
x_values = datetime_list  # Use datetime_list as x-values

temp = 0
for i, j in zip(sensors[2], sensors[4]):
    mean_values.append((i + j) / 2)
    std_values.append(np.std([i, j]))

min_values = np.minimum(sensors[2], sensors[4])
max_values = np.maximum(sensors[2], sensors[4])

fig = plt.figure(figsize=(10, 8))
grid = GridSpec(3, 3, fig)
plt.subplots_adjust(hspace=0.5)
ax1 = fig.add_subplot(grid[0:3, 0:2])

ax1.fill_between(x_values, min_values, max_values, color='lightcoral', alpha=0.5, label='Range')
ax1.plot(x_values, mean_values, 'r-', label='Mean, Median')
ax1.plot(x_values, max_values, 'blue', label='Maximum')
ax1.plot(x_values, min_values, 'yellow', label='Minimum')
ax1.set_title('Analysis of sensors 2, 4')
ax1.set_xlabel('Time')
ax1.legend()
plt.grid(True)

ax1.xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box2 = fig.add_subplot(grid[0, 2])
box2.plot(sensors[0], color="blue", marker='o', linestyle='-', markersize=2,linewidth=2)
box2.set_title("Sensor 0 (Temperature)")
plt.grid(True)

plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box3 = fig.add_subplot(grid[1, 2])
box3.plot(sensors[2], color="green", marker='o', linestyle='-', markersize=2, linewidth=2)
box3.set_title("Sensor 2 (Temperature)")
plt.grid(True)

plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box4 = fig.add_subplot(grid[2, 2])
box4.plot(x_values, sensors[4], color="yellow", marker='o', linestyle='-', markersize=2, linewidth=2)
box4.set_title("Sensor 4 (Temperature)")
plt.grid(True)

ax1.xaxis.set_major_locator(mdates.AutoDateLocator())
plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

plt.show()
```
# Standard deviation of remote analysis
<img width="max" alt="Screenshot 2023-12-12 at 11 47 45 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/8b1fccef-3c46-4771-bd78-ea5e526f2f17">

```.py
from matplotlib.gridspec import GridSpec
import numpy as np
from Quizzes.lib_api import get_sensors, smoothing, get_sensors_datetime
import matplotlib.pyplot as plt
import matplotlib.dates as mdates

ids = [0, 2, 4]
sensors = get_sensors(ids=ids)
datetime_list = get_sensors_datetime(ids=[2])
temp1 = sensors[2] + sensors[4]

mean_values = []
std_values = []
x_values = datetime_list  # Use datetime_list as x-values

temp = 0
for i, j in zip(sensors[2], sensors[4]):
    mean_values.append((i + j) / 2)
    std_values.append(np.std([i, j]))

min_values = np.minimum(sensors[2], sensors[4])
max_values = np.maximum(sensors[2], sensors[4])

fig = plt.figure(figsize=(10, 8))
grid = GridSpec(3, 3, fig)
plt.subplots_adjust(hspace=0.5)
ax1 = fig.add_subplot(grid[0:3, 0:2])

# ax1.fill_between(x_values, min_values, max_values, color='lightcoral', alpha=0.5, label='Range')
# ax1.plot(x_values, mean_values, 'r-', label='Mean, Median')
# ax1.plot(x_values, max_values, 'blue', label='Maximum')
# ax1.plot(x_values, min_values, 'yellow', label='Minimum')
ax1.errorbar(x_values, mean_values, std_values, fmt='o-', color='green', label='Standard Deviation', alpha=0.1)
ax1.set_title('Standard Deviation of sensors 2, 4')
ax1.set_xlabel('Time')
ax1.legend()
plt.grid(True)

ax1.xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box2 = fig.add_subplot(grid[0, 2])
box2.plot(sensors[0], color="blue", marker='o', linestyle='-', markersize=2,linewidth=2)
box2.set_title("Sensor 0 (Temperature)")
plt.grid(True)

plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box3 = fig.add_subplot(grid[1, 2])
box3.plot(sensors[2], color="green", marker='o', linestyle='-', markersize=2, linewidth=2)
box3.set_title("Sensor 2 (Temperature)")
plt.grid(True)

plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box4 = fig.add_subplot(grid[2, 2])
box4.plot(x_values, sensors[4], color="yellow", marker='o', linestyle='-', markersize=2, linewidth=2)
box4.set_title("Sensor 4 (Temperature)")
plt.grid(True)

ax1.xaxis.set_major_locator(mdates.AutoDateLocator())
plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

plt.show()
```

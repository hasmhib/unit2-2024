# Remote humidity analysis
<img width="max" alt="Screenshot 2023-12-12 at 11 45 32 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/daf70e3b-d88f-40ff-84c5-e41cee7ade94">

```.py
from matplotlib.gridspec import GridSpec
import numpy as np
from Quizzes.lib_api import get_sensors, smoothing, get_sensors_datetime
import matplotlib.pyplot as plt
import matplotlib.dates as mdates

ids = [1, 3, 5]
sensors = get_sensors(ids=ids)
datetime_list = get_sensors_datetime(ids=[1])
temp1 = sensors[1] + sensors[5]

mean_values = []
std_values = []
x_values = datetime_list  # Use datetime_list as x-values

temp = 0
for i, j in zip(sensors[1], sensors[5]):
    mean_values.append((i + j) / 2)
    std_values.append(np.std([i, j]))

min_values = np.minimum(sensors[1], sensors[5])
max_values = np.maximum(sensors[1], sensors[5])

fig = plt.figure(figsize=(10, 8))
grid = GridSpec(3, 3, fig)
plt.subplots_adjust(hspace=0.5)
ax1 = fig.add_subplot(grid[0:3, 0:2])

ax1.fill_between(x_values, min_values, max_values, color='lightblue', alpha=0.5, label='Range')
ax1.plot(x_values, mean_values, 'r-', label='Mean, Median')
ax1.plot(x_values, max_values, 'blue', label='Maximum')
ax1.plot(x_values, min_values, 'yellow', label='Minimum')
ax1.set_title('Analysis of sensors 1, 5')
ax1.set_xlabel('Time')
ax1.legend()
plt.grid(True)

ax1.xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box2 = fig.add_subplot(grid[0, 2])
box2.plot(sensors[1], color="blue", marker='o', linestyle='-', markersize=2,linewidth=0.5)
box2.set_title("Sensor 1 (Humidity)")
plt.grid(True)

plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box3 = fig.add_subplot(grid[1, 2])
box3.plot(sensors[3], color="green", marker='o', linestyle='-', markersize=2, linewidth=0.5)
box3.set_title("Sensor 3 (Humidity)")
plt.grid(True)

plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box4 = fig.add_subplot(grid[2, 2])
box4.plot(x_values, sensors[5], color="yellow", marker='o', linestyle='-', markersize=2, linewidth=0.5)
box4.set_title("Sensor 5 (Humidity)")
plt.grid(True)

ax1.xaxis.set_major_locator(mdates.AutoDateLocator())
plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

plt.show()
```

# Standard deviation of Remote humidity
<img width="max" alt="Screenshot 2023-12-12 at 11 47 15 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/6d298be1-ca3c-47d3-82b6-030a716e1724">

```.py
from matplotlib.gridspec import GridSpec
import numpy as np
from Quizzes.lib_api import get_sensors, smoothing, get_sensors_datetime
import matplotlib.pyplot as plt
import matplotlib.dates as mdates

ids = [1, 3, 5]
sensors = get_sensors(ids=ids)
datetime_list = get_sensors_datetime(ids=[1])
temp1 = sensors[1] + sensors[5]

mean_values = []
std_values = []
x_values = datetime_list  # Use datetime_list as x-values

temp = 0
for i, j in zip(sensors[1], sensors[5]):
    mean_values.append((i + j) / 2)
    std_values.append(np.std([i, j]))

min_values = np.minimum(sensors[1], sensors[5])
max_values = np.maximum(sensors[1], sensors[5])

fig = plt.figure(figsize=(10, 8))
grid = GridSpec(3, 3, fig)
plt.subplots_adjust(hspace=0.5)
ax1 = fig.add_subplot(grid[0:3, 0:2])

# ax1.fill_between(x_values, min_values, max_values, color='lightblue', alpha=0.5, label='Range')
# ax1.plot(x_values, mean_values, 'r-', label='Mean, Median')
# ax1.plot(x_values, max_values, 'blue', label='Maximum')
# ax1.plot(x_values, min_values, 'yellow', label='Minimum')
ax1.errorbar(x_values, mean_values, std_values, fmt='o-', color='green', label='Standard Deviation', alpha=0.1)
ax1.set_title('Standard Deviation of sensors 1, 5')
ax1.set_xlabel('Time')
ax1.legend()
plt.grid(True)

ax1.xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box2 = fig.add_subplot(grid[0, 2])
box2.plot(sensors[1], color="blue", marker='o', linestyle='-', markersize=2,linewidth=0.5)
box2.set_title("Sensor 1 (Humidity)")
plt.grid(True)

plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box3 = fig.add_subplot(grid[1, 2])
box3.plot(sensors[3], color="green", marker='o', linestyle='-', markersize=2, linewidth=0.5)
box3.set_title("Sensor 3 (Humidity)")
plt.grid(True)

plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

box4 = fig.add_subplot(grid[2, 2])
box4.plot(x_values, sensors[5], color="yellow", marker='o', linestyle='-', markersize=2, linewidth=0.5)
box4.set_title("Sensor 5 (Humidity)")
plt.grid(True)

ax1.xaxis.set_major_locator(mdates.AutoDateLocator())
plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

plt.show()
```

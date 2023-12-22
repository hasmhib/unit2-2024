```.py
from Quizzes.lib_api import get_sensors, smoothing
import matplotlib.pyplot as plt

my_sensors = get_sensors()

fig = plt.Figure(figsize=(10,8))
plt.subplot(2,1,1)
plt.plot(my_sensors[1],color='red')
plt.title("Sensor Outside")
plt.subplot(2,1,2)
x,y = smoothing(values = my_sensors[1])
plt.plot(x,y,color='black')
plt.show()
```

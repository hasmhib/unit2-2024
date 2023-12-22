```.py
#Server connected to ip 192.168.6.153

import requests
import matplotlib.pyplot as plt
import matplotlib
plt.style.use('ggplot')
matplotlib.use('MacOSX')

ip = '192.168.6.153'

requests = requests.get(f'http://{ip}/readings')
data = requests.json()

sensors = data['readings'][0]
print(f"There are {len(sensors)} records")

ids = []
for s in sensors:
    ids.append(s["sensor_id"])

print(ids)
#New data type : sets : shows unique values
print(set(ids))

fig = plt.figure(figsize=(10,8))
y = {1:[],2:[],3:[],4:[]}
ids_selected = [1,2,3,4]
for s in sensors:
    if s["sensor_id"] in ids_selected:
        key = s["sensor_id"]
        y[key].append(s['value'])
print(y)

t = 0
x = []
for _ in y[1]: #using sensor 1 as a reference
    x.append(t)
    t += 5 #Every 5 min

plt.subplot(2,2,1)
plt.plot(x,y[1],color='red')
plt.subplot(2,2,2)
plt.plot(x,y[2],color='blue')
plt.subplot(2,2,3)
plt.plot(x,y[3],color='green')
plt.subplot(2,2,4)
plt.plot(x,y[4],color='black')
plt.show()
```

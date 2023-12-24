```.py
import requests

def get_readings(ip:str='192.168.6.153'):

    data = requests.get(f'http://{ip}/readings')
    data = data.json()
    x = data['readings'][0]
    return x

def get_sensors(ids:list[int]=[1]):
    recordings = get_readings()
    my_sensors = {}
    for i in ids:
        my_sensors[i] = []
    for rec in recordings:
        id_sensor = rec['sensor_id']
        if id_sensor in ids:
            value = rec['value']
            my_sensors[id_sensor].append(value)

    return my_sensors

def get_sensors_datetime(ids:list[int]=[1]):
    recordings = get_readings()
    sensor_datetime = []
    for rec in recordings:
        id_sensor = rec['sensor_id']
        if id_sensor in ids:
            value = rec['datetime']
            sensor_datetime.append(value)

    return sensor_datetime

def smoothing(values:[], size_window:int=5):
    smoothed_values = []
    for i in range(0, len(values), size_window):
        window_mean = sum(values[i:i + size_window]) / size_window
        smoothed_values.append((i, window_mean))

    return smoothed_values
```

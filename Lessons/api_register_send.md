```.py
#api register and send
import requests

ip = '192.168.6.153'
username = 'yosuke'
password = "123456"

#we only need this once
request = requests.post(f'http://{ip}/register', json = {"username":username, "password":password})

answer = request.json()
print(answer)

request = requests.post(f'http://{ip}/login', json = {"username":username, "password":password})

token = request.json()["access_token"]

#create a sensor
new_sensor = {"type": "Tempereture","location":"Asama 25","name":"yosuke_temp1","unit":"C"}
header = {'Authorization': f"Bearer {token}"}
request = requests.post(f"http://{ip}/sensor/new", json = new_sensor, headers = header)

print(request.json())
```

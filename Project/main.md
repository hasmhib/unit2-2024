```.py
import serial
from datetime import datetime, timedelta
import requests
from time import sleep
# read data from sensor

def login(user={"username": "John", "password": "0405"}):
    user = {"username": "John", "password": "0405"}
    r = requests.post('http://192.168.6.142/reading/new', json=user)
    access_token = r.json()["access_token"]
    auth = {"Authorization": f"Bearer {access_token}"}
    return auth

def send_data(value, sensor_id):
    header = login()
    new_records = {"datetime": str(datetime.isoformat(datetime.now())), "sensor_id": sensor_id, "value": value}
    # Send an HTTP POST request to a specified URL with the new_record data and headers
    r = requests.post('http://192.168.6.142/reading/new', json=new_records, headers=header)
    json_data = r.json()
    print(json_data)
    return json_data["id"]

def read_arduino():
    arduino = serial.Serial(port="/dev/cu.usbserial-10", baudrate=9600, timeout=0.1)
    d1 = ""
    while len(d1) < 1:
        data = arduino.readline()
        d1 = data.decode("utf-8")
    print("d1 success")
    print(d1)
    d2 = ""
    while len(d2) < 1:
        data = arduino.readline()
        d2 = data.decode("utf-8")
    print("d2 success")
    print(d2)
    d3 = ""
    while len(d3) < 1:
        data = arduino.readline()
        d3 = data.decode("utf-8")
    print("d3 success")
    print(d3)
    return d1, d2, d3

def main():
    start_time = datetime.now()
    total_duration = timedelta(hours=48)  # Total duration for data collection

    while datetime.now() - start_time < total_duration:
        # Collect data for 5 minutes
        end_time = datetime.now() + timedelta(minutes=5)
        while datetime.now() < end_time:
            d1, d2, d3 = read_arduino()
            save_csv((d1, d2, d3))
            sleep(300)  # Sleep for 10 seconds between readings

    print("Data collection complete.")

def save_csv(data, file_name="reading.csv"):
    d1, d2, d3 = data
    print("Raw data:", d1, d2, d3)  # Add this line to print the raw data
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open(file_name, "a") as f:
        f. write(f"{timestamp},\n")
        if ',' in d1:
            humidity1, temperature1 = d1.split(',')
            f.write(f"{humidity1}, {temperature1}\n")
        if ',' in d2:
            humidity2, temperature2 = d2.split(',')
            f.write(f"{humidity2}, {temperature2}\n")
        if ',' in d3:
            humidity3, temperature3 = d3.split(',')
            f.write(f"{humidity3}, {temperature3}\n\n")

# get data from the url
def get_sensor(sensor_id, url: str = "192.168.6.153"):
    request = requests.get(f"http://{url}")
    data = request.json()
    readings = data["readings"][0]
    out = []
    for r in readings:
        if r["sensor_id"] == sensor_id:
            out.append(r["value"])
    return out

# make a list to draw the graph
import schedule

data = {"hum":[],"temp":[]}
def append_data():
    value = read_arduino() #wait until data is in the port
    msg = value.decode('utf-8')
    if not 'Hello' in msg:
        msg = msg.split()
        hum = msg[0].split(':')[1]
        temp = msg[1].split(':')[1]
        hum = float(hum[0:5])
        temp = float(temp[0:5])
        data["hum"].append(hum)
        data["temp"].append(temp)
        dt_string = datetime.now().strftime("%d/%m/%Y %H:%M:%S")
        print(data)
        with open("hum_temp_database.csv", "a") as file:
            file.write(f'\n{dt_string},{hum},{temp}')

dt_string = datetime.now().strftime("%d/%m/%Y %H:%M:%S")
print(f"Starting data collection at {dt_string}")

if __name__ == "__main__":
    main()


```

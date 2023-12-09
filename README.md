![11e470e9022f4fc5b367429bcbb285bc](https://github.com/comsci-uwc-isak/unit2_2023/assets/53995212/1d14b1d3-ae39-4ef3-8ec9-3329630eacae)

# Unit 2: A Distributed Weather Station for ISAK
  
## Criteria A: Planning
John, a student at an international boarding high school on top of the hill in Japan, faced a dilemma of spending over an hour trekking to the nearest supermarket for vegetables, including tomatoes and beans. Eager to optimize his time and explore different activities, he decided to produce vegetavles on his own. However, John recognized the importance of providing an ideal environment for his plants to thrive. To make an informed decision, he opted to gather data on temperature and humidity. With this information, he aimed to identify the most efficient location within his room for optimal plant growth. Concerned about the potential loss of his data due to any circumstances, John want his data to keep it somewhere safe. This way, even if the computer's data loss, he can recover his valuable information and continue refining his indoor gardening project.

## Proposed Solution
Considering the client requirements an adequate solution includes a low cost sensing device for humidity and temperature and a custom data script that process and anaysis the samples acquired. For a low cost sensing device an adequate alternative is the DHT11 sensor[^1] which is offered online for less than 5 USD and provides adequare precision and range for the client requirements (Temperature Range: 0°C to 50°C, Humidity Range: 20% to 90%). Similar devices such as the DHT22, AHT20 or the AM2301B [^2] have higher specifications, however the DHT11 uses a simple serial communication (SPI) rather than more eleborated protocols such as the I2C used by the alternatives. For the range, precision and accuracy required in this applicaiton the DHT11 provides the best compromise. Connecting the DHT11 sensor to a computer requires a device that provides a Serial Port communication. A cheap and often used alternative for prototyping is the Arduino UNO microcontroller [^3]. "Arduino is an open-source electronics platform based on easy-to-use hardware and software"[^4]. In additon to the low cost of the Arduino (< 6USD), this devide is programable and expandable[^1]. Other alternatives include diffeerent versions of the original Arduino but their size and price make them a less adequate solution.

Considering the budgetary constrains of the client and the hardware requirements, the software tool that I proposed for this solution is Python. Python's open-source nature and platform independence contribute to the long-term viability of the system. The use of Python simplifies potential future enhancements or modifications, allowing for seamless scalability without the need for extensive redevelopment [^5][^6]. In comparison to the alternative C or C++, which share similar features, Python is a High level programming language (HLL) with high abstraction [^7]. For example, memory management is automatic in Python whereas it is responsability of the C/C++ developer to allocate and free up memory [^7], this could result in faster applications but also memory problems. In addition a HLL language will allow me and future developers extend the solution or solve issues proptly.  

**Design statement**

``` Fill out here```

## Success Criteria

[^1]: Industries, Adafruit. “DHT11 Basic Temperature-Humidity Sensor + Extras.” Adafruit Industries Blog RSS, https://www.adafruit.com/product/386. 
[^2]: Nelson, Carter. “Modern Replacements for DHT11 and dht22 Sensors.” Adafruit Learning System, https://learn.adafruit.com/modern-replacements-for-dht11-dht22-sensors/what-are-better-alternatives.   
[^3]:“How to Connect dht11 Sensor with Arduino Uno.” Arduino Project Hub, https://create.arduino.cc/projecthub/pibots555/how-to-connect-dht11-sensor-with-arduino-uno-f4d239.  
[^4]:Team, The Arduino. “What Is Arduino?: Arduino Documentation.” Arduino Documentation | Arduino Documentation, https://docs.arduino.cc/learn/starting-guide/whats-arduino.  
[^5]:Tino. “Tino/PyFirmata: Python Interface for the Firmata (Http://Firmata.org/) Protocol. It Is Compliant with Firmata 2.1. Any Help with Updating to 2.2 Is Welcome. the Capability Query Is Implemented, but the Pin State Query Feature Not Yet.” GitHub, https://github.com/tino/pyFirmata. 
[^6]:Python Geeks. “Advantages of Python: Disadvantages of Python.” Python Geeks, 26 June 2021, https://pythongeeks.org/advantages-disadvantages-of-python/. 
[^7]: Real Python. “Python vs C++: Selecting the Right Tool for the Job.” Real Python, Real Python, 19 June 2021, https://realpython.com/python-vs-cpp/#memory-management. 

1. The solution provides a visual representation of the Humidity and Temperature values inside a dormitory (Local) and outside the house (Remote) for a period of minimum 48 hours. 
1. ```[HL]``` The local variables will be measure using a set of 3 sensors around the dormitory.
2. The solution provides a mathematical modelling for the Humidity and Temperature levels for each Local and Remote locations. ```(SL: linear model)```, ```(HL: non-lineal model)```
3. The solution provides a comparative analysis for the Humidity and Temperature levels for each Local and Remote locations including mean, standad deviation, minimum, maximum, and median.
4. ```(SL)```The Local samples are stored in a csv file and ```(HL)``` posted to the remote server as a backup.
5. The solution provides a prediction for the subsequent 12 hours for both temperature and humidity.
6. The solution includes a poster summarizing the visual representations, model and analysis created. The poster includes a recommendation about healthy levels for Temperature and Humidity.

_TOK Connection: To what extent does ```the use of data science``` in climate research influence our understanding of environmental issues, and what knowledge questions arise regarding the ```reliability, interpretation, and ethical implications``` of data-driven approaches in addressing climate change_

1. How does our use of technology shape our understanding of the environment
2. What responsibilities do we have as technologists when it comes to handling personal data related to our living spaces?
3. What cultural and contextual factors might impact our interpretation of the results, especially when comparing our local readings with those from the campus? 

# Criteria B: Design

## Flow diagram

<img width="421" alt="Screenshot 2023-12-05 at 11 42 08" src="https://github.com/hasmhib/unit2-2024/assets/142702159/b39c437f-54b5-4b89-9af8-2c546a712e28">

**fig1** flow diagram of the function, create_new_sensor

This flow diagram shows the function called create_new sensor. This function is for creating a new sensor in the API. By using login function, user can get the access token.
This functioin makes it available to post the data with new id.


<img width="433" alt="Screenshot 2023-12-07 at 21 12 59" src="https://github.com/hasmhib/unit2-2024/assets/142702159/87752997-7f81-415d-8c37-d2727ceef3a8">


**fig2** flow diagram of the function, get_sensor.

This flow diagram shows the function called get_sensor.By using request library, get data from API and arrange them as json file. Only pick the value with the specific sensor_id, and add to the list. The list is for drawing graph.

## System Diagram

![HL](https://github.com/comsci-uwc-isak/unit2_2023/assets/53995212/4891d5e9-b8ab-46ed-bd75-b606e25e3383)

**Fig.2** shows the system diagram for the proposed solution (**HL**). The indoor variables will be measured using an Arduino and three DHT11 sensors located inside a room. Three sensors are used to determine more precisely the physical values and include measurement uncertainty. The outdoor variables will be requested to the remote server using a GET request to the API of the server at ```192.168.6.153/readings```. The local values are stored in a CSV database locally and a backup copy will be store in the remote server using the **Weather API**. 


## Record of Tasks
| Task No | Planned Action                                                | Planned Outcome                                                                                                 | Time estimate | Target completion date | Criterion |
|---------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------|------------------------|-----------|
| 1       | Write the Problem context                        | a clear defenition of the problem | 10min         | Nov 22                 | A         |
|2| 	Write the list of materials| Have a full list of materials | 5min | Nov 28 | B
|3| 	Brainstorm and write ploblem definition| A clear design statement that suits the need of the client | 20min| Nov 29 |A|
|4 | make a code for arduino with Arduino IDE | define each sensor and | 30 min | December 2 |  C | 
|5| define read_arduino() | read data from arduino| 1 hour | Decemver 2 | C | 
|6| define send_csv() | send data I got from read_arduino() to reading_csv| 3 hours | December 2 | C | 
|7| define main()| set time to get temperature and humidity |  2 hours | December 2  | C | 
|8| define login() | require username and password to see the data to keep it safely| 1 hour | December 3 | C | 
|9| define send_data() | add data(datetime,sensor_id and value) to url | 3 hour | December 3 | C  | 
|10| make the function to get the list from csv file | organize the data to draw graph | 2 hour | December 4 | C  | 
|11| draw the flow diagram | make it claery how to organize the code | 1 hour | December 3 | C  | 



## Test Plan 
| Test Type | Target | Procedure | Expected Outcome |
|-----------|--------|-----------|------------------|
| Functional: Integrational testing | Connect to server | 1. Open the program file containing the code developed in order to connect to the server and extract or send data from/to a suitable place 2. Run the program in the terminal 3. Check if data is being collected and uploaded to the .csv file and to the server by looking at the adequate sensor id and see if it matches the id of sensors used for the data collecting|The program should run and print data into the remote server. It should make sure that all sensors are collecting data, and uploading it onto both a .csv file and the remote server.|
| Functional: Integrational testing | Crontab Functionality | 1. Open crontab terminal 2. Set the desired interval of time between each time the program runs. 3. Wait for the response from the program in order to see if it was succesfully executed. |The program contains a return that is visible and which is stored in a file in order to have proof that the program ran successfully. The program should be able to run in the background even though it is closed. The pogram should continue to run the program without stopping in the middle until crontab is disabled, and the data should continue to be collected.|
| Functional: Integrational testing | Sensor connectivity | 1. Connect all sensors to breadboard which is conneceted to the rasberry pi model 4 connected to the power source 2. Run get_readings function which collects humidity and temperature levels from all 4 sensors and returns a message if they are not properly connected  | The program should return readings for all sensors connected, and if there is an error within any of the sensors, an error message should appear. |
| Non-functional: Load testing | Testing if the program has little lag or glitches due to the amount of time the program is ran for (48 hours). Additionally, see if continously added data (readings) influence the proccessing of the program. | 1. Run the program. 2. Continously check up on the code, every 2-3 hours. | All data is up to date, and the program is still continously running and recoridng data wihtout any glitches or lag. |
| Non-functional: Response time | Testing if the sensor responds quickly to the running program and see how long it takes for the sensor to register and print out the current temperature and humidity| 1. Run the basic program that aims to print the current temperature and humidity the sensor collects.| The program returns the swiftly returns the current temperature and humidity the sensor collects without any lag or delay. |
| Non-functional：Code review | Reviewing if the code has adequate comments, function name, and variable name.As this reviews the quality of the code, there are no inputs. | The procedure included a review of the code from a external developer who is not familiar with techniques used in it. The developer then gave feedback on which parts are not understandable and names of which variables are not logical when looking at the purpose of the variable.|The code will include comments explaining what is occuring within the code. Furthermore, the names of variables are simple and it is easy to understand what is their usage in the program |



# Criteria C: Development

## List of techniques used
1. Functions

2. Lists

3. For loops

4. While loops

5. PIN connection validation

6. File reading

7. Writing in a csv file

8. Loging to the Api servers 

9. Sending data to Api servers

10. Reading data from the Api server

11. Plotting graph


## Development

## login and create a new sensor

```.py

import requests


def login():
    user = {"username": "Ayane", "password": "12"}
    r = requests.post('http://192.168.6.153/login', json=user)
    access_token = r.json()["access_token"]
    return {"Authorization": f"Bearer {access_token}"}

```

```.py


def create_new_sensor(name, sensor_type, location, unit=""):
    ip = "192.168.6.153"
    headers = login()
    sensor = {"name": name, "type": sensor_type, "location": location, "unit": unit}
    ans = requests.post(f"http://{ip}/sensor/new", json=sensor, headers=headers)
    print(ans.json())
    json = ans.json()
    return json["id"]
```


### what I got from the function
```.py
create_new_sensor("Ayane_no_t1","Temeperature","R2-10","C")
#{"type": "Temperature","owner_id": 5, "unit": "C", "location": "R2-10", "name": "Ayane_no_t1","id": 68},
create_new_sensor("Ayane_no_t2","Temeperature","R2-10","C")
# {"type": "Temperature", "owner_id": 5, "unit": "C", "location": "R2-10","name": "Ayane_no_t2","id": 69 },
create_new_sensor("Ayane_no_t3","Temeperature","R2-10","C")
# {"type": "Temperature","owner_id": 5,"unit": "C","location": "R2-10", "name": "Ayane_no_t3","id": 70},
create_new_sensor("Ayane_no_h1","Humidity","R2-10","%")
#{ "type": "Humidity", "owner_id": 5, "unit": "%","location": "R2-10", "name": "Ayane_no_h1","id": 71},
create_new_sensor("Ayane_no_h2","Humidity","R2-10","%")
# {"type": "Humidity","owner_id": 5, "unit": "%","location": "R2-10","name": "Ayane_no_h2","id": 72 },
create_new_sensor("Ayane_no_h3","Humidity","R2-10","%")
# {"type": "Humidity","owner_id": 5,"unit": "%","location": "R2-10","name": "Ayane_no_h3","id": 73}
```

I defined a function called login that facilitates user authentication to a web service. The function takes no arguments and is responsible for generating and returning an authorization token required for subsequent secured interactions with the service. Inside the function, a dictionary user is created with a predefined username and password. The requests.post method is then utilized to send a POST request to the specified URL ('http://192.168.6.153/login') with the user credentials provided as json data. The response from the server is parsed as json, and the access token, a crucial element for authorization, is extracted. Finally, the function constructs and returns a dictionary with an "Authorization" key, incorporating the obtained access token using the Bearer token authentication scheme. This token can be subsequently used in the headers of other HTTP requests to access secured endpoints on the web service.


Next, I defined the function create_new_sensor to create a new sensor in the URL. The function requires the name of the sensor, sensor type (in this case, Temperature or Humidity), location where the user wants to put the sensor, and unit (C or %). By using the login function, the user can log in to the IP ("192.168.6.153"). The requests.post method is utilized to send a POST request with the dictionary including the details the user input as a JSON file and the return of the login function as headers. In order to ensure the user could receive what they send to the server, I set the code so that the user can see the server's response with printing ans (equal to requests.post(f"http://{ip}/sensor/new", json=sensor, headers=headers)) as a JSON file. The results are presented in what I got from the function section, demonstrating the successful creation of new sensors with different specifications.





```.py
def read_arduino():
    arduino = serial.Serial(port="/dev/cu.usbserial-10", baudrate=9600, timeout=0.1)
    d1 = ""
    while len(d1< 1):
        data = arduino.readline()
    d1 = ""
    while len(d1 < 1):
        data = arduino.readline()
    d2 = ""
    while len(d2 < 1):
        data = arduino.readline()
    d3 = ""
    while len(d3 < 1):
        data = arduino.readline()
    d1 = d1.docode("utf-8")
    d2 = d2.docode("utf-8")
    d3 = d3.docode("utf-8")
    return d1, d2, d3
```
**code3** The code above shows how to read data from arduino. I defined the data from each sensor as d1, d2, d3 to send csv file.

```.py
def save_csv(data, file_name="reading.csv"):
    d1, d2, d3 = data
    print("Raw data:", d1, d2, d3)  # Add this line to print the raw data
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open(file_name, "a") as f:
        f. write(f"{timestamp},\n")
        if ',' in d1:
            humidity1, temperature1 = d1.split(',')
            f.write(f"Sensor 1: Humidity: {humidity1} Temperature: {temperature1}\n")
        if ',' in d2:
            humidity2, temperature2 = d2.split(',')
            f.write(f"Sensor 2: Humidity: {humidity2} Temperature: {temperature2}\n")
        if ',' in d3:
            humidity3, temperature3 = d3.split(',')
            f.write(f"Sensor 3: Humidity: {humidity3} Temperature: {temperature3}\n\n")

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
```
**code4** The code above shows how I set the interval to record the data every 5 min for 48 hours and send the data to csv file. Each data is splited by ",".

<img width="1120" alt="Screenshot 2023-12-09 at 13 18 27" src="https://github.com/hasmhib/unit2-2024/assets/142702159/a0079af5-aa2b-4e88-a1ac-3615b5881b37">

**fig5** This picture shows how is data seved to reading.csv.


```.py
def process_data():
    output=[]
    with open('reading.csv', 'r') as file:
        lines = file.readlines()
        for i in range(0,len(lines)-8,8):
            temp = lines[i:i+8]
            temp2 = []
            for text in temp:
                if text != "\n":
                    temp4=text[0:len(text)-1].strip(",").strip(" ")
                    temp2.append(temp4)
            temp2[0]=temp2[0][0:10]+","+temp2[0][11:]
            temp2[1]=temp2[1][:6]+temp2[1][7:]
            temp2[2] = temp2[2][:6] + temp2[2][7:]
            temp2[3] = temp2[3][:6] + temp2[3][7:]
            output.append(",".join(temp2))
    # Write the result back to a new file
    with open('formatted_data.csv', 'w') as output_file:
        output_file.write("\n".join(output))

def make_list():
    with (open("formatted_data.csv", "r") as file):
        lines = file.readlines()
        date = []
        t1 = []
        h1 = []
        t2 = []
        h2 = []
        t3 = []
        h3 = []
        for text in lines:
            lists = text.split(",")
            if len(lists) >= 7:
                date.append(lists[0])
                h1.append(float(lists[1]))
                t1.append(float(lists[2]))
                h2.append(float(lists[3]))
                t2.append(float(lists[4]))
                h3.append(float(lists[5]))
                t3.append(float(lists[6]))
        print(date)
        print(h2)
        print(h3)
        print(t1)
        print(t2)
        print(t3)
    return date,h1,t1,h2,t2,h3,t3


```
**code5**The codes above show how to reorganize the data in reading.csv and make a list from the new csv file.

<img width="636" alt="Screenshot 2023-12-09 at 13 18 32" src="https://github.com/hasmhib/unit2-2024/assets/142702159/11a08261-0173-41a4-8004-8821f78318b9">

**fig6** This picture shows how is the value reorganized in formatted_data.csv.

<img width="1325" alt="Screenshot 2023-12-09 at 13 30 50" src="https://github.com/hasmhib/unit2-2024/assets/142702159/bac41f82-0876-4884-a430-73d3e49d5900">

**fig7** This picture shows the result of the function, make_list.

```.py
def send_data(value:list,date:list,sensor_id):
    for x in range(len(value)):
        header = login()
        new_records = {"datetime":date[x], "sensor_id": sensor_id, "value" : value[x]}
        # Send an HTTP POST request to a specified URL with the new_record data and headers
        r = requests.post('http://192.168.6.153/reading/new', json=new_records, headers=header)
        out = r.json()
        print("Response Content:",out)

date = ['2023-12-03 23:13:25', '2023-12-03 23:18:28', '2023-12-03 23:23:31', '2023-12-03 23:28:34', '2023-12-03 23:33:37', '2023-12-03 23:38:40', '2023-12-03 23:43:43', '2023-12-03 23:48:46', '2023-12-03 23:53:48', '2023-12-03 23:58:51', '2023-12-04 00:03:54', '2023-12-04 00:08:57', '2023-12-04 00:14:00', '2023-12-04 00:19:03', '2023-12-04 00:24:06', '2023-12-04 00:29:09', '2023-12-04 00:34:12', '2023-12-04 00:39:15', '2023-12-04 00:44:17', '2023-12-04 00:49:20', '2023-12-04 00:54:23', '2023-12-04 00:59:26', '2023-12-04 01:04:29', '2023-12-04 01:09:32', '2023-12-04 01:14:35', '2023-12-04 01:19:38', '2023-12-04 01:24:41', '2023-12-04 01:29:44', '2023-12-04 01:34:47', '2023-12-04 01:39:50', '2023-12-04 01:44:52', '2023-12-04 01:49:55', '2023-12-04 01:54:58', '2023-12-04 02:00:01', '2023-12-04 02:05:04', '2023-12-04 02:10:07', '2023-12-04 02:15:10', '2023-12-04 02:20:13', '2023-12-04 02:25:16', '2023-12-04 02:30:19', '2023-12-04 02:35:21', '2023-12-04 02:40:24', '2023-12-04 02:45:27', '2023-12-04 02:50:30', '2023-12-04 02:55:33', '2023-12-04 03:00:36', '2023-12-04 03:05:39', '2023-12-04 03:10:42', '2023-12-04 03:15:45', '2023-12-04 03:20:48', '2023-12-04 03:25:51', '2023-12-04 03:30:54', '2023-12-04 03:35:56', '2023-12-04 03:40:59', '2023-12-04 03:46:02', '2023-12-04 03:51:05', '2023-12-04 03:56:08', '2023-12-04 04:01:11', '2023-12-04 04:06:14', '2023-12-04 04:11:17', '2023-12-04 04:16:20', '2023-12-04 04:21:23', '2023-12-04 04:26:25', '2023-12-04 04:31:28', '2023-12-04 04:36:31', '2023-12-04 04:41:34', '2023-12-04 04:46:37', '2023-12-04 04:51:40', '2023-12-04 04:56:43', '2023-12-04 05:01:46', '2023-12-04 05:06:49', '2023-12-04 05:11:52', '2023-12-04 05:16:55', '2023-12-04 05:21:57', '2023-12-04 05:27:00', '2023-12-04 05:32:03', '2023-12-04 05:37:06', '2023-12-04 05:42:09', '2023-12-04 05:47:12', '2023-12-04 05:52:15', '2023-12-04 05:57:18', '2023-12-04 06:02:20', '2023-12-04 06:07:23', '2023-12-04 06:12:26', '2023-12-04 06:17:29', '2023-12-04 06:22:32', '2023-12-04 06:27:35', '2023-12-04 06:32:38', '2023-12-04 06:37:41', '2023-12-04 06:42:44', '2023-12-04 06:47:46', '2023-12-04 06:52:49', '2023-12-04 06:57:52', '2023-12-04 07:02:55', '2023-12-04 07:07:59', '2023-12-04 07:13:01', '2023-12-04 07:18:04', '2023-12-04 07:23:07', '2023-12-04 07:28:10', '2023-12-04 07:33:13', '2023-12-04 07:38:16', '2023-12-04 07:43:19', '2023-12-04 07:48:22', '2023-12-04 07:53:25', '2023-12-04 07:58:28', '2023-12-04 08:03:30', '2023-12-04 08:08:33', '2023-12-04 08:13:36', '2023-12-04 08:18:39', '2023-12-04 08:23:42', '2023-12-04 08:28:45', '2023-12-04 08:33:48', '2023-12-04 08:38:51', '2023-12-04 08:43:54', '2023-12-04 08:48:57', '2023-12-04 08:54:00', '2023-12-04 08:59:03', '2023-12-04 09:04:05', '2023-12-04 09:09:08', '2023-12-04 09:14:11', '2023-12-04 09:19:14', '2023-12-04 09:24:17', '2023-12-04 09:29:20', '2023-12-04 09:34:23', '2023-12-04 09:39:26', '2023-12-04 09:44:29', '2023-12-04 09:49:32', '2023-12-04 09:54:34', '2023-12-04 09:59:37', '2023-12-04 10:04:40', '2023-12-04 10:09:43', '2023-12-04 10:14:46', '2023-12-04 10:19:49', '2023-12-04 10:24:52', '2023-12-04 10:29:55', '2023-12-04 10:34:58', '2023-12-04 10:40:01', '2023-12-04 10:45:04', '2023-12-04 10:50:07', '2023-12-04 10:55:09', '2023-12-04 11:00:12', '2023-12-04 11:05:15', '2023-12-04 11:10:18', '2023-12-04 11:15:21', '2023-12-04 11:20:24', '2023-12-04 11:25:27', '2023-12-04 11:30:30', '2023-12-04 11:35:33', '2023-12-04 11:40:36', '2023-12-04 11:45:39', '2023-12-04 11:50:42', '2023-12-04 11:55:44', '2023-12-04 12:00:47', '2023-12-04 12:05:50', '2023-12-04 12:10:53', '2023-12-04 12:15:56', '2023-12-04 12:20:59', '2023-12-04 12:26:02', '2023-12-04 12:31:05', '2023-12-04 12:36:08', '2023-12-04 12:41:11', '2023-12-04 12:46:14', '2023-12-04 12:51:17', '2023-12-04 12:56:19', '2023-12-04 13:01:22', '2023-12-04 13:06:25', '2023-12-04 13:11:28', '2023-12-04 13:16:31', '2023-12-04 13:21:34', '2023-12-04 13:26:37', '2023-12-04 13:31:40', '2023-12-04 13:36:43', '2023-12-04 13:41:46', '2023-12-04 13:46:49', '2023-12-04 13:51:51', '2023-12-04 13:56:54', '2023-12-04 14:01:57', '2023-12-04 14:07:00', '2023-12-04 14:12:03', '2023-12-04 14:17:06', '2023-12-04 14:22:09', '2023-12-04 14:27:12', '2023-12-04 14:32:15', '2023-12-04 14:37:18', '2023-12-04 14:42:21', '2023-12-04 14:47:24', '2023-12-04 14:52:26', '2023-12-04 14:57:29', '2023-12-04 15:02:32', '2023-12-04 15:07:35', '2023-12-04 15:12:38', '2023-12-04 15:17:41', '2023-12-04 15:22:44', '2023-12-04 15:27:47', '2023-12-04 15:32:50', '2023-12-04 15:37:53', '2023-12-04 15:42:56', '2023-12-04 15:47:59', '2023-12-04 15:53:02', '2023-12-04 15:58:05', '2023-12-04 16:03:08', '2023-12-04 16:08:11', '2023-12-04 16:13:14', '2023-12-04 16:18:16', '2023-12-04 16:23:19', '2023-12-04 16:28:22', '2023-12-04 16:33:25', '2023-12-04 16:38:28', '2023-12-04 16:43:31', '2023-12-04 16:48:34', '2023-12-04 16:53:37', '2023-12-04 16:58:40', '2023-12-04 17:03:43', '2023-12-04 17:08:46', '2023-12-04 17:13:49', '2023-12-04 17:18:51', '2023-12-04 17:23:54', '2023-12-04 17:28:57', '2023-12-04 17:34:00', '2023-12-04 17:39:03', '2023-12-04 17:44:06', '2023-12-04 17:49:09', '2023-12-04 17:54:12', '2023-12-04 17:59:15', '2023-12-04 18:04:18', '2023-12-04 18:09:21', '2023-12-04 18:14:24', '2023-12-04 18:19:26', '2023-12-04 18:24:29', '2023-12-04 18:29:32', '2023-12-04 18:34:35', '2023-12-04 18:39:38', '2023-12-04 18:44:41', '2023-12-04 18:49:44', '2023-12-04 18:54:47', '2023-12-04 18:59:50', '2023-12-04 19:04:53', '2023-12-04 19:09:56', '2023-12-04 19:14:58', '2023-12-04 19:20:01', '2023-12-04 19:25:04', '2023-12-04 19:30:07', '2023-12-04 19:35:10', '2023-12-04 19:40:13', '2023-12-04 19:45:16', '2023-12-04 19:50:19', '2023-12-04 19:55:22', '2023-12-04 20:00:25', '2023-12-04 20:05:28', '2023-12-04 20:10:31', '2023-12-04 20:15:34', '2023-12-04 20:20:37', '2023-12-04 20:25:39', '2023-12-04 20:30:42', '2023-12-04 20:35:45', '2023-12-04 20:40:48', '2023-12-04 20:45:51', '2023-12-04 20:50:54', '2023-12-04 20:55:57', '2023-12-04 21:01:00', '2023-12-04 21:06:03', '2023-12-04 21:11:06', '2023-12-04 21:16:09', '2023-12-04 21:21:12', '2023-12-04 21:26:15', '2023-12-04 21:31:17', '2023-12-04 21:36:20', '2023-12-04 21:41:23', '2023-12-04 21:46:26', '2023-12-04 21:51:29', '2023-12-04 21:56:32', '2023-12-04 22:01:35', '2023-12-04 22:06:38', '2023-12-04 22:11:41', '2023-12-04 22:16:44', '2023-12-04 22:21:47', '2023-12-04 22:26:50', '2023-12-04 22:31:52', '2023-12-04 22:36:55', '2023-12-04 22:41:58', '2023-12-04 22:47:01', '2023-12-04 22:52:04', '2023-12-04 22:57:07', '2023-12-04 23:02:10', '2023-12-04 23:07:13', '2023-12-04 23:12:16', '2023-12-04 23:17:19', '2023-12-04 23:22:22', '2023-12-04 23:27:24', '2023-12-04 23:32:27', '2023-12-04 23:37:30', '2023-12-04 23:42:33', '2023-12-04 23:47:36', '2023-12-04 23:52:39', '2023-12-04 23:57:42', '2023-12-05 00:02:45', '2023-12-05 00:07:48', '2023-12-05 00:12:51', '2023-12-05 00:17:54', '2023-12-05 00:22:56', '2023-12-05 00:27:59', '2023-12-05 00:33:02', '2023-12-05 00:38:05', '2023-12-05 00:43:08', '2023-12-05 00:48:11', '2023-12-05 00:53:14', '2023-12-05 00:58:17', '2023-12-05 01:03:20', '2023-12-05 01:08:23', '2023-12-05 01:13:26', '2023-12-05 01:18:29', '2023-12-05 01:23:32', '2023-12-05 01:28:35', '2023-12-05 01:33:38', '2023-12-05 01:38:40', '2023-12-05 01:43:43', '2023-12-05 01:48:46', '2023-12-05 01:53:49', '2023-12-05 01:58:52', '2023-12-05 02:03:55', '2023-12-05 02:08:58', '2023-12-05 02:14:01', '2023-12-05 02:19:04', '2023-12-05 02:24:07', '2023-12-05 02:29:10', '2023-12-05 02:34:13', '2023-12-05 02:39:15', '2023-12-05 02:44:18', '2023-12-05 02:49:21', '2023-12-05 02:54:24', '2023-12-05 02:59:27', '2023-12-05 03:04:30', '2023-12-05 03:09:33', '2023-12-05 03:14:36', '2023-12-05 03:19:39', '2023-12-05 03:24:42', '2023-12-05 03:29:45', '2023-12-05 03:34:47', '2023-12-05 03:39:50', '2023-12-05 03:44:53', '2023-12-05 03:49:56', '2023-12-05 03:54:59', '2023-12-05 04:00:02', '2023-12-05 04:05:05', '2023-12-05 04:10:08', '2023-12-05 04:15:11', '2023-12-05 04:20:14', '2023-12-05 04:25:17', '2023-12-05 04:30:19', '2023-12-05 04:35:22', '2023-12-05 04:40:25', '2023-12-05 04:45:28', '2023-12-05 04:50:31', '2023-12-05 04:55:34', '2023-12-05 05:00:37', '2023-12-05 05:05:40', '2023-12-05 05:10:43', '2023-12-05 05:15:46', '2023-12-05 05:20:49', '2023-12-05 05:25:52', '2023-12-05 05:30:54', '2023-12-05 05:35:57', '2023-12-05 05:41:00', '2023-12-05 05:46:03', '2023-12-05 05:51:06', '2023-12-05 05:56:09', '2023-12-05 06:01:12', '2023-12-05 06:06:15', '2023-12-05 06:11:18', '2023-12-05 06:16:21', '2023-12-05 06:21:24', '2023-12-05 06:26:27', '2023-12-05 06:31:29', '2023-12-05 06:36:32', '2023-12-05 06:41:35', '2023-12-05 06:46:38', '2023-12-05 06:51:41', '2023-12-05 06:56:44', '2023-12-05 07:01:47', '2023-12-05 07:06:50', '2023-12-05 07:11:53', '2023-12-05 07:16:55', '2023-12-05 07:21:58', '2023-12-05 07:27:01', '2023-12-05 07:32:04', '2023-12-05 07:37:07', '2023-12-05 07:42:10', '2023-12-05 07:47:13', '2023-12-05 07:52:16', '2023-12-05 07:57:19', '2023-12-05 08:02:22', '2023-12-05 08:07:25', '2023-12-05 08:12:28', '2023-12-05 08:17:30', '2023-12-05 08:22:33', '2023-12-05 08:27:36', '2023-12-05 08:32:39', '2023-12-05 08:37:42', '2023-12-05 08:42:45', '2023-12-05 08:47:48', '2023-12-05 08:52:51', '2023-12-05 08:57:54', '2023-12-05 09:02:57', '2023-12-05 09:08:00', '2023-12-05 09:13:03', '2023-12-05 09:18:05', '2023-12-05 09:23:08', '2023-12-05 09:28:11', '2023-12-05 09:33:14', '2023-12-05 09:38:17', '2023-12-05 09:43:20', '2023-12-05 09:48:23', '2023-12-05 09:53:26', '2023-12-05 09:58:29', '2023-12-05 10:03:32', '2023-12-05 10:08:35', '2023-12-05 10:13:37', '2023-12-05 10:18:40', '2023-12-05 10:23:43', '2023-12-05 10:28:46', '2023-12-05 10:33:49', '2023-12-05 10:38:52', '2023-12-05 10:43:55', '2023-12-05 10:48:58', '2023-12-05 10:54:01', '2023-12-05 10:59:04', '2023-12-05 11:04:07', '2023-12-05 11:09:10', '2023-12-05 11:14:13', '2023-12-05 11:19:15', '2023-12-05 11:24:18', '2023-12-05 11:29:21', '2023-12-05 11:34:24', '2023-12-05 11:39:27', '2023-12-05 11:44:30', '2023-12-05 11:49:33', '2023-12-05 11:54:36', '2023-12-05 11:59:39', '2023-12-05 12:04:42', '2023-12-05 12:09:45', '2023-12-05 12:14:48', '2023-12-05 12:19:51', '2023-12-05 12:24:53', '2023-12-05 12:29:56', '2023-12-05 12:34:59', '2023-12-05 12:40:02', '2023-12-05 12:45:05', '2023-12-05 12:50:08', '2023-12-05 12:55:11', '2023-12-05 13:00:14', '2023-12-05 13:05:17', '2023-12-05 13:10:20', '2023-12-05 13:15:23', '2023-12-05 13:20:26', '2023-12-05 13:25:28', '2023-12-05 13:30:31', '2023-12-05 13:35:34', '2023-12-05 13:40:37', '2023-12-05 13:45:40', '2023-12-05 13:50:43', '2023-12-05 13:55:46', '2023-12-05 14:00:49', '2023-12-05 14:05:52', '2023-12-05 14:10:55', '2023-12-05 14:15:58', '2023-12-05 14:21:01', '2023-12-05 14:26:03', '2023-12-05 14:31:06', '2023-12-05 14:36:09', '2023-12-05 14:41:12', '2023-12-05 14:46:15', '2023-12-05 14:51:18', '2023-12-05 14:56:21', '2023-12-05 15:01:24', '2023-12-05 15:06:27', '2023-12-05 15:11:30', '2023-12-05 15:16:33', '2023-12-05 15:21:35', '2023-12-05 15:26:38', '2023-12-05 15:31:41', '2023-12-05 15:36:44', '2023-12-05 15:41:47', '2023-12-05 15:46:50', '2023-12-05 15:51:53', '2023-12-05 15:56:56', '2023-12-05 16:01:59', '2023-12-05 16:07:02', '2023-12-05 16:12:05', '2023-12-05 16:17:08', '2023-12-05 16:22:11', '2023-12-05 16:27:13', '2023-12-05 16:32:16', '2023-12-05 16:37:19', '2023-12-05 16:42:22', '2023-12-05 16:47:25', '2023-12-05 16:52:28', '2023-12-05 16:57:31', '2023-12-05 17:02:34', '2023-12-05 17:07:37', '2023-12-05 17:12:40', '2023-12-05 17:17:42', '2023-12-05 17:22:45', '2023-12-05 17:27:48', '2023-12-05 17:32:51', '2023-12-05 17:37:54', '2023-12-05 17:42:57', '2023-12-05 17:48:00', '2023-12-05 17:53:03', '2023-12-05 17:58:06', '2023-12-05 18:03:09', '2023-12-05 18:08:12', '2023-12-05 18:13:15', '2023-12-05 18:18:18', '2023-12-05 18:23:21', '2023-12-05 18:28:23', '2023-12-05 18:33:26', '2023-12-05 18:38:29', '2023-12-05 18:43:32', '2023-12-05 18:48:35', '2023-12-05 18:53:38', '2023-12-05 18:58:41', '2023-12-05 19:03:44', '2023-12-05 19:08:47', '2023-12-05 19:13:50', '2023-12-05 19:18:53', '2023-12-05 19:23:55', '2023-12-05 19:28:58', '2023-12-05 19:34:01', '2023-12-05 19:39:04', '2023-12-05 19:44:07', '2023-12-05 19:49:10', '2023-12-05 19:54:13', '2023-12-05 19:59:16', '2023-12-05 20:04:19', '2023-12-05 20:09:22', '2023-12-05 20:14:24', '2023-12-05 20:19:27', '2023-12-05 20:24:30', '2023-12-05 20:29:33', '2023-12-05 20:34:36', '2023-12-05 20:39:39', '2023-12-05 20:44:42', '2023-12-05 20:49:45', '2023-12-05 20:54:48', '2023-12-05 20:59:51', '2023-12-05 21:04:54', '2023-12-05 21:09:57', '2023-12-05 21:15:00', '2023-12-05 21:20:02', '2023-12-05 21:25:05', '2023-12-05 21:30:08', '2023-12-05 21:35:11', '2023-12-05 21:40:14', '2023-12-05 21:45:17', '2023-12-05 21:50:20', '2023-12-05 21:55:23', '2023-12-05 22:00:26', '2023-12-05 22:05:29', '2023-12-05 22:10:32', '2023-12-05 22:15:35', '2023-12-05 22:20:37', '2023-12-05 22:25:40', '2023-12-05 22:30:43', '2023-12-05 22:35:46', '2023-12-05 22:40:49', '2023-12-05 22:45:52', '2023-12-05 22:50:55', '2023-12-05 22:55:58', '2023-12-05 23:01:01', '2023-12-05 23:06:04']
h1 = [20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 52.2, 46.2, 35.8, 32.8, 32.7, 20.0, 28.2, 20.0, 31.1, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 31.9, 28.3, 28.2, 31.8, 37.2, 20.0, 20.0, 20.0, 52.2, 20.0, 20.0, 20.0, 31.5, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 37.8, 53.0, 32.3, 43.9, 20.0, 34.5, 20.0, 20.0, 20.0, 45.7, 20.0, 20.0, 20.0, 20.0, 20.0, 53.3, 20.0, 20.0, 20.0, 33.8, 35.4, 39.3, 42.0, 45.6, 45.6, 45.6, 51.5, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 42.6, 46.5, 80.8, 52.5, 52.6, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 52.5, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0]
h2 = [37.7, 34.8, 35.6, 34.3, 34.0, 33.8, 33.0, 32.7, 32.6, 32.8, 32.6, 32.9, 32.4, 32.5, 32.0, 31.9, 32.0, 31.9, 32.1, 32.6, 32.0, 31.4, 32.4, 32.1, 31.7, 32.0, 32.7, 32.8, 32.9, 33.0, 32.2, 32.4, 32.6, 33.7, 32.6, 32.6, 32.1, 32.4, 32.0, 32.2, 32.5, 32.6, 32.7, 32.5, 32.3, 32.4, 32.5, 32.1, 32.2, 32.9, 32.6, 32.9, 33.0, 32.8, 32.7, 32.7, 32.5, 32.8, 32.6, 32.7, 32.5, 31.9, 32.2, 32.1, 32.0, 31.9, 32.2, 32.1, 31.9, 32.1, 32.0, 31.8, 32.2, 31.7, 32.1, 31.8, 31.8, 31.8, 31.9, 32.1, 31.8, 31.5, 31.5, 31.5, 31.3, 31.2, 31.3, 31.2, 31.5, 31.4, 31.3, 31.1, 31.0, 31.0, 31.0, 31.3, 31.0, 30.9, 30.7, 30.7, 30.9, 31.0, 31.2, 31.7, 31.6, 31.2, 31.0, 31.1, 30.7, 30.5, 30.5, 30.5, 30.8, 30.2, 30.5, 30.4, 30.7, 30.9, 30.6, 30.9, 30.2, 30.2, 30.1, 29.6, 29.9, 29.4, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 50.0, 37.8, 50.0, 32.4, 44.0, 35.6, 35.6, 28.6, 32.3, 37.7, 33.8, 27.8, 29.9, 34.0, 32.5, 28.8, 32.5, 28.0, 34.4, 34.5, 41.2, 36.4, 34.7, 20.0, 20.0, 79.2, 39.4, 20.0, 49.0, 20.0, 83.3, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 27.9, 28.1, 28.0, 20.0, 27.7, 27.7, 28.0, 28.1, 28.9, 29.0, 29.2, 29.8, 30.2, 31.1, 31.1, 31.1, 31.3, 31.4, 31.5, 31.6, 32.0, 32.3, 32.0, 32.1, 32.6, 32.5, 32.6, 32.8, 33.3, 33.1, 33.3, 33.0, 32.4, 33.4, 33.3, 32.3, 32.4, 32.3, 32.5, 32.6, 32.4, 32.6, 32.5, 32.4, 32.6, 32.7, 32.7, 32.4, 32.3, 32.9, 32.5, 32.5, 31.9, 32.7, 32.0, 32.5, 33.3, 32.8, 32.7, 32.5, 32.9, 32.8, 32.5, 32.6, 33.0, 32.9, 32.8, 32.2, 31.7, 31.8, 31.2, 31.9, 31.4, 32.7, 32.3, 31.9, 32.0, 31.0, 31.0, 31.1, 31.0, 30.7, 31.7, 32.3, 31.7, 31.9, 32.3, 33.0, 31.6, 32.8, 33.0, 32.4, 33.3, 33.4, 33.7, 33.3, 34.0, 33.1, 33.1, 34.1, 33.2, 32.9, 33.4, 32.7, 33.3, 32.9, 32.7, 32.6, 33.3, 32.5, 33.0, 33.6, 32.3, 32.3, 31.6, 32.4, 32.6, 33.2, 32.9, 31.9, 32.9, 32.4, 32.6, 33.5, 33.2, 32.0, 31.9, 32.5, 33.2, 32.3, 32.0, 31.6, 32.8, 32.8, 32.6, 32.2, 31.4, 31.4, 32.1, 31.8, 31.2, 31.0, 30.8, 31.4, 31.6, 31.5, 31.5, 31.5, 32.1, 32.1, 32.4, 32.0, 32.5, 32.8, 32.2, 32.8, 32.1, 32.7, 32.3, 31.9, 32.0, 32.2, 31.6, 30.8, 30.9, 31.0, 30.9, 31.0, 30.9, 30.6, 30.1, 29.8, 29.6, 29.7, 29.4, 29.5, 29.3, 29.1, 28.8, 28.7, 28.4, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 28.1, 28.7, 28.6, 28.9, 28.5, 28.8, 28.6, 29.0, 28.9, 29.0, 28.8, 28.6, 28.2, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 28.2, 28.7, 28.2, 28.9, 28.7, 29.3, 28.8, 28.4, 28.6, 28.4, 28.7, 28.3, 20.0, 20.0, 29.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 28.6, 28.5, 28.2, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 28.2, 28.4, 28.6, 28.7, 29.1, 28.9, 28.8, 28.6, 28.9, 28.3, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 29.1, 29.5, 30.3, 30.1, 30.5, 31.5, 32.2, 32.8, 32.5, 31.1, 31.1, 31.4, 30.7, 31.4, 31.1, 30.2, 30.2, 30.0]
h3 = [74.9, 75.2, 75.2, 74.7, 74.8, 74.3, 73.4, 73.1, 73.1, 73.5, 73.4, 73.4, 72.6, 72.4, 72.0, 71.7, 71.9, 72.5, 73.4, 74.3, 74.6, 75.2, 75.4, 75.4, 74.8, 74.5, 74.6, 74.9, 75.1, 75.3, 75.0, 74.9, 75.2, 75.4, 75.0, 74.7, 74.7, 74.3, 73.4, 73.1, 73.7, 73.8, 73.5, 73.2, 73.1, 72.7, 72.9, 72.9, 73.2, 74.0, 74.4, 74.3, 74.7, 74.9, 75.3, 75.2, 75.2, 75.4, 75.2, 75.2, 75.0, 74.4, 74.2, 73.9, 73.8, 73.9, 73.8, 74.2, 74.4, 74.4, 73.8, 73.4, 73.1, 72.7, 72.9, 73.2, 73.0, 73.5, 73.6, 74.0, 74.2, 74.1, 73.3, 72.5, 72.1, 71.8, 72.0, 72.2, 72.6, 72.8, 72.3, 71.8, 71.7, 71.6, 71.8, 71.7, 71.4, 70.5, 68.9, 69.4, 69.5, 69.7, 69.6, 70.0, 69.7, 69.4, 69.4, 69.0, 68.3, 67.8, 68.4, 68.9, 68.4, 67.5, 66.9, 66.0, 66.4, 66.6, 65.9, 66.0, 63.8, 64.7, 64.7, 64.8, 64.6, 62.1, 59.0, 54.3, 55.2, 52.4, 49.1, 45.5, 44.7, 44.7, 44.8, 41.4, 40.4, 37.6, 20.0, 78.4, 30.9, 31.3, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 41.4, 20.0, 55.9, 40.3, 33.3, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 40.1, 20.0, 20.0, 38.7, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 56.2, 37.2, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 33.8, 34.8, 36.3, 37.3, 38.4, 39.0, 39.4, 39.9, 40.3, 40.8, 41.3, 41.5, 41.8, 42.0, 42.1, 42.4, 43.2, 42.1, 42.0, 42.1, 42.5, 42.5, 42.6, 42.6, 42.9, 43.2, 43.5, 43.8, 44.2, 44.7, 45.1, 45.7, 46.1, 46.7, 47.2, 47.4, 47.8, 48.1, 48.4, 48.8, 48.7, 48.9, 49.0, 49.0, 49.3, 49.7, 49.9, 50.1, 50.2, 50.3, 50.3, 50.5, 50.4, 50.4, 50.6, 50.7, 50.8, 51.5, 50.8, 51.0, 50.8, 50.5, 50.4, 50.2, 50.3, 50.3, 50.3, 50.2, 50.2, 50.3, 50.5, 50.7, 50.9, 51.1, 51.3, 51.3, 51.3, 51.3, 51.3, 51.4, 51.6, 51.7, 51.6, 51.6, 51.6, 51.5, 51.5, 51.6, 51.6, 51.5, 51.4, 51.3, 51.2, 51.1, 51.1, 51.1, 51.0, 51.0, 51.1, 51.1, 51.2, 51.3, 51.3, 51.4, 51.4, 51.6, 51.5, 51.4, 51.5, 51.4, 51.3, 51.3, 51.1, 50.9, 50.9, 51.0, 51.0, 51.0, 51.0, 51.2, 51.3, 51.5, 51.8, 51.9, 52.2, 52.3, 52.3, 52.3, 52.4, 52.3, 52.2, 52.3, 52.2, 52.4, 52.2, 52.2, 51.9, 51.8, 51.8, 51.7, 51.5, 51.5, 51.4, 51.4, 51.3, 51.2, 51.1, 50.7, 50.5, 50.3, 50.2, 49.9, 49.7, 49.8, 49.9, 49.8, 49.9, 49.7, 49.7, 50.0, 50.0, 50.0, 50.0, 50.0, 50.2, 49.9, 49.8, 49.8, 49.8, 49.6, 49.3, 49.5, 49.2, 49.1, 49.2, 48.9, 48.6, 48.7, 48.8, 49.0, 49.1, 49.2, 49.2, 49.0, 48.1, 48.4, 49.0, 48.6, 48.3, 47.8, 47.2, 46.6, 46.1, 45.3, 45.1, 45.4, 45.0, 44.9, 45.0, 44.8, 44.9, 44.9, 44.6, 43.9, 43.0, 41.7, 41.1, 40.3, 38.8, 38.0, 36.8, 34.5, 34.3, 34.2, 34.7, 34.7, 35.0, 36.0, 37.5, 37.9, 38.6, 39.1, 39.7, 40.4, 40.9, 40.9, 41.2, 41.3, 41.3, 41.2, 41.2, 41.3, 41.9, 42.3, 42.3, 41.9, 41.8, 41.5, 41.5, 41.6, 41.6, 41.9, 41.9, 42.5, 42.9, 42.9, 42.7, 43.0, 42.9, 42.8, 42.9, 42.8, 43.3, 43.4, 43.9, 43.7, 43.7, 44.3, 44.5, 44.7, 44.8, 44.8, 44.5, 43.3, 41.7, 41.1, 40.6, 40.0, 40.4, 40.6, 40.5, 42.3, 42.9, 42.8, 43.0, 43.2, 43.5, 43.2, 42.8, 43.2, 43.8, 43.8, 43.6, 44.0, 44.2, 44.1, 44.5, 44.2, 44.3, 44.6, 44.8, 45.0, 45.2, 45.6, 45.8, 45.9, 45.7, 45.6, 45.7, 45.9, 46.1, 45.7, 45.6, 45.7, 46.0, 45.0, 44.7, 44.4, 44.0, 44.3, 44.4, 44.3, 44.4, 43.5, 43.6, 43.1, 43.6, 44.1, 44.3, 44.7, 44.4, 44.4, 44.3, 44.3, 44.9, 45.2, 45.2, 45.0, 45.0, 43.6, 43.1, 43.5, 45.2, 47.0, 47.3, 47.6, 47.7, 48.1, 48.3, 48.3, 48.3, 48.4, 48.3, 48.5, 48.5, 48.7, 48.9, 49.0, 49.2, 49.4, 49.6, 49.8, 49.7, 49.8, 49.7, 49.9, 49.9, 50.1, 50.0, 49.8, 49.5, 49.2]
t1 = [15.5, 14.6, 16.1, 16.2, 16.2, 16.6, 16.6, 16.1, 15.8, 15.7, 16.0, 16.3, 16.2, 16.5, 16.4, 16.1, 16.1, 15.6, 15.5, 15.7, 15.7, 15.5, 15.8, 15.8, 15.7, 15.0, 14.7, 14.9, 15.0, 16.4, 16.8, 15.6, 15.0, 15.5, 15.5, 15.3, 15.5, 15.7, 15.4, 15.4, 15.3, 15.2, 15.2, 15.2, 15.7, 15.2, 15.5, 15.4, 15.3, 15.3, 14.9, 15.2, 14.9, 15.4, 15.0, 15.4, 14.9, 14.8, 14.7, 15.1, 15.2, 15.1, 15.1, 15.1, 15.1, 15.1, 15.3, 15.2, 15.1, 15.3, 15.3, 15.1, 15.3, 15.1, 15.1, 15.1, 15.2, 14.9, 15.0, 15.0, 15.2, 15.2, 15.1, 15.2, 15.2, 15.0, 15.0, 15.0, 14.4, 14.8, 15.2, 15.4, 15.1, 15.1, 14.9, 15.2, 15.1, 15.2, 15.2, 14.8, 15.0, 14.8, 14.7, 15.3, 15.3, 15.1, 15.0, 15.3, 15.3, 15.3, 15.1, 14.5, 14.7, 15.3, 14.8, 14.9, 14.7, 14.9, 14.8, 15.1, 14.7, 14.4, 14.5, 14.5, 14.5, 14.6, 14.6, 14.6, 14.6, 15.0, 15.3, 15.6, 16.5, 17.1, 18.0, 18.3, 18.6, 19.2, 19.7, 20.0, 20.3, 20.6, 21.0, 21.1, 21.4, 21.6, 21.8, 22.1, 22.2, 22.1, 22.2, 22.5, 22.6, 22.5, 22.7, 22.7, 22.6, 22.7, 22.9, 22.9, 23.3, 23.4, 23.6, 23.7, 23.6, 23.8, 23.8, 23.8, 23.6, 23.6, 23.7, 23.8, 23.7, 23.9, 24.2, 24.0, 24.1, 24.0, 23.9, 23.8, 23.5, 23.4, 23.5, 23.4, 23.3, 23.4, 23.0, 22.7, 22.4, 22.2, 22.2, 21.9, 21.9, 21.7, 21.7, 20.9, 19.8, 18.5, 17.7, 17.0, 17.2, 16.5, 15.7, 15.8, 18.9, 20.0, 20.5, 20.8, 21.2, 21.4, 21.5, 21.6, 21.4, 21.5, 21.4, 21.3, 21.3, 21.4, 21.3, 21.3, 21.2, 21.2, 21.4, 21.4, 21.4, 21.5, 21.5, 21.4, 21.3, 21.3, 21.3, 21.2, 21.2, 21.3, 21.1, 21.1, 21.2, 21.2, 21.0, 20.9, 21.0, 21.2, 21.3, 21.2, 21.4, 21.4, 21.4, 21.2, 21.3, 21.6, 21.7, 21.8, 21.9, 22.0, 22.1, 22.1, 21.8, 21.9, 22.0, 22.0, 21.7, 21.5, 21.4, 21.6, 21.4, 21.5, 21.4, 21.8, 22.0, 22.1, 22.2, 22.0, 21.9, 22.1, 22.1, 22.1, 21.9, 21.9, 21.9, 22.0, 22.3, 22.3, 22.4, 22.2, 22.4, 22.3, 22.3, 22.4, 22.4, 22.4, 22.0, 22.1, 21.9, 21.8, 21.6, 21.6, 21.4, 21.7, 21.8, 21.8, 21.6, 21.3, 21.3, 21.2, 21.2, 20.9, 21.0, 21.1, 20.8, 20.9, 20.7, 20.6, 20.3, 20.4, 20.6, 20.6, 20.6, 20.6, 20.7, 20.8, 20.8, 20.7, 20.7, 20.4, 20.4, 20.2, 20.2, 19.8, 19.9, 19.9, 19.8, 19.8, 19.8, 19.8, 19.6, 19.8, 19.6, 19.6, 19.5, 19.4, 19.4, 19.6, 19.7, 19.5, 19.4, 19.2, 19.1, 19.4, 19.8, 19.5, 19.3, 19.6, 19.7, 19.6, 19.5, 19.4, 19.6, 19.5, 19.6, 19.3, 19.2, 18.8, 19.1, 19.3, 19.3, 19.2, 18.9, 18.8, 18.7, 18.7, 18.8, 18.8, 18.9, 18.9, 18.9, 18.8, 19.0, 19.3, 19.2, 19.1, 18.9, 19.1, 18.9, 18.7, 18.7, 19.0, 19.2, 18.9, 18.7, 18.8, 18.8, 18.8, 18.8, 18.9, 18.8, 18.7, 18.6, 18.6, 18.6, 18.7, 18.8, 18.8, 18.9, 18.7, 18.6, 18.5, 18.4, 18.1, 18.2, 18.4, 18.4, 18.7, 18.6, 18.5, 18.4, 18.3, 18.5, 18.6, 19.1, 20.0, 20.3, 19.8, 19.1, 18.9, 18.8, 18.6, 18.7, 18.8, 18.6, 18.6, 18.3, 18.4, 18.3, 18.7, 18.6, 18.7, 18.5, 18.6, 18.4, 18.4, 18.2, 18.2, 18.4, 18.4, 18.4, 18.6, 18.4, 18.7, 18.8, 18.7, 18.7, 18.6, 18.4, 18.8, 18.7, 18.7, 18.9, 19.1, 19.2, 19.0, 19.2, 19.1, 18.8, 18.6, 18.7, 18.7, 18.8, 18.7, 18.5, 18.5, 18.3, 18.5, 18.4, 18.5, 18.4, 18.4, 18.4, 18.1, 18.6, 18.4, 18.7, 19.1, 19.3, 19.4, 19.3, 18.9, 19.2, 19.4, 19.5, 19.7, 19.6, 19.6, 19.1, 19.0, 18.7, 18.6, 18.9, 19.0, 19.3, 19.4, 18.9, 19.0, 19.4, 19.6, 19.5, 19.5, 19.1, 19.3, 19.2, 19.1, 19.3, 18.4, 18.6, 19.0, 19.1, 19.2, 19.2, 19.2, 18.9, 18.9, 19.0, 19.2, 19.2, 19.1, 18.9, 18.9, 19.2, 19.2, 19.1, 18.8, 19.1, 19.3, 19.3, 19.4, 19.5, 19.0, 18.6, 18.8, 19.0, 18.9, 18.1, 18.1, 18.3, 17.4, 17.7, 18.2, 17.9, 17.8, 18.2, 18.2, 18.6, 18.3, 18.6, 18.6, 18.8, 18.9, 18.8, 19.0, 19.1, 19.2, 19.5, 19.4, 19.3, 19.4, 19.4, 19.6, 19.7, 19.7, 19.6, 19.4]
t2 = [16.1, 16.7, 17.0, 17.3, 17.3, 17.7, 17.7, 17.4, 17.3, 17.2, 17.4, 17.6, 17.6, 17.7, 17.8, 17.7, 17.6, 17.4, 17.2, 17.1, 17.2, 17.0, 17.1, 17.4, 17.4, 16.9, 16.7, 16.7, 16.7, 17.6, 18.0, 17.3, 16.8, 17.0, 17.2, 17.0, 17.3, 17.3, 17.1, 17.1, 17.0, 16.9, 16.8, 17.0, 17.3, 17.0, 17.1, 17.1, 17.1, 16.9, 16.8, 16.8, 16.7, 16.9, 16.7, 17.0, 16.6, 16.5, 16.5, 16.7, 16.8, 16.8, 16.8, 16.8, 16.9, 16.8, 16.9, 16.8, 16.8, 16.9, 16.9, 16.9, 17.0, 17.0, 16.8, 16.9, 16.9, 16.8, 16.8, 16.8, 17.0, 16.9, 16.9, 16.8, 16.9, 16.8, 16.8, 16.8, 16.5, 16.6, 16.8, 17.1, 16.9, 16.8, 16.8, 16.9, 16.8, 16.9, 16.9, 16.7, 16.8, 16.7, 16.5, 16.8, 16.8, 16.9, 16.8, 17.0, 17.0, 17.0, 16.9, 16.3, 16.5, 17.0, 16.7, 16.8, 16.6, 16.7, 16.7, 16.8, 16.6, 16.4, 16.5, 16.5, 16.5, 16.6, 16.6, 16.5, 16.5, 16.7, 16.8, 16.9, 17.7, 18.4, 19.3, 19.6, 19.8, 20.5, 21.1, 21.4, 21.8, 22.2, 22.7, 22.7, 23.0, 23.2, 23.6, 23.7, 23.8, 23.7, 23.8, 24.3, 24.2, 24.2, 24.3, 24.4, 24.3, 24.3, 24.6, 24.7, 24.9, 25.0, 25.4, 25.4, 25.3, 25.2, 25.3, 25.3, 25.4, 25.3, 25.3, 25.4, 25.4, 25.5, 25.6, 25.5, 25.6, 25.6, 25.5, 25.5, 25.0, 25.0, 25.0, 24.9, 24.8, 24.8, 24.4, 23.9, 23.7, 23.5, 23.5, 23.1, 23.2, 23.0, 23.0, 17.9, 15.3, 12.9, 12.9, 12.6, 11.9, 11.4, 11.3, 12.7, 18.2, 19.9, 20.5, 20.9, 21.1, 21.5, 21.9, 22.0, 21.8, 21.7, 21.7, 21.6, 21.5, 21.4, 21.3, 21.4, 21.3, 21.3, 21.3, 21.3, 21.4, 21.3, 21.3, 21.2, 21.3, 21.4, 21.4, 21.2, 21.0, 21.1, 21.0, 21.1, 21.0, 21.0, 21.0, 20.9, 21.0, 21.0, 21.1, 20.9, 21.0, 21.0, 21.2, 21.0, 21.0, 21.1, 21.3, 21.3, 21.4, 21.6, 21.6, 21.7, 21.5, 21.3, 21.5, 21.5, 21.3, 21.2, 21.2, 21.3, 21.2, 21.1, 21.0, 21.5, 21.5, 21.8, 21.9, 21.5, 21.0, 21.2, 21.1, 21.1, 21.1, 21.2, 21.2, 21.2, 21.4, 21.6, 21.8, 21.4, 21.5, 21.6, 21.5, 21.9, 21.9, 21.8, 21.4, 21.5, 21.3, 21.4, 21.2, 21.2, 21.0, 21.2, 21.3, 21.5, 21.5, 20.9, 20.9, 21.0, 20.9, 20.8, 20.7, 20.8, 20.5, 20.5, 20.5, 20.5, 20.2, 20.4, 20.6, 20.4, 20.4, 20.3, 20.5, 20.6, 20.7, 20.5, 20.5, 20.3, 20.3, 20.0, 20.0, 19.8, 20.0, 20.0, 20.0, 20.0, 20.0, 19.8, 19.7, 19.8, 19.7, 19.8, 19.7, 19.5, 19.5, 19.6, 19.8, 19.7, 19.6, 19.2, 19.2, 19.6, 19.9, 19.7, 19.5, 19.7, 19.8, 19.7, 19.6, 19.6, 19.8, 19.7, 19.9, 19.6, 19.4, 19.0, 19.3, 19.6, 19.6, 19.5, 19.3, 19.1, 19.0, 19.2, 19.1, 19.0, 19.0, 19.3, 19.3, 19.2, 19.4, 19.6, 19.6, 19.5, 19.4, 19.5, 19.1, 19.0, 18.9, 19.3, 19.5, 19.0, 18.8, 18.9, 19.1, 18.9, 19.0, 19.1, 19.0, 18.9, 18.9, 18.8, 18.9, 18.8, 18.9, 18.9, 19.1, 19.1, 19.1, 19.0, 19.0, 19.0, 19.0, 19.0, 19.0, 19.2, 19.3, 19.4, 19.6, 20.1, 20.6, 20.5, 20.8, 21.8, 22.0, 21.6, 21.0, 21.0, 20.9, 20.8, 20.8, 20.8, 20.5, 20.4, 20.3, 20.1, 19.9, 19.9, 19.9, 19.8, 19.8, 19.7, 19.7, 19.6, 19.7, 19.7, 19.5, 19.5, 19.5, 19.6, 19.7, 19.9, 19.8, 19.7, 19.8, 19.8, 19.9, 19.8, 19.8, 19.8, 19.8, 19.8, 19.8, 19.8, 19.8, 19.8, 19.7, 19.7, 19.6, 19.7, 19.7, 19.6, 19.5, 19.4, 19.4, 19.3, 19.3, 19.2, 19.3, 19.2, 19.1, 19.4, 19.5, 19.4, 19.3, 19.7, 19.7, 19.8, 19.9, 19.6, 19.7, 19.9, 20.0, 20.2, 20.1, 20.0, 19.8, 19.8, 19.8, 19.7, 19.6, 19.7, 19.9, 19.9, 19.6, 19.5, 19.6, 19.6, 19.5, 19.5, 19.4, 19.5, 19.6, 19.6, 19.5, 19.2, 19.3, 19.4, 19.3, 19.4, 19.3, 19.2, 19.3, 19.2, 19.2, 19.4, 19.6, 19.6, 19.6, 19.6, 19.7, 19.8, 19.7, 19.6, 19.7, 20.0, 19.9, 19.9, 20.0, 19.7, 19.7, 19.8, 19.7, 19.7, 19.3, 19.3, 19.3, 19.0, 18.9, 19.0, 19.0, 18.9, 18.9, 18.9, 19.4, 19.2, 19.5, 19.3, 19.5, 19.4, 19.5, 19.6, 19.7, 19.7, 19.9, 20.1, 20.0, 20.0, 20.1, 20.1, 20.0, 20.1, 20.2, 20.0]
t3 = [-0.4, -0.6, -0.6, -0.4, -0.4, -0.5, -0.6, -0.1, -1.8, -1.9, -1.9, -2.0, -2.0, -0.2, -0.4, -0.5, -0.4, -1.8, -1.6, -1.4, -1.4, -1.7, -1.6, -1.5, -1.3, -1.4, -1.7, -2.0, -0.1, -0.2, -0.3, -0.2, -2.0, -0.1, -0.1, -1.7, -1.6, -2.0, -0.3, -0.4, -0.2, -0.2, -0.2, -0.1, -0.4, -0.3, -0.4, -0.6, -0.4, -0.2, -0.2, -0.2, -0.1, -1.9, -1.8, -1.9, -1.7, -1.7, -1.9, -2.0, -0.1, -0.3, -0.3, -0.3, -0.3, -0.3, -0.3, -0.1, -0.1, -0.4, -0.4, -0.4, -0.4, -0.3, -0.2, -0.3, -0.3, -0.1, -0.3, -0.1, -0.3, -0.3, -0.4, -0.5, -0.5, -0.4, -0.5, -0.5, -1.9, -0.2, -0.4, -0.6, -0.5, -0.5, -0.4, -0.3, -0.4, -0.6, -0.6, -0.2, -0.5, -0.5, -0.1, -0.6, -0.8, -0.9, -0.9, 0.2, 0.1, 0.3, 0.1, 0.0, 0.6, 0.7, 0.9, 1.0, 0.4, 1.0, 1.0, 1.6, 1.3, 1.0, 1.3, 1.3, 1.9, 3.0, 3.6, 4.0, 3.7, 5.8, 6.5, 8.9, 7.9, 7.3, 8.6, 9.6, 10.0, 12.2, 16.6, 24.9, 27.7, 26.7, 31.1, 31.3, 33.9, 35.7, 36.9, 40.7, 36.0, 27.0, 29.6, 32.1, 31.2, 33.1, 33.2, 30.2, 27.9, 23.6, 22.4, 28.4, 33.4, 31.3, 25.6, 34.8, 36.6, 33.4, 33.7, 33.5, 27.2, 23.2, 24.0, 25.6, 19.6, 26.2, 28.5, 31.5, 27.6, 31.0, 27.9, 18.3, 14.8, 14.4, 15.7, 21.5, 23.8, 30.6, 27.6, 27.0, 27.6, 25.4, 15.4, 12.0, 10.8, 9.5, 9.1, 10.7, 16.2, 19.1, 14.6, 13.5, 13.7, 9.7, 8.0, 7.1, 6.6, 6.6, 6.4, 6.1, 5.6, 5.0, 4.6, 4.1, 3.7, 3.5, 3.2, 3.1, 2.9, 2.6, 2.4, 2.1, 2.0, 2.1, 1.9, 1.7, 1.7, 1.6, 1.3, 1.2, 1.2, 1.0, 1.0, 0.9, 0.8, 0.8, 0.7, 0.6, 0.4, 0.5, 0.3, 0.2, 0.2, 0.1, 0.1, 0.1, -0.9, -0.9, -0.8, -0.9, -0.8, -0.9, -0.8, -0.7, -0.6, -0.4, -0.4, -0.4, -0.4, -0.4, -0.4, -0.3, -0.4, -0.3, -0.2, -0.2, -2.0, -0.2, -0.1, -2.0, -2.0, -1.9, -1.9, -1.8, -1.8, -1.7, -1.8, -1.8, -1.8, -1.7, -1.7, -1.7, -1.6, -1.6, -1.6, -1.6, -1.6, -1.6, -1.6, -1.6, -1.5, -1.5, -1.5, -1.5, -1.5, -1.4, -1.3, -1.4, -1.3, -1.3, -1.3, -1.3, -1.2, -1.2, -1.3, -1.3, -1.3, -1.3, -1.4, -1.3, -1.4, -1.4, -1.4, -1.4, -1.4, -1.5, -1.5, -1.5, -1.4, -1.4, -1.4, -1.5, -1.5, -1.6, -1.6, -1.6, -1.6, -1.6, -1.7, -1.7, -1.7, -1.7, -1.7, -1.7, -1.6, -1.7, -1.8, -1.7, -1.8, -1.8, -1.8, -1.8, -1.9, -1.8, -1.9, -2.0, -2.0, -2.0, -0.1, -0.2, -0.3, -0.4, -0.4, -0.4, -0.5, -0.6, -0.6, -0.6, -0.7, -0.7, -0.8, -0.8, -0.7, -0.6, -0.7, -0.7, -0.7, -0.8, -0.8, -0.7, -0.7, -0.7, -0.6, -0.8, -0.7, -0.7, -0.8, -0.9, -0.9, 0.0, 0.1, 0.1, 0.3, 0.3, 0.3, 0.6, 0.9, 1.0, 1.1, 1.3, 1.4, 1.7, 1.9, 2.1, 2.1, 2.4, 2.6, 2.8, 2.9, 3.2, 3.5, 3.8, 4.2, 4.6, 4.9, 5.0, 5.1, 5.2, 5.1, 4.9, 4.9, 5.1, 5.6, 6.2, 7.0, 7.3, 7.4, 8.3, 9.3, 9.4, 10.4, 11.1, 10.8, 10.6, 10.4, 10.1, 9.8, 8.9, 8.6, 8.6, 8.0, 7.7, 7.5, 7.3, 7.1, 7.4, 7.4, 7.5, 7.4, 7.4, 7.3, 7.3, 6.9, 6.9, 7.2, 7.4, 7.4, 7.6, 7.4, 7.6, 7.3, 7.0, 6.8, 6.5, 6.3, 6.6, 6.4, 6.3, 6.3, 6.6, 6.5, 6.4, 6.2, 6.1, 5.9, 5.8, 5.9, 5.7, 5.7, 5.7, 5.7, 5.7, 5.6, 5.7, 5.9, 6.0, 5.9, 5.9, 5.8, 5.7, 5.7, 5.5, 5.4, 5.5, 5.3, 5.3, 5.3, 5.3, 5.2, 5.0, 4.7, 4.8, 4.8, 4.7, 4.6, 4.6, 4.5, 4.5, 4.5, 4.4, 4.4, 4.4, 4.2, 4.2, 4.1, 4.1, 4.0, 3.9, 3.8, 3.8, 4.1, 3.8, 3.7, 3.7, 3.6, 3.5, 3.4, 3.4, 3.5, 3.4, 3.5, 3.3, 3.4, 3.5, 3.5, 3.3, 3.3, 3.3, 3.3, 3.3, 3.3, 3.2, 3.2, 3.2, 3.2, 3.2, 3.2, 3.1, 3.2, 3.1, 2.9, 3.0, 2.9, 3.1, 3.3, 3.3, 3.4, 3.5, 3.4, 3.4, 3.4, 3.4, 3.4, 3.5, 3.3, 3.4, 3.4, 3.3, 3.4, 3.4, 3.3, 3.4, 3.4, 3.4, 3.4, 3.4, 3.4, 3.3, 3.3, 3.3, 3.3, 3.2]

send_data(h1,date, 71)
send_data(h2,date,72)
send_data(h3,date, 73)
send_data(t1,date,68)
send_data(t2,date, 69)
send_data(t3,date,70)
```

**code6** The code above shows how to send data to the surver and receive what user sent to it.

<img width="1343" alt="Screenshot 2023-12-09 at 11 58 04" src="https://github.com/hasmhib/unit2-2024/assets/142702159/aeb02410-2a0f-42d6-a239-7ce4014e3ff3">

**fig8** This picture shows the reslut of the send_data function and proof that I could send data to the surver.

# Criteria D: Functionality
A 7 min video demonstrating the proposed solution with narration

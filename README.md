<img width="max" alt="Screenshot 2023-12-14 at 2 59 21 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/dfa23af2-fb53-4291-b06d-0bfbe748497d">

# Unit 2: A Distributed Weather Station for ISAK
  
## Criteria A: Planning
John, a student at an international boarding high school on top of the hill in Japan, faced a dilemma of spending over an hour trekking to the nearest supermarket for vegetables, including tomatoes and beans. Eager to optimize his time and explore different activities, he decided to produce vegetavles on his own. However, John recognized the importance of providing an ideal environment for his plants to thrive. To make an informed decision, he opted to gather data on temperature and humidity. With this information, he aimed to identify the most efficient location within his room for optimal plant growth. Concerned about the potential loss of his data due to any circumstances, John want his data to keep it somewhere safe. This way, even if the computer's data loss, he can recover his valuable information and continue refining his indoor gardening project.

## Proposed Solution
Considering the client requirements an adequate solution includes a low cost sensing device for humidity and temperature and a custom data script that process and anaysis the samples acquired. For a low cost sensing device an adequate alternative is the DHT11 sensor[^1] which is offered online for less than 5 USD and provides adequare precision and range for the client requirements (Temperature Range: 0°C to 50°C, Humidity Range: 20% to 90%). Similar devices such as the DHT22, AHT20 or the AM2301B [^2] have higher specifications, however the DHT11 uses a simple serial communication (SPI) rather than more eleborated protocols such as the I2C used by the alternatives. For the range, precision and accuracy required in this applicaiton the DHT11 provides the best compromise. Connecting the DHT11 sensor to a computer requires a device that provides a Serial Port communication. A cheap and often used alternative for prototyping is the Arduino UNO microcontroller [^3]. "Arduino is an open-source electronics platform based on easy-to-use hardware and software"[^4]. In additon to the low cost of the Arduino (< 6USD), this devide is programable and expandable[^1]. Other alternatives include diffeerent versions of the original Arduino but their size and price make them a less adequate solution.

Considering the budgetary constrains of the client and the hardware requirements, the software tool that I proposed for this solution is Python. Python's open-source nature and platform independence contribute to the long-term viability of the system. The use of Python simplifies potential future enhancements or modifications, allowing for seamless scalability without the need for extensive redevelopment [^5][^6]. In comparison to the alternative C or C++, which share similar features, Python is a High level programming language (HLL) with high abstraction [^7]. For example, memory management is automatic in Python whereas it is responsability of the C/C++ developer to allocate and free up memory [^7], this could result in faster applications but also memory problems. In addition a HLL language will allow me and future developers extend the solution or solve issues proptly.  

**Design statement**

Our team will create a device and program that will calculate both humiditiy and temperature in a room of John's house. To do this, we will use a Raspberry Pi 4 and three DHT_11 sensors to collect the humidity and temperature. The program will upload the collected data onto a server in real-time to reinforce the reliability and validity of our calculated data. We will use the device to record the humidity and temperature inside of a room for 48 hours, and some spots on campus will be able to access the data through an online server anytime using a granted access token. Further, John can use the data collected to compare to local data information on optimal humidity and temperature. This project will take approximately 4 weeks and will be evaluated according to the criteria set above.

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

The use of data science in climate research has a impact on our understanding of environmental issues. By handling large datasets and advanced computer techniques, data science enables us to identify problems, make predictions, and understand the complex interactions within our environment. This leads us to more sensitive decision-making and policy development.

1. How does our use of technology shape our understanding of the environment?
 
   Our use of technology, particularly in data collection and analysis, shapes our understanding of the environment by providing detailed informations that were previously npt able to have connections with. Technologies like remote sensing, Senosor devices, and advanced computer models allow 
   us to monitor environmental changes in real-time, predict future scenarios, and assess the effectiveness of intervention strategies. 
  
2. What responsibilities do we have as technologists when it comes to handling personal data related to our living spaces?

   As technologists, we have a responsibility to handle personal data with care, especially when it comes to living spaces such as this John's case. This involves ensuring data privacy, securing data against unauthorized access, and being transparent about how the data is used to clients. 
   These ethical considerations include respecting individual privacy, making sure to informimg consent, and considering the impact of data collection on communities. These challenges in balancing the need for comprehensive environmental data with the right to personal privacy.

3. What cultural and contextual factors might impact our interpretation of the results, especially when comparing our local readings with those from the campus?
   
   Interpreting environmental data requires an understanding of cultural and contextual factors, especially when comparing data from different locations, like local readings and remote servor on a campus. Cultural perceptions of climate change and local environmental factors can influence how 
   data is interpreted and used. For instance, data rising temperatures may be perceived differently in a places that traditionally experiences hotter climates compared to one that does not.
   
# Criteria B: Design

## Flow diagram


<img width="max" alt="Screenshot 2023-12-12 at 17 52 19" src="https://github.com/hasmhib/unit2-2024/assets/142702159/40d01f12-8573-425e-9361-bd0272ee90e9">

**fig1** flow diagram of the function, create_new_sensor

This flow diagram shows the function called create_new sensor. This function is for creating a new sensor in the API. By using login function, user can get the access token.
This functioin makes it available to post the data with new id.



<img width="max" alt="Screenshot 2023-12-12 at 17 40 26" src="https://github.com/hasmhib/unit2-2024/assets/142702159/efae5279-ec76-474c-9c53-215ba8ae7bc1">


**fig2** flow diagram of the function, get_sensor.

This flow diagram shows the function called get_sensor. By using request library, get data from API and arrange them as json file. Only pick the value with the specific sensor_id, and add to the list. The list is for drawing graph.


<img width="max" alt="flow diagram" src="https://github.com/hasmhib/unit2-2024/assets/142702159/56abd646-f1b5-4b0b-978f-686a90a44165">

**fig3** flow diagram of the function
This flow diagram shows the function called get_sensor_datatime. This function is for getting time when the data from specific sensor_id is taken.

## System Diagram

![HL](https://github.com/comsci-uwc-isak/unit2_2023/assets/53995212/4891d5e9-b8ab-46ed-bd75-b606e25e3383)

**fig4** shows the system diagram for the proposed solution (**HL**). The indoor variables will be measured using an Arduino and three DHT11 sensors located inside a room. Three sensors are used to determine more precisely the physical values and include measurement uncertainty. The outdoor variables will be requested to the remote server using a GET request to the API of the server at ```192.168.6.153/readings```. The local values are stored in a CSV database locally and a backup copy will be store in the remote server using the **Weather API**. 


## Record of Tasks
| Task No | Planned Action                                                | Planned Outcome                                                                                                 | Time estimate | Target completion date | Criterion |
|---------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------|------------------------|-----------|
| 1       | Write the Problem context                        | a clear defenition of the problem | 10min         | Nov 22                 | A         |
|2| 	Write the list of materials| Have a full list of materials | 5min | Nov 28 | B
|3| 	Brainstorm and write ploblem definition| A clear design statement that suits the need of the client | 20min | Nov 29 | A |
|4 | make a code for arduino with Arduino IDE | define each sensor and | 30 min | December 2 | C | 
|5| define read_arduino() | read data from arduino| 1 hour | Decemver 2 | C | 
|6| define send_csv() | send data I got from read_arduino() to reading_csv| 3 hours | December 2 | C | 
|7| define main()| set time to get temperature and humidity |  2 hours | December 2  | C | 
|8| define login() | require username and password to see the data to keep it safely| 1 hour | December 3 | C | 
|9| define send_data() | add data(datetime,sensor_id and value) to url | 3 hour | December 3 | C | 
|10| make the function to get the list from csv file | organize the data to draw graph | 2 hour | December 4 | C | 
|11| draw the flow diagram | make it claery how to organize the code | 1 hour | December 3 | C |
|12| collect the data from sensors | get data to analyze  | 48 hour | December 4-6 | C  | 
|13| draw graphs of each sensor| See the change of value specificly | 3 hour | December 7 | C | 
|14| draw smooth graphs of each sensor | See the cange of the value simply | 2 hour | December 8 | C | 
|15| draw graphs of each remote sensors | See the cange of the value specificly | 2 hour | December 8-9 | C | 
|16| analyze the data from remote sensors | to draw the graph to easy to compare to other one | 3 hour | December 9 | C | 
|17| draw graphs of mean, median range, maximum and minimum | clienct can compare to other data easisly | 2 hour | December 9 | C | 
|18| draw graphs of standard deviation | See the data variationb easily  | 4 hour | December 10 | C | 
|19| draw  prediction graphs | show the prediction for 12 hours | 3 hour | December 11 | C | 
|20| make a poster | visualize the result and analysis of the project | 2 hour | December 11 | C  | 
|21| draw graphs of standard deviation | See the data variationb easily  | 4 hour | December 11-12 | C  |
|22| write the explanations of each code | client can see how we worked to follow the demand  | 8 hour | December 12-14 | C  | 
|23| Ayane caught influenza | the efficiency reduced by half | 💀 | December 12 | 💀 | 
|24| Yosuke caught influenza as well | the end of our project | 💀 | December 13 | 💀 | 




























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

# Data storing
## login and create a new sensor

I defined a function called login that facilitates user authentication to a web service. The function takes no arguments and is responsible for generating and returning an authorization token required for subsequent secured interactions with the service. Inside the function, a dictionary user is created with a predefined username and password. The requests.post method is then utilized to send a POST request to the specified URL ('http://192.168.6.153/login') with the user credentials provided as json data. The response from the server is parsed as json, and the access token, a crucial element for authorization, is extracted. Finally, the function constructs and returns a dictionary with an "Authorization" key, incorporating the obtained access token using the Bearer token authentication scheme. This token can be subsequently used in the headers of other HTTP requests to access secured endpoints on the web service.


**code1** The function called login.
```.py

import requests

def login():
    user = {"username": ***, "password": ***}
    r = requests.post('http://192.168.6.153/login', json=user)
    access_token = r.json()["access_token"]
    return {"Authorization": f"Bearer {access_token}"}

```

Next, I defined the function create_new_sensor to create a new sensor in the URL. The function requires the name of the sensor, sensor type (in this case, Temperature or Humidity), location where the user wants to put the sensor, and unit (C or %). By using the login function, the user can log in to the IP ("192.168.6.153"). The requests.post method is utilized to send a POST request with the dictionary including the details the user input as a JSON file and the return of the login function as headers. In order to ensure the user could receive what they send to the server, I set the code so that the user can see the server's response with printing ans (equal to requests.post(f"http://{ip}/sensor/new", json=sensor, headers=headers)) as a JSON file. The results are presented in what I got from the function section, demonstrating the successful creation of new sensors with different specifications.


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

In the code, I am using a function create_new_sensor repeatedly to create different sensor objects, each with different attributes such as type, owner ID, unit, location, and name. 

**code2** The function called create_new_sensor.

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

# 1. The client wants The solution that provides a visual representation of the Humidity and Temperature values inside a dormitory (Local) and outside the house (Remote) for a period of minimum 48 hours.

We fulfilled success criteria 1 by developing a system to collect and visualize humidity and temperature data both locally and remotely over 48 hours. For visualization, I created line graphs with Matplotlib, presenting clear informations in environmental conditions. This was enhanced with a smoothing function to make clients easier to read. Despite some sensor issues, the adapted graphs effectively provided a comprehensive analysis of the conditions, meeting the criteria of delivering visual representations of the data over the required duration.

## Getting data every 5 min for 48 hours.

I start by noting the current time using datetime.now() and set the total duration for data collection to 48 hours. The code then enters a loop that continues until the total duration of 48 hours is reached by using while loop. Inside this loop, there's another while loop for collecting data every 5 minutes. This is achieved by setting an end time 5 minutes ahead of the current time. Within this 5-minute loop, I read data from an Arduino device using the read_arduino function and save this data to a CSV file with save_csv. After each data collection, the program waits for 300 seconds (5 minutes) before collecting data again. Once the 48 hours are up, the program prints a message saying "Data collection complete.

```.py
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


# Plotting the graphs for local and remote humidity and temperature

## Separate the columns

First, I needed to separate the columns of my CSV files and create columns. By renaming the columns, I made the DataFrame more understandable and easier to manipulate for future developers. For example, if you want to access the data for 'Room Humidity 1', you can simply use data['Room Humidity 1'], thanks to this clear and descriptive naming.

The CSV file contains data in a comma-separated format. Each line in the file represents a record with different data points. 

This line consists of a date, a time, humidity of sensor1, temperature of sensor1, humidity of sensor2, temperature of sensor2, humidity of sensor3 and temperature of sensor3,  each separated by a comma.

After loading the data, the DataFrame has default of column headers (0, 1, 2, ...). To make the data easier to work with, I assigned names to each column to makes other developers easy to understand when they see my code. 
I did this by setting the data.columns attribute.

**code1** Shows the part of the program to assigning column names
```.py
data.columns = ['Date', 'Time', 'Room Humidity 1', 'Room Temperature 1',
                'Room Humidity 2', 'Room Temperature 2', 'Room Humidity 3', 'Room Temperature 3'
```

This line replaced the default headers with the names I chose, corresponding to the type of data in each column: 'Date', 'Time', and then converting 'Room Humidity' and 'Room Temperature' labels for the various sensors.
By renaming the columns and separating it, I made the DataFrame more understandable and easier to manipulate for future developers.

## Plotting the graph of local humidity and temperature

After separating the columns, I plot the graphs for the local humidity and temperature data recorded during 48 hours.

On the first row of the code, I am connecting the 'Date' and 'Time' columns of the DataFrame. This is because to create a single string for each row that represents both the date and time.

In this code, I'm creating a detailed line graph to visualize room temperature data over time using Matplotlib in Python. I set the figure size and plot three humidity and temperature datasets, each representing different room humidity and temperatures, with different colors. The y-axis limits are adjusted to show the entire range of humidity and temperature data. To make a graph more easier to visualize, I add labels, a title, a legend, and a grid. The x-axis dates are formatted to display both the date and time, and I use auto-formatting features to ensure these labels are clear and non-overlapping. This approach allows me to effectively present a visual comparison of humidity and temperature changes over time in different rooms.


**code2** Shows code used for plotting graphs for humidity data recorded during 48 hours.
```.py
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

***code3** Shows code used for plotting graphs for temperature data recorded during 48 hours.
```.py
data['Datetime'] = pd.to_datetime(data['Date'] + ' ' + data['Time'])

plt.figure(figsize=(15, 6))

plt.plot(data['Datetime'], data['Room Temperature 1'], label='Room Temperature 1', color='orange')

plt.plot(data['Datetime'], data['Room Temperature 2'], label='Room Temperature 2', color='purple')

plt.plot(data['Datetime'], data['Room Temperature 3'], label='Room Temperature 3', color='brown')

plt.ylim(data[temperature_types].min().min(), data[temperature_types].max().max())

plt.xlabel('Date and Time')
plt.ylabel('Temperature (°C)')
plt.title('Temperature Over Time')
plt.legend()
plt.grid(True)

plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m-%d %H:%M'))
plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
plt.gcf().autofmt_xdate()

plt.show()
```

**fig2** Shows the raw graph of humidity data recorded during 48 hours by using **code10**
<img width="max" alt="Screenshot 2023-12-12 at 11 30 57 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/135507c4-9b9f-4539-9b7b-d2317d5ba44b">

**fig3** Shows the raw graph of temperature data recorded during 48 hours by using **code11**
<img width="max" alt="Screenshot 2023-12-12 at 11 31 56 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/b943561e-3fb2-40af-a152-367dd1994482">

## Smoothing these raw graphs to visualize the data easily

The clients wants easy visualization, as may difficult for them only the raw graph. Therefore, in this code, I define a function named smoothing to apply a simple moving average smoothing technique to a list of values so that the clients can visualize more easily. The function takes two parameters, a list of values and size_window parameter with a default value of 5. I used through the list in steps of size_window, calculating the mean of each window of values. I sum the values in the current window and divide by the window size to get the average. I then store a tuple containing the window's starting index and the calculated mean in smoothed_values. This results in a list of tuples, each has the average value of a segment of the list.


**code4** show the code to make a smooth graph
```.py
def smoothing(values:[], size_window:int=5):
    smoothed_values = []
    for i in range(0, len(values), size_window):
        window_mean = sum(values[i:i + size_window]) / size_window
        smoothed_values.append((i, window_mean))

    return smoothed_values
```

**fig4** Shows the smoothed version of humidity data recorded during 48 hours
<img width="max" alt="Screenshot 2023-12-13 at 7 06 02 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/e0449b70-1f02-4908-b5c1-974bf28bd61e">

**fig5** Shows Shows the smoothed version of temperature data recorded during 48 hours
<img width="max" alt="Screenshot 2023-12-13 at 7 08 36 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/250200be-6be4-4945-bc34-15bf555f10b3">

## Plot graphs of remote humidity and temperature

The client wants the visual representation of the Humidity and Temperature values outside the house (Remote) for a period of minimum 48 hours as well. Therefore, I created a graph with the data from remote humidity and temperature. Firdstly, I needed to get a data from each sensors, and I also needed to track when each sensor reading was taken. This is done by using functions get_sensors and get_sensors_datetime. After this, I used Matplotlib and GridSpec to create a comprehensive visualization of sensor data.

get_sensors :In get_sensors, I used sensor readings for specified IDs. I initialize a dictionary to store readings for each ID and then identify through all recordings, adding the values to the corresponding lists in the dictionary if the sensor ID matches. This function organizes sensor data by ID, making it easy to access and analyze specific sensor readings.

**code5** shows the code to get the data from specific sensor.

```.py
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
```

get_sensors_datetime : I follow a similar approach but I focus on extracting datetime information. I create a list and append the datetime of each relevant recording, allowing me to track each sensor reading taken. This is used for time series analysis or when I need to use sensor readings with specific time points. 

**code6** shows the codes to get data with specific time points.
```.py
def get_sensors_datetime(ids:list[int]=[1]):
    recordings = get_readings()
    sensor_datetime = []
    for rec in recordings:
        id_sensor = rec['sensor_id']
        if id_sensor in ids:
            value = rec['datetime']
            sensor_datetime.append(value)

    return sensor_datetime
```

In this code, I used Matplotlib and GridSpec to create a comprehensive visualization of sensor data. I first retrieve sensor readings using a custom library and calculate statistical values like mean and standard deviation. The main plot, spanning a large grid, illustrates the range, mean, and minimum and maximum of combined data from selected sensors. This is done using fill_between for range visualization and line plots for mean and extremes, providing a clear visual summary of sensor data over time. Additionally, I create smaller subplots for each sensor, plotting their individual readings in different colors and styles for detailed analysis. These subplots offer a focused view on each sensor's data. The x-axis across the plots is formatted to display time using mdates, makes client easier to visualise the data. Finally, I display the entire figure, showing both the overall datas and specific details of the sensors' readings in a unified layout.

**code7** Shows code used for plotting graphs for remote humidity (sensors 1, 3, 5)
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

**code8** Shows code used for plotting graphs for remote temperature (sensors 0, 2, 4)
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
box4.plot(x_values, sensors[4], color="yellow", marker='o', linestyle='-', markersize=2, linewidth=2)We fulf
box4.set_title("Sensor 4 (Temperature)")
plt.grid(True)

ax1.xaxis.set_major_locator(mdates.AutoDateLocator())
plt.gca().xaxis.set_major_locator(mdates.AutoDateLocator())
fig.autofmt_xdate()

plt.show()
```

However, for remote humidity, it seems that sensor 3 is broken and not functioning properly. Therefore, I calculated range, mean, minimum, maximum and standard deviation of combined data from sensor 1,5 to make teh data more accurate and proper. 
This applies to remote temperature as well. For remote temperature, it seems that sensor 0 is broken and not functioning properly. Therefore, I calculated range, mean, minimum, maximum and standard deviation of combined data from sensor 2,4 to make teh data more accurate and proper.

**fig6** Shows the graph of sensors1,3,5 (humidity) and the analysis of sensors 1,5. This includes range, mean, minimum, maximum of combined data from selected sensors.
<img width="max" alt="Screenshot 2023-12-12 at 11 45 32 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/daf70e3b-d88f-40ff-84c5-e41cee7ade94">

**fig7** Shows the graph of sensors1,3,5 (humidity) and the standard deviation of combined data from selected sensors.
<img width="max" alt="Screenshot 2023-12-12 at 11 47 15 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/6d298be1-ca3c-47d3-82b6-030a716e1724">

**fig8** Shows the graph of sensors0,2,4 (temperature) and the analysis of sensors 2,4. This includes range, mean, minimum, maximumof combined data from selected sensors.
<img width="max" alt="Screenshot 2023-12-12 at 11 45 58 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/b2818635-fca8-4832-aff3-dd5d1b7fb1be">

**fig9** Shows the graph of sensors0,2,4 (temperature) and the standard deviation of combined data from selected sensors.
<img width="max" alt="Screenshot 2023-12-12 at 11 47 45 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/8b1fccef-3c46-4771-bd78-ea5e526f2f17">

# 2. The client requested that the local variables will be measured using a set of 3 sensors around the dormitory.

## get data from arduino
I defined a function named read_arduino to retrieve data from an Arduino device. This function utilizes the Serial library, providing the capability to distinguish and collect data from the Arduino. It requires parameters such as the port, which signifies the Arduino's name, baudrate, representing the communication speed, and timeout, specifying the duration for connection timeout. Three variables, namely d1, d2, and d3, are initialized as empty strings. However, as nothing is appended to them within the while loop, the loop persists indefinitely. Inside the loop, the readline method is invoked on the Arduino data. Notably, each sensor's data (d1, d2, and d3) should be received in succession, yet the current implementation reads the same data for each sensor in a loop. Furthermore, the code attempts to decode the binary data into a Unicode string using the UTF-8 encoding. UTF-8 is chosen for its ability to represent every character in the Unicode character set. It's worth noting that the code might have some logical issues, as the while loop conditions are not effectively checking the length of the data, and the variables d1, d2, and d3 are assigned the same decoded data.

**code1** The code shows how to read data from arduino.
```.py
def read_arduino():
    arduino = serial.Serial(port="/dev/cu.usbserial-10", baudrate=9600, timeout=0.1)
    d1,d2,d3 = "","",""
    while len(d1< 1):
        data = arduino.readline()
    while len(d2 < 1):
        data = arduino.readline()
    while len(d3 < 1):
        data = arduino.readline()
    d1 = data.decode("utf-8")
    d2 = data.decode("utf-8")
    d3 = data.decode("utf-8")
    return d1, d2, d3
```


## the sensor we used

**fig00** the Raspberry Pi 4 and three DHT_11 sensors

<img width="572" alt="Screenshot 2023-12-14 at 9 03 38" src="https://github.com/hasmhib/unit2-2024/assets/142702159/9f1e1240-7b97-405c-a4b7-c914afe16e7f">


## the environment we collected the data

**fig00** the location we put the sensor in John's room

<img width="649" alt="Screenshot 2023-12-14 at 9 03 06" src="https://github.com/hasmhib/unit2-2024/assets/142702159/3da431e5-be43-4ea2-896f-06366604501a">

# 3,6. The solution provides a mathematical modelling for the Humidity and Temperature levels for each Local and Remote locations. (linear model and non-lineal model), The solution provides a prediction for the subsequent 12 hours for both temperature and humidity.

I fulfilled the success criteria of providing a mathematical modeling and 12-hour prediction for humidity and temperature at both local and remote locations by implementing linear and quadratic regression models.

## Linear Regression Implementation

I defined a linear_regression function to calculate the slope and intercept for a linear fit. This function takes x (timestamps) and y (sensor data) as inputs and computes the coefficients of the linear equation.
Using this function, I applied linear regression to the sensor data.

**code00** Shows a part of a code to create a linear model of both humidity and temperature over 48 hours

```.py
def linear_regression(x, y):
    n = len(x)
    slope = (n * np.sum(x * y) - np.sum(x) * np.sum(y)) / (n * np.sum(x**2) - (np.sum(x))**2)
    intercept = (np.sum(y) - slope * np.sum(x)) / n
    return slope, intercept
```

Using the regression coefficients, I calculated the predicted values (y_pred) for the existing timestamps and extended this to predict future values for the next 12 hours.

```.py
for temp_type, color in zip(humidity_types, colors_humidity):
    x = data['DatetimeNumeric'].values
    y = data[temp_type].values

    slope, intercept = linear_regression(x, y)

    y_pred = slope * x + intercept

    future_timestamps = np.arange(x[-1], x[-1] + 12 * 3600, 3600)
    future_y_pred = slope * future_timestamps + intercept
```

**fig00** Shows the linear Model Humidity Over Time with Future Prediction
<img width="max" alt="Screenshot 2023-12-14 at 9 13 08 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/18cfb737-509a-4845-ae6f-c946a0c46690">

**fig00** Shows the linear Model Temperature Over Time with Future Prediction
<img width="max" alt="Screenshot 2023-12-14 at 9 13 36 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/55bf568e-c732-4e43-9cb6-77590c203cd0">

**fig00** Shows the humidity and Linear Model Over Time with Future Prediction
<img width="max" alt="Screenshot 2023-12-14 at 9 10 43 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/e4b65534-6e26-46b0-a0af-f0547a8c4a1a">

**fig00** Shows the temperature and Linear Model Over Time with Future Prediction
<img width="max" alt="Screenshot 2023-12-14 at 9 14 21 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/ac95ca5c-db63-4465-a0ce-33ca7b626dd2">


## Quadratic Regression imprementation

For a more detailed analysis, I employed quadratic regression using the fit_and_predict_quadratic function. 

**code00** Shows the part of the code to plot a quadaratic model for both humidity and temperature over time

I used Polynomial.fit(X, y, 2) from the numpy.polynomial.polynomial module to fit a quadratic polynomial to the data. The 2 indicates that I am fitting a polynomial of degree 2, which corresponds to a quadratic equation.
I also used the coefficients I got from the polynomial fitting to figure out the predicted values. This means I followed a usual formula for a quadratic equation: coefs[0] + coefs[1] * X + coefs[2] * X squared. In this formula, coefs[0] is the starting point of the line, coefs[1] is the slope of the line, and coefs[2] shows how the line curves.

```.py
def fit_and_predict_quadratic(X, y):
    coefs = Polynomial.fit(X, y, 2).convert().coef
    predictions = coefs[0] + coefs[1] * X + coefs[2] * X ** 2
    return predictions, coefs
```
I start a loop that goes through each temperature column one by one. The "enumerate" part helps me keep track of both the column's name (column) and its position (i).
I use the fit_and_predict_quadratic function I defined previously, and defined the curve of the model.

**code00** Shows the part of the code to plot a quadaratic model for temperature over time (This applies to humidity as well)

```.py
for i, column in enumerate(['Room Temperature 1', 'Room Temperature 2', 'Room Temperature 3']):
    X = data['Timestamp']
    y = data[column]
    predictions, coefs = fit_and_predict_quadratic(X, y)
    plt.plot(data['Datetime'], y, label=f'Original {column}', color=colors[i])
    plt.plot(data['Datetime'], predictions, label=f'Quadratic Fit for {column}', linestyle='--', color=colors[i])
    future_predictions = coefs[0] + coefs[1] * future_timestamps + coefs[2] * future_timestamps ** 2
    plt.plot(future_datetimes, future_predictions, label=f'12h Prediction for {column}', linestyle=':', color=colors[i])
```

**fig00** Shows the Quadratic Model Humidity Over Time with Future Prediction
<img width="max" alt="Screenshot 2023-12-14 at 9 41 15 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/343d2ff4-51c9-44a3-a3a9-981978a3e1de">

**fig00** Shows the Quadratic Model Temperature Over Time with Future Prediction
<img width="max" alt="Screenshot 2023-12-14 at 9 41 47 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/e1cdab7b-f99f-418c-a246-129abc3e6d75">

**fig00** Shows the Humidity and Quadratic Model Over Time with Future Prediction
<img width="max" alt="Screenshot 2023-12-14 at 9 42 09 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/04c324dc-381f-4485-a6c6-7c4765956bed">

**fig00** Shows the Temperature and Quadratic Model Over Time with Future Prediction
<img width="max" alt="Screenshot 2023-12-14 at 9 42 35 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/ece1b33a-210d-403b-a721-bde267a80795">


# 4. The solution provides a comparative analysis for the Humidity and Temperature levels for each Local and Remote locations including mean, standad deviation, minimum, maximum, and median.

In this code, I am working with a dataset to analyze and visualize humidity data. 

I calculate the mean of the humidity data. I do this for each row in my dataset by using data[humidity_types].mean(axis=1). This gives me the average humidity value for each moment or entry in my data.
I also calculate the standard deviation with data[humidity_types].std(axis=1). This tells me how much the humidity varies at different times.
I used the same ways to calculate maximum, minimum, and median as well. 
By doing all this, I get a good understanding of the humidity data, such as how high or low it usually is, how much it changes, and what the most common readings are. This is important for analyzing and visualizing the data effectively.
I implenetd the same methods in temperature as well, by using Matplotlib and GridSpec to create a comprehensive visualization of both humidity and tenperature data.


**code00** Shows the part of the code to calculate the mean, standard deviation, maximum, minimum, and median of humidity over 48 hours. 

```.py
ax1 = fig.add_subplot(gs[0])
mean_values = data[humidity_types].mean(axis=1)
std_values = data[humidity_types].std(axis=1)
max_values = data[humidity_types].max(axis=1)
min_values = data[humidity_types].min(axis=1)
median_values = data[humidity_types].median(axis=1)
```

**fig00** Shows the graph with the analysis of local humidity and temperature over 48 hours.
<img width="max" alt="Screenshot 2023-12-14 at 1 11 36 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/c2900f52-1a8c-45b9-8c94-2b6e8a4b3429">

**fig00** Shows the graph with the standard deviation of local humidity and temperature over 48 hours.
<img width="max" alt="Screenshot 2023-12-14 at 1 12 03 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/ff90dd7c-c0fa-4ee4-9882-9b662abb509f">


# 5. The Local samples are stored in a csv file and posted to the remote server as a backup.

To fulfill success criteria 5, I developed a system for data backup and remote transfer. First, I collected data using Arduino sensors, saving it every five minutes to a local CSV file over a 48-hour period. I then reorganized this data for clarity and extracted important information into a new CSV file. Finally, using a send_data function, I transmitted this data to a remote server, ensuring a reliable backup. This process ensured not only the local storage of data but also its safe transfer to a remote server, meeting the criteria for data backup and redundancy.

I defined save_csv which is designed to save data obtained from sensors, presumably related to humidity and temperature, into a CSV file named "reading.csv." The function takes tuple data as input, which contains three string elements, each representing the raw data from different sensors. Additionally, a default file name is set as "reading.csv." The function first prints the raw data for reference. It then generates a timestamp using the current date and time, and appends this timestamp to the CSV file. Subsequently, the function checks each sensor's data for the presence of a comma (','), indicating a humidity-temperature pair. If a comma is found, the data is split into humidity and temperature values, which are then written to the CSV file along with the timestamp. This process is repeated for all three sensors, and each set of humidity and temperature values is followed by two newline characters, creating a structured format in the CSV file.



**code1** The code shows how I send the data to csv file. 

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
```

**fig1** This picture shows how is data seved to reading.csv.
<img width="max" alt="Screenshot 2023-12-09 at 13 18 27" src="https://github.com/hasmhib/unit2-2024/assets/142702159/a0079af5-aa2b-4e88-a1ac-3615b5881b37">

I defined process_data to read data from a CSV file named "reading.csv" and processes it to create a new formatted CSV file named "formatted_data.csv." The function reads the lines from the input file, and for each set of eight lines, representing data from different sensors, it extracts and manipulates specific portions to achieve a desired format. The temporal information is adjusted, and unnecessary characters like commas and spaces are stripped. The processed data is then appended to an output list. Finally, the formatted data is written to the "formatted_data.csv" file. The function essentially takes raw data in a specific structure, refines it, and outputs a new CSV file with a modified format, potentially more suitable for analysis or presentation.

**code2** The codes show how to reorganize the data in reading.csv and make a list from the new csv file.
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
```

I designed the function below, "make_list" to rearrange the data from the "formatted_data.csv" file into a list format. It begins by opening the CSV file, reading each line sequentially. Empty lists are initialized for date, temperature sensors (t1, t2, and t3), and humidity sensors (h1, h2, and h3). Subsequently, a for loop is employed to iterate through the values separated by commas in each line, and these values are successively appended to their respective lists. The result is a well-organized list structure that can facilitate further data processing and analysis.

**code00** The codes show the function called make_list for making list.
```.py
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


**fig2** This picture shows how is the value reorganized in formatted_data.csv.
<img width="max" alt="Screenshot 2023-12-09 at 13 18 32" src="https://github.com/hasmhib/unit2-2024/assets/142702159/11a08261-0173-41a4-8004-8821f78318b9">

**fig3** This picture shows the result of the function, make_list.
<img width="max" alt="Screenshot 2023-12-09 at 13 30 50" src="https://github.com/hasmhib/unit2-2024/assets/142702159/bac41f82-0876-4884-a430-73d3e49d5900">

I created the function "send_data" with the purpose of transmitting data, encompassing a list of values, a date as a list, and a sensor ID, to a remote server at the address "http://192.168.6.153/reading/new". Within the function, a for loop iterates over the length of the value list. The "login" function is imported to retrieve authentication headers, and a new record is defined as a dictionary comprising datetime, sensor_id, and the current value. Utilizing the request post method, I send this new record as a JSON file along with the obtained headers. Additionally, I incorporated a print statement to display the sent data, ensuring transparency and verification of the data transmission process.
**code3** The code above shows how to send data to the surver and receive what user sent to it.
```.py
def send_data(value:list,date:list,sensor_id):
    for x in range(len(value)):
        header = login()
        new_records = {"datetime":date[x], "sensor_id": sensor_id, "value" : value[x]}
        # Send an HTTP POST request to a specified URL with the new_record data and headers
        r = requests.post('http://192.168.6.153/reading/new', json=new_records, headers=header)
        out = r.json()
        print("Response Content:",out)

date,h1,t1,h2,t2,h3,t3 = make_list()

send_data(h1,date, 71)
send_data(h2,date,72)
send_data(h3,date, 73)
send_data(t1,date,68)
send_data(t2,date, 69)
send_data(t3,date,70)
```

**fig4** This picture shows the reslut of the send_data function and proof that I could send data to the server.
<img width="max" alt="Screenshot 2023-12-09 at 11 58 04" src="https://github.com/hasmhib/unit2-2024/assets/142702159/aeb02410-2a0f-42d6-a239-7ce4014e3ff3">


# 7. The solution includes a poster summarizing the visual representations, model and analysis created. The poster includes a recommendation about healthy levels for Temperature and Humidity.
![back ground](https://github.com/hasmhib/unit2-2024/assets/142702159/a64e793d-e080-4468-bc7a-5fdb4d244bfe)



# Criteria D: Functionality
A 7 min video demonstrating the proposed solution with narration

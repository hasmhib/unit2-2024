![11e470e9022f4fc5b367429bcbb285bc](https://github.com/comsci-uwc-isak/unit2_2023/assets/53995212/1d14b1d3-ae39-4ef3-8ec9-3329630eacae)

# Unit 2: A Distributed Weather Station for ISAK
  
## Criteria A: Planning
John, a student at an international boarding high school on top of the hill in Japan, faced a dilemma of spending over an hour trekking to the nearest supermarket for vegetables, including tomatoes and beans. Eager to optimize his time and explore different activities, he decided to produce vegetavles on his own. However, John recognized the importance of providing an ideal environment for his plants to thrive. To make an informed decision, he opted to gather data on temperature and humidity. Armed with this information, he aimed to identify the most efficient location within his room for optimal plant growth. Concerned about the potential loss of his data due to any circumstances, John wantshis data to keep it somewhere safe. This way, even if the computer's data loss, he can recover his valuable information and continue refining his indoor gardening project.

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

## System Diagram

![HL](https://github.com/comsci-uwc-isak/unit2_2023/assets/53995212/4891d5e9-b8ab-46ed-bd75-b606e25e3383)

**Fig.1** shows the system diagram for the proposed solution (**HL**). The indoor variables will be measured using an Arduino and three DHT11 sensors located inside a room. Three sensors are used to determine more precisely the physical values and include measurement uncertainty. The outdoor variables will be requested to the remote server using a GET request to the API of the server at ```192.168.6.153/readings```. The local values are stored in a CSV database locally and a backup copy will be store in the remote server using the **Weather API**. 


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
|9| define send_data() | add data(datetime,sensor_id and value) to url | 1 hour | December 3 | C  | 

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



# Criteria D: Functionality

A 7 min video demonstrating the proposed solution with narration

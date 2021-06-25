# Project Step by Step Procedure:
.........................................................................................................................
step1: Upload the code provided on both the ESP32 boards and modify the print data to easily identify the sender node and receiver nodes. (Using ESP now) 

step2: With the boards connected to your computer, open a serial connection with each board.
 We can use the Serial Monitor, or  use a software like PuTTY and open two windows for both the ESP32 boards. We  should see that both boards receive data.

step3:  To connect the two different  ESP32 borad, sensor monitoring log data with an ESP32 and a DHT module and store all sensor data in a CSV file on the microSD storage.

Step 4: To collect the sensor data to populate on .csv file to secure table format data from both the sensors on sd card.
 First initialize our sensor and microSD storage on the ESP32 board.Then store sensor data in microSD storage after sensing temperature and humidity with the DHT module.
After storing the sensor data, the program will enter sleep mode.

Step 5: To syncronize the data to one table using PLX-DAQ  software will log the data on excel sheet on the by sending a serial data to the computer.
..................................................................................................................................................................................................
Design:

1. ESP-NOW communication protocol to send data from one board of ESP32 to other ESP32 board.

2.One ESP32 acts as a sender and other board  ESP32 act as receivers.
The ESP32 sender receives an acknowledge message if the messages are successfully delivered. 


3.To send data via ESP-NOW, we need to know the receiver both boards’ MAC address,both board has a unique MAC address.
Then, create a structure that contains the data we want to send. We called this structure test_struct and it contains two integer variables. 
You can change this to send whatever variable types you want.

4.Next, define the OnDataSent() function. This is a callback function that will be executed when a message is sent.
 In this case, this function prints if the message was successfully delivered or not and for which MAC address. 
After that, we need to pair with other ESP-NOW device to send data. That’s what we do in the next lines – register peers:

5. Now that the card is mounted without any errors, we can read the values from the DHT sensor.
 Open the file "/sdcard/data1.csv" in the append mode (see the second parameter of the fopen function),
 taking care not to overwrite the previous values, and write the current humidity and temperature in the file by using the fprintf() function.

5.Now that a new record is added to the file "/sdcard/data1.csv" , we can close the file by calling the function fclose and passing the file descriptor.

6.Now that we have the latest reading stored on our file  and the file is closed, and  prepare it for another deep sleep period. After that, the same process will be done repeatedly.

7.To enable our program to enter sleep mode, we call esp_deep_sleep_start(). Before calling esp_deep_sleep_start(), we set our wake-up timer.
 In this program, we wake up every 20 seconds.

8. It will generate a data1.csv file. we can use Microsoft Excel to visualize the data1.csv file. we can visualization of the sensor data. similarly data2.csv is generated and next file.

9. To log the data on excel sheet:  Used to Syncronize the data on one table by writing a VBA Macros.
PLX-DAQ is Microsoft Excel Plug-in software that helps us to write values from ESP to directly into an Excel file on our Laptop or PC. 
This is used for two reasons:
i.we can write and monitor the data at the same time and provides us way to plot them as graphs.
ii.To use this software with ESP we have to send the data serially in a specific pattern just like displaying value on serial monitor. 
﻿# Fire alarm in C++

## Introduction

This smart fire alarm application is part of a series of how-to Intel® Internet of Things (IoT) code sample exercises using the Intel® IoT Developer Kit, Intel® Edison board, Intel® IoT Gateway, cloud platforms, APIs, and other technologies.

From this exercise, developers will learn how to:

- Connect the Intel® Edison board or Intel® IoT Gateway, computing platforms designed for prototyping and producing IoT and wearable computing products.
- Interface with the Intel® Edison board or Intel® Arduino/Genuino 101 board IO and sensor repository using MRAA and UPM from the Intel® IoT Developer Kit, a complete hardware and software solution to help developers explore the IoT and implement innovative projects.
- Run these code samples in the Intel® System Studio IoT Edition (Eclipse IDE for C/C++ and Java\* development) for creating applications that interact with sensors and actuators, enabling a quick start for developing software for the Intel® Edison board or the Intel® Galileo board.
- Set up a web application server to store fire alarm data using Azure* Redis Cache from Microsoft, Redis Store\* from IBM Bluemix\*, or ElastiCache\* using Redis\* from Amazon Web Services\ (AWS)*, different cloud services for connecting IoT solutions including data analysis, machine learning, and a variety of productivity tools to simplify the process of connecting your sensors to the cloud and getting your IoT project up and running quickly.
- Invoke the services of the Twilio\* API for sending text messages.
- Set up a MQTT-based server using IoT Hub from Microsoft Azure\*, IoT from IBM Bluemix\*, or IoT from Amazon Web Services\ (AWS)*, different cloud machine to machine messaging services based on the industry standard MQTT protocol.

## What it is

Using an Intel® Edison board or Intel® IoT Gateway, this project lets you create a smart fire alarm that:

- constantly monitors for unsafe temperature levels.
- audibly notifies of alerts using the buzzer.
- visually notifies of alerts using the LCD.
- keeps track of fire alarm data, using cloud-based storage.
- sends text messages to alert others of a possible fire.

## How it works

This smart fire alarm monitors the ambient temperature using the Grove* Temperature Sensor.

If the temperature is above a certain threshold (set to 28 degrees Celsius for this example), it sounds an alarm through the buzzer and displays an alert on the LCD.

In addition, it can send an SMS to a specified number through Twilio*, warning them of a possible fire danger.

Optionally, it can also log fire events using the Intel IoT Examples Datastore or an MQTT server running in your own Microsoft Azure\*, IBM Bluemix\*, or AWS account.

## Hardware requirements

Grove* Starter Kit containing:

1. Intel® Edison board with an Arduino* breakout board
2. Grove Base Shield V2
3. [Grove Temperature Sensor](http://iotdk.intel.com/docs/master/upm/node/classes/grovetemp.html)
4. [Grove Buzzer](http://iotdk.intel.com/docs/master/upm/node/classes/buzzer.html)
5. [Grove RGB LCD](http://iotdk.intel.com/docs/master/upm/node/classes/jhd1313m1.html)

DFRobot\* Starter Kit for Intel® Edison, containing:

1. Intel® Edison with an Arduino\* breakout board
2. [Analog Temperature Sensor](http://iotdk.intel.com/docs/master/upm/node/classes/grovetemp.html)
3. [Buzzer](http://iotdk.intel.com/docs/master/upm/node/classes/buzzer.html)
4. [LCD Keypad Shield](http://iotdk.intel.com/docs/master/upm/node/classes/sainsmartks.html)

## Software requirements

1. [Intel® System Studio (Eclipse IDE for C/C++ and Java* development)](https://software.intel.com/en-us/node/672439)
2. Microsoft Azure\*, IBM Bluemix\*, or AWS account (optional)
3. Twilio\* account

### How to set up

This sample is already one of the IoT examples included in Intel® System Studio. To start using it, follow these steps:

1. From the main menu, select **Intel® IoT > Import IoT Examples**.<br>
![](./../../images/cpp/import-iot-examples.png)
2. Expand the tree view for **C++ > How To Code Samples > Fire Alarm** and click **Import Example**.<br>
![](./../../images/cpp/click-how-to-code-samples.png)
3. Select your developer board from the selection window then select **Next**.<br>
![](./../../images/cpp/select-board.png)
4. Select **Intel® IoT C/C++ project** from the Select a project type window then click **Next**.<br>
![](./../../images/cpp/select-project-type.png)
5. Select **Yocto** from the Selct target OS dropdown menu then click **Next**.<br>
![](./../../images/cpp/select-os.png)
6. The next tab will ask for connection name and target name. If you do not know these click **Search Target**.<br>
![](./../../images/cpp/search-target.png)
7. Select your Edison from the dropdown list. Select **OK**.<br>
![](./../../images/cpp/click-how-to-code-samples.png)
8. Your connection name and target name should be filled in. Select **Finish**.<br>
![](./../../images/cpp/finish-target.png)
9. A new window will open for you and you will need to choose a name for your project and click **Next**.<br>
![](./../../images/cpp/enter-project-name.png)
10. Your project source files will now be available on the on the upper left of your IDE by default.<br>
![](./../../images/cpp/project-src-imported.png)

### Connecting the Grove* sensors

You need to have the Grove* Base Shield V2 connected to an Arduino\*-compatible breakout board to plug all the Grove devices into the Grove Base Shield V2. Make sure you have the tiny VCC switch on the Grove Base Shield V2 set to **5V**.

1. Plug one end of a Grove cable into the Grove Temperature Sensor, and connect the other end to the A0 port on the Grove Base Shield V2.<br>
![](./../../images/js/fire-alarm.jpg)
2. Plug one end of a Grove cable into the Grove Buzzer and connect the other end to the D5 port on the Grove Base Shield V2.
3. Plug one end of a Grove cable into the Grove RGB LCD and plug the other end into any of the I2C ports on the Grove Base Shield V2.

### Connecting the DFRobot\* sensors

![](./../../images/js/fire-alarm-dfrobot.jpg)

You need to have a LCD Keypad Shield connected to an Arduino\*-compatible breakout board to plug all the DFRobot\* devices into the LCD Keypad Shield.

1. Plug one end of a DFRobot\* cable into the Analog Temperature Sensor, and connect the other end to the A1 port on the LCD Keypad Shield.

2. Plug one end of a DFRobot\* cable into the Buzzer, and connect the other end to the A2 port on the LCD Keypad Shield.

### Intel® Edison board setup

This example uses the **restclient-cpp** library to perform REST calls to the remote data server. The code can be found in the **lib** directory. The **restclient-cpp** library requires the **libcurl** package, which is already installed on the Intel® Edison board by default.

In addition, this example uses the **twilio-cplusplus** library to perform REST calls to the Twilio* SMS server. The code for **twilio-cplusplus** can be found in the **lib** directory. The **twilio-cplusplus** library requires the **ssl** and **crypto** packages, which are already installed on the Intel® Edison board by default.

### Twilio* API Key

To optionally send text messages, you need to register for an account and get an API key from the Twilio* web site:

[https://www.twilio.com](https://www.twilio.com)

You cannot send text messages without obtaining a Twilio API key first. You can still run the example, but without SMS alerts.

### Intel® IoT Gateway setup

You can run this example using an Intel® IoT Gateway connected to an Arduino\*/Genuino\* 101.

Make sure your Intel® IoT Gateway is setup, by following the directions on the web site here:

https://software.intel.com/en-us/node/633284

The Arduino\*/Genuino\* 101 needs to have the Firmata\* firmware installed. If you have IMRAA installed on your gateway, this will be done automatically. Otherwise, install the StandardFirmata or ConfigurableFirmata sketch manually onto your Arduino\*/Genuino\* 101.

### Data store server setup

Optionally, you can store the data generated by this sample program in a back-end database deployed using Microsoft Azure\*, IBM Bluemix\*, or AWS, along with Node.js\*, and a Redis\* data store.

For information on how to set up your own cloud data server, go to:

[https://github.com/intel-iot-devkit/intel-iot-examples-datastore](https://github.com/intel-iot-devkit/intel-iot-examples-datastore)

### MQTT server setup

You can also optionally store the data generated by this sample program using [MQTT](http://mqtt.org/), a Machine To Machine messaging server. You can use MQTT to connect to Microsoft\* Azure\*, IBM\* Bluemix\*, or AWS\*.

For information on how to connect to your own cloud MQTT messaging server, go to:

[https://github.com/intel-iot-devkit/intel-iot-examples-mqtt](https://github.com/intel-iot-devkit/intel-iot-examples-mqtt)

## Configuring the example for your hardware kit

To configure the example for the specific hardware kit that you are using, either Grove\* or DFRobot\*:

1. From the main menu, select **Project > Properties** dialog box is displayed.
![](./../../images/cpp/click-project-properties.png)
2. Expand the section **C/C++ General**. <br>Click on the **Paths and Symbols** sub-section, and click on the **Symbols** tab.
![](./../../images/cpp/click-gen-path-symbols.png)
3. Now click on **GNU C++**, and click on the **Add** button.
![](./../../images/cpp/click-gnupp-add.png)
4. In the **Name** field, enter "INTEL_IOT_KIT". In the **Value** field, enter either "GROVEKIT" (this is the default) or "DFROBOTKIT", depending on which hardware kit you wish to use.
![](./../../images/cpp/add-name-and-var.png)
5. Your new name symbol and value will now be displayed. Click **OK**.
![](./../../images/cpp/name-var-ok.png)
6. Another dialog box will appear asking to rebuild project. Click **OK**.
![](./../../images/cpp/path-symbol-rebuild-ok.png)

### Connecting your Intel® Edison board to Intel® System Studio

1. On the **Target SSH Connections** tab, right-click your device and select **Connect**.<br>
![](./../../images/cpp/cpp-connection-eclipse-ide-win4.png)

If prompted for the username and password, the username is **root** and the password is whatever you specified when configuring the Intel® Edison board.

### Running the example with the cloud server

To run the example with the optional backend data store, you need to set the `SERVER` and `AUTH_TOKEN` environment variables. You can do this in Intel® System Studio as follows:

1. From the **Run** menu, select **Run Configurations**.<br> The **Run Configurations** dialog box is displayed.
2. Under **C/C++ Remote Application**, click **doorbell**.<br> This displays the information for the application.
3. In the **Commands to execute before application** field, add the following environment variables, except use the server and authentication token that correspond to your own setup:

        chmod 755 /tmp/fire-alarm; export SERVER="http://intel-iot-example-data.azurewebsites.net/logger/fire-alarm"; export AUTH_TOKEN="Enter Auth Token Here"; export TWILIO_SID="Enter Twilio SID Here"; export TWILIO_TOKEN="Enter Twilio Token Here"; export TWILIO_TO="Enter Number to Send to here Formattted 555-555-5555"; export TWILIO_FROM="Enter Number to be Sent From Here Formated 555-555-5555"

4. Click **Apply** to save your new environment variables.

Now when you run your program using the **Run** button, it should be able to call your server to save the data right from the Intel® Edison board or Intel® IoT Gateway.

### Running the code on the Intel® Edison board or Intel® IoT Gateway

When you're ready to run the example, click **Run** at the top menu bar in Intel® System Studio.<br>
![](./../../images/cpp/cpp-run-eclipse.png)

This compiles the program using the Cross G++ Compiler, links it using the Cross G++ Linker, transfers the binary to the Intel® Edison board or Intel® IoT Gateway, and then executes it on the board itself.

After running the program, you should see output similar to the one in the image below.<br>
![](./../../images/cpp/cpp-run-eclipse-successful-build.png)

Successful output should be similar to the one in the image below.<br>
![](./../../images/cpp/cpp-equp-act-mon-successful-output.png)

When the program is uploaded to the Intel® Edison board, the program starts to continuously monitor the temperature. If it exceeds the threshold, the `Fire Alarm!` message is displayed on the LCD.<br>
![](./../../images/cpp/fire-alarm-lcd.jpg)

When the temperature sensor is heated, another output message is displayed in the Intel® System Studio console, similar to the image above. This means you sent your SMS alert successfully.<br>
![](./../../images/cpp/cpp-run-eclipse-successful-output-sms-sent.png)

IMPORTANT NOTICE: This software is sample software. It is not designed or intended for use in any medical, life-saving or life-sustaining systems, transportation systems, nuclear systems, or for any other mission-critical application in which the failure of the system could lead to critical injury or death. The software may not be fully tested and may contain bugs or errors; it may not be intended or suitable for commercial release. No regulatory approvals for the software have been obtained, and therefore software may not be certified for use in certain countries or environments.

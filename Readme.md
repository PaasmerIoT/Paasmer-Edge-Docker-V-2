# Paasmer-Edge-Docker-V-2
**Paasmer-Edge-Docker-V-2** for Raspberry-pi Running **Paasmer OS**.

## Overview

The **Paasmer-Edge-Docker-V-2** for Raspberry-pi Running **Paasmer OS** is a collection of Docker containers that enables you to do Analytics on edge and connect to the Paasmer IoT Platform. The **Paasmer-Edge-Docker-V-2** also consists of Paasmer Python library and Python SDK to connect to the Paasmer Gateway. Python Library now simplifies the Subscribing and publishing and is capable to handle various feed types in a single function call. It also has a sample **Machine Learning Docker** model that monitors the Health condition based on the Blood Pressure and Blood Sugar level sent from an sample Android App. 

## Paasmer OS
**Paasmer OS** is a container-based OS available for Single Board Computers. Currently, we only support the Raspberry-Pi. Support for other devices coming soon.

## Paasmer Edge Analytics 
**Paasmer Edge Analytics** is the key feature in Paasmer-Docker which provides you to do analytics on the sensor data. Presently we are providing Filter, Aggregate, Average and Feed monitoring algorithms, where you can analyze your sensor data based on your Analytics condition. Support for more algorithms on Analytics can be added in the future.

### Analytics and Features
* **Filter** - Can be used to Filter the sensor data based on Analytics conditions.
* **Aggregate** - Can be used to Find the Minimum, Maximum, Mean and Standard Deviation on the last n number of feed inputs. Where n is an integer given in the Analytics condition. 
* **Average** - Can be used to Find the Average of the last n number of feed inputs. Where n is an integer given in the Analytics condition.
* **Feed Monitoring** - Can be used to monitor the value changes in the feed by continuously monitoring the feeds. 


## Paasmer Python Library
**Paasmer Library** is set of functions that can be used to connect, subscribe and publish to the Paasmer gateway easily and more efficiently in a single function call. It can also support Edge Analytics on any feed while publishing. It has separate CallBack for each feed and thus making the connection simple.

## Machine Learning in Paasmer
Paasmer has the capability to **Machine Learning** now. **Paasmer-Edge-Docker-V-2** consists of a sample POC which monitors the Health condition, predicting the Health fall rate of a person from Andriod Application with Blood Pressure and Blood Sugar level based on the Breakfast timings.

### Andriod App
Paasmer Machine Learning POC is done with help of **PAASMER ML** App. This is a sample application that generates random readings of Blood Pressure, Blood Sugar Level and Breakfast time for performing ML. 

#### Usage 
Provide the IP address of the Paasmer Gateway, Patients Name and Time interval of send values from App to the ML Docker.

**Note- The Mobile phone must be connected to the local network where the Paasmer Gateway is connected.**

## Pre Requisites
Registration on the [PAASMER portal](http://developers.paasmer.co) is necessary to connect the devices to the **Paasmer IoT Platform**. A Raspberry-Pi board with SD card.


# Installation

### OS Image Downloading

#### For Windows
* Download the zip file [click here](https://github.com/PaasmerIoT/Paasmer-Edge-Docker-V-2/releases/download/1.0/paasmerOS.zip) and extract it.

#### For Linux
* Download the run file. [click here](https://github.com/PaasmerIoT/Paasmer-Edge-Docker-V-2/releases/download/1.0/paasmerOS) to download.

* Run the file using the command.
```
$ sh paasmerOS
```
This will extract the customized Paasmer OS image to your home directory.

### Docker Initialization

* Flash the SD card with the ISO image.

* Insert the card into the Raspberry-Pi and boot it. Login with `Username: pi` and `Password: raspberry`

* Get started with RaspberryPi and [click here](https://thepihut.com/blogs/raspberry-pi-tutorials/83502916-how-to-setup-wifi-on-raspbian-jessie-lite) to setup WiFi connection.

* Navigate to the paasmer-docker folder using the command.
```
cd /home/pi/
```

* Run the paasmer-docker.run
```
$ sh paasmer-docker.run
```
* This will install and build the necessary dockers
* Enter a UserName and DeviceName. The UserName is what you used in developers.paasmer.co for registration and give a unique DeviceName for your device and that must be alphanumeric without any spaces[a-z A-Z 0-9].

* Wohooo! That's all. Your device should be connected to the Paasmer platform.

## Getting started with Paasmer Python Library
Here is a very simple example that connects to the Paasmer Gateway, subscribes and Publishes to Paasmer platform enabling the user to access and read the feeds.

### Importing Paasmer Library
Open `paasmer-python-sdk` directory and start building the script.

```
from Paasmer import *
```
### Connecting to the Paasmer Edge docker device
```
test = Paasmer()
test.host = "localhost"   #IP address of the Paasmer Edge docker device.
test.connect()
```


### Subscribing 
```
#Callback functions for subscribed feeds
def feed1_CB(name):
    print("This is in feed1")
    print(name)

#subscribing to the feeds with callback functions
test.subscribe("feed1",feed1_CB)

```
The Subscribe functions need the following as parameters,
```
subscribe(feedname,callback function name)
```
- Feedname
- Call back Function name 

### Loop start
```
test.loop_start()
```

### Publishing the feed details 
The Publish functions need the following as parameters,
```
    test.publish("feed2",feedValue = 9,feedType = "sensor")

```
- Feedname
- Feedvalue
- Feedtype (The Feedtype is to be sensor or actuator)
```

You can use the Analytics in the following way,
- Filter - provide the analytics condition like "function(x) x < 5.0"
- Aggregate - provide the number of values you want to do aggregate
- FeedMonitoring
- Average - provide the number of values you want to do average

To syntax for Publishing Analytics are,
```
#publishing the feed details with filter analytics 
    test.publish("feed4",feedValue = 5,analytics = "filter",analyticsCondition="function(x) x > 3.0")

#publishing the feed details with aggregate analytics
    test.publish("feed6",feedValue = 22,analytics = "aggregate",analyticsCondition = "10")

#publishing the feed details with average analytics
    test.publish("feed8",feedValue = 28,analytics = "average",analyticsCondition = "10")

#publishing the feed details with feedMonitoring
    test.publish("feed7",feedValue = 22,analytics = "feedMonitoring")
```
** Note - A sample code is provided in `paasmer-python-sdk` directory **

## Support

The support forum is hosted on the GitHub, issues can be identified by users and the Team from Paasmer would be taking up requests and resolving them. You could also send a mail to support@paasmer.co with the issue details for a quick resolution.

## Note

* The Paasmer OS utilizes the features provided by raspbian OS and Docker engine.



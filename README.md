# Smart IoT Switch Control Using ESP8266 and MQTT

## Overview

This project implements a smart IoT switch control system using an **ESP8266 NodeMCU** and the **MQTT protocol**.

The ESP8266 connects to the Internet through Wi-Fi and communicates with an MQTT broker. A user can send `ON` or `OFF` commands from an MQTT client, and the ESP8266 controls a GPIO output accordingly.

Currently, the GPIO output is used for testing through the Serial Monitor. A relay can be connected later to control an actual electrical load.

## System Architecture

```text
        Phone / Browser
              |
              | MQTT
              v
        HiveMQ MQTT Broker
              |
              | Internet
              v
        ESP8266 NodeMCU
              |
              | GPIO5 (D1)
              v
       Switch Output
       (Relay - Future)
```

## Features

* ESP8266-based IoT switch
* Wi-Fi connectivity
* MQTT Publish/Subscribe communication
* Remote `ON` / `OFF` control
* MQTT command topic
* Serial Monitor control
* GPIO output control
* Automatic MQTT reconnection
* PlatformIO project structure
* GitHub version control

## Hardware

### Currently Used

* ESP8266 NodeMCU
* USB cable
* Computer
* Wi-Fi / mobile hotspot


## Software

* Visual Studio Code
* PlatformIO
* Arduino Framework
* ESP8266 Platform
* PubSubClient MQTT library
* HiveMQ MQTT Broker
* Git / GitHub

## MQTT Configuration

### Broker

```text
Host: broker.hivemq.com
Port: 1883
Protocol: MQTT
```

### Command Topic

```text
smart_switch/command
```

Commands:

```text
ON
OFF
```

Example:

```text
Browser
   |
   | Publish: ON
   v
smart_switch/command
   |
   v
ESP8266
   |
   v
GPIO5 = HIGH
```

## Current Testing

The ESP8266 successfully:

1. Connects to Wi-Fi.
2. Obtains an IP address.
3. Connects to the MQTT broker.
4. Subscribes to `smart_switch/command`.
5. Receives MQTT messages.
6. Processes `ON` and `OFF` commands.
7. Changes GPIO5 accordingly.
8. Accepts commands through the Serial Monitor.

Example output:

```text
WiFi connected!
IP address: 172.20.10.2

MQTT Connected!
Subscribed to command topic

Message received on topic: smart_switch/command
Message: ON

SWITCH = ON
GPIO = HIGH
```

## Project Structure

```text
Smart-IoT-Switch/
│
├── include/
├── lib/
├── src/
│   └── main.cpp
├── test/
└── platformio.ini
```

## How It Works

The ESP8266 first connects to a Wi-Fi network. After obtaining an IP address, it connects to the MQTT broker and subscribes to the command topic.

When an MQTT client publishes:

```text
ON
```

the ESP8266 receives the message and sets GPIO5 HIGH.

When:

```text
OFF
```

is received, GPIO5 is set LOW.

The same `ON` and `OFF` commands can also be entered through the Serial Monitor.



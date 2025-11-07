
# Lab 01: ESP32 WiFi configuration

  

Welcome to your very first hands-on project in the world of IoT (Internet of Things) and embedded systems! 
This article is a compilation of useful Wi-Fi functions for the ESP32. We’ll cover the following topics: scan Wi-Fi networks, connect to a Wi-Fi network, get Wi-Fi connection strength, check connection status, reconnect to the network after a connection is lost, Wi-Fi status, Wi-Fi modes, get the ESP32 IP address, set a fixed IP address and more.

  


## Objectives

  

- Configure ESP32 in WiFi Station (STA) mode to connect to existing wireless networks.

- Understand WiFi connection states, signal strength monitoring, and network reconnection strategies.

- Use Serial Monitor for debugging WiFi connection issues and viewing IP address assignments.

- Implement connection timeout handling and auto-reconnect functionality for reliable IoT deployments.

  


  


## What You'll Learn

  

- ESP32 WiFi modes: Station (STA), Access Point (AP), and combination mode (STA+AP).

- Essential WiFi library functions: WiFi.begin(), WiFi.status(), WiFi.localIP(), and WiFi.RSSI().

- Connection state machine: scanning, connecting, obtaining IP, and maintaining connection.

- Best practices for handling WiFi credentials and connection failures in production devices.

  


## Prerequisites

  

- ESP32 development board (ESP32 DevKit, NodeMCU-32S, or similar variant).

- Arduino IDE with ESP32 board support installed via Board Manager.

- USB cable for programming and serial communication.

- Access to a WiFi network with known SSID and password (2.4 GHz band required, as ESP32 does not support 5 GHz).

  

## Hardware Requirements

  

- 1× ESP32 development board (any variant with WiFi capability).

- 1× USB cable (typically USB-A to Micro-USB or USB-C depending on your board).

- Computer with Arduino IDE installed.

  

**Note:** No external components are required for this lab. The ESP32's on-board LED will indicate connection status in advanced examples.


## Including the WIFI library
The first thing you need to do to use the ESP32 Wi-Fi functionalities is to include the WiFi.h library in your code, as follows:
``` #include  <WiFi.h>```

## ESP32 Wi‑Fi Modes

The ESP32 can act as a Wi‑Fi station, access point, or both. Use `WiFi.mode()` with the desired mode.

cpp

`WiFi.mode(WIFI_STA);  // Station mode  WiFi.mode(WIFI_AP);  // Access Point mode  WiFi.mode(WIFI_AP_STA);  // Access Point + Station mode` 

## Mode Descriptions

-   `WIFI_STA`: The ESP32 connects to an existing access point (station mode).
    
-   `WIFI_AP`: Other devices (stations) can connect to the ESP32 (access point mode).
    
-   `WIFI_AP_STA`: The ESP32 acts as an access point while also connecting to another access point.



#### Set the ESP32 as an Access Point
To set the ESP32 as an access point, set the Wi-Fi mode to access point:

```c
WiFi.mode(WIFI_AP)
```

And then, use the  softAP()  method as follows:

```c
WiFi.softAP(ssid, password);
```

ssid  is the name you want to give to the ESP32 access point, and the  password  variable is the password for the access point. If you don’t want to set a password, set it to  NULL.

There are also other optional parameters you can pass to the  softAP()  method. Here are all the parameters:
```c
WiFi.softAP(const char* ssid, const char* password, int channel, int ssid_hidden, int max_connection)
```

-   ssid: name for the access point – maximum of 63 characters;
-   password:  **minimum of 8 characters**; set to  NULL  if you want the access point to be open;
-   channel: Wi-Fi channel number (1-13)
-   ssid_hidden: (0 = broadcast SSID, 1 = hide SSID)
-   max_connection: maximum simultaneous connected clients (1-4)


### Wi-Fi Station + Access Point

The ESP32 can be set as a Wi-Fi station and access point simultaneously. Set its mode to  WIFI_AP_STA.

```c
WiFi.mode(WIFI_AP_STA);
```
<img width="768" height="416" alt="image" src="https://github.com/user-attachments/assets/1d71a772-be3b-4ffa-871e-11be1bcf5534" />

## Scan Wi-Fi Networks

The ESP32 can scan nearby Wi-Fi networks within its Wi-Fi range. In your Arduino IDE, go to  **File** >  **Examples** >  **WiFi** >  **WiFiScan**. This will load a sketch that scans Wi-Fi networks within the range of your ESP32 board.

![ESP32 Scan WiFi Networks](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/02/ESP32-WiFi-Scan-Networks_Wi-Fi-Scan.png?resize=750%2C397&quality=100&strip=all&ssl=1)

This can be useful to check if the Wi-Fi network you’re trying to connect is within the range of your board or other applications. Your Wi-Fi project may not often work because it may not be able to connect to your router due to insufficient Wi-Fi strength.

Here’s the example:

```c
/*
  Example from WiFi > WiFiScan
  Complete details at https://RandomNerdTutorials.com/esp32-useful-wi-fi-functions-arduino/
*/

#include "WiFi.h"

void setup() {
  Serial.begin(115200);

  // Set WiFi to station mode and disconnect from an AP if it was previously connected
  WiFi.mode(WIFI_STA);
  WiFi.disconnect();
  delay(100);

  Serial.println("Setup done");
}

void loop() {
  Serial.println("scan start");

  // WiFi.scanNetworks will return the number of networks found
  int n = WiFi.scanNetworks();
  Serial.println("scan done");
  if (n == 0) {
      Serial.println("no networks found");
  } else {
    Serial.print(n);
    Serial.println(" networks found");
    for (int i = 0; i < n; ++i) {
      // Print SSID and RSSI for each network found
      Serial.print(i + 1);
      Serial.print(": ");
      Serial.print(WiFi.SSID(i));
      Serial.print(" (");
      Serial.print(WiFi.RSSI(i));
      Serial.print(")");
      Serial.println((WiFi.encryptionType(i) == WIFI_AUTH_OPEN)?" ":"*");
      delay(10);
    }
  }
  Serial.println("");

  // Wait a bit before scanning again
  delay(5000);
}

```


You can upload it to your board and check the available networks as well as the RSSI (received signal strength indicator).

WiFi.scanNetworks()  returns the number of networks found.

```c
int n = WiFi.scanNetworks();
```

After the scanning, you can access the parameters about each network.

WiFi.SSID()  prints the SSID for a specific network:

```c
Serial.print(WiFi.SSID(i));
```

WiFi.RSSI()  returns the RSSI of that network. RSSI stands for  **R**eceived  **S**ignal  **S**trength  **I**ndicator. It is an estimated measure of power level that an RF client device is receiving from an access point or router.

```c
Serial.print(WiFi.RSSI(i));
```

Finally,  WiFi.encryptionType()  returns the network encryption type. That specific example puts a * in the case of open networks. However, that function can return one of the following options (not just open networks):

-   WIFI_AUTH_OPEN
-   WIFI_AUTH_WEP
-   WIFI_AUTH_WPA_PSK
-   WIFI_AUTH_WPA2_PSK
-   WIFI_AUTH_WPA_WPA2_PSK
-   WIFI_AUTH_WPA2_ENTERPRISE

![ESP32 Scan WiFi Networks Example Serial Monitor](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/02/Scan-WiFi-Networks-ESP32-Arduino-IDE-Serial-Monitor.png?resize=733%2C541&quality=100&strip=all&ssl=1)

  

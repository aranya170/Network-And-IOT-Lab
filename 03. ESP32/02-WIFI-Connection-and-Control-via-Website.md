# Lab 02: WiFi Connection and LED Control via Website

## Objective
Learn how to connect your ESP32 to a WiFi network and control an onboard or external LED using a simple website (web interface).

## Learning Outcomes
- Understand WiFi connection with IoT devices
- Learn how to set up a web server on ESP32
- Link web interface controls to physical hardware

## Required Components
- ESP32 DevKit
- LED (or use built-in)
- 220Ω Resistor (if external LED)
- Breadboard & Jumper wires
- WiFi network access

## Theory
### What is IoT?
The Internet of Things (IoT) connects physical objects to the internet, enabling remote monitoring and control.

### WiFi in IoT Development
The ESP32 has built-in WiFi, making it ideal for connecting devices and sensors to the internet.

### Web Interface
A web server lets you control IoT hardware from any device with a web browser without extra apps.

## Steps
### 1. Circuit Connection
- Use built-in LED (GPIO2) or:
  - Connect the anode (long leg) of LED to GPIO2 through a 220Ω resistor
  - Connect the cathode (short leg) to GND

### 2. Code Example
```cpp
#include <WiFi.h>

const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";

WiFiServer server(80);
const int LED_PIN = 2;

void setup() {
  Serial.begin(115200);
  pinMode(LED_PIN, OUTPUT);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nWiFi connected");
  server.begin();
  Serial.print("IP Address: ");
  Serial.println(WiFi.localIP());
}

void loop() {
  WiFiClient client = server.available();
  if (client) {
    while (!client.available()) delay(1);
    String request = client.readStringUntil('\r');
    client.flush();
    int value = LOW;
    if (request.indexOf("/LED=ON") != -1) value = HIGH;
    if (request.indexOf("/LED=OFF") != -1) value = LOW;
    digitalWrite(LED_PIN, value);
    client.println("HTTP/1.1 200 OK");
    client.println("Content-Type: text/html");
    client.println();
    client.println("<html><body><h1>LED Control</h1>");
    client.println("<a href='/LED=ON'><button>Turn ON</button></a>");
    client.println("<a href='/LED=OFF'><button>Turn OFF</button></a>");
    client.println("</body></html>");
    break;
  }
}
```

### 3. Upload and Run
- Enter your WiFi credentials
- Upload to ESP32 board
- Open Serial Monitor to find your ESP32's IP address
- Connect to this IP from your browser
- Use ON/OFF buttons to control the LED

## Challenge
- Add more controls (e.g., change blink rate)
- Add a status indicator (shows current LED state)

## Key Concepts
- WiFi library for ESP32
- HTTP server basics
- Linking web input to hardware output

## Safety Notes
- Use the correct GPIO pin for LEDs
- Avoid short circuits

---
**Lab Duration:** 45-60 minutes  
**Difficulty Level:** Beginner to Intermediate
**Prerequisite:** Blink LED (Lab 01)

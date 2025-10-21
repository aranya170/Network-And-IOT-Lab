# Lab 06: IoT Data Visualization with Node-RED

## Objective
Visualize sensor data using Node-RED dashboard and flow programming. Integrate your ESP32 with a Node-RED server for real-time graphical feedback.

## Learning Outcomes
- Use of Node-RED for IoT visualization
- Create dashboards for sensor output
- Learn flow-based programming

## Required Components
- ESP32/Arduino (WiFi enabled)
- Sensor (DHT11, DHT22, etc.)
- Node-RED installed on PC/Raspberry Pi/cloud (with dashboard nodes)
- WiFi network

## Steps
1. Install Node-RED (https://nodered.org/)
2. Add dashboard nodes (`node-red-dashboard`)
3. ESP32: Use HTTP or MQTT to publish sensor readings to Node-RED

## Sample Code (ESP32 HTTP POST)
```cpp
#include <WiFi.h>
#include <HTTPClient.h>
const char* ssid = "YOUR_SSID";
const char* password = "YOUR_PASSWORD";

void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) { delay(500); }
}
void loop() {
  if (WiFi.status() == WL_CONNECTED) {
    HTTPClient http;
    http.begin("http://[NODE_RED_IP]:1880/sensor");
    http.addHeader("Content-Type", "application/json");
    int temp = 25; // Replace with sensor value
    String payload = "{\"temp\":" + String(temp) + "}";
    http.POST(payload);
    http.end();
  }
  delay(5000);
}
```

## Node-RED Flow
- HTTP input node (endpoint `/sensor`)
- Parse JSON
- Display on dashboard gauge/chart node

## Challenge
- Add multiple sensors to dashboard
- Trigger alerts on threshold

## Safety Notes
- Network firewalls may block data, open necessary ports

---
**Lab Duration:** 60 minutes
**Difficulty Level:** Intermediate
**Prerequisite:** ESP32 WiFi and Sensor Labs
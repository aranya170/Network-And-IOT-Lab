# Lab 09: OTA (Over-the-Air) Firmware Update for IoT Devices

## Objective
Learn how to update firmware on ESP32/Arduino devices remotely via WiFi, increasing maintainability and security of deployed IoT solutions.

## Learning Outcomes
- OTA programming basics
- Update code without physical access
- Firmware version management

## Required Components
- ESP32/Arduino board
- WiFi network

## Steps
1. Install ArduinoOTA library
2. Basic setup code example (ESP32):

```cpp
#include <WiFi.h>
#include <ArduinoOTA.h>
const char* ssid = "YOUR_SSID";
const char* password = "YOUR_PASSWORD";
void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) delay(500);
  ArduinoOTA.setHostname("esp32-iot-device");
  ArduinoOTA.begin();
}
void loop() {
  ArduinoOTA.handle();
}
```

3. Upload initial firmware via USB
4. For subsequent uploads, select 'Network Port' and upload from IDE wirelessly

## Challenge
- Setup password-protected OTA
- Version control via custom messages

## Safety Notes
- Secure OTA channels (set OTA password)
- Monitor network for unauthorized updates

---
**Lab Duration:** 40 minutes
**Difficulty Level:** Advanced
**Prerequisite:** WiFi, basic IoT coding

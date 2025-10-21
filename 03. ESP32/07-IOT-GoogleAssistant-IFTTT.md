# Lab 07: Controlling Devices with Google Assistant and IFTTT

## Objective
Enable remote control of your IoT devices (relay/LED) using Google Assistant through IFTTT and webhooks.

## Learning Outcomes
- Integrating voice assistants with IoT projects
- Webhooks and API-triggered actions
- Smart home innovation basics

## Required Components
- ESP32/Arduino with WiFi
- Relay or LED
- IFTTT (ifttt.com) account
- Google Assistant on mobile

## Steps
1. Connect ESP32 to WiFi (code similar to previous labs)
2. Register free IFTTT account
3. Create a webhook (trigger: Google Assistant phrase, action: webhook URL)
4. On ESP32, add code to listen for specific HTTP requests and control relay/LED accordingly

## ESP32 Web Server Example (Snippet)
```cpp
#include <WiFi.h>
WiFiServer server(80);
void setup() {
  WiFi.begin("SSID", "PASSWORD");
  pinMode(2, OUTPUT); // Use GPIO 2 for LED/Relay
  server.begin();
}
void loop() {
  WiFiClient client = server.available();
  if (client) {
    String request = client.readStringUntil('\r');
    if (request.indexOf("/on") != -1) digitalWrite(2, HIGH);
    if (request.indexOf("/off") != -1) digitalWrite(2, LOW);
    client.stop();
  }
}
```

## IFTTT Webhook URL
- Example: `http://[ESP32-IP]/on` or `/off`
- Action: Google Assistant phrase triggers URL

## Challenge
- Add multiple voice commands for different devices

## Safety Notes
- Use secure networks
- Do not expose devices directly to the public internet

---
**Lab Duration:** 60-90 minutes
**Difficulty Level:** Intermediate/Advanced
**Prerequisite:** WiFi, Web server, Relay control
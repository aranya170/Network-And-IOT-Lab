# Lab 04: Sending Sensor Data to the Cloud (ThingSpeak MQTT)

## Objective
Learn how to send sensor data from ESP32/Arduino to a cloud IoT platform (ThingSpeak) using MQTT protocol.

## Learning Outcomes
- Data publishing via MQTT
- Integration with IoT cloud platforms
- Real-time data visualization

## Required Components
- ESP32/Arduino board
- DHT11/DHT22 sensor (or similar)
- Internet access
- ThingSpeak account (free)

## Steps
### 1. Sensor and WiFi Setup
Connect sensor and connect ESP32 to WiFi (see previous labs).

### 2. Create ThingSpeak Channel
- Sign up at thingspeak.com
- Create a new Channel for your data
- Note the Write API Key

### 3. Install Libraries
- PubSubClient (MQTT)
- DHT sensor library

### 4. Sample Code
```cpp
#include <WiFi.h>
#include <PubSubClient.h>
#include "DHT.h"
#define DHTPIN 4
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
const char* mqttServer = "mqtt.thingspeak.com";
const char* mqttUser = "YOUR_THINGSPEAK_USERNAME";
const char* mqttPassword = "YOUR_MQTT_API_KEY";
const char* topic = "channels/YOUR_CHANNEL_ID/publish/YOUR_MQTT_API_KEY";
WiFiClient wifiClient;
PubSubClient client(wifiClient);
void setup() {
  Serial.begin(115200);
  dht.begin();
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) { delay(500); }
  client.setServer(mqttServer, 1883);
}
void loop() {
  if (!client.connected()) client.connect("ESP32Client", mqttUser, mqttPassword);
  float t = dht.readTemperature();
  float h = dht.readHumidity();
  String payload = String("field1=") + t + "&field2=" + h;
  client.publish(topic, payload.c_str());
  delay(20000);
}
```

### 5. Visualize Data
- View your data live on ThingSpeak dashboard

## Challenge
- Plot multiple fields
- Use other sensors

## Key Concepts
- MQTT protocol basics
- Data serialization (string construction)
- IoT dashboard visualization

## Safety Notes
- Protect your API keys
- Never expose credentials in public code

---
**Lab Duration:** 45-60 minutes
**Difficulty Level:** Intermediate
**Prerequisite:** WiFi, Sensor Data, Web Control
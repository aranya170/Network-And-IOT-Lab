# Lab 03: Reading Sensor Data (DHT11/DHT22 Temperature & Humidity)

## Objective
Learn how to interface a DHT11/DHT22 temperature and humidity sensor with ESP32/Arduino and display real-time sensor data.

## Learning Outcomes
- Sensor interfacing
- Data acquisition from analog/digital sensors
- Serial output for monitoring data

## Required Components
- ESP32/Arduino board
- DHT11 or DHT22 sensor
- 10kΩ Resistor (optional for pull-up)
- Breadboard, jumper wires

## Theory
- Sensors are the backbone of IoT—collecting environmental data.
- DHT11/DHT22 output digital signals with temperature and humidity information.

## Circuit Connection
- VCC of sensor to 3.3V
- GND to GND
- DATA to GPIO4 (for example)
- Optional: 10kΩ resistor between VCC and DATA as pull-up (for stability)

## Code Example
```cpp
#include "DHT.h"
#define DHTPIN 4
#define DHTTYPE DHT11 // Change to DHT22 if using that sensor
DHT dht(DHTPIN, DHTTYPE);
void setup() {
  Serial.begin(115200);
  dht.begin();
}
void loop() {
  float humidity = dht.readHumidity();
  float temp = dht.readTemperature();
  Serial.print("Humidity: "); Serial.print(humidity); Serial.print(" %\t");
  Serial.print("Temperature: "); Serial.print(temp); Serial.println(" *C");
  delay(2000);
}
```

## Upload and Monitor
- Upload code and open Serial Monitor (baud 115200)
- Observe real-time temperature and humidity

## Challenge
- Display temperature in Fahrenheit
- Output data to an OLED display

## Safety Notes
- Do not reverse VCC/GND
- Power off before wiring

---
**Lab Duration:** 30 minutes  
**Difficulty Level:** Beginner
**Prerequisite:** Blink LED and WiFi Lab
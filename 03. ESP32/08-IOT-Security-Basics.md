# Lab 08: Security in IoT—Basic Encryption and Safe Practices

## Objective
Understand the security challenges in IoT and learn to implement basic encryption (e.g. WiFi WPA2, simple AES), strong authentication, and device/network safety practices.

## Learning Outcomes
- Grasp importance of IoT security
- Learn WiFi security types
- Apply simple encryption for data transmission
- Understand device authentication best practices

## Required Components
- ESP32/Arduino
- Secure WiFi network

## Theory
Security in IoT includes confidentiality, integrity, authentication, and access control. Common attacks are eavesdropping, spoofing, and device hijacking. Strong passwords, HTTPS, and encrypted MQTT/HTTP are essential.

## WiFi Security Example
Always use WPA2 (never open WiFi). Use strong passwords.

## Basic Encryption Example (ESP32 Arduino)
```cpp
#include <AESLib.h> // Arduino AES library (install from Library Manager)
AESLib aesLib;
String data = "Hello IoT";
char cleartext[128];
char ciphertext[128];
strcpy(cleartext, data.c_str());
const char* key = "abcdefghijklmnop"; // 16 chars
int len = aesLib.encrypt( cleartext, key, ciphertext );
Serial.println("Encrypted: " + String(ciphertext));
```

## Best Practices
- Unique strong passwords for every device
- Change default credentials
- Regular firmware updates
- Avoid exposing unmapped devices to the internet

## Challenge
- Set up HTTPS on ESP32 (advanced libraries)
- Use JWT or simple token for requests

## Safety Notes
- Encryption ≠ 100% safe. Update libraries and keys regularly.

---
**Lab Duration:** 40-60 minutes
**Difficulty Level:** Intermediate/Advanced
**Prerequisite:** IoT network and sensor basics

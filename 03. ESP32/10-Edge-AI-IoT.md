# Lab 10: Advanced IoT—Edge AI (Sensor Data Analysis on Device)

## Objective
Deploy simple machine learning models on ESP32 for edge-based anomaly detection or sensor data analysis.

## Learning Outcomes
- Understanding of TinyML and Edge AI
- Deploying trained models on microcontrollers
- Real-time analytics without cloud/server

## Required Components
- ESP32 (or suitable ARM-based board)
- Sensor (e.g., vibration, temperature)
- Trained model in TensorFlow Lite micro format
- Arduino IDE, Python for model export

## Theory
- Edge AI allows analytics and predictions with no internet dependency
- Enables faster response, privacy, and efficiency

## Workflow
1. Collect sensor data and label it (using Arduino + Serial/CSV)
2. Train model in Python (e.g., anomaly detection with TensorFlow)
3. Convert/export model to TensorFlow Lite for Microcontrollers
4. Add the model to Arduino project and use it to predict/classify on-device

## Code Snippet Example (TinyML Inference)
```cpp
#include "model.h" // Model C array
#include <TensorFlowLite.h>
TfLiteTensor input_tensor, output_tensor;
void setup() {
  // TinyML setup
}
void loop() {
  // Collect sensor reading, preprocess
  // Run on model, get prediction
}
```

## Challenge
- Use model to predict hardware faults or unusual events
- Add local triggers when anomaly is detected

## Safety Notes
- Ensure sufficient device memory
- Validate predictions

---
**Lab Duration:** 90 minutes
**Difficulty Level:** Advanced
**Prerequisite:** Sensor data, Python basics, Lab 1–9 experience

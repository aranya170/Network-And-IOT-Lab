# Lab 01: Blink LED - Your First IoT Project

Welcome to your very first hands-on project in the world of IoT (Internet of Things) and embedded systems! If you're new to electronics or programming, don't worry—this lab is designed specifically for beginners. We'll guide you step by step through building a simple circuit and writing code to make an LED blink. Think of this as the "Hello World" program for hardware: it's simple, fun, and teaches foundational concepts that you'll use in more advanced projects.
By the end of this lab, you'll feel confident working with microcontrollers like Arduino or ESP32, and you'll have a blinking light to show off!

## Objective
The goal is to learn the basics of microcontroller programming by controlling an LED (a small light) using an Arduino or ESP32 board. You'll connect hardware components, write a simple program, and upload it to make the LED turn on and off repeatedly.

## Learning Outcomes
- Understand basic microcontroller pin configuration
- Learn digital output control
- Understand GPIO (General Purpose Input/Output) pins
- Introduction to Arduino IDE and code structure
- Learn basic timing functions

## Required Components
- ESP32 DevKit
- LED (any color)
- 220Ω Resistor
- Breadboard
- Jumper wires
- USB cable for programming

## Theory

### What is an LED?
A Light Emitting Diode (LED) is a semiconductor device that emits light when current flows through it. LEDs have polarity - the longer leg is positive (anode) and shorter leg is negative (cathode).

### GPIO Pins
GPIO pins can be configured as either input or output. For blinking an LED, we configure a pin as OUTPUT to control voltage levels (HIGH = 3.3V/5V, LOW = 0V).

### Arduino Code Structure
Every Arduino sketch has two main functions:
- `setup()` - Runs once when the program starts
- `loop()` - Runs repeatedly after setup()

## Circuit Diagram

```
Arduino/ESP32          Resistor       LED
    Pin 13 ----------- 220Ω -------- Anode(+)
    GND ------------------------------ Cathode(-)
```

**Note:** Always use a current-limiting resistor with LEDs to prevent damage.

## Circuit Connection Steps

1. **Insert LED** into breadboard
   - Long leg (anode) in one row
   - Short leg (cathode) in another row

2. **Connect Resistor**
   - One end to LED anode row
   - Other end to a new row

3. **Connect Jumper Wires**
   - Digital pin 13 to resistor (connected to LED anode)
   - GND pin to LED cathode

4. **Connect USB** cable from Arduino to computer

![Components](https://cdn.sparkfun.com/assets/learn_tutorials/3/1/0/Arduino_circuit_01_1.png)
*Caption: Labeled components for the LED blink project: jumper wires, resistor, LED, breadboard, and Arduino Uno board.*


## Code Implementation

### Basic Blink Code (Arduino/ESP32)

```cpp
// Pin definition
const int LED_PIN = 13;  // Built-in LED on most Arduino boards
// For ESP32, use GPIO 2: const int LED_PIN = 2;

void setup() {
  // Initialize the LED pin as output
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  // Turn LED ON
  digitalWrite(LED_PIN, HIGH);
  delay(1000);  // Wait for 1 second (1000 milliseconds)
  
  // Turn LED OFF
  digitalWrite(LED_PIN, LOW);
  delay(1000);  // Wait for 1 second
}
```

### Code Explanation

- **`const int LED_PIN = 13;`** - Defines a constant for pin number
- **`pinMode(LED_PIN, OUTPUT);`** - Configures pin 13 as output
- **`digitalWrite(LED_PIN, HIGH);`** - Sends 5V to pin (LED ON)
- **`digitalWrite(LED_PIN, LOW);`** - Sends 0V to pin (LED OFF)
- **`delay(1000);`** - Pauses program for 1000ms (1 second)

## Upload and Test

### Steps to Upload Code

1. **Open Arduino IDE**
2. **Select Board**
   - Tools → Board → Arduino Uno (or your board)
   - For ESP32: Tools → Board → ESP32 Dev Module
3. **Select Port**
   - Tools → Port → COM3 (or your port)
4. **Copy and paste the code**
5. **Click Upload button** (→ icon)
6. **Observe** - LED should blink every second

## Expected Output
The LED will turn ON for 1 second, then OFF for 1 second, repeating continuously.

## Experiments and Modifications

### Experiment 1: Change Blink Speed
Modify delay values to change blink speed:
```cpp
digitalWrite(LED_PIN, HIGH);
delay(250);  // LED ON for 0.25 seconds
digitalWrite(LED_PIN, LOW);
delay(250);  // LED OFF for 0.25 seconds
```

### Experiment 2: SOS Pattern (Morse Code)
```cpp
void loop() {
  // S - three short blinks
  for(int i = 0; i < 3; i++) {
    digitalWrite(LED_PIN, HIGH);
    delay(200);
    digitalWrite(LED_PIN, LOW);
    delay(200);
  }
  
  delay(400);  // Pause between letters
  
  // O - three long blinks
  for(int i = 0; i < 3; i++) {
    digitalWrite(LED_PIN, HIGH);
    delay(600);
    digitalWrite(LED_PIN, LOW);
    delay(200);
  }
  
  delay(400);  // Pause between letters
  
  // S - three short blinks
  for(int i = 0; i < 3; i++) {
    digitalWrite(LED_PIN, HIGH);
    delay(200);
    digitalWrite(LED_PIN, LOW);
    delay(200);
  }
  
  delay(2000);  // Wait before repeating SOS
}
```

### Experiment 3: Multiple LEDs
Connect 3 LEDs to pins 11, 12, 13:
```cpp
const int LED1 = 11;
const int LED2 = 12;
const int LED3 = 13;

void setup() {
  pinMode(LED1, OUTPUT);
  pinMode(LED2, OUTPUT);
  pinMode(LED3, OUTPUT);
}

void loop() {
  // Sequential blinking
  digitalWrite(LED1, HIGH);
  delay(300);
  digitalWrite(LED1, LOW);
  
  digitalWrite(LED2, HIGH);
  delay(300);
  digitalWrite(LED2, LOW);
  
  digitalWrite(LED3, HIGH);
  delay(300);
  digitalWrite(LED3, LOW);
}
```

### Experiment 4: Breathing Effect (PWM)
```cpp
const int LED_PIN = 9;  // Must use PWM-capable pin

void setup() {
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  // Fade in
  for(int brightness = 0; brightness <= 255; brightness++) {
    analogWrite(LED_PIN, brightness);
    delay(5);
  }
  
  // Fade out
  for(int brightness = 255; brightness >= 0; brightness--) {
    analogWrite(LED_PIN, brightness);
    delay(5);
  }
}
```

## Troubleshooting

| Problem | Possible Cause | Solution |
|---------|---------------|----------|
| LED doesn't light up | LED connected backwards | Reverse LED polarity |
| LED very dim | Wrong resistor value | Use 220Ω resistor |
| Upload error | Wrong port selected | Check Tools → Port |
| Board not detected | Driver not installed | Install CH340/CP2102 driver |
| LED stays on/off | Code not uploaded | Re-upload code |

## Key Concepts Review

1. **Digital Output** - Sends HIGH (5V) or LOW (0V) signals
2. **pinMode()** - Configures pin as INPUT or OUTPUT
3. **digitalWrite()** - Sets pin to HIGH or LOW
4. **delay()** - Pauses program execution
5. **Resistor** - Limits current to protect LED

## Challenge Questions

1. How would you make LED blink 5 times then pause for 3 seconds?
2. What happens if you remove the resistor?
3. How can you calculate the correct resistor value for different LEDs?
4. What is PWM and how does it create a breathing effect?
5. Can you create a traffic light sequence with 3 LEDs?

## Next Steps
In the next lab, you will learn to connect your ESP32 to WiFi and control the LED through a website, taking your first step into true IoT development!

## Additional Resources

- Arduino Reference: https://www.arduino.cc/reference/en/
- LED Resistor Calculator: https://www.digikey.com/en/resources/conversion-calculators/conversion-calculator-led-series-resistor
- Ohm's Law: V = IR (Voltage = Current × Resistance)

## Safety Notes
- Always disconnect power before changing circuit connections
- Use appropriate resistor values to prevent component damage
- Check polarity of components before connecting
- Avoid short circuits by carefully checking connections

---

**Lab Duration:** 30-45 minutes  
**Difficulty Level:** Beginner  
**Prerequisites:** None
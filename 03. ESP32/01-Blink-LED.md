# Lab 01: Blink LED - Your First IoT Project

Welcome to your very first hands-on project in the world of IoT (Internet of Things) and embedded systems! If you're new to electronics or programming, don't worry—this lab is designed specifically for beginners. We'll guide you step by step through building a simple circuit and writing code to make an LED blink. Think of this as the "Hello World" program for hardware: it's simple, fun, and teaches foundational concepts that you'll use in more advanced projects.

By the end of this lab, you'll feel confident working with microcontrollers like Arduino or ESP32, and you'll have a blinking light to show off!

## Objective
The goal is to learn the basics of microcontroller programming by controlling an LED (a small light) using an Arduino or ESP32 board. You'll connect hardware components, write a simple program, and upload it to make the LED turn on and off repeatedly.

## Learning Outcomes
After completing this lab, you'll be able to:
- Understand how to configure microcontroller pins for basic operations.
- Control digital outputs to turn devices like LEDs on and off.
- Work with GPIO (General Purpose Input/Output) pins, which are the "connectors" on your board.
- Use the Arduino IDE (Integrated Development Environment) software to write and upload code.
- Implement basic timing functions to create delays in your program.

## Required Components
Here's what you'll need to get started. These are common, inexpensive items you can find at electronics stores or online (e.g., Amazon, Adafruit, or SparkFun). If you're using a starter kit, these should be included.

- **Arduino Uno or ESP32 DevKit**: The "brain" of your project. Arduino Uno is great for beginners; ESP32 adds WiFi capabilities for future projects.
- **LED (any color)**: A small light bulb that glows when electricity flows through it. Colors like red, green, or blue are fine.
- **220Ω Resistor**: This protects the LED by limiting the current. Look for one with color bands: red-red-brown-gold.
- **Breadboard**: A reusable board for connecting components without soldering—perfect for prototyping.
- **Jumper wires**: Short cables (male-to-male) to connect everything. Get a variety pack with different colors for organization.
- **USB cable**: For connecting your board to the computer (usually USB-A to USB-B for Arduino, or USB-C for some ESP32 boards).

![Components](images/components.jpg)
*Caption: Labeled components for the LED blink project: jumper wires, resistor, LED, breadboard, and Arduino Uno board.*

**Tip for Beginners:** If you're unsure about identifying components, check the packaging or use an online resistor color code calculator. LEDs have two legs: the longer one is the positive side (anode), and the shorter is negative (cathode).

## Theory

### What is an LED?
An LED, or Light Emitting Diode, is a tiny electronic component that lights up when electric current passes through it in one direction. It's like a one-way street for electricity! LEDs are energy-efficient and come in various colors. Remember the polarity: connect the positive leg to power and the negative to ground. If reversed, it won't light up (but won't damage it either).

### What is a Microcontroller?
A microcontroller is a small computer on a chip, like the Arduino Uno or ESP32. It can read inputs (e.g., buttons) and control outputs (e.g., lights). In this project, we're using it to send signals to the LED.

### GPIO Pins
GPIO stands for General Purpose Input/Output. These are the numbered pins on your board that you can program to send or receive signals. For this lab, we'll set a pin as an "output" to control the LED by switching between HIGH (on, about 5V for Arduino or 3.3V for ESP32) and LOW (off, 0V).

### Arduino Code Structure
Arduino programs (called "sketches") are written in a language similar to C++. Every sketch has two main parts:
- **`setup()`**: This runs once when you power on the board. Use it to initialize things, like setting pin modes.
- **`loop()`**: This runs over and over forever after setup. It's where the main action happens, like blinking the LED.

**Beginner Note:** Don't worry if coding seems intimidating—we'll explain every line!

## Circuit Diagram

Here's a simple text-based diagram:

For a visual representation, see the image below.

![Circuit Diagram](images/circuit_diagram.jpg)
*Caption: Diagram showing the Arduino connected to an LED via a resistor on a breadboard.*

**Important Safety Note:** Always include the resistor! Without it, too much current could burn out the LED or damage your board.

## Circuit Connection Steps

Let's build the circuit step by step. Take your time and double-check connections to avoid shorts.

1. **Prepare the Breadboard**: The breadboard has rows of holes connected horizontally (except across the middle gap). Use it to "plug in" components easily.
   
2. **Insert the LED**: Place the LED on the breadboard. Put the longer leg (anode, +) in one row and the shorter leg (cathode, -) in a different row, spanning the middle gap if needed.

3. **Connect the Resistor**: Attach one end of the 220Ω resistor to the same row as the LED's anode. The other end goes to a new row.

4. **Connect Jumper Wires**:
   - Use one jumper from your board's digital pin 13 to the resistor's free end (the row not connected to the LED).
   - Use another jumper from the board's GND (ground) pin to the LED's cathode row.

5. **Power Connection**: Plug the USB cable into your board and computer. The board should light up (power LED on).

![Assembled Circuit](images/assembled_circuit.jpg)
*Caption: Real photo of an Arduino Uno with LED blink circuit on a breadboard.*

![Alternate Circuit View](images/alternate_circuit.jpg)
*Caption: Another view of the assembled LED blink circuit.*

**Pro Tip:** Use different colored wires (e.g., red for positive, black for ground) to keep things organized and reduce errors.

## Code Implementation

### Basic Blink Code (Works for Arduino Uno or ESP32)

Copy this code into the Arduino IDE. For ESP32, change the pin to 2 if pin 13 isn't available (ESP32 has a built-in LED on pin 2).

```cpp
// Pin definition - this is like naming your LED's "address"
const int LED_PIN = 13;  // Use 13 for Arduino Uno; for ESP32, try 2 for the built-in LED

void setup() {
  // Setup runs once: tell the board this pin is for output (sending signals)
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  // Loop runs forever: turn the LED on
  digitalWrite(LED_PIN, HIGH);  // HIGH means "on" (sends voltage)
  delay(1000);  // Wait 1 second (1000 milliseconds)
  
  // Turn the LED off
  digitalWrite(LED_PIN, LOW);   // LOW means "off" (no voltage)
  delay(1000);  // Wait another second
}
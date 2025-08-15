# 6-Pin Gas Sensor with Arduino in Tinkercad

This tutorial guides you through setting up a **6-pin gas sensor** (e.g., MQ-2) with an **Arduino Uno** in Tinkercad to detect gas concentrations. The sensor’s analog output will be read and displayed in the Serial Monitor, with an LED indicating high gas levels. This is ideal for learning about gas sensing and Arduino programming in a virtual environment.

## Prerequisites

- A Tinkercad account (free at [tinkercad.com](https://www.tinkercad.com)).
- Basic understanding of Arduino programming and the Tinkercad interface.
- No physical hardware is required, as Tinkercad simulates all components.

## 1. Components Needed

- Arduino Uno R3
- 6-pin gas sensor (e.g., MQ-2)
- Breadboard
- Jumper wires
- LED
- 220-ohm resistor (for the LED)

## 2. Pinout for 6-Pin Gas Sensor (MQ-2)

The 6-pin MQ-2 gas sensor typically has two sets of pins (three on each side), often labeled as A0, GND, VCC, and duplicated on the other side (H1, Terminal 1, Terminal 2). In Tinkercad, the sensor may appear with a simplified interface, but the connections are based on the standard MQ-2 pinout. Only one set of pins is needed for basic operation.

### Gas Sensor to Arduino
| Gas Sensor Pin | Arduino Pin / Connection |
|----------------|--------------------------|
| A0             | Analog pin A0            |
| GND            | Arduino GND              |
| VCC            | Arduino 5V               |
| H1             | GND (or leave unconnected if not needed) |
| Terminal 1     | GND (or leave unconnected) |
| Terminal 2     | GND (or leave unconnected) |

### LED to Arduino
| LED Pin   | Arduino Pin / Connection |
|-----------|--------------------------|
| Anode     | Digital pin 8            |
| Cathode   | 220-ohm resistor to GND  |

> **Note**: The H1, Terminal 1, and Terminal 2 pins are often used for the sensor’s heater circuit. In Tinkercad, connecting only one GND pin is usually sufficient, as the simulation simplifies the heater connections. If the sensor requires all GND pins to be connected, link them to the breadboard’s GND rail.[](https://www.instructables.com/Anay-Shah-Gas-Detector-Arduino-Tinkercad/)

## 3. Set Up the Circuit in Tinkercad

### Create a New Circuit
- Log in to Tinkercad and click **Circuits** > **Create new Circuit**.
- Rename the circuit (e.g., "Gas Sensor Detector") by clicking the default name in the top left.

### Add Components
From the components panel (right side), drag the following to the workspace:
- **Arduino Uno R3**
- **Gas Sensor** (search for "gas sensor" or "MQ-2")
- **Breadboard** (small)
- **LED**
- **220-ohm Resistor**
- **Jumper wires**

### Wire the Circuit
1. **Power the Breadboard**:
   - Connect Arduino’s **5V** pin to the red (+) rail on the breadboard (use a red wire).
   - Connect Arduino’s **GND** pin to the blue (-) rail on the breadboard (use a black wire).
2. **Connect the Gas Sensor**:
   - **A0** to Arduino pin **A0**.
   - **GND** to the breadboard’s blue (-) rail (GND).
   - **VCC** to the breadboard’s red (+) rail (5V).
   - **H1**, **Terminal 1**, **Terminal 2** to the breadboard’s blue (-) rail (GND), or leave unconnected if Tinkercad’s sensor model doesn’t require them.
3. **Connect the LED**:
   - **Anode** (longer leg) to Arduino pin **8**.
   - **Cathode** (shorter leg) to a 220-ohm resistor, then connect the resistor to the breadboard’s blue (-) rail (GND).

## 4. Arduino Code

### Open the Code Editor
- Click the **Code** button in Tinkercad’s top right corner.
- Select **Text** mode and click **Continue** if prompted.
- Delete any default code.

### Paste the Code
Copy and paste the following code into the editor:

```cpp
int gasSensorPin = A0; // Analog pin for gas sensor
int ledPin = 8;        // Digital pin for LED
int gasValue = 0;      // Variable to store gas sensor value

void setup() {
  pinMode(ledPin, OUTPUT);    // Set LED pin as output
  Serial.begin(9600);         // Initialize serial communication
}

void loop() {
  gasValue = analogRead(gasSensorPin); // Read gas sensor value
  float voltage = gasValue * (5.0 / 1023.0); // Convert to voltage

  // Print gas value and voltage to Serial Monitor
  Serial.print("Gas Value: ");
  Serial.print(gasValue);
  Serial.print(" | Voltage: ");
  Serial.print(voltage);
  Serial.println(" V");

  // Turn on LED if gas value exceeds threshold (e.g., 300)
  if (gasValue > 300) {
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }

  delay(500); // Wait for 500 milliseconds
}
```

### Code Explanation
- `int gasSensorPin = A0;`: Defines the analog pin (A0) for the gas sensor’s output.
- `int ledPin = 8;`: Defines the digital pin (8) for the LED.
- `Serial.begin(9600);`: Initializes serial communication at 9600 baud rate.
- `gasValue = analogRead(gasSensorPin);`: Reads the analog value (0-1023) from the sensor.
- `float voltage = gasValue * (5.0 / 1023.0);`: Converts the analog value to a voltage (0-5V).
- `if (gasValue > 300)`: Lights the LED if the gas value exceeds 300 (adjust this threshold based on your sensor’s sensitivity in Tinkercad).
- `delay(500);`: Pauses for 500ms between readings to avoid overwhelming the Serial Monitor.

## 5. Simulate and Test

### Start Simulation
- Click **Start Simulation** in Tinkercad’s top right corner.

### Open Serial Monitor
- Click the **Serial Monitor** button at the bottom of the code editor.
- Ensure the baud rate is set to **9600** (matching `Serial.begin(9600);`).

### Test the Gas Sensor
- In Tinkercad, click the gas sensor to open its properties panel. Adjust the simulated gas concentration (e.g., using the slider or input field) to mimic different gas levels.
- Observe the Serial Monitor for gas value and voltage readings.
- When the gas value exceeds 300, the LED should light up; otherwise, it remains off.

### Adjust Threshold
- If the LED triggers too easily or not at all, adjust the threshold value (300) in the code to match the sensor’s response in Tinkercad.

## 6. Troubleshooting

- **No Readings in Serial Monitor**:
  - Verify the baud rate is 9600 in both the code and Serial Monitor.
  - Check that the A0 pin is correctly connected to the sensor’s A0 pin.
- **LED Not Lighting**:
  - Ensure the LED is connected correctly (anode to pin 8, cathode to resistor to GND).
  - Adjust the threshold value (300) in the code if the gas values are outside the expected range.
- **Sensor Not Responding**:
  - Confirm all sensor pins (especially VCC and GND) are connected properly.
  - In Tinkercad, ensure the gas sensor is set to simulate varying gas levels.
- **Unstable Readings**:
  - Increase the `delay(500)` value to slow down readings, or check for loose connections in the Tinkercad workspace.

## 7. Next Steps

- **Add an LCD**: Use a 16x2 LCD to display gas values (refer to a LiquidCrystal library tutorial).
- **Add a Buzzer**: Connect a buzzer to alert when gas levels are high.
- **Calibrate the Sensor**: Experiment with different threshold values to fine-tune detection for specific gases (e.g., methane, LPG).
- **Save and Share**: Name your Tinkercad project and share the link to showcase your work.

✅ You have successfully set up and simulated a **6-pin gas sensor** with Arduino in Tinkercad![](https://www.instructables.com/Anay-Shah-Gas-Detector-Arduino-Tinkercad/)[](https://www.learnelectronicsindia.com/post/creating-a-gas-sensor-circuit-using-tinkercad)
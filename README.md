# Arduino-Sound-Detection-Based-Automation
Sound-Triggered Motor &amp; LED Project for Beginners
# Sound Sensor Controlled Motor & LED Project

## 🔊 How It Works
The sound sensor detects **clapping or any loud sound**, and sends a digital signal (`HIGH`) to the Arduino. Based on this signal:
- The **Arduino turns ON the motor and LED**.
- After a few seconds, the **Arduino turns them OFF again**.

---

## 🔌 Wiring Diagram Overview

### 🔈 Sound Sensor Module

| Sensor Pin | Connect To Arduino |
|------------|--------------------|
| VCC        | 5V                 |
| GND        | GND                |
| D0         | D2                 |

### ⚙️ DC Motor (via Transistor Circuit)

| Component              | Connection                                        |
|------------------------|--------------------------------------------------|
| Motor + (Red wire)     | 5V (External battery or Arduino 5V temporarily)  |
| Motor – (Black wire)   | Collector of NPN Transistor                      |
| Transistor Base        | Arduino D3 (via 1kΩ resistor)                    |
| Transistor Emitter     | GND                                              |
| Flyback Diode (1N4007) | Across motor terminals (Anode to Motor –, Cathode to +) |

### 💡 LED

| LED Leg           | Connection                   |
|------------------|------------------------------|
| Long (Anode)      | Arduino D4 (via 220Ω resistor) |
| Short (Cathode)   | GND                          |

---

## 🧠 Arduino Code

```cpp
const int soundPin = 2;   // Signal from sound sensor
const int motorPin = 3;   // Controls motor via transistor
const int ledPin = 4;     // Controls LED

void setup() {
  pinMode(soundPin, INPUT);   // Set sensor pin as input
  pinMode(motorPin, OUTPUT);  // Set motor control pin as output
  pinMode(ledPin, OUTPUT);    // Set LED pin as output
}

void loop() {
  int sound = digitalRead(soundPin); // Read sound signal

  if (sound == HIGH) {
    digitalWrite(motorPin, HIGH);  // Turn motor ON
    digitalWrite(ledPin, HIGH);    // Turn LED ON
    delay(3000);                   // Wait for 3 seconds
    digitalWrite(motorPin, LOW);   // Turn motor OFF
    digitalWrite(ledPin, LOW);     // Turn LED OFF
  }
}

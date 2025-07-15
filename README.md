# Arduino 4-Servo “Sweep → Hold” Demo

This project demonstrates how to control four Micro Servo (SG90) motors using an Arduino Uno in **Tinkercad Circuits**.

It performs a 2-second sweep (from 0° to 180° and back), then stops and holds all motors at 90°.

---

## 🧰 Components

- Arduino Uno R3  
- 4 × Micro Servo (SG90)  
- Jumper wires (male-to-female)  

> In Tinkercad, you don’t need an external power supply. The Arduino 5V rail is sufficient.

---

## 🔌 Wiring

| Servo | Signal Pin | VCC (5V)       | GND         |
|-------|------------|----------------|-------------|
| 1     | 9          | Arduino 5V     | Arduino GND |
| 2     | 10         | Arduino 5V     | Arduino GND |
| 3     | 11         | Arduino 5V     | Arduino GND |
| 4     | 3          | Arduino 5V     | Arduino GND |

![Wiring Diagram](images/Wiring.png)

---

## 💻 Code (`src/servo_sweep_hold.ino`)

```cpp
#include <Servo.h>

// attach four servos to any PWM pins you like
Servo s1, s2, s3, s4;
const int pin1 = 9;
const int pin2 = 10;
const int pin3 = 11;
const int pin4 = 3;

void setup() {
  s1.attach(pin1);
  s2.attach(pin2);
  s3.attach(pin3);
  s4.attach(pin4);

  unsigned long start = millis();
  int angle = 0;
  int step  = 1;      // degrees per iteration
  const int delayMs = 10;

  // run the classic “sweep” back and forth for 2 seconds
  while (millis() - start < 2000) {
    s1.write(angle);
    s2.write(angle);
    s3.write(angle);
    s4.write(angle);

    angle += step;
    if (angle <= 0 || angle >= 180) step = -step;

    delay(delayMs);
  }

  // after 2 s, park all servos at 90°
  s1.write(90);
  s2.write(90);
  s3.write(90);
  s4.write(90);
}

void loop() {
  // nothing to do here—servos stay at 90°
}

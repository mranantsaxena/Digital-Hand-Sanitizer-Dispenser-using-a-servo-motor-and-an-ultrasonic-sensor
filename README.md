# 🧴 Automatic Hand Dispenser — Arduino UNO

A touchless automatic hand sanitizer dispenser built using Arduino UNO, HC-SR04 ultrasonic sensor, and a servo motor. Simulated and tested on Tinkercad.

Simulation Link : https://www.tinkercad.com/things/fgr9Dz8ctDW-digital-hand-dispenser?sharecode=FqUha_WxQ4o1KYe16cgYsvhaExsQWlDCZz9Y7BMqyFs

## 📋 Description

This project uses an ultrasonic sensor to detect when a hand is placed within 20 cm of the dispenser. Once detected, the servo motor rotates 90 degrees to press the pump and dispense sanitizer automatically. When the hand is removed, the servo returns to its original position.

---

## 🛠️ Components Used

- Arduino UNO
- HC-SR04 Ultrasonic Sensor
- Servo Motor
- Breadboard
- Jumper Wires

---

## 🔌 Pin Connections

| Component | Pin |
|---|---|
| HC-SR04 VCC | Arduino 5V |
| HC-SR04 GND | Arduino GND |
| HC-SR04 TRIG | Arduino Digital Pin 7 |
| HC-SR04 ECHO | Arduino Digital Pin 6 |
| Servo Signal | Arduino Digital Pin 5 |
| Servo VCC | Arduino 5V |
| Servo GND | Arduino GND |

---

## ⚙️ How It Works

1. The ultrasonic sensor continuously measures distance
2. When a hand is detected within **20 cm**, the servo rotates to **90°** and dispenses sanitizer
3. The servo holds for **2 seconds**
4. The servo automatically returns to **0°**
5. The system waits **1 second** and is ready for the next dispense

---

## 💻 Code

```cpp
#include <Servo.h>

Servo myServo;

const int trigPin  = 7;
const int echoPin  = 6;
const int servoPin = 5;

void setup() {
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  myServo.attach(servoPin);
  myServo.write(0);
  Serial.println("Ready!");
}

void loop() {
  long duration, distance;

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration / 29 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance >= 1 && distance <= 20) {
    Serial.println("DISPENSING!");
    myServo.write(90);
    delay(2000);
    myServo.write(0);
    delay(1000);
  }

  delay(500);
}
```

---

## 🖥️ Simulation

This project was fully built and simulated on **Tinkercad Circuits**. Open the Serial Monitor during simulation and drag the ultrasonic sensor slider below 20 cm to trigger the dispenser.

---

## 🚀 Future Improvements

- Add an LCD display to show distance in real time
- Add a buzzer alert when sanitizer is low
- Use a water pump instead of a servo for real dispensing
- Add a counter to track number of dispenses

---

## 👨‍💻 Author

Made with ❤️ using Tinkercad and Arduino UNO

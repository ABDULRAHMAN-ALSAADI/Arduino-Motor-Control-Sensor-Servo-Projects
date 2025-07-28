# 🚀 Arduino Motor Control & Sensor Servo Projects

This repository contains two Arduino projects created and simulated using **Tinkercad** as part of my learning and internship tasks. Each project demonstrates different real-world control mechanisms using sensors, motors, and driver ICs.

---

## ⚙️ Project 1: 4-Motor Vehicle Control with L293D

TinkerCad link : https://www.tinkercad.com/things/lz9jEudcWxk-servo-with-ultrasonic

### 🛠️ Components Used:
- 1 × Arduino Uno
- 1 × L293D Motor Driver IC
- 4 × DC Motors
- Power Supply (from Arduino)
- Jumper wires and breadboard

### 🎯 Behavior:
The 4 motors are connected via the L293D IC and controlled in timed sequences:
- Move **Forward** for 30 seconds
- Move **Backward** for 60 seconds
- Turn **Left** for 30 seconds
- Turn **Right** for 30 seconds

This project simulates a basic directional robot controlled by time-based logic.

### 📷 Screenshots  
<img width="1706" height="727" alt="TASK 5 ELECTRIC" src="https://github.com/user-attachments/assets/e4b1bd47-4719-443d-8e15-0fcbc5cb3361" />

### 🧠 code

```cpp
// Motor Pins
const int motor1 = 5;
const int motor2 = 6;
const int motor3 = 9;
const int motor4 = 10;

void setup() {
  pinMode(motor1,OUTPUT);
  pinMode(motor2,OUTPUT);
  pinMode(motor3,OUTPUT);
  pinMode(motor4,OUTPUT);
  
  // Move Forward
  digitalWrite(motor1, LOW);
  digitalWrite(motor2, HIGH);
  digitalWrite(motor3, LOW);
  digitalWrite(motor4, HIGH);
  delay(30000);
 
  // Move Backward
  digitalWrite(motor1, HIGH);
  digitalWrite(motor2, LOW);
  digitalWrite(motor3, HIGH);
  digitalWrite(motor4, LOW);
  delay(60000);
 
  // Turn Right and Lift  
  digitalWrite(motor1, HIGH);
  digitalWrite(motor2, LOW);
  digitalWrite(motor3, LOW);
  digitalWrite(motor4, HIGH);
  delay(30000);
  
  digitalWrite(motor1, LOW);
  digitalWrite(motor2, HIGH);
  digitalWrite(motor3, HIGH);
  digitalWrite(motor4, LOW);
  delay(30000);
  
  // STOP MOTOR 
  digitalWrite(motor1, LOW);
  digitalWrite(motor2, LOW);
  digitalWrite(motor3, LOW);
  digitalWrite(motor4, LOW);
  
}

void loop() {
 
  
  }

```

---

## 🤖 Project 2: Servo with Ultrasonic Distance Detection

## 🔧 Note:

This circuit was originally meant to be built using an L293D motor driver shield, but the shield is not available in simulation platforms like Tinkercad, Wokwi, or Proteus.
Although the L293D IC is available, it only works correctly with DC motors in these simulators — it doesn't function properly with servo motors.
As a result, I implemented the circuit without the L293D to simulate the desired behavior using available components.

### 🛠️ Components Used:
- 1 × Arduino Uno
- 1 × HC-SR04 Ultrasonic Sensor
- 1 × Servo Motor
- 
### 🎯 Behavior:
This circuit controls a servo motor based on distance readings from the ultrasonic sensor:

- If **no object is near** (`distance > 10 cm`):  
  → The servo rotates **between 0° and +90°** quickly.

- If an **object is detected within 10 cm**:  
  → The servo **stops for 1 second**,  
  → Then rotates **between 0° and -90°** (simulated using 180°).

  ---

### 📷 Screenshots 

<img width="1706" height="727" alt="Spectacular Curcan-Leelo" src="https://github.com/user-attachments/assets/832872ba-c212-4b1e-8972-84deb28ae002" />

### 🧠 Code 

```cpp
#include <Servo.h>

Servo myServo;

const int trigPin = 7;
const int echoPin = 6;
const int servoPin = 9;

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  myServo.attach(servoPin);
  Serial.begin(9600);
}

void loop() {
  // Measure distance
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance > 10 || distance == 0) {
    // Object far — swing between 0 and +90 fast
    myServo.write(0);
    delay(200);
    myServo.write(90);
    delay(200);
  } else {
    // Object near — pause then swing between 0 and -90
    delay(1000);
    myServo.write(0);
    delay(200);
    myServo.write(180); // -90° direction
    delay(200);
  }
}
```
  

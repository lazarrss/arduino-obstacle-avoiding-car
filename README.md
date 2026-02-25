# Arduino Robot Car (L293D Motor Shield + HC-SR04 + Servo)

An autonomous robot car built with **Arduino Uno** and an **L293D Motor Control Shield**, using **two DC motors** for movement, an **HC-SR04 ultrasonic sensor** for distance measurement, and a **servo motor** to move the sensor mount.

This project combines purchased and existing components; the hardware assembly and the full control code were developed independently.

---

## Components
- Arduino Uno
- Motor Control Shield (L293D + 74HC595)
- 2× DC motors (with gearbox)
- HC-SR04 ultrasonic sensor
- Servo motor (sensor mount)
- Chassis, wiring, and power supply

---

## Procurement (how the parts were sourced)
- Robot chassis and DC motors: AliExpress  
- HC-SR04 ultrasonic sensor and servo motor: local electronics store (Belgrade)  
- Arduino Uno, Motor Control Shield, wires, and power supply: already available

---

## System Architecture

The system consists of three main blocks:

1) **Arduino Uno** – control logic (reads sensors, makes decisions, outputs control signals)  
2) **Motor Control Shield** – motor power and direction control  
3) **Sensors & actuators** – interaction with the environment (HC-SR04 + servo + DC motors)

Arduino processes sensor data and decides what to do, while the motor driver executes physical movement.

---

## Key Hardware Details

### Arduino Uno
Runs the program, reads sensor data, and sends control signals to the motor driver.  
It cannot power DC motors directly due to limited output current, so a motor driver is required.

### Motor Control Shield (L293D)
Acts as an interface between Arduino and the DC motors.

- **L293D** provides H-bridge motor control:
  - changes motor direction
  - supplies enough current/voltage for motor operation
- **74HC595 shift register** allows controlling more outputs with fewer Arduino pins,
  meaning some Arduino pins are reserved and cannot be used for other components.

### DC Motors
Two geared DC motors (left and right wheel), connected to **M3** and **M4** outputs on the motor shield.  
Direction is changed by switching polarity inside the L293D H-bridge.

### Servo Motor
Moves the sensor mount. The servo is controlled directly from Arduino (not through the motor driver) because it has its own internal electronics and only requires:
- PWM signal
- power (5V)
- ground (GND)

### Ultrasonic Sensor (HC-SR04)
Measures distance using ultrasound. Arduino triggers a short pulse on **TRIG**, the sensor emits ultrasound and listens for the echo.  
The **ECHO** pulse width corresponds to travel time and is used to compute distance.

---

## Wiring / Pin Mapping

### Pins used by Motor Shield
- **D4** – LATCH (74HC595)
- **D7** – ENABLE
- **D8** – DATA
- **D12** – CLOCK
- **D3, D5, D6, D11** – PWM signals for motor speed control

### Motors
- Left & right DC motors → **M3** and **M4** on the motor shield

### Servo Motor
- Signal → **D9**
- VCC → **5V**
- GND → **GND**

### HC-SR04
- VCC → **5V**
- GND → **GND**
- TRIG → **D2**
- ECHO → **D13**

Pins **D2** and **D13** were chosen because they are not used by the motor shield.

---

## Power

- Arduino, servo, and ultrasonic sensor use **5V**
- DC motors use a **separate motor supply** through the shield’s **EXT_PWR** connector
- All components share **common ground (GND)**, which is required for stable operation

Separating motor power helps avoid voltage drops and noise caused by the motors.

---

## Physical Assembly

- Chassis assembled according to manufacturer instructions
- DC motors mounted to the chassis
- Motor Control Shield stacked directly on Arduino Uno
- Motors connected to **M3/M4** via screw terminals on the shield
- Servo and HC-SR04 mounted at the front of the robot
- All components connected with a shared ground

---

## Software

The code is written from scratch and includes:
- DC motor control via the motor shield
- Servo control via PWM
- Distance reading from the HC-SR04
- Movement logic (square movement + obstacle reactions)

The code is structured into functions for readability and easier extension.

---

## Project Goal

The goal is to understand how microcontrollers, motor drivers, and sensors work together, while independently assembling the hardware and writing the control software.  
This project can serve as a foundation for further robotics improvements.

---

## Authors
Milica Mitrović, Lazar Stojanović

---

## Video

https://github.com/user-attachments/assets/3c1dffab-615d-453e-a5f6-fa4fef0758a9

## Pictures

![arduino3](https://github.com/user-attachments/assets/eda07da6-2221-46be-833d-07ae303fff5c)
![arduino2](https://github.com/user-attachments/assets/958577e1-8cb0-433d-9b0a-df58cb623fd4)
![arduino1](https://github.com/user-attachments/assets/412fe774-9205-45ac-b068-cad3735ebc36)




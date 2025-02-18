# Smart Door Project

## Overview
The Smart Door project introduces a modern approach to automated door systems by integrating infrared (IR) sensing technology with the CH32V003 RISC-V processor. The system functions by detecting objects within its range using an IR sensor, which communicates detection signals to the processor. Upon receiving these signals, the processor controls a servo motor to open or close the door automatically, providing smooth and convenient access control. This project aims to deliver a secure, efficient, and user-friendly solution for door automation, removing the need for manual operation.

## Components Required
- **CH32V003 RISC-V Processor**
- **IR Sensor**
- **Servo Motor (SG90)**
- **Power Supply**
- **Breadboard**
- **Jumper Wires**

### Component Specifications
The CH32V003 RISC-V processor operates with a supply voltage between 1.8V and 3.6V, offering versatile GPIO pins for device interfacing and support for communication protocols like SPI, I2C, and UART. The IR sensor functions at 3.3V or 5V, detecting infrared radiation emitted or reflected by nearby objects and converting it into an electrical signal. The servo motor requires a voltage supply between 4.8V and 6V and uses PWM signals for accurate position control, with its current draw depending on the applied load and torque.

## Circuit Connections
### IR Sensor
- **Signal Pin**: Connected to **PD3** of the CH32V003 processor.
- **VCC Pin**: Connected to the **3.3V** supply pin.
- **GND Pin**: Connected to the **GND** pin of the processor.

The IR sensor generates digital signals to indicate the presence of an object, which the processor uses to initiate the door-opening mechanism.

### Servo Motor
- **Control Pin (PWM)**: Connected to **PD2** of the CH32V003 processor.
- **VCC Pin**: Connected to a **5V** power supply.
- **GND Pin**: Connected to the **GND** pin of the processor.

The servo motor's position is regulated by PWM signals from the processor, enabling smooth and controlled door movements.

With these connections in place, the Smart Door system efficiently detects motion, activates the servo motor, and automates the door's operation without manual intervention.
| **Component**   | **Pin**           | **CH32V003x Pin** |
|---------------- |-------------------|-------------------|
|Servo Motor(SG90)| VCC (Red Wire)  | VIN                 |
|                 | PWM (Yellow Wire) | PD2               |
|                 | GND (Brown Wire)  | GND               |
| IR Sensor       | VCC               | VIN               |
|                 | OUT               | PD3               |
|                 | GND               | GND               |

### Diagram
![Cirkit Designer IDE - Brave 16-02-2025 10 58 51 PM](https://github.com/user-attachments/assets/f980c916-6f78-4620-96ee-b5703fe341d3)

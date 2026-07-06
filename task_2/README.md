# Task 2: Sensor-Based Simulation - IoT Radar System

---

## Project Title
**Ultrasonic Radar System using Arduino**

## Project Description
This project simulates a real-time **Radar System** using an Ultrasonic Sensor, Servo Motor, and OLED Display. The system continuously sweeps the area using a servo motor and detects objects with the help of an HC-SR04 Ultrasonic Sensor. The detected distance is displayed both on the OLED screen and visualized like a radar.

This simulation was developed and tested on **Wokwi**, an excellent online Arduino and IoT simulator.

## Simulation Platform
- **Software**: [Wokwi - Online Arduino Simulator](https://wokwi.com/)  
- Wokwi is a powerful browser-based simulator that allows us to build and test IoT projects without physical hardware.

## Components Used (Virtual)
- Arduino Uno
- HC-SR04 Ultrasonic Sensor
- MG90S Servo Motor
- SSD1306 OLED Display (128x64)

## Working Principle
1. The Servo Motor rotates from 0° to 180° continuously (sweeping motion).
2. At each position, the Ultrasonic Sensor measures the distance to any object in front.
3. The distance is displayed on the OLED screen.
4. A simple radar-like visualization is also shown on the OLED display.

## How to Run the Project
1. Open the project in [Wokwi](https://wokwi.com/).
2. Click on the **Play** button to start the simulation.
3. Observe the servo movement and real-time distance readings on the OLED.

## Screenshots
*(Screenshots folder lo unnai)*

- `circuit.png` → Complete Circuit Diagram
- `simulation.png` → Running Simulation
- `output1.png`, `output2.png` → Different outputs

## Wokwi Project Link
(Paste your Wokwi Share link here)

---

## Code File
`sketch.ino` - Full Arduino Code is available in this folder.

---

**Submitted as part of CodeAlpha IoT Internship - June 2026 Batch**

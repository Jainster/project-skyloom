# Quadcopter Project using Espressif SDK (Project Skyloom)

This project implements a quadcopter controlled by an **ESP32** microcontroller, utilizing the **Espressif SDK** and FreeRTOS for real-time task management. The system handles sensor integration, motor control, overheating protection, and battery management without relying on a traditional flight controller.

## Technology Stack

- **ESP32 (Espressif SDK)**: Central control unit, responsible for handling real-time tasks, sensor data, motor control, and communication.
- **FreeRTOS**: Manages concurrent tasks, ensuring low-latency handling of sensor data and motor control loops.
- **DC Motors with PWM Control**: Controls standard DC motors via PWM signals for precise speed adjustment and flight stability.
- **10-Axis IMU (Inertial Measurement Unit)**: Provides real-time orientation, gyroscopic, and accelerometer data to stabilize flight.
- **Battery Management**: Monitors battery health, voltage, and current to avoid power failure mid-flight.
- **Overheating Management**: Continuously monitors the temperature of the motors and the ESP32, shutting down components when overheating thresholds are crossed.
- **Wireless Communication**: Supports ESP-NOW or Wi-Fi for sending and receiving commands from a remote controller or base station.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo-name/quad-project.git
   cd quad-project

# Project Skyloom: Quadcopter using Espressif SDK (ESP32)

**Project Skyloom** is a quadcopter powered by an **ESP32** microcontroller, using the **Espressif SDK** and **FreeRTOS** for real-time task scheduling. The system controls motor drivers, integrates sensor data, manages power, and facilitates wireless communication to enable autonomous and remote-controlled flight.

## Architecture Overview

The project follows a **modular architecture**, where subsystems like sensors, motors, and communication function as independent components. These components operate through **FreeRTOS tasks** and **queues**, ensuring real-time performance. This approach allows for easy expansion or modification without impacting overall stability.

### Core Modules and Interactions

1. **Control Unit (ESP32)**:
   - **Role**: The ESP32 serves as the central controller, managing sensor data, motor control, and communication.
   - **Responsibilities**:
     - Processes real-time data from the IMU sensor to maintain flight stability.
     - Executes control algorithms to adjust motor speeds via PWM signals.
     - Monitors battery levels and manages power consumption.
   - **Design**: Runs **FreeRTOS** with dedicated tasks for each subsystem (IMU, motor control, communication). These tasks interact via message queues to ensure real-time, low-latency performance.

2. **Motor Control System**:
   - **Role**: Controls the quadcopter’s motors via **PWM** using two **TB6612 motor drivers**.
   - **Responsibilities**: Adjusts motor speeds based on real-time control inputs for stable flight.
   - **Design**: A FreeRTOS task generates PWM signals for the motor drivers, continuously adjusting motor speeds in response to IMU data.

3. **Sensor Integration (IMU)**:
   - **Role**: The **GY-91 IMU** sensor provides real-time orientation, gyroscope, and accelerometer data.
   - **Responsibilities**: Feeds sensor data to the control unit for flight stabilization.
   - **Design**: Communicates with the ESP32 via I2C/SPI. A FreeRTOS task handles sensor data processing and forwards it to the motor control task for real-time adjustments.

4. **Battery Management**:
   - **Role**: Monitors battery voltage and current, ensuring safe operation.
   - **Responsibilities**: Provides alerts for low battery levels and initiates safe shutdowns when necessary.
   - **Design**: A FreeRTOS task periodically checks the battery's health and interacts with other components when thresholds are crossed.

5. **Wireless Communication (Remote Controller)**:
   - **Role**: The quadcopter can be remotely controlled using **ESP-NOW** or **Wi-Fi**. The remote not only sends flight commands but can also receive important telemetry data like battery status, orientation, and other critical metrics.
   - **Responsibilities**:
     - Sends flight control commands to the quadcopter from a remote device.
     - Receives telemetry data for status monitoring and potential adjustments.
   - **Design**: A FreeRTOS task manages communication, exchanging messages with other tasks to relay control commands and send back critical flight data.

## Technology Stack

- **ESP32 (Espressif SDK)**: The main control unit responsible for managing real-time tasks, sensor data, motor control, and wireless communication.
- **FreeRTOS**: Manages the concurrent execution of tasks such as sensor data processing, motor control, and communication.
- **DC Motors with PWM Control**: Motors are driven by PWM signals from the **TB6612 motor drivers**, adjusting speed for flight stabilization.
- **9-Axis GY-91 IMU**: Provides real-time orientation, gyroscope, and accelerometer data.
- **Battery Management**: Monitors the health of the battery to avoid power failures mid-flight.
- **Wireless Communication**: Supports **ESP-NOW** or **Wi-Fi** for remote control and telemetry data transfer between the quadcopter and the controller.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo-name/skyloom.git
   cd skyloom

# Project Skyloom: Quadcopter using Espressif SDK (ESP32)

**Project Skyloom** is a quadcopter powered by an **ESP32** microcontroller using the **Espressif SDK** and **FreeRTOS** for real-time task scheduling and control. The architecture handles critical functions like sensor integration, motor control, power management, and communication within a real-time environment, enabling autonomous flight without a traditional flight controller.

## Architecture Overview

The system follows a **modular architecture**, where subsystems—sensors, motors, communication, and safety features—operate as independent components. These components interact through **FreeRTOS tasks** and **queues**, ensuring responsive, real-time performance. This design supports scalability and robustness, allowing developers to easily extend or modify individual components without impacting overall system stability.

### Core Modules and Interactions

1. **Control Unit (ESP32)**:
   - **Role**: Acts as the central controller, coordinating sensor data, motor control, and wireless communication.
   - **Responsibility**: 
     - Receives data from the IMU sensor for orientation and stability.
     - Executes real-time control algorithms to adjust motor speeds using PWM signals.
     - Manages power consumption, battery health, and overheating.
   - **Design**: Runs **FreeRTOS**, where each subsystem (IMU, motor control, communication) operates as a dedicated task. Tasks interact via message queues to ensure real-time, low-latency performance.

2. **Motor Control System**:
   - **Role**: Controls the quadcopter’s DC motors using **PWM (Pulse Width Modulation)**.
   - **Responsibility**: Adjusts motor speeds based on control signals for stable flight.
   - **Design**: PWM control is implemented within a FreeRTOS task that continuously adjusts motor speeds in real-time based on sensor input.

3. **Sensor Integration (IMU)**:
   - **Role**: A 10-axis **Inertial Measurement Unit (IMU)** supplies real-time orientation, gyroscopic, and accelerometer data.
   - **Responsibility**: Feeds the control unit with sensor data for flight stabilization.
   - **Design**: Communicates via I2C/SPI and is managed by a FreeRTOS task that processes data and sends it to the motor control task for real-time adjustments.

4. **Battery Management**:
   - **Role**: Monitors battery health, voltage, and current to prevent mid-flight power failure.
   - **Responsibility**: Ensures safe battery operation by providing alerts when voltage is low and safely powers down when needed.
   - **Design**: Managed by a FreeRTOS task that periodically checks battery levels and interacts with other components when thresholds are crossed.

5. **Overheating Protection**:
   - **Role**: Monitors the temperature of motors and the ESP32, preventing component damage.
   - **Responsibility**: Shuts down or reduces power to components when overheating is detected.
   - **Design**: Implemented as an independent task that monitors temperature sensors and triggers emergency sequences when necessary.

6. **Wireless Communication**:
   - **Role**: Supports remote control and telemetry via **ESP-NOW** or **Wi-Fi**.
   - **Responsibility**: Receives flight commands from a remote controller or base station and transmits telemetry data (e.g., battery status, orientation).
   - **Design**: A dedicated task handles wireless communication, interacting with other tasks through message queues to send or receive data.

## Technology Stack

- **ESP32 (Espressif SDK)**: The central control unit responsible for managing real-time tasks, sensor data, motor control, and wireless communication.
- **FreeRTOS**: Manages concurrent tasks, ensuring low-latency handling of sensor data and motor control loops.
- **DC Motors with PWM Control**: Drives the quadcopter’s motors using PWM signals for speed adjustment and flight stability.
- **10-Axis IMU (Inertial Measurement Unit)**: Provides real-time orientation, gyroscopic, and accelerometer data to stabilize the flight.
- **Battery Management**: Monitors battery health, voltage, and current to avoid power failure mid-flight.
- **Overheating Management**: Continuously monitors motor and ESP32 temperature, shutting down components when overheating thresholds are crossed.
- **Wireless Communication**: Supports **ESP-NOW** or **Wi-Fi** for sending and receiving commands from a remote controller or base station.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo-name/skyloom.git
   cd skyloom

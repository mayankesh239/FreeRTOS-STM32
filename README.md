# 🚀 STM32 FreeRTOS Project Collection

This repository contains a collection of STM32 embedded projects built using **STM32CubeIDE** and **FreeRTOS**, demonstrating essential real-time OS features such as mutexes, semaphores, task prioritization, queue-based communication, and GPIO control.

All projects target the **STM32 Nucleo-F401RE** board and communicate debug messages over **USART2 (115200 baud)** using a UART terminal Moserial.

---

## 📁 Project List

### 🧵 Mutex Priority Inversion Demonstration
Simulates **priority inversion** with two tasks (High and Medium priority) competing for a mutex to access UART.
- 🔐 FreeRTOS Mutex
- 🧠 Priority Inversion Simulation
- 🛠 HPT blocks when MPT holds the mutex

### 🔁 Queue-Based Inter-Task Communication
Demonstrates **FreeRTOS queues** with two sender tasks (High & Low priority) and a receiver task.
- 📤 Sender_HPT → sends 222 every 2s
- 📤 Sender_LPT → sends 111 every 1s
- 📥 Receiver prints messages every 3s

### 🚦 Semaphore-Based GPIO Sync
Uses a **binary semaphore** for task synchronization and user-button-triggered control via **PC13** GPIO.
- 🔧 CMSIS-RTOS API
- 🧠 Tasks: High, Normal, Low
- 👆 NormalTask waits for button press
- 🔁 HighTask gets blocked until semaphore is released

### 🕹️ Task Scheduling & Dynamic Control
Demonstrates **task suspension/resumption** and preemption in FreeRTOS.
- 🧠 Task1 (Normal): 1s loop
- 🚀 Task2 (Above Normal): 2s loop
- ⏸️ Task1 suspended at 4th Task2 run, resumed at 7th

### 💡 Dual LED Blinking
A simple STM32 project blinking two LEDs at different intervals using **STM32 HAL**.
- 🟢 LED1 → 1s delay
- 🔴 LED2 → 2s delay

---

## 🛠 Setup & Requirements

- **Board**: STM32 Nucleo-F401RE
- **IDE**: STM32CubeIDE
- **RTOS**: FreeRTOS (CMSIS v1 or v2)
- **Terminal**: Moserial / PuTTY / TeraTerm
- **Baudrate**: 115200 (USART2)
- **OS**: Linux or Windows

### UART Configuration
| Parameter       | Value        |
|----------------|--------------|
| Baud Rate      | 115200       |
| Data Bits      | 8            |
| Stop Bits      | 1            |
| Parity         | None         |
| Flow Control   | None         |
| Port           | /dev/ttyACMx or COMx |

---

## 🧪 Running the Projects

1. Open the desired project in **STM32CubeIDE**.
2. Build and flash it to your STM32 Nucleo board.
3. Open your serial terminal and connect to the correct port at **115200 baud**.
4. Observe the UART messages for behavior and task interaction.

---

## 🎯 Learning Objectives

These projects aim to provide hands-on experience with:
- Real-time task scheduling and delays
- Mutex and semaphore synchronization
- Queue-based communication
- GPIO-triggered task synchronization
- Task preemption and dynamic control
- STM32 HAL with FreeRTOS integration

---

## 📸 Sample Outputs
### 💡 Dual LED Blinking
https://github.com/user-attachments/assets/e94aba7f-35ae-41b2-b04c-0cd07f7cb909

### 🧵 Mutex Priority Inversion Demonstration
![image](https://github.com/user-attachments/assets/cb2e021b-c87f-4081-b5b0-97ad3590666d)

### 🔁 Queue-Based Inter-Task Communication
![image](https://github.com/user-attachments/assets/28f9a019-cfd1-46c3-9984-edc19c90f692)

### 🚦 Semaphore-Based GPIO Sync
![image](https://github.com/user-attachments/assets/da03fa88-5d26-4134-b5aa-a19a4c258ef2)


### 🕹️ Task Scheduling & Dynamic Control
![image](https://github.com/user-attachments/assets/23d97d68-c6ba-4f7e-83cf-00d465a17446)    


Sample UART logs and images of Moserial output can also be found inside each project folder.

---
Each folder includes:
- `Core/` source files
- `.ioc` configuration file
- `README.md` with project-specific instructions

---

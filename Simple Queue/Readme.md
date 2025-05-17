# STM32 FreeRTOS Queue Communication Example

This repository demonstrates a FreeRTOS project on an STM32 Nucleo board using **inter-task communication** through a **queue**. The system involves **two sender tasks** (one high-priority, one low-priority) and a **receiver task**, with UART2 output used for logging via a serial terminal (e.g., Moserial, Tera Term, PuTTY).

## 🛠️ Features

- Implements **FreeRTOS Queue** for inter-task communication.
- Three tasks:
  - **Sender_HPT**: High-priority sender that sends a constant value `222`.
  - **Sender_LPT**: Low-priority sender that sends a constant value `111`.
  - **Receiver**: Receives integers from the queue and prints over UART.
- Queue depth of 5.
- UART logging via USART2 at 115200 baud.
- UART interrupt used for receiving external input (prepared for future extensions).

## 🔧 Requirements

- **Board**: STM32F401RE Nucleo (or compatible)
- **IDE**: STM32CubeIDE
- **Toolchain**: HAL library with FreeRTOS enabled
- **Terminal**: Any serial terminal (Moserial, PuTTY, etc.)

## 🚀 How it works

1. On startup, the integer queue is created with capacity for 5 `int` elements.
2. `Sender_HPT_Task` and `Sender_LPT_Task` send values to the queue every 2s and 1s respectively.
3. `Receiver_Task` receives from the queue every 3s and transmits the received value over UART.
4. If the queue creation fails, a message is logged.

### 🧠 Task Priorities

| Task Name     | Priority | Delay (ms) | Sends |
|---------------|----------|------------|-------|
| Sender_HPT    | 3 (high) | 2000       | `222` |
| Sender_LPT    | 2        | 1000       | `111` |
| Receiver      | 1        | 3000       | N/A   |

## 📦 Output Example
![image](https://github.com/user-attachments/assets/28f9a019-cfd1-46c3-9984-edc19c90f692)

## 🧪 How to Test
- Flash the code to the STM32 Nucleo board using STM32CubeIDE.
- Connect to USART2 (typically via STLink USB port).
- Open a serial terminal (baud rate: 115200).
- Observe the message flow between sender and receiver tasks.

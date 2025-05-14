# ⚙️ STM32 FreeRTOS Example – Task Scheduling with Priorities

This project demonstrates a basic STM32 FreeRTOS application using STM32CubeIDE where two tasks run with different priorities and periodic delays.

- ✅ **Task1 (Default Task)**: Executes every 1 second with normal priority.
- ✅ **Task2**: Executes every 2 seconds with higher priority than Task1.
- ✉️ Each task transmits a message over UART (`USART2`) to indicate execution.

---

## 📌 Target Hardware

- **Board**: Nucleo-F401RE (or compatible STM32 board)
- **MCU**: STM32F401RE
- **IDE**: STM32CubeIDE
- **RTOS**: FreeRTOS (CMSIS-RTOS v1 API)

---

## 🧠 Task Behavior

| Task Name     | Priority        | Execution Interval | Action                        |
|---------------|------------------|---------------------|-------------------------------|
| Default Task  | `osPriorityNormal` | 1 second            | Sends `"Hello, Task1 here!!"` |
| Task2         | `osPriorityAboveNormal` | 2 seconds            | Sends `"Hello, Task2 here!!"` |

Even though Task2 runs less frequently, it can **preempt** Task1 if it becomes ready during Task1's execution due to its **higher priority**.

---

## 📡 UART Configuration

- **Port**: `USART2`
- **Baud Rate**: `115200`
- **Settings**: 8-N-1, No Flow Control
- **TX Pin**: `PA2` (Nucleo ST-Link virtual COM port)

---

## Output

![image](https://github.com/user-attachments/assets/09a56b09-7cc1-4723-967e-35277eb11814)

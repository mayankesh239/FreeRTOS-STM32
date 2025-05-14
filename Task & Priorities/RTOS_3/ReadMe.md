# ⚙️ STM32 FreeRTOS Example – Task Scheduling with Priorities

This project demonstrates a basic STM32 FreeRTOS application using STM32CubeIDE where two tasks run with different priorities and periodic delays.

- ✅ **Task1 (Default Task)**: Executes every 1 second with normal priority.
- ✅ **Task2**: Executes every 2 seconds with higher priority than Task1.
- ✉️ Each task transmits a message over UART (`USART2`) to indicate execution.
- 🧩 Task2 suspends and resumes Task1 based on internal logic.

---

## 📌 Target Hardware

- **Board**: Nucleo-F401RE (or compatible STM32 board)
- **MCU**: STM32F401RE
- **IDE**: STM32CubeIDE
- **RTOS**: FreeRTOS (CMSIS-RTOS v1 API)

---

## 🧠 Task Behavior

| Task Name     | Priority                 | Execution Interval | Action                        |
|---------------|---------------------------|---------------------|-------------------------------|
| Default Task  | `osPriorityNormal`        | 1 second            | Sends `"Hello, Task1 here!!"` |
| Task2         | `osPriorityAboveNormal`   | 2 seconds           | Sends `"Hello, Task2 here!!"`<br>Suspends and resumes Task1 |

**Task Preemption:**  
Although Task2 runs less frequently, its higher priority allows it to preempt Task1 when both are ready.

**Suspend/Resume Logic:**

- When Task2 prints its message for the **4th time**, it **suspends** the Default Task.
- When Task2 prints its message for the **7th time**, it **resumes** the Default Task.

This demonstrates **dynamic task control** in FreeRTOS using `osThreadSuspend()` and `osThreadResume()`.

---

## 📡 UART Configuration

- **Port**: `USART2`
- **Baud Rate**: `115200`
- **Settings**: 8-N-1, No Flow Control
- **TX Pin**: `PA2` (Nucleo ST-Link virtual COM port)

---

## 📤 Output Example

![image](https://github.com/user-attachments/assets/23d97d68-c6ba-4f7e-83cf-00d465a17446)


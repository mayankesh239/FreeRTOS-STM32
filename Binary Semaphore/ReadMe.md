# RTOS-Based STM32 Project with Semaphore Synchronization

## Overview

This STM32-based embedded project demonstrates the use of FreeRTOS (CMSIS-RTOS) with semaphores and thread prioritization. Three tasks — High, Normal, and Low priority — compete to access a shared resource using a binary semaphore. The program communicates over UART to show task execution flow.

## Features

- Uses **CMSIS-RTOS (FreeRTOS)** for real-time task management.
- Implements **binary semaphore** for mutual exclusion.
- Demonstrates task priority handling (`AboveNormal`, `Normal`, and `BelowNormal`).
- Integrates **UART communication** for runtime debug messages.
- Uses **GPIO input** (User Button on PC13) for task synchronization.
- Compatible with **Moserial** terminal for UART monitoring on Linux.

## Hardware

- STM32 Nucleo/Discovery board (tested with STM32F4 series).
- User Push Button (connected to `PC13`).
- UART2 used for debugging (`TX`/`RX` via USB).

## UART Configuration

- **Baud rate:** 115200  
- **Data bits:** 8  
- **Stop bits:** 1  
- **Parity:** None  
- **Flow control:** None

## Terminal Setup (Moserial)

Install `moserial` on Linux:

```bash
sudo apt install moserial
```

## Configure moserial with:

- **Port:** /dev/ttyUSBx or /dev/ttyACMx (depending on your board)
- **Baud rate:** 115200
- **Flow control:** None
- **Encoding:** ASCII
- **✅ Enable “**Show Control Characters**” for better debug visibility

## Task Behavior
- **Low Task:** Continuously runs and prints messages every 500ms.
- **High Task:** Attempts to acquire semaphore and logs messages.
- **Normal Task:**
  - Waits for semaphore.
  - Waits for button press (PC13 goes LOW) before releasing semaphore.
  - Demonstrates external input synchronization with RTOS.

> 🔴 Make sure to press the user button to let the NormalTask proceed. This sets GPIOC pin 13 to LOW.



## Dependencies
- STM32 HAL drivers
- CMSIS-RTOS (FreeRTOS)
- STM32CubeMX for project generation

## Output
![image](https://github.com/user-attachments/assets/da03fa88-5d26-4134-b5aa-a19a4c258ef2)



## Explaination

Here's a clear breakdown of what's happening in your output log:

---

### 🔧 **Background Setup**

User has:

* **3 FreeRTOS tasks**: `HighTask`, `NormalTask`, and `LowTask`.
* A **binary semaphore** used for synchronization.
* `NormalTask` waits on GPIO pin `PC13` to go **LOW** (i.e., user button press).
* All tasks use `HAL_UART_Transmit()` to print debug messages.
* `HighTask` has higher priority than `NormalTask`, and `LowTask` has lower priority.

---

### 🧵 Output Breakdown

```
Entered HighTask and waiting for semaphore
Semaphore acquired by high task
Leaving HighTask and releasing the semaphore
```

✅ `HighTask` starts first (due to higher priority).
✅ It acquires the semaphore and finishes execution, releasing the semaphore.

---

```
Entered NormalTask and waiting for semaphore
Semaphore acquired by normal task
```

✅ Now `NormalTask` starts and **acquires the semaphore**.
⏳ It is now **waiting for GPIO pin PC13 to go LOW** (i.e., for user to press the button). It halts at this line:

```c
while(HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13)); // waits while pin is HIGH
```

So execution is paused **until user press the button**.

---

```
Entered HighTask and waiting for semaphore
```

✅ `HighTask` again becomes ready and tries to acquire the semaphore, but **can't**, because `NormalTask` hasn't released it yet (still waiting for GPIO press). So it blocks here.

---

```
Leaving NormalTask and releasing the semaphore
```

✅ user **pressed the button**, GPIOC pin 13 goes LOW, so `NormalTask` proceeds, prints this, and releases the semaphore.

---

```
Semaphore acquired by high task
Leaving HighTask and releasing the semaphore
```

✅ Now `HighTask`, which was waiting, gets unblocked and acquires the semaphore.
✅ It runs and finishes.

---

```
Entered LowTask
Leaving LowTask
```

✅ Finally, `LowTask` runs (it’s low priority so it gets CPU only when others are idle).
✅ It executes its short task and finishes.

---

### 📌 Summary

This output shows proper functioning of:

* **Semaphore synchronization**
* **Task priority preemption**
* **GPIO wait for user input**
* **UART debug output**

It demonstrates **how `NormalTask` stalls on the button press** and **`HighTask` waits for the semaphore** until it's released.



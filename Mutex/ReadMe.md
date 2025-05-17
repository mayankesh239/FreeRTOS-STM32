## STM32 FreeRTOS Mutex Demonstration
This project demonstrates the use of a FreeRTOS mutex to simulate a classic priority inversion problem on an STM32 microcontroller using STM32CubeIDE. It involves two tasks of different priorities (High and Medium) that compete for access to a shared UART resource.

### 🧠 Concept
- Mutex is used to control access to the UART transmit function.
- Two tasks are created:
  - High-Priority Task (HPT) – priority 3
  - Medium-Priority Task (MPT) – priority 2
- Both tasks attempt to acquire the same mutex before transmitting data over USART.
- HAL_Delay(2000) inside the critical section simulates a long processing time.
- The system prints task status over UART2 (via a terminal like Moserial).  
- This project indirectly demonstrates priority inversion, where a higher-priority task (HPT) is blocked by a lower-priority task (MPT) holding the mutex.

### 🛠️ Setup & Requirements
- Board: STM32 Nucleo (e.g., STM32F401RE)
- IDE: STM32CubeIDE
- RTOS: FreeRTOS 
- UART Terminal: Moserial, TeraTerm, PuTTY, etc.
- Baudrate: 115200 (USART2)

### 🔄 Task Behavior
- Task	Priority	Action
- HPT	3	Takes mutex, sends message, waits 2 sec
- MPT	2	Takes mutex, sends message, waits 2 sec

### 📦 How to Use
- Flash the code to the STM32 Nucleo board using STM32CubeIDE.
- Open a UART terminal like Moserial and connect to /dev/ttyACM0 (Linux) or COMx (Windows) at 115200 baud.
- Observe the output showing the task scheduling and mutex protection in action.

### 💡 Learning Outcome
- This project gives practical insight into:
- RTOS task priority management
- Mutex usage in FreeRTOS
- UART handling with mutual exclusion
- The effect of blocking delays and task preemption

### 🧪 Output Sample
![image](https://github.com/user-attachments/assets/cb2e021b-c87f-4081-b5b0-97ad3590666d)

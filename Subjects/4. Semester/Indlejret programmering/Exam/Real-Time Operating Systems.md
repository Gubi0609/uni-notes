**Operating System**
- Supports computers basic functions
- Provides services to other programs
- Has a scheduler for multi-tasking
- Single core processors swap quickly between tasks to simulate parallel execution
- Most OS are **not real-time**

**RTOS**
- Responds to events within a strictly defined time (deadline)
- Scheduler is _deterministic_
- Used especially in embedded systems (microcontrollers)
- Priority assigned to each thread = task
- Processes data as it comes in typically without buffer delay

- Implemented where meeting **deadlines is critical** for task completion
- The results only make sense if delivered within time constraints
	- E.g. In car systems. **Airbag** should be **instantly**.

**FreeRTOS**
- RTOS small enough for microcontrollers
	- Embedded controllers don't have the capacity for _full RTOS_
- FreeRTOS provides only
	- Real-time scheduling functionality
	- Inter-task communication
	- Timing and synchronization primitives
- Basically a **real-timer _kernel_** more than it is a full OS

**FreeRTOS Scheduler**
- Preemptive
	- Always runs the highest available task. Tasks of identical priority share CPU time using round robin time slicing
- Co-operative
	- Context switches only occur if a task blocks or explicitly calls taskYIELD()
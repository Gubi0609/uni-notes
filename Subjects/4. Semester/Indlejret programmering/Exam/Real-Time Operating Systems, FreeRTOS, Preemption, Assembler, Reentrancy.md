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
- Has **message queues** for inter-task communication
- Has **binary- and counting semaphores**
- **Mutexes**

**FreeRTOS Scheduler**
- Preemptive
	- Always runs the highest available task. Tasks of identical priority share CPU time using round robin time slicing
- Co-operative
	- Context switches only occur if a task blocks or explicitly calls `taskYIELD()`
		- Tasks use different resources of the microcontroller (register, stack, etc) - This is **context**
		- When the kernel switches tasks, it **saves its context**
		  When a task is resumed, the **context is restored**


**FreeRTOS Task States**
- Tasks can have 4 different states
	- **Running**
	- **Ready**
		- Able to be executed, but not actively running
	- **Blocked**
		- Waiting for a temporal or external event
		- Could be waiting for a queue or semaphore event
	- **Suspended**
		- Not available for scheduling
		- Only enter or exit suspend via `vTaskSuspend()` and `vTaskResume()`

# Preemption
- Interrupting a task without its cooperation, but with the intention to resume it later
- When the kernel switches tasks, it saves the current tasks context
	- When a task is resumed the context is restored
	- This is what the **TCB** (Task Control Block) is used for

# Assembler
- **Assembly:** Low-level close to hardware programming language
	- Very close to machine code instructions
- There is a direct mapping from assembler instructions to processor instructions
- Assembly contains _macros_, _directives_, _comments_, _symbolic names_ of memory locations and so on
- Source code needs to be assembled into binary machine code
- **The Assembler is a program, that translates _assembly source code_ into machine language object code**
- Assembly can be used _together with C_
- Reasons to use Assembly/Assembler
	- **Optimization:** _Speed_, _Size_ (smaller, faster code)
	- **Strict timing:** For _time critical_ tasks, _real-time_, No ambiguity about how the code will be compiled (For C, the compiler chooses how to interpret the code, and compile in either a more flexible or faster manner. Assembly is more simple in this regard, thus the programmer can more easily decide how it should compiler.)
- Assembly uses the _instruction set_ for the specific hardware it needs to run on.
- C and assembly can be mixed either _inline_ or at _linking_
	- **Inline:** Appears directly in C code
		- `asm("ldr   r3, [r7, #6]");`
	- **Linked Assembler:** Separate assembler source files which are linked at _build-time_ (see [[State machines, Cortex M4, Bit manipulation, Build process#Build process|Subject one for exam]])
		- `Label: ldr   r3, [r7, #6]; Comment`

# Reentrancy
- A function is reentrant (or pure) if, while it is being executed, it can be called again by itself or by another function **and it works every time**
	- More than one instance of a function can run at the same time
- Errors related to reentrance are hard to debug because
	- They show up rarely
	- They can provide different faults
	- They are dependent on memory configurations

A function is reentrant if
- All variables are used atomic or are allocated to the _specific instance_ of the function (so not static)
- Common resources like hardware and global variables are used atomic or are protected by task synchronization elements (semaphores/mutexes)
- It never changes its own code
- It never calls functions which are not reentrant

- **Atomic operations are ones that cannot be interrupted**
	- Pieces of code can be turned atomic by wrapping it in `interrupt disable`
	- Disabling interrupts reduces the real-time performance of the system by inducing latency on interrupts
		- Better to use semaphores

- A _recursive function_ (one that calls itself) must necessarily also be reentrant
	- Reentrant function is not necessarily recursive


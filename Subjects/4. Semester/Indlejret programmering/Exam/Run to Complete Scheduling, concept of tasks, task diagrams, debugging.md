- Used for scheduling tasks
- Schedulers are either preemptive or non-preemptive
- **Preemptive**
	- Task switch is controlled by the system
	- Can interrupt a running process and allocate CPU to another process
	- **Round Robin**, **Shortest Remaining Time First**, **Priority Scheduling (preemptive version)**
- **Non-preemptive**
	- Depends on co-operation of tasks
	- Waits for tasks to end or move to _waiting state_
	- **RTCS**
	- _FCFS_, _Shortest Job First_, _Priority Scheduling (non-preemptive)_

**RTCS**
- Each task runs until is is finished
- Scheduling is based on ticks
	- When system is in idle state, the next sequence of tasks start on the next tick
	- If a task occupies CPU beyond next tick, the system simply waits for the next
- Tick is basic unit of time for task scheduling

![[Pasted image 20260524091858.png]]
If **C** takes to long, the system waits for the next incoming tick as described above

- RTCS is a _very simple_ **non-preemptive** scheduler
- RTCS has _Tasks_, _Task States_, _Task Events_ and a queue of _Tasks_ that all go in to the scheduling
- RTCS uses tick timers to start the sequence of tasks from the task queue.

# Concept of tasks
- A task is an independent thread of execution that can compete with other concurrent tasks for processor execution time.
- A task is defined by
	- A name
	- A unique ID (Process-ID)
	- A priority
	- A *task control block* (TCB)
	- A stack (the space allocated for its data)
	- A task routine (the function)
- For task creation, there are the following _criteria_
	- Parallelism
		- Simultaneous and independent functionality
	- Timing
		- Different timing constraints
	- Priority
		- Divide tasks with different priority
		- How important is it to run/complete this task?
	- Structure
		- Each task handles _one_ well defined problem
	- Coupling
		- Divide problems into _loosely_ coupled tasks
	- Periodicity
		- A task that must execute with a fixed period is a task by itself

# Task diagrams
![[Pasted image 20260529092657.png]]

- Compared to state machines, task diagram describe multiple tasks and the _flow of information_ while state machines describe the single thread of execution based on states and transitions between them.
	- **State machines and task diagrams are compatible - A solution can contain both**
- The difference between _shared memory_ and _event buffer_ is
	- **Shared memory:** Keeps its value after it has been read. This could be a _state variable_
	- **Event buffer:** Gets destroyed after reading and processing (a one deep queue)
- Tasks can also communicate with each other using _queues_
	- Basically and event buffer with more items. Items still get destroyed after reading (unless `queuePeek` is used)

**Example**
![[Pasted image 20260529093213.png]]

# Debugging
- Is used to inspect where in code the code the program gets to or inspecting the value of variables/registers
- Simplest version is toggling a pin (could be connected to a LED) to show either that the program is alive, or use different LEDs/colors to show the currently executing code.
	- Can be toggled on/off in start/end of function to show time it takes to execute or wait
- `assert` can be used to print a message with line number and source file to a terminal or display, then stop the program. (This only happens if the argument value to `assert` is **0**)

- To get more detalied and intelligent debug messages compared to pin toggling, one can print messages to a serial port (e.g. UART to a computer) to show the current state of the program
	- Downside is that it uses *more ram and program memory for `printf` routine*

- For non-hardware tests **PC simulator** can be used
	- Can only be done with hardware independent code (so no toggling LEDs obviously)

**ROM monitor**
- Uses RAM, ROM and execution time for debugging
- Could be problematic when debuggin Interrupt Service Routines
- Connects to the target device using serial port

**ICE - In Circuit Emulators**
- Replaces the microprocessor on the board
- Can be problematic at high frequencies because of the cable connecting the ICE to the board
- Can also be problematic with fine pitch and BGA circuits
- Is mostly used with **8-bit** and **16-bit** processors
- Pretty expensive (more that 20k DKK)

**ICD (In Circuit Debugger)** or **OCD (On Chip Debugger)**
- Is build _into the CPU_
- Consumes no RAM or ROM
- Has a hardware interface of 4-10 pins
	- JTAG (Joint Test Action Group)
	- BDM (Background Debug Monitor)


**Code Composer Studio**
- Debugging can also be done using breakpoints and steps in CCS
- Is done while the code is running on the actual device
- Can also be used to see registers and their values in real time.
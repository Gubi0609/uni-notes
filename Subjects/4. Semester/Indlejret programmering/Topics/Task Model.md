> A task is an independent thread of execution that can compete with other concurrent tasks for processor execution time.

A task is defined by a set of _parameters_ and supporting data structures
- A name
- A unique ID
- A priority
- A task control block (TCB)
- A stack
- A task routine


Regarding [[Subjects/4. Semester/Indlejret programmering/Topics/State Machines|State Machines]], they fit _into tasks_ meaning that each task can have its own state machine describing the states of the one task.

# Dividing applications into tasks
Done by experience and intuition

Criteria for task creation
- Parallelism
	- Simultaneous and independent functionality
- Timing
	- Different timing constraints
- Priority
	- Divide tasks with different priority
- Structure
	- Each task handles one well defined problem
- Coupling
	- Divide problem into loosely coupled tasks.
	- Should rely mostly on itself but have an interface to other tasks (does not need to wait for another task to complete before executing).
- Periodicity
	- A task that must execute with a fixed period is a task by itself.

# Task diagram elements
![[Pasted image 20260223125936.png]]

A shared memory element keeps its value after it has been read (e.g. a state variable (`STATE1`, `STATE2`, ...) or the `ticks` variable from SysTick).

An event from the event buffer gets destroyed after reading and processing.

> [!example]- Task Diagram - Speedometer
> ![[Pasted image 20260223132529.png]]
> The encoder interrupt runs every time the wheel completes a turn. When we also have the time tick, we can calculate the RPM and from that the speed of the vehicle.

> [!example]- [[Subjects/4. Semester/Indlejret programmering/PDFs/Assignment2.pdf|Assignment2]] task diagram
> ![[Pasted image 20260223133328.png]]
> We can see that there is a _protected mode_ layer and _application mode_ layer. This division is so that the users input is separate from the protected mode, meaning that the input won't affect that mode.

---
#embedded 
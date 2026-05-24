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
	- When system is in idle state, the next 
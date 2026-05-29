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


# Task diagrams


# Debugging

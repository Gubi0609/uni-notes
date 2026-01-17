# Topics to be covered
- [ ] Semaphore
- [ ] Critical section
- [ ] Synchronization problems
- [ ] Monitors
- [ ] Deadlock
	- [ ] Prevention
	- [ ] Avoidance
	- [ ] Detection
- [ ] Address binding/mapping
- [ ] Contiguous memory allocation
- [ ] Paging
- [ ] Demand paging
- [ ] Page replacement
- [ ] Trashing

# Relevant lectures
- [[L9 - Process synchronization]]
- [[L10 - Deadlocks]]
- [[L11 - Memory]]
- [[L12 - Virtual memory]]

# Relevant materials
- [[COS - lecture 9 - Itslearning.pdf]]
- [[COS - lecture 10 - Itslearning.pdf]]
- [[COS - lecture 11 - Itslearning.pdf]]
- [[COS - lecture 12 - Itslearning.pdf]]

# Topics
## Process synchronization
Processes can execute concurrently or in parallel [[COS - lecture 9 - Itslearning.pdf#page=3|L9 page 3]]
**Concurrent**
- CPU scheduler switches rapidly between processes to provide concurrent execution.
- Processes may only _partially_ complete before being stopped in favor of another process.

**Parallel**
- Multiple instruction streams (different processes) execute _simultaneously_ on separate processing cores.

Can both cause issues regarding the integrity of data shared by several processes.

### Bounded buffer [[COS - lecture 9 - Itslearning.pdf#page=4|L9 page 4 - 8]]
A shared _bounded_ buffer is implemented as a **circular** array with two logical pointers.

Write pointer points to the next _free_ position in the buffer
Read pointer points to the next _full_ position in the buffer

Buffer is empty, when in == out
Buffer is full, when (in+1) == out

_Race condition_ can occur here

**Example** [[COS - lecture 9 - Itslearning.pdf#page=8|L9 page 8]]
`counter++` (producer) will be performed as
```
register1 = counter
register1 += 1
counter = register1
```

and `counter--` (consumer) will be performed as
```
register2 = counter
register2 -= 1
counter = register2
```

$T_0$: producer execute `register1 = counter` (register1 = 5)
$T_1$: producer execute `register1 += 1` (register1 = 6)
$T_2$: consumer execute `register2 = counter` (register2 = 5)
$T_3$: consumer execute `register2 -= 1` (register2 = 4)
$T_4$: producer execute `counter = register1` (counter = 6)
$T_5$: consumer execute `counter = register2` (counter = 4)

As we can see, the counter has value 4 in the end, which is wrong.
If $T_4$ and $T_5$ was performed in reverse order, counter would have been 6, which is also wrong.
The correct result is $5$.

#### Race condition
Two processes access the same data at the same time, thus risking producing or using wrong data.

> The system's substantive behavior is dependent on the sequence or timing of other uncontrollable events, leading to unexpected or inconsistent results.

Can also occur if there is no timing/_synchronization_ between child processes, thereby allowing them both to have the **same** PID (**P**rocess **ID**)

### Critical-section problem
We imagine a system of $n$ number of processes.
Each process has a segment of code (**critical section**) in which it accesses (and updates) data, that is shared with at least one other process.

The _critical-section problem_ is then to design a protocol, that the processes can use to synchronize their activities, so as to cooperatively share data.

Must satisfy the following three requirements
- **Mutual exclusion**: If a process $P_i$ is in its _critical section_ then **no other** process may be in their critical sections, that manipulate _the same variable_ as $P_i$.
- **Progress**:
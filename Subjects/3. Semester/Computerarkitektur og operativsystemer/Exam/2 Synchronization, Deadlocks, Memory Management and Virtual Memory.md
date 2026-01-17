# Topics to be covered
- [x] Semaphore
- [x] Critical section
- [x] Synchronization problems
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

### Critical-section problem [[COS - lecture 9 - Itslearning.pdf#page=10|L9 page 10]]
We imagine a system of $n$ number of processes.
Each process has a segment of code (**critical section**) in which it accesses (and updates) data, that is shared with at least one other process.

The _critical-section problem_ is then to design a protocol, that the processes can use to synchronize their activities, so as to cooperatively share data.

Must satisfy the following three requirements
- **Mutual exclusion**: If a process $P_i$ is in its _critical section_ then **no other** process may be in their critical sections, that manipulate _the same variable_ as $P_i$.
- **Progress**: If _no process_ is currently in its critical section, and _some processes_ are trying to enter theirs, then the system **must** eventually allow one of them to proceed. The selection **cannot be delayed forever**. Only processes that are _not_ in their _remainder section_ (doing anything else than entering, using or exiting shared critical section) should be involved in the decision-making process. This ensures, that processes not using the critical section, are not blocking entry into the critical section.
- **Bounded Waiting**: The must me a _limit_ on how many times other processes can enter their critical section _after_ a process has requested entry and _before_ that request is granted. (**No starvation**)

### Semaphores
A _Semaphore_ is an **integer variable** that is accessed only through two standard _atomic_ operations: `wait()` and `signal()`.

[[COS - lecture 9 - Itslearning.pdf#page=11|L9 page 11]]
**`wait()`** is used when a process wants _access_ to its critical section (also called _spinlock_ or _busy waiting_)
	`semaphore--`
**`signal()`** is used when a process wants to _leave_ its critical section.
	`semaphore++`

If two concurrently running processes $P_1$ and $P_2$ both have a semaphore statement $S_1$ and $S_2$, we want to implement such that _S2 can be executed **only after** S1 has completed_. We can do this using a shared _semaphore sync_. [[COS - lecture 9 - Itslearning.pdf#page=12|L9 page 12]]
```
S1
signal(synch);

wait(synch);
S2
```

In practice it is not always an advantage to use _busy waiting_ as the process spends its CPU time _just waiting_.
We can use a _semaphore queue_ instead. [[COS - lecture 9 - Itslearning.pdf#page=13|L9 page 13]]
We have a queue _list_ and we add a process to the queue _if the semaphore value is negative_, and remove another process from the queue _if the semaphore value is 0 or higher_.

#### Deadlocks
A deadlock can occur when two or more processes are _blocked forever_, each waiting for the other to release a resource
```
# Process A
wait(S1)
wait(S2)  # Blocks here

# Process B
wait(S2)
wait(S1)  # Blocks here
```
Here process A acquires S1 and waits for S2, but Process B acquires S2 and waits for S1. _Infinitely waiting_

#### Starvation
Starvation occurs when a process is perpetually denied access to a resource, even though it is eligible to proceed.
Can happen if semaphore scheduling policy _always prioritizes new_ requests.

#### Priority Inversion
When a _lower priority_ process holds a semaphore needed by a _higher priority_ process, thereby causing the higher priority process to wait.

#### Incorrect initialization
Semaphores must be initialized correctly (e.g. with the right initial value) else the system may behave unpredictably.
A binary semaphore should be initialized to _1_ (unlocked)
	If initialized to _0_ (locked), no process can acquire it, leading to a deadlock.

#### Busy waiting
Some semaphore implementations use _busy waiting_ where a process repeatedly checks if the semaphore is available, _wasting CPU cycles_.

#### Semaphore limits
Semaphores have a fixed range (e.g. 0 to N). If a process releases a semaphore more times than it acquires it, the semaphore's value can exceed its limit, leading to undefined behavior.

### Monitors [[COS - lecture 9 - Itslearning.pdf#page=16±L9 page 16]]
A **monitor** is a programming construct consisting of
- **Shared data** (variables, data structures)
- **Procedures** (or methods) that operate on the shared data
- **Synchronization mechanisms** to ensure that only one process/thread can execute a monitor procedure at a time.

**Mutual Exclusion**
Only _one process/thread_ can execute monitor procedure at any given time
Automatically enforced by monitor.

**Condition Variables**
Monitors use _condition variables_ to allow processes to wait for specific conditions to be met.
Are used with `wait` `signal` and `broadcast`
- `wait`: Releases the monitor's lock and suspends the calling process until another process signals the condition
- `signal`: Wakes up one waiting process (if any) and transfers control to it
- `broadcast`: Wakes up all waiting processes.

**Encapsulation**
Shared data is **hidden** inside the monitor and can only be accessed through the monitor's procedures.
Prevents incorrect or unauthorized acces to shared resources.

#### How it works
1. A process calls a monitor procedure
2. The monitor ensures, that only _one process_ is active inside it at a time
3. If a process needs to wait for a condition (e.g. a buffer is empty), it calls `wait` on a condition variable
4. Another process signals the condition (e.g. adds an item)
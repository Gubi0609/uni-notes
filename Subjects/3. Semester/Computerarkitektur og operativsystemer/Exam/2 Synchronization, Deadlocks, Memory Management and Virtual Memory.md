# Topics to be covered
- [x] Semaphore
- [x] Critical section
- [x] Synchronization problems
- [x] Monitors
- [x] Deadlock
	- [x] Prevention
	- [x] Avoidance
	- [x] Detection
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
4. Another process signals the condition (e.g. adds an item to the buffer) waking up the waiting process.

> A monitor cannot do more, than what is possible with semaphores.

## Deadlocks
Several threads fight for a limited number of resources. [[COS - lecture 10 - Itslearning.pdf#page=3|L10 page 3]]
A thread requests resources. If the resources are _not available_ at that time, the thread enters a _waiting state_. Sometimes a waiting thread _can never again change state_, because the resources it has requested are _held by other waiting threads_.

Can arise in a system, if the following four conditions hold simultaneously [[COS - lecture 10 - Itslearning.pdf#page=4|L10 page 4]]
1. **Mutual exclusion**: At least one resource must be held in a nonsharable mode.
	1. Only one thread at a time can use the resource.
	2. Another thread requesting that resource must be delayed until the resource has been released
2. **Hold and wait**: A thread holds at least one resource while waiting for additional resources held by other threads.
3. **No preemption**: A resource is only released voluntarily by the thread that holds it when it has completed its task.
4. **Circular wait**: $T_0$ waits for a resource held to $T_n$, which waits for a resource held by $T_0$. This can either be for just _two_ processes or more.

If we can ensure that just _one_ of the conditions are _not met_, deadlock _cannot occur_.
### Avoiding deadlock
Several strategies can be used to avoid deadlock

#### Ignoring the problem [[COS - lecture 10 - Itslearning.pdf#page=10|L10 page 10]]
Ignore the problem and pretend that it never occurred.
Unix, Linux, Windows and more.
It is then up to the kernel and application developers to write programs that handle deadlocks (typically using a [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Protocol COS - lecture 10 - Itslearning.pdf page=10 L10 page 10|protocol]])

#### Protocol [[COS - lecture 10 - Itslearning.pdf#page=10|L10 page 10]]
Use a protocol to make sure deadlock _**never**_ occurs.
i.e _deadlock prevention and avoidance_
#### Allow [[COS - lecture 10 - Itslearning.pdf#page=10|L10 page 10]]
Allow deadlock to occur, and then detect it and recover afterwards.
i.e. _deadlock detection and recovery_
e.g. databases

### Deadlock prevention
We look at each of the _deadlock conditions_ and try to break/avoid that condition

#### Mutual exclusion [[COS - lecture 10 - Itslearning.pdf#page=12|L10 page 12]]
If we want to break this condition, all resources must be shareable.

It is unrealistic to think, that such a system exists.
	e.g. mutex, semaphore, CPU time etc.

#### Hold and Wait [[COS - lecture 10 - Itslearning.pdf#page=13|L10 page 13]]
A thread can _only_ start program execution when _**all**_ the resources it needs to perform its work can be allocated.

E.g. retrieve data from DVD → save it in a file → read-only file → print

**Protocol 1**
allocate DVD, file, printer → perform work → release resources

**Protocol 2**
allocate DVD, file → copy → release resources
allocate file → sort → release resources
allocate file, printer → print → release resources

_Poor utilization of resources and possibility of starvation_

#### No Preemption [[COS - lecture 10 - Itslearning.pdf#page=14|L10 page 14]]
A thread holds resources and requests another resource that cannot be _immediately_ allocated to it, must _implicitly release_ (devote) all its allocated resources.

_Is often used in connection with resources, whose state can be easily saved_.
##### Alternative
A thread that holds resources and requests new resources
- If they are available, they are taken
- If they are _allocated_ to a _waiting_ thread, they are taken
- If they are _not available_ and allocated to a _running_ thread, the thread has to _wait_ and all the allocated resources are preempted.

A thread can only continue, once it has received all the resources it has been deprived of (preempted), as well as those it lacked.

#### Circular wait [[COS - lecture 10 - Itslearning.pdf#page=15|L10 page 15]]
Each resource type in the system is assigned a unique integer number, which allows us to compare two resources and to determine whether one precedes another in our ordering.

The rule is that all threads only request resources in _ascending_ number order.
E.g.
R1 → R3 → R27 → R33

If
R1 → R3 → R27 → R33 → _next is R5_. Release R27 and R33 and start over
R1 → R3 → _R5_ → R27 → R33

### Deadlock avoidance [[COS - lecture 10 - Itslearning.pdf#page=16|L10 page 16]]
Deadlock avoidance is a strategy used by OS'es to _dynamically ensure_ that the system never enters a deadlocked state.
Unlike [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Deadlock prevention|deadlock prevention]], which imposes _strict rules_, deadlock avoidance requires the system to _make informed decisions_ about resource allocation based on the _current state_ and future needs processes (or threads).

Key idea is to _only grant resource requests_ if they keep the system in a _safe state_
- **Beforehand info**: Each thread declares the _maximum number of resources_ it might need during its lifetime.
- **Resource allocation state**: The system keeps track of
	- How many resources are _available_
	- How many resources are _allocated_ to each thread
	- The _maximum demand_ of each thread (the above point)

#### How the system avoids deadlocks
1. _Before allocating_ resources, the system checks if the allocation will leave the system in a _safe state_.
2. If the allocation leads to a _safe state_, the request is _granted_.
3. If the allocation leads to an _unsafe state_, the request is _denied_, and the thread must _wait_.

#### Safe state [[COS - lecture 10 - Itslearning.pdf#page=17|L10 page 17]]
A system is in a _safe state_ if there exists at least _one sequence_ in which all threads can _execute to completion_ without causing a deadlock. The sequence is called a _safe sequence_.
- In a safe state, the system can allocate resources to threads in such a way, that each thread can eventually finish.
- If a system is in a safe state, it _cannot be deadlocked_.

##### Example
|       | _Maximum needs_ | _Current needs_ |
| ----- | --------------- | --------------- |
| $T_0$ | 10              | 5               |
| $T_1$ | 4               | 2               |
| $T_2$ | 9               | 2               |
With _available resources being 12_
The _safe sequence_ here is then <$T_1$, $T_0$, $T_2$> as

$T_1$ can finish with its current resources (_2_) and release its maximum (_4_), thus leaving more resources available
$T_0$ can finish with its current resources (_5_) plus the newly available resources, and so on.

#### Unsafe state [[COS - lecture 10 - Itslearning.pdf#page=18|L10 page 18]]
An _unsafe state_ is one where _no safe sequence exists_.
If the system enters an unsafe state, it _may_ lead to a deadlock, but _not always_. The system must however _avoid_ entering unsafe states to _guarantee deadlock avoidance_.

##### Example
Take the example from above, but give $T_2$ 3 more resources for its _current needs_. It is now _5_, and the system cannot find a _safe sequence_.

#### Claim edge [[COS - lecture 10 - Itslearning.pdf#page=19|L10 page 19]]
A claim edge indicates, that a thread $T_i$ may request resource $R_j$ _at some time in the future_.
When thread $T_i$ requests resource $R_j$, the _claim edge_ sis converted to a _request edge_.
Similarly, when a resource $R_j$ is _released_ by $T_i$, the _assignment edge_, is reconverted to a _claim edge_.

Resources must be claimed _beforehand_ in the system. That is, before thread $T_i$ starts executing, _all_ its claim edges must already be made.

#### Banker's algorithm [[COS - lecture 10 - Itslearning.pdf#page=22|L10 page 22]]
Not in depth, only emphasizing the following
- A new thread entering the system must state its maximum needs for the different types of resources. _These needs must not exceed the total number of different types of resources_.
- When a thread requests a set of resources, the system checks if this allocation will leave the system in a _safe state_.
	- If yes, allocate
	- If no, thread has to wait.

### Deadlock detection [[COS - lecture 10 - Itslearning.pdf#page=26|L10 page 26]]
The system is allowed to enter a deadlock

On a periodic basis, the system checks for the existence of _cycles_.

> Best suited for systems with one instance of each resource type.

### Deadlock recovery [[COS - lecture 10 - Itslearning.pdf#page=30|L10 page 30]]
After detecting deadlock, we must recover from it

There a two main ways to recover

#### 1. Process/Thread Termination
- Terminate _one or more threads_ involved in the deadlock
- Releases resources held by terminated threads, allowing other threads to proceed.

**How threads are chosen for termination**
- _Priority_: Terminate the thread with the lowest priority
- _Age_: Terminate the _youngest_ thread (least work lost)
- _Resource Usage_: Terminate the thread hold the _fewest_ resources
- _Cost_: Terminate the thread, that is easiest or cheapest to _restart_.

#### 2. Resource Preemption
- _Forcefully take resources_ from one or more threads and allocate them to others
	- Like _stealing_ resources to break the circular wait.

**How it works**
- Select a victim thread and preempt its resources.
- Roll back the victim thread to a safe state (if possible)
- Restart the victim thread later.

## Memory Management
When processes are executed in a system, they access _memory_ to [[COS - lecture 11 - Itslearning.pdf#page=3|L11 page 3]]
- _Fetch instructions_ - in connection with program execution
- _Save data_ - as a result of calculations
- _Retrieve data_ - which must be included in new calculations or something else

Which means, when multiple processes run on the same system, they must share memory.

### Memory separation
The OS must be protected from access by _user processes_ and user processes must be protected from _one another_.
This protection must be provided by hardware. [[COS - lecture 11 - Itslearning.pdf#page=4|L11 page 4]]

Each process has a separate memory space. Separate per-process memory space protects the processes from each other and is _fundamental_ to having multiple processes loaded in memory for concurrent execution [[COS - lecture 11 - Itslearning.pdf#page=4|L11 page 4]]

To separate memory spaces, the _base register_ holds the smallest legal physical memory address, while the _limit register_ specifies the size of the range. [[COS - lecture 11 - Itslearning.pdf#page=4|L11 page 4]]

Is accomplished by having the CPU compare _every generated address_ with the registers. [[COS - lecture 11 - Itslearning.pdf#page=5|L11 page 5]]
If a process executing in _user mode_ attempts to access OS memory or other users' memory results in a trap to the OS, which treats the attempt as a fatal error. [[COS - lecture 11 - Itslearning.pdf#page=5|L11 page 5]]
Prevents a user process from modifying the code or data structures of either the OS or other users.

## Address binding
To run a _program_, the program must be brought into memory and placed within the context of a _process_. [[COS - lecture 11 - Itslearning.pdf#page=6|L11 page 6]]
Most systems allow a user process to reside in _any part_ of the physical _memory_. [[COS - lecture 11 - Itslearning.pdf#page=6|L11 page 6]]

The binding of a process' instructions and data to memory addresses can be done at any step along the way [[COS - lecture 11 - Itslearning.pdf#page=6|L11 page 6]]
- **Compile time:** If the location in memory, where a process will reside, is known at compile time, _absolute code_ can be generated.
- **Load time:** If the location is not know at compile time, the compiler must generate relocatable code (final binding is delayed until load time).
- **Execution time:** If the process can be moved from one _memory segment_ to another during its execution, the binding must be delayed until run time.
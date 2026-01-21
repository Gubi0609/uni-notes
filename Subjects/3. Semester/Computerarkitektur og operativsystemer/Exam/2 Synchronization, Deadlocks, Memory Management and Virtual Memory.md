# Topics to be covered
- [x] Semaphore
- [x] Critical section
- [x] Synchronization problems
- [x] Monitors
- [x] Deadlock
	- [x] Prevention
	- [x] Avoidance
	- [x] Detection
- [x] Address binding/mapping
- [x] Contiguous memory allocation
- [x] Paging
- [x] Demand paging
- [x] Page replacement
- [x] Trashing

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
- **Bounded Waiting**: There must be a _limit_ on how many times other processes can enter their critical section _after_ a process has requested entry and _before_ that request is granted. (**No starvation**)

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

### Monitors [[COS - lecture 9 - Itslearning.pdf#page=16|L9 page 16]]
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
When thread $T_i$ requests resource $R_j$, the _claim edge_ it's converted to a _request edge_.
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

### Base register scheme (Memory Separation)
The OS must be protected from access by _user processes_ and user processes must be protected from _one another_.
This protection must be provided by hardware. [[COS - lecture 11 - Itslearning.pdf#page=4|L11 page 4]]

Each process has a separate memory space. Separate per-process memory space protects the processes from each other and is _fundamental_ to having multiple processes loaded in memory for concurrent execution [[COS - lecture 11 - Itslearning.pdf#page=4|L11 page 4]]

To separate memory spaces, the _base register_ holds the smallest legal physical memory address, while the _limit register_ specifies the size of the range. [[COS - lecture 11 - Itslearning.pdf#page=4|L11 page 4]]

Is accomplished by having the CPU compare _every generated address_ with the registers. [[COS - lecture 11 - Itslearning.pdf#page=5|L11 page 5]]
If a process executing in _user mode_ attempts to access OS memory or other users' memory results in a trap to the OS, which treats the attempt as a fatal error. [[COS - lecture 11 - Itslearning.pdf#page=5|L11 page 5]]
Prevents a user process from modifying the code or data structures of either the OS or other users.

### Optimization strategies
We may want to optimize our use of memory. For this, we can use the following strategies

#### Dynamic loading [[COS - lecture 11 - Itslearning.pdf#page=9|L11 page 9]]
Before an entire process and all data of said process should be in the _physical memory_ when it was to be executed.

Now we use _dynamic loading_ to only load a _routine_ when it is called.
All routines are kept _on disk_ in a relocatable load format.

Basically, not all functionality in a program should be used _every time_. We can instead only load the needed parts, and take up less space in memory, making more room for more processes at the _same time_.

> Dynamic loading does not require special support from the OS. It is the users/developers responsibility to design their programs to take advantage of this.

#### Dynamic Linking [[COS - lecture 11 - Itslearning.pdf#page=10|L11 page 10]]
Dynamically linked libraries (_DLL_'s) are system libraries, that are linked to user programs when the programs are run. This ensures, that only one instance of a specific library is active/filling in memory, when running processes, instead of every process needing its own copy of a library.

Some OS support only _static linking_, in which the system libraries are treated like any other object module and are combined by the loader into the binary program image.

_Dynamic linking_ is similar to _dynamic loading_. Here _linking_ is postponed until execution time, rather than _loading_.

> Unlike dynamic loading, this requires _some_ help from the OS. If the processes in memory are protected from one another, then the OS is the only entity, than can check, whether the needed routine is in a memory space that can allow multiple processes to access.

#### Swapping [[COS - lecture 11 - Itslearning.pdf#page = 30|L11 page 30]]
Makes it possible for the total physical address space of all processes to _exceed_ the real physical memory of the system.
This increases the degree of multiprogramming in a system.

Basically, $P_1$ is swapped out for $P_2$, and meanwhile $P_1$ is in a _backing store_, while $P_2$ is in main memory.

### Contiguous memory allocation
Contiguous memory allocation is a memory management scheme, where each process is allocated a _single, continuous block of memory_. Meaning, that the entire address space of a process is stored in _one unbroken segment_ of physical memory.

In this regard, we look back at the [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Base register scheme (Memory Separation)|base register scheme]] from before. Keeping address space for each process in blocks, also helps _protect memory_, by not allowing $P_1$ to access the address space of $P_2$. [[questions-cos-11.pdf#page=11|L11 page 11]]


By using _contiguous memory allocation_ we can _compact_ our memory to allow room for _new blocks_. [[COS - lecture 11 - Itslearning.pdf#page=12|L11 page 12]]
For this we use the following three strategies [[COS - lecture 11 - Itslearning.pdf#page=13|L11 page 13]]
- **First-fit:** Allocates to the _first_ hole in the set of holes, that is _large enough_ for the process.
- **Best-fit:** Allocates to the _smallest_ hole in the set of holes, that is _large enough_ for the process.
	- The entire set (memory) must be searched (unless it is sorted by size)
	- The strategy leaves the smallest hole in the memory (utilization)
- **Worst-fit:** Allocates to the _largest_ hole in the list
	- The entire set must be searched (unless it is sorted by size)
	- The strategy leaves the largest hole in the memory (which may be large enough to use for other processes)

> First-fit and best-fit are better than worst-fit, in terms of decreasing time and memory utilization

#### Fragmentation [[COS - lecture 11 - Itslearning.pdf#page=14|L11 page 14]]
Fragmentation may occur when using _contiguous memory allocation_.
##### External fragmentation
Free memory blocks are scattered and not contiguous, making it difficult to allocate large blocks even if there is enough total free memory.
##### Internal fragmentation
Allocated memory may have unused space because it is allocated in fixed-size blocks
##### Memory wastage
_Due to fragmentation, memory bay not be used efficiently._


## Address binding
To run a _program_, the program must be brought into memory and placed within the context of a _process_. [[COS - lecture 11 - Itslearning.pdf#page=6|L11 page 6]]
Most systems allow a user process to reside in _any part_ of the physical _memory_. [[COS - lecture 11 - Itslearning.pdf#page=6|L11 page 6]]

The binding of a process' instructions and data to memory addresses can be done at any step along the way [[COS - lecture 11 - Itslearning.pdf#page=6|L11 page 6]]
- **Compile time:** If the location in memory, where a process will reside, is known at compile time, _absolute code_ can be generated.
- **Load time:** If the location is not know at compile time, the compiler must generate relocatable code (final binding is delayed until load time).
- **Execution time:** If the process can be moved from one _memory segment_ to another during its execution, the binding must be delayed until run time.

### Logical/Physical address space [[COS - lecture 11 - Itslearning.pdf#page=7|L11 page 7]]
- **Logical address:** An address generated by the _CPU_
- **Physical address:** An address loaded into the _memory-address register_ of the memory

The set of logical addresses generated by a program is a _logical address space_.
The set of all physical addresses corresponding to these logical addresses is a _physical address space_.

- Binding addresses at either _compile or load_ time generates _identical logical and physical addresses_.
- Binding addresses at _execution time_ results in _different logical and physical addresses_.

The **MMU** (**M**emory-**M**anagement **U**nit) handles _run-time logical to physical_ address _mapping_.

The _MMU scheme_ is a generalization of the [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Base register scheme (Memory Separation)|base register scheme]] from before. The value in the _relocation register_ (base register) is added to every address generated by a user process at the time the address is sent to memory. [[COS - lecture 11 - Itslearning.pdf#page=8|L11 page 8]]

The _MMU_ works as a middle-man between physical memory and the CPU/process.
The process runs in memory locations from 0 to _max_ (being the logical memory locations it made), but in reality, it runs in _R+0_ to _R+max_. This translation is handled by the _MMU_.

## Paging
The implementation involves breaking _physical memory_ into fixed-size blocks called _frames_ and breaking _logical memory_ into blocks of the _same size_ called _pages_. [[COS - lecture 11 - Itslearning.pdf#page=19|L11 page 19]]

This way, a _memory block_ of segments/processes may be kept together in _logical memory_, but may be _separated_ in _physical memory_. 
A _page table_ is used to translate from _logical_ to _physical_ memory. [[COS - lecture 11 - Itslearning.pdf#page=20|L11 page 20]]
The _page table_ is stored in **TLB** (**T**ranslation **L**ookaside **B**uffer), which is a cache for page table entries to speed up address translation. [[COS - lecture 11 - Itslearning.pdf#page=21|L11 page 21]]
If a page number does _not_ exist in **TLB**, the system reverts to the normal way of translating (page table). [[COS - lecture 11 - Itslearning.pdf#page=22|L11 page 22]]

This way, we have no [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#External fragmentation|external fragmentation]], only [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Internal fragmentation|internal fragmentation]].

By using _paging_ we have more _efficient memory usage_ as pages can be allocated _non-contiguously_ in physical memory, reducing memory wastage.
This whole process is handled by the _MMU_ (for more on MMU, see [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Address binding|address binding]] above).

The OS keeps track of the _available frames_ in a free-frame list. [[COS - lecture 11 - Itslearning.pdf#page=23|L11 page 23]]
This makes it faster to assign processes frames from the list, rather than searching for a free frame each time.

### Protection [[COS - lecture 11 - Itslearning.pdf#page=24|L11 page 24]]
One additional bit (valid/invalid) is usually attached to _each entry_ in the page table.
- When the bit is set to _valid_, the associated page is _in the process's logical address space_
- When the bit is set to _invalid_, the associated page is _not in the process's logical address space_.

### Shared pages [[COS - lecture 11 - Itslearning.pdf#page=25|L11 page 25]]
Multiple page tables (and thus processes) can share the same physical memory frames.
E.g.
- Process A's page 5 → frame 10
- Process B's page 3 → frame 10

This is good for using shared libraries.

This also enables _IPC_ (Inter-Process Communication) by allowing processes to communicate by reading and writing to the same memory locations.

The OS sets permissions (read, write, execute) for shared pages.

### Hierarchical page table [[COS - lecture 11 - Itslearning.pdf#page=25|L11 page 26]]
A page table can be divided into several _smaller_ page tables.

The advantage of this, is that we do not have to have such a large amount of page table related data in memory. [[COS - lecture 11 - Itslearning.pdf#page=27|L11 page 27]]
The cost for this is longest access times (which can be (partially) remedied with **TLB**s) 

### Inverted page table [[COS - lecture 11 - Itslearning.pdf#page=29|L11 page 29]]
This makes it so that only _one_ page table is in the _whole system_. One entry for each page of physical memory.
Reduces administration, but loses the ability to share pages.

## Demand Paging
Similar to the [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Swapping COS - lecture 11 - Itslearning.pdf page = 30 L11 page 30|swapping]] with paging technique (see [[COS - lecture 11 - Itslearning.pdf#page=31|L11 page 31]])

The processes are stored on the _disk's swap space_, but unlike the swapping technique, the individual pages of the process are loaded into memory, when they are needed [[COS - lecture 12 - Itslearning.pdf#page=7|L12 page 7]]

When a process is executing, some pages will be in memory, while some will be in secondary storage. [[COS - lecture 12 - Itslearning.pdf#page=8|L12 page 8]]
We use the [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Protection COS - lecture 11 - Itslearning.pdf page=24 L11 page 24|valid/invalid]] bit in the page table to distinguish the two cases.

### Fault handling [[COS - lecture 12 - Itslearning.pdf#page=9|L12 page 9]]
If a process tries to acces a page marked _invalid_, the process fails, and the OS brings in the missing page from secondary storage, and the instruction (from the process) restarts.

The restart is _crucial_ to demand paging.

Since we have the _state_ of the interrupted process, it should be straight forward to restart the process in exactly the same place and _state_ (except, that now the desired page is in memory) [[COS - lecture 12 - Itslearning.pdf#page=10|L12 page 10]]
In most cases this works, but if an instruction tries to modify _several_ different locations (**block move**) it does not.
- **Solution 1:** The microcode computes and attempts to access both ends of both blocks
- **Solution 2:** Uses temporary registers to hold the values of overwritten locations. If a page fault occurs, all the old values are written back into memory _before_ the trap occurs.

## Page replacements
If no _free frames_ remain for [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Demand Paging|demand paging]] we use _page replacements_. [[COS - lecture 12 - Itslearning.pdf#page=14|L12 page 14]]

It basically works in the following way [[COS - lecture 12 - Itslearning.pdf#page=15|L12 page 15]]
1. Find a _victim_ (a frame _not currently being used_) (swap the page out on the disk, if it is modified)
2. Correct the [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Protection COS - lecture 11 - Itslearning.pdf page=24 L11 page 24|valid/invalid]] bit for the page, that changed victim to invalid.
3. Swap in the desired page.
4. Update the [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Protection COS - lecture 11 - Itslearning.pdf page=24 L11 page 24|valid/invalid]] bit and continue the process from where the page fault occurred.

To do this in practice, a _frame allocation algorithm_ and a _page replacement algorithm_ must be used. [[COS - lecture 12 - Itslearning.pdf#page=16|L12 page 16]]
- **Frame allocation algorithm:** Deciding how many frames (physical memory blocks) to allocate to each process
- **Page-replacement algorithm:** Deciding _which_ page to remove from memory, when a new page needs to be loaded and memory is full.

To evaluate how well a page replacement algorithm works, we use a _reference string_ to simulate and evaluate how well it will work **without needing to run the actual process on a real system** [[COS - lecture 12 - Itslearning.pdf#page=16|L12 page 16]]

Suppose we have an address sequence
`0100, 0432, 0101, 0162, 0102, 0103, 0104, 0101, 0611, 0102, 0103, 0104, 0101, 0610, 0102, 0103, 0104` and so on

and suppose that each page is 100 bytes. Then we can reduce the address sequence to the following _reference string_
`1, 4, 1, 6, 1, 6, 1, 6, 1, 6, 1`
Where we just care what 100 byte block we acces, and not how many times it is accessed or what specific byte is accessed.

We use this reference string to _simulate_ how many page faults occur. A page replacement algorithm will then decide which page to replace when a new page is accessed and the frames are full.

The number of page faults _decreases_ as the number of frames _increases_. [[COS - lecture 12 - Itslearning.pdf#page=17|L12 page 17]]


### First in First out (FIFO) algorithm [[COS - lecture 12 - Itslearning.pdf#page=18|L12 page 18]]
A FIFO replacement algorithm creates a FIFO queue to hold all the pages in memory.
We _replace_ the page at the _head_ of the queue. When a page is brought into memory, we _insert_ it at the _tail_ of the queue.

#### Problem
If the page selected for replacement (head of queue) is in active use, a fault will occur, when we replace the page, requiring us to almost immediately retrieve the active page from secondary memory.
A bad replacement choice increases the page fault rate and slows process execution.

### Optimal page-replacement (OPT) algorithm [[COS - lecture 12 - Itslearning.pdf#page=19|L12 page 19]]
The algorithm replaces the page that _**will** not be used_ for the _longest period_ of time.
It has the _lowest page-fault rate_ of all algorithms.

#### Problem
The optimal page-replacement algorithm is difficult to implement, because it requires _future knowledge_ of the _reference string_.

### Least Recently Used (LRU) algorithm [[COS - lecture 12 - Itslearning.pdf#page=20|L12 page 20]]
Since the [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Optimal page-replacement algorithm COS - lecture 12 - Itslearning.pdf page=19 L12 page 19|optimal page replacement algorithm]] is not feasible, we can _approximate_ it by using the _recent past_ as an approximation of the _near future_.
We now replace the page that _**has not been** used_ for the _longest period_ of time.

LRU associates with _each page_ the _time_ of that page's _last use_.

### LRU stack based [[COS - lecture 12 - Itslearning.pdf#page=21|L12 page 21]]
Another way to implement LRU is to keep a _stack of page numbers_.
When a page is used, it is removed from the stack and put on the top. This way, the most recently used pages are always at the top, and the least recently used page is at the bottom.

Can be implemented using a _doubly linked list_ with a head pointer and a tail pinter.
- No search for a replacement. _The tail pointer points to the bottom of the stack_, which is the LRU page.

### LRU Second Chance (clock) [[COS - lecture 12 - Itslearning.pdf#page=22|L12 page 22]]
Many systems provide som help in the form of a _reference bit_. The reference bit for a page is set to _1_ by the hardware whenever that _page is referenced_.

- If the value is _0_ the page is replaced
- If the reference bit is set to _1_, we give that page a second chance and move on to select next FIFO page.
	- When a page gets a second chance, its reference bit is set to _0_.

This is implemented using a circular queue, where all the pages form one big circular array.

### LRU _Enhanced_ Second Chance [[COS - lecture 12 - Itslearning.pdf#page=23|L12 page 23]]
In addition to the reference bit, a _modify_ (or _dirty_) _bit_ is introduced to reflect if a page is modified or not.
For a page, which is _not modified_ we need not write the memory page to storage, since it is already in storage.

We can have 4 possible cases

|     | Reference | Modified |
| --- | --------- | -------- |
| 1   | 0         | 0        |
| 2   | 0         | 1        |
| 3   | 1         | 0        |
| 4   | 1         | 1        |
1. **Not used or modified** - Best candidate for replacement
2. **Not used but modified** - Must be written back before replacement
3. **Used but not modified** - Will probably be used again soon
4. **Used and modified** - Will probably be used again soon and also written to storage first.

The algorithm replaces the first page encountered in the lowest numbered case.
The _major difference_ is the preference for replacing clean pages in order to reduce the number of I/O's required.

### Counting based page replacement [[COS - lecture 12 - Itslearning.pdf#page=24|L12 page 24]]
Some algorithms uses a _counter_ to keep count of the _number_ of references that have been made to each page. This is used when selecting which to replace.

#### Least Frequently Used (LFU)
The page with the _smallest_ count is replaced based on the philosophy that actively used pages should have a large reference count.

#### Most Frequently Used (MFU)
The page with the _largest_ count is replaced.
Based on the argument, that the page with the smallest count balue was probably just brought into memory, and therefor need to be used shortly.

#### Neither LFU or MFU are common
The implementation of these algorithms are _expensive_ and they do not approximate _OPT_ replacement well

## Page Buffering
Systems commonly have a pool of _free frames_. [[COS - lecture 12 - Itslearning.pdf#page=25|L12 page 25]]
- When a page fault occurs, the victim frame is chosen, and the wanted replacement page is read into a free frame (from the pool) _before_ the victim is written out
- The system may periodically review processes and reclaim pages to the pool
- This will usually be done, when the number of pages in the pool is below a minimum threshold.

The system may also have a list of modified pages [[COS - lecture 12 - Itslearning.pdf#page=25|L12 page 25]]
- Whenever the paging device is _idle_, a modified page is selected and written to secondary storage. Its [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#LRU _Enhanced_ Second Chance COS - lecture 12 - Itslearning.pdf page=23 L12 page 23|modified bit]] is reset, and the page can be replaced later.

The system can keep track of the content of pages in its free frame pool [[COS - lecture 12 - Itslearning.pdf#page=25|L12 page 25]]
- When a page fault occurs, the system first checks if the desired page is in the free frame pool. If it is, we can just collect it from there, instead of picking it up from secondary storage.

## Allocation of frames
Besides [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Page replacements|page replacement]] the other important issue when implementing [[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Demand Paging|demand paging]] is _frame allocation_. [[COS - lecture 12 - Itslearning.pdf#page=26|L12 page 26]]
- How do we _allocate_ a fixed amount of free memory (frames) among the various processes?

There a _two_ main methods/schemes to do this. [[COS - lecture 12 - Itslearning.pdf#page=26|L12 page 26]]
- **Equal** (or fixed) allocation
- **Proportional** allocation

A process is also in place for the minimum number of frames a process is assigned [[COS - lecture 12 - Itslearning.pdf#page=26|L12 page 26]]
- Defined by the _computer architecture_.
- The _maximum number_ is defined by the amount of available _physical memory_.

### Equal allocation [[COS - lecture 12 - Itslearning.pdf#page=27|L12 page 27]]

We have a system with _n_ frames with a _m_ kB frame size.

The OS occupies _k_ kB → $k\cdot m$ frames

$n-k\cdot m$ frames for user processes.

The remaining frames for user processes are divided equally among the processes, with the leftovers being placed in the free-frame buffer pool.

> Since the processes can have very different sizes, this may _not be fair_ distribution of resources.

#### Example
We have a system of _128_ frames with a _1_ kB frame size

The OS occupies _35_ kB → _35_ frames.

That's _93_ frames left for user processes.

We have _5_ processes, so the get _18 frames each_ ($5*18=90$ frames). The leftover 3 frames are placed in the free-frame buffer pool.

### Proportional allocation [[COS - lecture 12 - Itslearning.pdf#page=28|L12 page 28]]
Instead of dividing everything equally, we do some calculations to find out what a process might need.

Assume we have _m_ free frames for user processes and _n_ number of processes.

$s_i$ is the virtual memory of process $p_i$. We define $S$ to be the total virtual memory
## $$S=\sum_{i=1}^n s_i$$
The number of frames allocated to process $p_i$ is defined as
## $$a_i=\frac {s_i}S\cdot m$$
So for a system with _62_ available free frames, and _2_ processes.
Process $p_1$ is _10_ kB, and process $p_2$ is _127_ kB.
## $$S=10+127=137$$
The number of frames allocated to each frame
## $$a_1=\frac {10}{137}\cdot 62=4.53\approx 4$$$$a_2=\frac {127}{137}\cdot 62=57.47\approx 57$$
_We can see that this proves a much fairer allocation_.

### Global and Local allocation [[COS - lecture 12 - Itslearning.pdf#page=29|L12 page 29]]
Another important factor is how frames are allocated to processes when there are no more available frames in page replacement.

#### Local allocation
Page replacement occurs _within_ the process's _own frames_
- More consistent performance for each process without influence of different external circumstances (the other processes)
- _Possibly poorer utilization of memory_

#### Global allocation
Page replacement occurs _among the set of all frames_ including those from all _lower-priority processes_.
- Execution time for processes can vary greatly due to the _theft_
- Better system throughput, so therefore most commonly used.

## Non Uniform Memory Access (NUMA) [[COS - lecture 12 - Itslearning.pdf#page=30|L12 page 30]]
We have until now assumed that all main memory is created equally. On _NUMA_ systems with _multiple CPUs_ a given CPU can access _local memory_ section _faster_ than it can access other CPUs memory section.

_The OS must take into account the CPU affiliation of processes_

## Thrashing
High paging activity is called _thrashing_ [[COS - lecture 12 - Itslearning.pdf#page=31|L12 page 31]]
This occurs when a process spends _almost all its time_ on page replacement.

> Processes leave the ready queue for CPU and queue up for the paging device.

To avoid the effects of thrashing, we use a _local replacement algorithm_ [[COS - lecture 12 - Itslearning.pdf#page=32|L12 page 32]]
[[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Local allocation|Local allocation]] requires that each process select _only_ from its _own set_ of allocated frames.
- In this way, if one process starts thrashing, it cannot steal frames from another process and cause that to thrash too.

To _prevent_ thrashing we must provide a process with as many frames as it needs. [[COS - lecture 12 - Itslearning.pdf#page=32|L12 page 32]]
- One strategy is to use _locality model_ to figure out the _current need_ of a process.
	- Processes move from one locality to another
	- Localities may have overlap

### Locality [[COS - lecture 12 - Itslearning.pdf#page=33|L12 page 33]]
_Locality_ refers to the _tendency_ of a program to _access the same set of memory_ locations repeatedly over a _short period_.
There are _three_ main types
- **Temporal Locality:** Recently accessed memory locations are likely to be accessed again soon (e.g. loops, variables in a function)
- **Spatial Locality:** Memory locations near a recently accessed location are likely to be accessed soon (e.g. array traversal, sequential code execution)
- **Sequential Locality:** Instructions or data are accessed in a sequential order (e.g. execution code line by line)

_Good_ locality means fewer page faults, as the working set (actively used pages) are in RAM

#### Working set model [[COS - lecture 12 - Itslearning.pdf#page=34|L12 page 34]]
Is based on the assumption of _locality_.

A _working set window_ is defined from the most recent page references. The set of pages in the working set window is the _working set_.

A process performs well if it has enough pages that cover its working set. _The working set can vary over time_.

> If the sum of _working set_ sizes (total demand for frames) exceeds the amount of physical memory, _thrashing occurs_.


### The best solution to Thrashing and high Page fault is always **More Memory!**


## Virtual Memory
[[2 Synchronization, Deadlocks, Memory Management and Virtual Memory#Optimization strategies|Previously]] we discussed some memory optimization strategies. These all had the same goal
> Allow as many processes as possible to be in memory at the same time for multiprogramming

These strategies tend to require that an _entire_ process is loaded in memory before it can execute [[COS - lecture 12 - Itslearning.pdf#page=3|L12 page 3]]

_Virtual_ memory allows the execution of processes that are _not completely_ in memory. [[COS - lecture 12 - Itslearning.pdf#page=3|L12 page 3]]
This frees programmers from the concerns of memory-storage limitations.
Virtual memory also allows processes to share files and libraries, and to implement shared memory.

### Basic Idea [[COS - lecture 12 - Itslearning.pdf#page=4|L12 page 4]]
The virtual memory viewed by the programmer is contiguous, separate and _larger than the physical memory_.

### Virtual Address Space [[COS - lecture 12 - Itslearning.pdf#page=5|L12 page 5]]
The _virtual address space_ of a process refers to the _logical (or virtual)_ view of how a process is stored in memory
A process begins at address _0_ and ends at address _max_ in contiguous virtual memory.

There is a gap between [[1 Processes, Threads, CPU Scheduling#Process|stack and heap]] that is part of the virtual address space.
This space requires physical frames _only_
- When the stack or heap _grow_
- Or when libraries or other shared objects are dynamically linked during the program execution.

> A shared page/library is stored in the space between stack and heap in two separate processes [[COS - lecture 12 - Itslearning.pdf#page=6|L12 page 6]]

## Copy on write [[COS - lecture 12 - Itslearning.pdf#page=12|L12 page 12]]
Is a technique to _speed up_ creation of a child process.

When using `fork()` to create a child process, the system creates a _duplicate_ of the parent process.

The copying of the parent's address space _may be unnecessary_ since many child processes invoke `exec()` immediately after creation.
Instead _copy-on-write_ is used to allow the parent and child processes _initially to share the same pages_.

These _shared pages_ are marked as **copy-on-write pages**, meaning that if _either_ process writes to a shared page, _a copy of the shared page is created_. [[COS - lecture 12 - Itslearning.pdf#page=13|L12 page 13]]
Only the page, that is modified is copied. All other shared pages remain untouched (until they are written to)
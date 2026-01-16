# Topics to be covered
- [ ] Definition of processes and threads
- [ ] Inter-process communication
- [ ] Thread models
- [ ] Process and thread scheduling
- [ ] CPU scheduling algorithms

# Relevant lectures
- [[L8 - Multithread programming]]
- [[L7 - Overview of Operating System Service]]

# Relevant materials
- [[COS - lecture 8 - Itslearning.pdf]]
- [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf]]

# Topics
- System calls are an essential part of any operating system [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=7|L7 page 7]]
	- Can also be accessed by programmer through an **API** (**A**pplication **P**rogramming **I**nterface) which serves as a link between system call and programmer [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=8|L7 page 8]]
	- System calls can access items _directly_ or indirectly through a _register table_ [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=9|L7 page 9]]
	- Can be used for _process control_, _file manipulation_, _device manipulation_, _information maintenance_, _communication_, or _protection_ [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=10|L7 page 10]]

- A _single tasking OS_ runs only _one_ process at a time [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=12|L7 page 12]]
	- This is preferable for smaller/slower computers/chips
- A _multi tasking OS_ runs _multiple_ processes at a time [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=13|L7 page 13]]
	- This is preferable for most other computers

- Code is compiled through multiple steps [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=14|L7 page 14]]
	- First it is compiled and relevant (included) files are linked. This is handled by the _development tool_
	- It is now an executable file, that needs to be loaded in to memory
	- _Loading_ is performed by the _OS_ and dynamically linked libraries are also linked at this stage.
	- It is now a program in memory
- It is often so, that the compield code now only can be run on _one_ OS, but if a _virtual machine_ is used, it can be used as an **API** to run the code on most OS'es [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=15|L7 page 15]]

## OS structures
**Monolithic structures** [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=16|L7 page 16]]
- The _entire_ OS runs as a single, large program in **kernel space**
- All OS services (process management, memory management, file systems etc.) are part of the same executable, and share the same memory space.
- Components communicate directly via function calls
- Because everything is interconnected, a bug in _one_ component can crash the entire system
- An example of this is _Unix_.

**Monolithic plus modular** [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=17|L7 page 17]]
- The OS kernel remains _monolithic_. That is to say, all core services (process management, memory management etc.) runs in kernel space as a single program
- **Non essential components** (eg. device drivers, file systems, networking protocols etc.) are implemented as _loadable modules_ the can be dynamically added or removed at runtime. (without recompiling the kernel)
- Dynamic loading reduces memory usage and improves system stability
- Modules run in kernel space, so a buggy module can _still_ crash the system
- An example of this is _Linux_ or _FreeBSD_.

**Layered structure** [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=18|L7 page 18]]
- The OS is designed in to a _hierarchy_ of layers
- Each layer _provides_ a service to the layer above, and _uses_ a service from the layer below
- _Hardware_ at the **bottom**, and _User Interface_ at the **top**.
- Each layer communicates _directly_ with the layer above/below.
- Structure example
	- UI
	- System Call Interface
	- Kernel (Core OS functions (process and memory management))
	- Hardware Abstraction (Manages low-level hardware interactions)
	- Hardware (Physical Components)
- Larger performance overhead, as a layer will need to communicate through all _intermediate_ layers to get to the desired layer
- An example of this is _MULTICS_ or _Windows NT_

**Microkernel** [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page = 19|L7 page 19]]
- Minimizes the amount of code running in kernel space
- Moves as many services as possible to _user space_, where they run as _separate processes_
- Prioritizes _modularity_, _stability_, and _security_.
- Kernel handles only _essential functions_. (Process and memory management, Inter-process communication, basic hardware abstraction)
- Device drivers, file systems, networking runs in _user space_
- Processes communicate with the kernel via *IPC mechanisms*
- If a user-space service crashes, it doesn't affect the kernel or other services
- It has more _performance overhead_ because IPC is slower than function calls in a monolithic kernel
- An example of this is _macOS/iOS_

**Hybrid systems** [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page =21|L7 page 21]]
- MacOS is a hybrid system
- In User Experience layer it uses _Aqua_
- in Application Framework layer it uses _Cocoa_
- In Core Framework layer it uses _Quicktime_ and _OpenGL_ for graphics and media
- In the Kernel environment (Darwin) it uses _Mach microkernel_ and _BSD Unix kernel_

## Process
- A process is an instance of a _program_ that is **currently** executing in memory [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=25|L7 page 25]]
- Unlike a program (stored on disk (actually just a file)) a process is _active_ (uses CPU time, memory and other resources)
- When a program is run, the OS creates a process for it

A Process has following structure [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=25|L7 page 25]]
- **Stack**
	- Located at the top of the process's memory space
	- Used for function calls, local variables, and return addresses
	- _Grows_ downward (toward lower memory addresses) as functions are called
	- Automatically managed by OS and CPU
	- For _temporary_ short-lived data
- **Heap**
	- Used for _dynamic memory allocation_ (e.g. memory allocated with `malloc` in C or `new` in C++/Java)
	- _Grows_ **upward** as memory is allocated
	- For _long-lived_ dynamically allocated data
- **Data**
	- Contains global and static *variables*
	- Fixed size, determined at compile time
- **Text (or code)**
	- Contains **executable code** of the program
	- Typically **read-only** to prevent accidental modification
	- For _actual program instructions_

The **stack** and **heap** grow towards each other, but don't overlap

Structure is used to manage memory efficiently

### Process Control Block (PCB) [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=27|L7 page 27]]
- Information that the OS stores about the running process (e.g. its state) is stored in a **PCB** to make the best possible use of the system's recources
- The **PCB**'s for each _process_ is stored in _scheduling queues_
	- The _ready queue_ is for processes ready to be run
	- The _wait queue_ is for processes, that are not ready to run

## Interprocess Communication (IPC) models [[Subjects/3. Semester/Computerarkitektur og operativsystemer/PDFs/COS - Lecture 7 - Itslearning.pdf#page=31|L7 page 31]]
### Message passing
- The processes run _independently_ but shares _messages_ to run together
- The overhead from message passing is _smaller_ than with shared memory, as the kernel doesn't need to allocate memory space for shared memory

### Shared memory
- The processes run _on shared memory_ and must cooperate with using said shared memory
- For passing _large amounts_ of data, shared memory is better than message passing, as the data doesn't need to be messaged through processes, but is already in said shared memory
- At the start of the processes, the kernel should allocate memory to be used as shared memory (_Overhead_)

## Multithreading
- Multiple _threads_ run simultaneously [[COS - lecture 8 - Itslearning.pdf#page=3|L8 page 3]]
- A multithreaded server _listens_ continuously for client requests, then creates a new thread to service request [[COS - lecture 8 - Itslearning.pdf#page=4|L8 page 4]]
	- Has a *fast response*, as it always listens for requests
	- Provides a good opportunity for threads to collaborate on tasks, enabling _resource sharing_
	- Threads are in the same address space, so it is more efficient to schedule them
	- Threads can be run on _different CPU cores_ in parallel

On a _single core_ system, the processes/threads are switched _rapidly_ enabling each process to make progress [[COS - lecture 8 - Itslearning.pdf#page=5|L8 page 5]]

On a _multi core_ system, multiple threads run in _parallel_ on each core (_switching_ can still be used here, to run multiple processes on same core) [[COS - lecture 8 - Itslearning.pdf#page=5|L8 page 5]]

**Data parallelism** [[COS - lecture 8 - Itslearning.pdf#page=6|L8 page 6]]
- The calculation of a dataset is distributed over several cores (e.g. arrays)

**Task parallelism** [[COS - lecture 8 - Itslearning.pdf#page=6|L8 page 6]]
- _Tasks_, not data, are distributed across multiple cores. Each task performs a unique operation.

### Amdahl's Law [[COS - lecture 8 - Itslearning.pdf#page=7|L8 page 7]]
## $$speedup \leq \frac {1}{S+\frac{1-S}N}$$
**S** is the portion of the application, that must be performed serially on a system
**(1-S)** is the portion of the application, that can be performed in parallel on a system
**N** is the number of CPU cores

### Challenges of multicore programming [[COS - lecture 8 - Itslearning.pdf#page=7|L8 page 7]]
- Applications must be examined to find areas, that can be divided into separate concurrent tasks
- Tasks must perform equal work of equal value
- Data must be divided (just as tasks are) into separate cores
- If two or more tasks depend on/access the _same_ data, the tasks must be _synchronized_
- Concurrent programs are more difficult to test and debug, than single-threaded programs.

### Multithreading models
#### Many to one model [[COS - lecture 8 - Itslearning.pdf#page=8|L8 page 8]]
- _Several_ user threads, combine in to _one_ kernel thread

#### One to one model [[COS - lecture 8 - Itslearning.pdf#page=9|L8 page 9]]
- _One_ user thread corresponds **directly** to _one_ kerne thread

#### Many to many model [[COS - lecture 8 - Itslearning.pdf#page=10|L8 page 10]]
- _Many_ user threads can correspond to _many_ kernel threads
- The _kernel_ and _user_ space, does not need to have same amount of threads

#### Two level model [[COS - lecture 8 - Itslearning.pdf#page=11|L8 page 11]]
- [[1 Processes, Threads, CPU Scheduling#Many to many model COS - lecture 8 - Itslearning.pdf page=10 L8 page 10|many to many model]] and [[1 Processes, Threads, CPU Scheduling#One to one model COS - lecture 8 - Itslearning.pdf page=9 L8 page 9|one to one model]] run alongside each other
- A thread can be bound to a specific kernel thread

### Process and thread scheduling [[COS - lecture 8 - Itslearning.pdf#page=12|L8 page 12]]
It is approximately _30 times faster_ to create a **thread** than a **task**/process
It is approximately _5 times faster_ to schedule a **thread** than a **task**/process

User threads are scheduled in the _user-space_ by the application
Support for creation etc can possibly be obtained by the kernel through user-space libraries


### Physical versus Logical view [[COS - lecture 8 - Itslearning.pdf#page=30|L8 page 30]]
While the processor might only have 4 cores and 2 threads in each, the OS sees _each thread_ as its own CPU.

## CPU scheduling
- The scheduling is split into **CPU bursts** and **I/O bursts** [[COS - lecture 8 - Itslearning.pdf#page=13|L8 page 13]]

**CPU burst**
- The process _uses_ the CPU to perform calculation
- Most CPU bursts are _short_, meaning that they don't take up CPU usages for very long time [[COS - lecture 8 - Itslearning.pdf#page=14|L8 page 14]]

**I/O burst**
- The process is _waiting_ for I/O operations (e.g. waiting for read/write to a file, waiting for user input)
- It basically can _request_ and I/O operation, and waits for it to perform/be done

CPU scheduling aims to efficiently manage these cycles to minimize CPU idel time, and ensure that the CPU is always busy.

### First Come, First Served (FCFS) Scheduling [[COS - lecture 8 - Itslearning.pdf#page=16|L8 page 16]]
- A process is completed _fully_ no matter its size, only depending on the order in which the _come in_
- Average waiting time will be
## $$P_A=\frac {\sum^nP_n}{n}$$
where $P_n$ is the waiting time for process $n$, and $n$ is the number of processes

Subject to **convoy effect**, where all the other processes wait for the _one big_ process to finish. [[COS - lecture 8 - Itslearning.pdf#page=17|L8 page 17]]

### Shortest Job First (SJF) Scheduling
The shortest process is finished first

#### Non-Preemptive Scheduling [[COS - lecture 8 - Itslearning.pdf#page=18|L8 page 18]]
All waiting/burst times for all processes are known _beforehand_.
Processes are scheduled according to shortest time

#### Preemptive Scheduling [[COS - lecture 8 - Itslearning.pdf#page=19|L8 page 19]]
Processes are processed, queued, and _stopped_ as they come in
Take the following example

| Process | Arrival Time | Burst time |
| ------- | ------------ | ---------- |
| $P_1$   | 0            | 8          |
| $P_2$   | 1            | 4          |
| $P_3$   | 2            | 9          |
| $P_4$   | 3            | 5          |
$P_1$ comes in at time $0$ and begins processing. 
At time $1$ $P_2$ comes in. As $P_1$ has a remaining burst time of $8-1=7$, and $P_2$ has a burst time of $4$, $P_1$ is stopped, and $P_2$ begins processing.
At time $2$, $P_3$ arrives. $P_2$ still has the smallest burst time, so it continues processing. $P_3$ has a _larger_ burst time, so it is placed _after_ $P_1$ in the queue.
At time $3$, $P_4$ comes in. $P_2$ still has the smallest burst time, so it continues processing. Now $P_4$ has a _smaller_ burst time, than $P_1$, so it is placed _before_ $P_1$ in the queue.
The processes now all continue.

Though the total process time is the same, the _average_ waiting time decreases with _preemptive scheduling_.

### Predicting burst time [[COS - lecture 8 - Itslearning.pdf#page=20|L8 page 20]]
We need to know the burst time of an incoming process, so we start with a _guess_ $\tau_0$ 
A weight $\alpha$, is multiplied with the current burst, and $\tau_{n+1}$ is estimated by adding previous guesses, and _reducing_ their weight for each iteration.
## $$\tau_{n+1}=\alpha\cdot t_n+(1-\alpha)\alpha t_{n-1}+...+(1-\alpha)^j\alpha t_{n-j}+...+(1-\alpha)^{n+1}\tau_0$$
### Round Robin (RR) Scheduling [[COS - lecture 8 - Itslearning.pdf#page=21|L8 page 21]]
One of the most widely used CPU scheduling algorithms
Designed to be fair and ensure that all processes get a chance to use the CPU.

Each process has a _time slice_/_time quantum_, where it gets to run.
If a process is not finished within its time slice, it stops (gets _preempted_) and moves to the _back_ of the queue.

So if a process is the _only_ process running, it will just run in 'loops'/time slices until it finishes.

A rule of thumb for selecting _time slice_ is that **80%** of CPU bursts should be _shorter_ than the time quantum.

### Priority scheduling [[COS - lecture 8 - Itslearning.pdf#page=22|L8 page 22]]
A process has a _priority_ that is used to determine in which order, the programs must run.
This _priority_ is NOT dependent on burst time.

#### Starvation
Starvation is a problem with priority scheduling, as _low-priority_ processes can be continuously postponed in favor of _high-priority_ processes.

#### Aging
Aging is a technique to _prevent_ starvation.
The priority of a process is _gradually increased_ as it waits in the ready queue.
Ensures that even low-priority processes eventually get a chance to execute.

### Priority scheduling with Round-Robin [[COS - lecture 8 - Itslearning.pdf#page=24|L8 page 24]]
First [[1 Processes, Threads, CPU Scheduling#Priority scheduling COS - lecture 8 - Itslearning.pdf page=22 L8 page 22|Priority]] is used to select the processes, but if _several_ processes have the same priority, then [[1 Processes, Threads, CPU Scheduling#Round Robin (RR) Scheduling COS - lecture 8 - Itslearning.pdf page=21 L8 page 21|Round Robin Scheduling]] is used.

### Multilevel Queue Scheduling [[COS - lecture 8 - Itslearning.pdf#page=25|L8 page 25]]
- Processes are _permanently_ assigned to **different queues** based on specific characteristics (e.g. foreground/background, priority, process type etc)
- Each queue can have its own **scheduling algorithm** (e.g. Round Robin for one queue and FCFS for another queue)
- _Queues_ are prioritized, so that processes in _higher-priority_ queues always run _before_ those in _lower-priority_ queues
	- E.g. **System processes** (highest priority), **Interactive processes** (medium priority), **Batch processes** (lowest priority)

[[1 Processes, Threads, CPU Scheduling#Starvation|Starvation]] can occur if high priority processes keep coming in.
### Multilevel Feedback queue scheduling [[COS - lecture 8 - Itslearning.pdf#page=26|L8 page 26]]
- Similar to [[1 Processes, Threads, CPU Scheduling#Multilevel Queue Scheduling COS - lecture 8 - Itslearning.pdf page=25 L8 page 25|Multilevel Queue Scheduling]], but processes can _move between queues_ based on their behavior (e.g. burst history, aging etc)
- Dynamic movement helps prevent starvation and adapts to process needs.
#### How It Works
- **Example Setup:**
    - **Queue 0:** Highest priority, Round Robin with time quantum = 8.
    - **Queue 1:** Medium priority, Round Robin with time quantum = 16.
    - **Queue 2:** Lowest priority, FCFS.
- **Process Movement:**
    - A new process enters the highest-priority queue (Queue 0).
    - If it doesn’t complete within the time quantum, it moves to Queue 1.
    - If it still doesn’t complete, it moves to Queue 2.
    - **Aging:** Processes in lower queues can be periodically moved to higher queues to prevent starvation.

### Multi-processor scheduling [[COS - lecture 8 - Itslearning.pdf#page=27|L8 page 27]]
Two approaches for Multi core CPU scheduling

#### Asymmetric multiprocessing
_One_ processor handles the scheduling, I/O processing etc., i.e. system adminstration.
Other processors are response for _only_ user code

#### Symmetric multiprocessing (SMP)
Each processor is self-scheduling, but can either have a _common_ ready queue or its _own_ private ready queue.

To achieve balanced workload in such systems, further two approaches can be used
##### Push migration
An administrative process periodically checks on the load on _each_ processor, and distributes the load by moving threads from _overloaded_ processors to _idle_ processors.
##### Pull migration
_Idle_ processors **pull** processes from the ready queues of busy processors.
##### Combination
A combination of both strategies often occurs in real systems

#### Processor Affinity
A process wants to stay on the processor on which it is currently running, as it would be costly to move it around (due to cache etc.)
- **Soft connection** - The computer _tries_ to keep the process on the same processor, **but no guarantee**
- **Hard connection** - The process is _guaranteed_ to run on the designated processor.
- **Variant** - Allows the process to specify a set of processors on which it can run.


### Memory stall [[COS - lecture 8 - Itslearning.pdf#page=29|L8 page 29]]
A _thread_ has both a **Compute Cycle** (computes something) and a **Memory Stall Cycle** (reads/ writes from/to memory)

For a _multithreaded multicore system_, the threads can be aligned such that one threads _Memory Stall Cycle_ lines up with another threads _Compute Cycle_ thereby minimizing CPU idle time.


### Software to hardware threads
Multiple threads can exist in software, while only a 
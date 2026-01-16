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

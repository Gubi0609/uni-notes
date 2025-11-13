# Multicore programming
![[Pasted image 20251107093159.png]]
We here see an example of a single-threaded process and a multithreaded process, where multiple processes are running alongside each other.

## Multithreaded server
![[Pasted image 20251107093310.png]]

**Responsiveness**:
	Faster response/reaction

**Resource** **sharing**:
	Provides a good opportunity for threads to collaborate on tasks.

**Economy**:
	Since threads are in the same address space, it is more efficient to schedule them.

**Scalability**:
	Threads can be run on different CPU cores in parallel

Used as a means to start another process without having to interrupt a running process.
	**EG.**
		Client wants to start a new process, but the process running is crucial, and must not be interrupted. We start the new process with multithreading and don't stop the running process.

## Concurrent execution on a single-core system (concurrency)
Very much like **async** from the pico
![[Pasted image 20251107093829.png]]
Rapidly switching between processes thereby allowing each process to make progress

## Parallel exectuion on a multicore system (parallelism)
![[Pasted image 20251107093906.png]]

Used to run multiple threads by dividing them between CPU cores.

### Data prallelism
![[Pasted image 20251107094003.png]]

The calculation of a dataset is distributed over several cores. E.g. Arrays
### Task parallelism
![[Pasted image 20251107094012.png]]

**Task parallelism** tasks, not data, are distributed across multiple cores. Each task performs a unique operation

## Amdahl's Law
![[Pasted image 20251107094121.png]]
**S** is the portion of the application that must be performed serially on a system
**(1-S)** is is the portion of the application that can be performed in parallel on a system
**N** is the number of CPU cores

## Challenges of multicore programming
1) **Identifying tasks.** This involves examining applications to find areas that can be divided into separate, concurrent tasks.
2) **Balance.** While identifying tasks that can run in parallel, programmers must also ensure that the tasks perform equal work of equal value.
3) **Data splitting**. Just as applications are divided into separate tasks, the data accessed and manipulated by the tasks must be divided to run on separate cores.
4) **Data dependency.** The data accessed by the tasks must be examined for dependencies between two or more tasks. When one task depends on data from another, synchronization must be ensured.
5) **Testing and debugging.** concurrent programs are inherently more difficult than single-threaded applications in terms of testing and debugging.

# Multithreading models

## Many-to-one model
![[Pasted image 20251107094422.png]]

As a user, you can onyl touch/handle _user threads_ but not the _kernel threads_ as that is controlled by the kernel.
Not ideal, as *one* user thread can block access to the kernel thread from the other user threads. 

## One-to-One model
![[Pasted image 20251107094441.png]]

This avoids the blocking of the previous example, as each user thread, has access to their own kernel threads.
**This model is the most popular and is used both by Windows and Linux (maybe also MacOS??)**

## Many-to-Many model
![[Pasted image 20251107094501.png]]

In this model, any of the user threads can get access to any of the kernel threads.

For robot example:
	User (eg. a remote-controller) is user level
	ROS and hardware is on kernel level


## Two-level model
(besides Many-to-Many, a thread can be bound to a specific kernel thread)
![[Pasted image 20251107094534.png]]

This is a hybrid model of One-to-One and Many-to-Many model, as we have a special thread reserved for special processes.

> [!example]- Example - Solaris
> ![[Pasted image 20251107094607.png]]
> Notice:
> It is approx. 30 times faster to create a thread than a task (process)
> It is approx. 5 times faster to schedule a thread than a task (process)
> **User threads are scheduled in the user-space by the application itself, support for creation, etc. can possibly obtained by the kernel through libraries in user-space**


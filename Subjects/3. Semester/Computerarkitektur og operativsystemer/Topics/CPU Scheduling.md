# Basic concept
![[Pasted image 20251107095529.png]]

**CPU-burst:** (???????)
**IO-burst:** (????)

## CPU-burst histogram
![[Pasted image 20251107095616.png]]

For most of the burst, it is relatively short, as the highest frequency is in the start.
# Scheduling Parameters (Design Objectives)
When designing a scheduling algorithm, there can be different goals to aim for:

**CPU utilization:** it is important to make the best possible use of the CPU, i.e., high utilization. In real systems, the utilization will be between 40% - 90%.

**Throughput:** the number of user processes that are executed per unit of time, often sec. This is a measure of productivity.

**Turnaround time:** the lifespan of the individual user processes is measured from the time they are allocated resources and access is given to the system until their resources are released and they leave the system. That is, the sum of waiting times in all queues, CPU time and doing I/O.

**Waiting time:** only the sum of waiting times in the ready queue is measured during the lifetime of a process.

**Response time:** the time that elapses from a request being registered until a response is started is measured.

**Variance in response time:** The aim here is to have as little variance as possible in the response time. A
large variance gives the user the impression that the system is unstable, although this is not the case

We weigh these options when designing our scheduling algorithm to achieve the best performance depending on our needs.
# Scheduling algorithms

## First come, First served (FCFS) Scheduling
![[Pasted image 20251107100934.png]]

We execute a process in the order, that they come in.

In this example the three processes arrive in a different order, reducing the average waiting time noticeably
![[Pasted image 20251107101101.png]]

**Convoy effect:** all the other processes wait for the one big process to
get off the CPU.

This is just like in the supermarket, where on idiot walks up with a full CART full of groceries, and everyone else has to wait 5-10 minuttes for this ding-head to finish. If everyone else (with small nice baskets) went first, everyone else would have to wait less.

## Shortest Job First (SJF) Scheduling

We look at the burst time (basically equal to size) of the process to determine in which order it should go.

### Non-Preemptive scheduling
![[Pasted image 20251107101129.png]]

We can see, that the shortest burst time goes first, and lastly is the longest burst time

The above example is _Non-Preemptive scheduling_.


### Preemptive scheduling
![[Pasted image 20251107101345.png]]

We handle them in the order they come in, but we evaluate at _each time_ (what???) the time needed for each process. We can see, that we split P1 in to two.
We start evaluating **P1**, (because it comes in at time 0). At time 1 we receive **P2** and suspend **P1** to finish **P2** instead (because it has shorter burst time). While finishing **P2** we receive both **P3** and **P4**, but their burst times are larger than the remaining time of **P2**, so we finish that first. Now that **P2** is done, we check which process to take next: **P1** = 7, **P3** = 9, **P4** = 5. **P4** has the shortest burst time, so we finish that, then **P1**, then **P3**.

The above example is _Preemptive scheduling_

## Prediction of Burst Time
Since we need to know the burst time of an incoming process, we need to estimae/predict the burst time

![[Pasted image 20251107102202.png]]

$\tau_o$ is the start guess
$\alpha$ is the relative weight of recent and past history in the prediction.

You can predict something about the near future if you know the present and the past (from the present to the past, smaller weights will be used).

==It doesn't work in the same way, but think about a Kalman filter. It also predicts the future from past and present data (and a weight for each data point)!!==

## Round-Robin (RR) Scheduling
![[Pasted image 20251107102551.png]]

If time slice goes towards infinity, then this algorithm is the same as FCFS.

## Effect of the size of time slice on context switches
![[Pasted image 20251107103140.png]]
A good rule of thumb is that 80% of CPU bursts should be shorter than the time quantum.


## Priority scheduling
![[Pasted image 20251107103349.png]]


**Starvation problems can occur here!! (aging is a solution to this)**


### Priority scheduling with Round-Robin
![[Pasted image 20251107103535.png]]

First, priorities are used to select the processes. But if several processes have the same priority,
then Round-Robin scheduling is used.

# Multilevel Queue Scheduling
![[Pasted image 20251107103802.png]]

## Multilevel **Feedback** Queue Scheduling
![[Pasted image 20251107103831.png]]

# Multiple-processor scheduling

> CPU scheduling obviously becomes more complex when there are multiple CPUs in the system.

## Two approaches
* **Asymmetric multiprocessing** - Here it is a processor that does the scheduling, I/O processing, etc., i.e., system administration. Other processors are responsible for only user code
* **Symmetric multiprocessing (SMP)** - Each processor is self-scheduling but can either have a common ready queue or its own private ready queue.
  To achieve balanced workload in such systems, two approaches can be used:
	* **Push migration** - here an administrative process periodically checks the load on each processor and evenly distribute the load by moving or pushing threads from overloaded to idle processors.
	* **Pull migration** - here idle processors pull processes from the ready queues of busy processors.
	* Combination of both strategies often occurs in real systems

## Processor Affinity
**Processor Affinity** – a process has an affinity for the processor on which it is currently running, as it
is costly to move it to another processor (due to cache, etc.).
- **Soft connection** – here you try to keep the process on a processor, but no guarantee.
- **Hard connection** – here the process is guaranteed to run on the designated processor.
- A variant allows the process to specify a set of processors on which it can run

## SMP - Symmetric multiprocessing
![[Pasted image 20251107104631.png]]

## Memory stall
![[Pasted image 20251107104651.png]]

In _memory stall cycle_ the CPU is idle, and not in use. We try to take advantage of this in the multithreaded multicore system, where we turn off one thread, while, the other is running. This will make it look like, we have double the physical memory.

![[Pasted image 20251107104830.png]]

We can see it in this example. We only have 4 physical cores, but by using SMP (image above) the operating system "thinks" that we have 8.

Example:
- **UltraSPARC T3:** It has **16 physical cores**, and **8 hardware threads per core.**
- **Intel Itanium:** It has **2 physical cores** (dual-core), and **2 hardware threads per core.**

## Two levels of scheduling
![[Pasted image 20251107105028.png]]

- Software threads are scheduled by software (kernel threads of OS and user threads of processes, via thread library)
- A hardware thread is the physical place where a software thread runs
- The physical CPU determines which hardware thread to run


==NEXT SECTION WILL BE COVERED ON 14-11-2025 (NEXT TIME)==



# Real-time CPU scheduling

- **Soft real-time system:** provide no guarantee as to when a critical real-time process will be scheduled. They guarantee only that the process will be given preference over noncritical processes.
- **Hard real-time system:** have stricter requirements. A task must be serviced by its deadline; service after the deadline has expired is the same as no service at all

![[Pasted image 20251107105315.png]]


# Algorithm evalution

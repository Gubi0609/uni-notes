
# Message passing
![[Pasted image 20251107092539.png]]

The processes run independently but share messages to run together.

The overhead from message passing is smaller than shared memory, as the kernel doesn't need to allocate room for shared memory.
# Shared memory
![[Pasted image 20251107092550.png]]

The processes run on shared memory and must cooperate with using said memory.
For passing large amounts of data, shared memory is better, as the data doesn't need to be send through processes with messages, but is already in shared memory.
At the start of the processes, the kernel should allocate memory to be used as shared memory. _This is an overhead with shared memory_

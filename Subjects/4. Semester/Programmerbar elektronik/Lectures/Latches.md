A latch is a level sensitive memory cell that is transparent to signals passing from the D input to the Q output when enabled and holds the value of D on Q at the time when it becomes disabled. The Q-bar output signal is always the inverse of the Q output signal

![[Pasted image 20260226123016.png]]
![[Pasted image 20260226123026.png]]
![[Pasted image 20260226123034.png]]

# Modelling of a D-type transparent latch
![[Pasted image 20260226123105.png]]
**if** without **else** is the simplest implementation of D-type transparent latch.

When we have `process(d, en)`, it is a _variable sensitive_ process, which will execute when either value change.

Since we do not have a clock signal, but are only reliant on the hardware time, the time to execute the above will be defined by the _propagation delay_ of the logic gates in hardware.

## With clear input
![[Pasted image 20260226123912.png]]

Latches will clear by setting the output Q to 
Is an edge triggered memory device that transfers a signal's value on its D input to its Q output when an active edge transition occurs on its _clock input_

![[Pasted image 20260226124319.png]]
![[Pasted image 20260226124328.png]]

The output value is _held until the next active clock edge_. The Q-bar signal is always the inverse of the Q output signal.

# Modelling of a D-type flip-flop
![[Pasted image 20260226124447.png]]

There a different models of flip-flops with +ve and -ve edge triggered are shown in the architectures above.
- Number 1 and 2 uses VHDL attributes to detect the `clk` signal edge.
- Number 3 and 4 uses a function call for the same purpose.

In a noisy envirom

## With reset
![[Pasted image 20260226124748.png]]
The first architecture models a D-type flip-flop with an *asynchronous reset* input, this is
the commonly used D-type flip-flop, while the second architecture models D-type flip-
flop with a *synchronous reset* as appears from the process sensitivity list and the if
statements sequence.
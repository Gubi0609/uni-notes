Is an edge triggered memory device that transfers a signal's value on its D input to its Q output when an active edge transition occurs on its _clock input_

![[Pasted image 20260226124319.png]]
![[Pasted image 20260226124328.png]]

The output value is _held until the next active clock edge_. The Q-bar signal is always the inverse of the Q output signal.

# Modelling of a D-type flip-flop
![[Pasted image 20260226124447.png]]

There a different models of flip-flops with +ve and -ve edge triggered are shown in the architectures above.
- Number 1 and 2 uses VHDL attributes to detect the `clk` signal edge.
- Number 3 and 4 uses a function call for the same purpose.

In a noisy environment the function call (architecture 3 and 4) are best to use, since we can implement further checks to make sure we only trigger on an actual clock pulse.
- E.g. If we use the first architecture, and the current signal is _1_, we then have some noise (while still being on _1_), changing the signal to _high_. The system recognizes an _event_ on the `clk` because of the noise, and since the signal is still _high_, the system thinks it is another _rising edge_ meaning, that it thinks we have gone through a whole nother cycle.
- If we have a more complex and sophisticated function to check for a _true rising edge_, we can avoid this fault.

## With reset
![[Pasted image 20260226124748.png]]
The first architecture models a D-type flip-flop with an *asynchronous reset* input, this is
the commonly used D-type flip-flop, while the second architecture models D-type flip-
flop with a *synchronous reset* as appears from the process sensitivity list and the if
statements sequence.
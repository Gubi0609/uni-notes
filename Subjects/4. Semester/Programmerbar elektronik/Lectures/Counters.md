A register that goes through a predetermined sequence of binary values (states), upon the application of input pulses on one or more inputs, is called a counter. Counters count the number of occurrences of an event, that is, input pulses that occur either randomly or at uniform intervals of time. Counters are used extensively in digital design for all kinds of applications. Apart from general purpose counting, counters can be used as clock dividers and for generating timing control signals.
![[Pasted image 20260226133306.png]]

# Modelling
When modelling this, we might think that we can simply say `q <= q + 1`, but this is **NOT** possible, since `q` is an output, and we can not simply read it. Thus we need an _internal signal_ `q_sig` which we will assign the value, and then assign `q` to `q_sig`.
- If we want to use `q_sig <= q_sig + 1` we must also set `q_sig` to the _unsigned type_, since if we use a standard logic vector, the calculation would not be possible.
	- We can then convert from unsigned to standard logic vector later on.

![[Pasted image 20260226133943.png]]

Beneath the blue square, `count_temp` is set to unsigned.
![[Pasted image 20260226134018.png]]

To increase the count width, we can simply change the width of the `count_out` and `count_temp`.
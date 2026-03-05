![[Pasted image 20260305122636.png]]

- A device that acts as the link between a keypad and a digital device
- Primary function is to provide a digital output equal to the key pressed on the keypad.
	- E.g. **Key 1** → 0001, **Key 2** → 0010, **Key 3** → 0011, ..., **Key 15** → 1111


This could for example be done by using a _2 to 4 Decoder_ on the inputs and a _4 to 2 Encoder_ on the outputs. We would then have 4 logic values in total, forming the binary number above.
- To switch through the input rows, we should use a [[Subjects/4. Semester/Programmerbar elektronik/Topics/Counters|counter]], which will count up on CLK pulse, and thus switch through the rows (because its output will be binary).
- Because the counter will keep counting up even when a button is pushed, we should add a NOR gate from the output to the ENABLE pin of the counter, to disable it when an output is registered.
- To save the output, we could use a [[Latches|latch]]

- We could also have a 4 bit counter, use the two MSBs (3-2) as the input for the Row 2 to 4 Decoder, and use the two LSBs (1-0) as the select pins for a [[Multiplexer]] and the inputs for the multiplexer will be the columns of the keypad. The output from the multiplexer is only _one bit_ and will be used as an _inverted feedback_ for the enable pin, which will disable the clock, when a button is pressed.
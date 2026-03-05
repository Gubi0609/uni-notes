![[Pasted image 20260305122636.png]]

- A device that acts as the link between a keypad and a digital device
- Primary function is to provide a digital output equal to the key pressed on the keypad.
	- E.g. **Key 1** → 0001, **Key 2** → 0010, **Key 3** → 0011, ..., **Key 15** → 1111


This could for example be done by using a _2 to 4 Decoder_ on the inputs and a _4 to 2 Encoder_ on the outputs. We would then have 4 logic values in total, forming the binary number above.
- To switch through the input rows, we should use a _counter_, which will count up on CLK pulse, and thus switch through the rows (because its output will be binary).
# State machine
- Finite State Machines
- A computational model
	- Model used to show how a program is run
- Can only  be in one state at a time
- Has a finite number of states
- Two versions:
	- **Moore machine** - Output values are only dependent on the state
	- **Mealy machine** - Output values are determined by both states and inputs
- Can be implemented in code using `if` or `switch` statements
- Changes state based in response to and _input_
	- Change is called **transition**
- **Transitions** happen upon _conditions_ such as
	- **Events** - An event occurs, for example a button press
	- **Special conditions** - Could be a timeout that runs out or a reset signal.
	- **External state** - Another parallel state machine might change state, activating a transition in this state machine.
- **Transitions** bring _outputs_ with them
	- **Hardware output** - A light or similar turns on in the real world.
	- **Message to other system parts** - A "message" is sent to another part of the system. Could be a queue or a state variable that gets updated
	- **Start timer** - A timer is started. Can be used for timing events or hardware outputs for example. Could of course also be used for internal logic.

![[Pasted image 20260524085136.png]]

![[Pasted image 20260524085230.png]]

# Cortex M4
- Is an ARM processor
	- **Advanced RISC Machine**
		- *R*educed *I*nstruction *S*et *C*omputer
	- Small set of simple and general instructions
		- Advantages:
			- Instructions take one cycle time
			- Simplified instruction set leads to better performance
			- Less chip space due to smaller instruction set
			- Reduced per chip cost, as it uses smalller chips
		- Disadvantages
			- Performance will vary according to the code being executed
			- RISC requires very fast memory systems to feed various instructions
	- Could e.g. be a Qualcomm Snapdragon chip

- ARM has good performance per Watt (energy efficient)


- Cortex M4 is **32 bit**
- On chip memory, 256 KB flash, 32 KB SRAM, ROM, 2 KB EEPROM
- Fast interrupt handling
- System debug with extensive breakpoint and trace capabilities
- VERY low power consumption with **sleep mode**
- Has a Memory Protection Unit

**Peripherals**
- **Nested Vectored Interrupt Controller** (NVIC)
- **System Control Block** - provides system implementation information and system control, including configuration, control and reporting of system exceptions
- **System timer** _Systick_ - 24 bit count down timer
- **Memory Protection Unit** (MPU) - Defines memory attributes for different memory regions. Provides up to eight different regions and an optional predfeined background region
- **Floating point Unit** (FPU) - For operations on single-precision, 32-bit floating point values.

**Registers**
- Has multiple general purpose registers, that programmers can use for programmes
- Has a stack pointer for pointing to a place in the stack
- Has a program counter, to keep track of what is executing, and what needs to execute next
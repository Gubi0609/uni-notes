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

**Interrupts**
- A signal to the processor of something needing emidiate attention.
- Could be a hardware (button) or software (timer) interrupt.
- Processor stops the currently  executing code and handles the Interrupt Service Routine attached with that interrupt before starting the code again.
- Different interrupts (e.g. GPIO port A, B and so on OR Timers) have different numbers in the NVIC. So e.g. GPIO Port A is vector number 16, and INTERRUPT NUMBER 0

# Bitmanipulation
- A binary variable can either be 0 or 1, but not the other, while it is one of them (so if 1, it cna not be 0)
- OR, AND, NOT operations
- Also XOR
- In a _statement_ like this `A = B + 4`, A and B are _variables_, = is the _assignment operator_, + is the _arithmetic operator_, 4 is a _constant value_ and B + 4 is an _expression_
- There are arithmetic operators:
	- +, -, \*, /, %
- Increment and decrement operators
	- ++, --
	- There is a difference between a++ and ++a
		- Post- and pre-increment. Variable is either incremented BEFORE using in expression or after. (useful for `b=++a` which will increment a and assign to b. If it was `b=a++`, a would be assigned to b and THEN incremented).
- Assign and compund
	- =, +=, -=, \*= ,/=
- Relational
	- \==, >, <, !=, >=, <=
- Logical
	- &&, ||, !
- Bitwise
	- &, |, ^, ~, <<, >>

- Numbers and such can be displayed in binary using `0b` and hex using `0x`
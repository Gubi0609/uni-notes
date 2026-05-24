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
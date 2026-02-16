There is a main _super loop_ which will be running all the time, and its functionality will only change upon an [[Assignment 1 solution|ISR]]
- E.g. changing the state of a LED. The super loop will only set it to a color, and the color to set will change upon a button ISR.

The super loop is not necessarily the _main function_, as the main function will also have system initialization.

A state machine can be illustrated as an _information flow view_
![[Pasted image 20260216125013.png]]

Or as a _layered view_
![[Pasted image 20260216125028.png]]
![[Pasted image 20260216125037.png]]

Since a technical problem is usually divided into states (like auto/manual mode) it is natural to represent it using a state machine
![[Pasted image 20260216125622.png]]

# Notations
- **Moore machine** – output values are only dependent on the state
- **Mealy machine** – output values are determined by both states and inputs

# Elements
![[Pasted image 20260216125735.png]]

**Condition for arrows**
- Events
- Special Conditions
	- Timeout
	- Reset

**Outputs for arrows**
- Hardware output
- Message to other parts of the system
- Start timer

There is a main _super loop_ which will be running all the time, and its functionality will only change upon an [[Assignment 1 solution|ISR]]
- E.g. changing the state of a LED. The super loop will only set it to a color, and the color to set will change upon a button ISR.

The super loop is not necessarily the _main function_, as the main function will also have system initialization.

A state machine can be illustrated as an _information flow view_
![[Pasted image 20260216125013.png]]

Or as a _layered view_
![[Pasted image 20260216125028.png]]
![[Pasted image 20260216125037.png]]


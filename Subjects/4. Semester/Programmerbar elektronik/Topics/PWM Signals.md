- Shows how much time the signal is _high_ in an analog fashion
- The signal $t_{on}$ (see illustration below) is considered when the signal is high
- To describe the amount of time we are on compared to off, we use _duty cycle_
![[Pasted image 20260305133613.png]]

# Building PWM signal
![[Pasted image 20260305133632.png]]

We basically count up, and when we hit the _duty cycle match_, we turn **on** the signal using a [[Subjects/4. Semester/Programmerbar elektronik/Topics/Comparators|comparator]], we turn off the signal again, when the counter resets to 0, as the comparator will no longer match.
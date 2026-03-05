- Shows how much time the signal is _high_ in an analog fashion
- The signal $t_{on}$ (see illustration below) is considered when the signal is high
- To describe the amount of time we are on compared to off, we use _duty cycle_
![[Pasted image 20260305133613.png]]

# Building PWM signal
![[Pasted image 20260305133632.png]]

We basically count up, and when we hit the _duty cycle match_, we turn **on** the signal using a [[Subjects/4. Semester/Programmerbar elektronik/Topics/Comparators|comparator]], we turn off the signal again, when the counter resets to 0, as the comparator will no longer match.

> [!example]- PWM generator
> We want a 1 Hz signal of a 125 MHz clock signal. We should calculate
> 1. The needed bit size of the counter
> $$\log_2 125 \text{MHz} = \log_2 125,000,000\text{Hz}=26.9=27\text{ bits}$$
> 2. The comparator threshold for a PWM signal with 50% duty cycle
> $$125,000,000\cdot 0.5 = 62,500,000$$
> 3. The comparator threshold for a PWM signal with 10% duty cycle
> $$125,000,000\cdot 0.1 = 12,500,000$$

# PWM Clock divider
![[Pasted image 20260305135259.png]]
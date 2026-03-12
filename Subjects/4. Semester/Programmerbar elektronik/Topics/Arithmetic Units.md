
# Adders
One of the basic building blocks for ComputerArithemtic Logic units (ALUs) and Digital Signal Processing
- Operator on binary vectors

## Hald Adder (HA)
Adds two _single binary_ digits A and B
- Has two outputs, **sum (S)** and **carry (C)**
- S = A XOR B
- C = A AND B

![[Pasted image 20260312123125.png]]![[Pasted image 20260312123130.png]]

## Full Adder (FA)
Adds _three bits_, often written **A**, **B** and **C_in**.
- A and B are the operands, and C_in is a bit carried in from the previous less-significant stage (e.g. from a half adder)
![[Pasted image 20260312123333.png]]
![[Pasted image 20260312123340.png]]

## Ripple-carry adder
An iterative array to perform binary addition, full adders chained together.

![[Pasted image 20260312123613.png]]

- The longest path delay is from (A_0 OR B_0) to S_3. This may be a disadvantage.
	- Or from C_i.0 to C_0.3
- The advantage is that it requires _less_ hardware.

## Carry-look-ahead adder
A hierarchical adder to improve performance over ripple adder.
- It however takes more resources
- Based on Propogate and Generate concept
- P = A XOR B
- G = A AND B
- P and G can be calculated in advance since none of them depends on the carry bit (C_in)

![[Pasted image 20260312123916.png]]

# Subtractors


# Multiplication

# Dividers
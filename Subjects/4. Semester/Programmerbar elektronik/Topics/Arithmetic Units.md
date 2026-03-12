
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
Can be done _by addition_ by adding **2's complement**
- $A\geq B \Rightarrow A-B$ - Basically, if A is larger than or equal to B, the result will be above 0, and thus represented as a normal binary
- $A< B \Rightarrow A-B \Rightarrow \text{2's complement}$ - If A is less than B, the result will be negative, and thus represented by two's complement.

![[Pasted image 20260312124248.png]]
The **S** pin, is basically to select if we want to _add_ or _subtract_
The output pin C_4, can be used to tell if the result is negative or not
- 0 for positive
- 1 for negative

# Multiplication
Can be implemented using a _shift register_ as wide as the product and an _accumulator_ for the partial and final product

![[Pasted image 20260312125341.png]]

> [!example]- 
> ![[IMG_1430 1.jpeg]]
> We look at one bit of the multiplier for each iteration starting from the right. If the current bit of the multiplier is _1_, we print out the multiplicand in whole. If the current bit is _0_, we print out 0. For each iteration, we shift the result _1_ bit to the left.
> Lastly we add together all the results. In the above picture, the intermediate results are added together, _but this is not needed_.

# Dividers
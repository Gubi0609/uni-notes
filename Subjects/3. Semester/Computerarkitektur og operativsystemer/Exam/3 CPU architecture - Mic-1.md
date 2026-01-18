# Topics to be covered
- [ ] Mic-1
- [ ] Data path
- [ ] Data path timing
- [ ] Control unit
- [ ] Microinstructions
- [ ] Registers
- [ ] IJVM architecture
- [ ] Instruction set design

# Relevant lectures
- [[L4 - Mikroarkitektur]]
- [[L5 - Micro-assembly og IJVM]]
- [[L2 - En Simpel Computer]]
- [[L1 - Kombinatoriske Logiske Kredse]]

# Relevant materials
- [[COS_lecture01.pdf]]
- [[COS_lecture02.pdf]]
- [[COS_lecture04.pdf]]
- [[COS_lecture05.pdf]]

# Topics
We have a layered computermodel following this structure [[COS_lecture01.pdf#page=4|L1 page 4]]. The indent is the thing _between layers_
- **Level 5:** High Level Language (e.g. C, C++)
	- Compiler
- **Level 4:** Assembly Language
	- Assembler
- **Level 3:** Operating System
	- Partial Interpretation
- **Level 2:** Instruction Set Architecture (ISA)
	- Interpretation
- **Level 1:** Micro Architecture
	- Hardware
- **Level 0:** Digital Logic

A computer is build of _combinatoric logical circuits_. [[COS_lecture01.pdf#page=5|L1 page 5]]

To convert from _binary_ to _base 10_ (decimal) [[COS_lecture01.pdf#page=14|L1 page 14]]
## $$\text{base}_{10}=\sum_{i=0}^nd_i\cdot2^i$$
If it is any other base (e.g. base 8, base 16), just replace the _2_ with the desired base.

To _convert from binary to octal_ [[COS_lecture01.pdf#page=22|L1 page 22]]
- Collect three bits _from the right_ and convert til octal.
- e.g.
	- 010 100 111 001 → 2 4 7 1

To _convert from binary to hexadecimal_ [[COS_lecture01.pdf#page=23|L1 page 23]]
- Collect _four_ bits from the right and convert til hex
- e.g.
	- 0101 0011 1001 → 5 3 9

## Gates
A gate can calculate different functions with _binary input_ (high 1, low 0) [[COS_lecture01.pdf#page=38|L1 page 38]]


## Boolean algebra [[COS_lecture01.pdf#page=52|L1 page 52]]
![[Pasted image 20260118092626.png]]

## ALU
To calculate in a computer, an **ALU** is used (**A**rithmetic **L**ogic **U**nit) [[COS_lecture01.pdf#page=54|L1 page 54]]
An ALU has _four functions_

| $F_0$ | $F_1$ | out       |
| ----- | ----- | --------- |
| 0     | 0     | A _AND_ B |
| 0     | 1     | A _OR_ B  |
| 1     | 0     | _NOT_ B   |
| 1     | 1     | A + B     |
### Encoder [[COS_lecture01.pdf#page=57|L1 page 57]]
An _ALU_ is equipped with an _encoder_, what chooses an output based on _input_

| $F_0$ | $F_1$ | $E_3$ | $E_2$ | $E_1$ | $E_0$ |
| ----- | ----- | ----- | ----- | ----- | ----- |
| 0     | 0     | 0     | 0     | 0     | _1_   |
| 0     | 1     | 0     | 0     | _1_   | 0     |
| 1     | 0     | 0     | _1_   | 0     | 0     |
| 1     | 1     | _1_   | 0     | 0     | 0     |

### Logical unit [[COS_lecture01.pdf#page=59|L1 page 59]]
The logical unit is used to actually _perform_ the calculations
It has different outputs based on $E$

If $E_0$ is enabled → output: A _AND_ B
If $E_1$ is enabled → output: A _OR_ B
If $E_2$ is enabled → output: _NOT_ B

### Full Adder
The full adder is used to _add_ A and B together

If $E_3$ is enabled, the full adder is used.

The full adder has an _output_ and a _carry output_ if the addition _exceeds_ a value that can be shown by a one bit number (0 or 1)
There is also a _carry in_, that is used when coupling multiple _ALUs_ for more complex calculations.

| A   | B   | Carry In | Carry Out | Out |
| --- | --- | -------- | --------- | --- |
| 0   | 0   | 0        | 0         | 0   |
| 0   | 1   | 0        | 0         | 1   |
| 1   | 0   | 0        | 0         | 1   |
| 1   | 1   | 0        | 1         | 0   |
| 0   | 0   | 1        | 0         | 1   |
| 0   | 1   | 1        | 1         | 0   |
| 1   | 0   | 1        | 1         | 0   |
| 1   | 1   | 1        | 1         | 1   |
### 8-bit ALU [[COS_lecture01.pdf#page=61|L1 page 61]]
Multiple ALUs can be coupled together to form for example an 8-bit ALU by combining 8 ALUs.


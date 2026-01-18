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

## Von Neumann-architecture
- Articles published by Von Neumann were the starting point for forming the modern computer [[COS_lecture02.pdf#page=15|L2 page 15]]
	- Is basically about _saving programinstruktions in memory_ besides the data.
	- _Program and data_ is in the _same memory_ and the program decides what should happen
	- _Flexible_ compared to older computers, that were hardwired to _one_ task
	- Has _no predefined_ purpose
	- Re-programmable

The architecture consists of _three_ independent components [[COS_lecture02.pdf#page=16|L2 page 16]]
- **CPU**
	- Is the _brain_
	- _Control unit_
		- Decodes instructions
		- Sends control signals to the ALU, registers and memory
		- Ensures the data flows correctly between CPU, memory and I/O devices
		- _Manages clock signals_
		- Executes a sequence of operations corresponding to an instruction (e.g. LOAD).
			- Sequence is called _microinstructions_ [[COS_lecture02.pdf#page=39|L2 page 39]]
	- Has _registers_
	- Contains the _ALU_
- **Memory**
	- Saves _programs_ and _data_
	- Divided into Random Access Memory (**RAM**) and Read-Only Memory (**ROM**)
- **Input/Output (I/O) Interface**
	- Interface with the world (keyboard, screen, printer, etc.)

The three components _communicate_ using an **address**-, **data**-, and **control bus**. [[COS_lecture02.pdf#page=16|L2 page 16]]
- Both _data_ and _instructions_ are on the **data bus** [[COS_lecture02.pdf#page=20|L2 page 20]]
- Adresses for data and instructions registers flow on the **address bus** [[COS_lecture02.pdf#page=20|L2 page 20]]

## Instructions
The general form of an instructions is
**Opcode**, **Operand**, **...**, **Operand**

The four most _simple_ instructions (used in microprocessors are)

When writing the _registers_ in the following, it is important to remember that the _program_ and _data_ are BOTH in memory at the same time, meaning that the memory addresses must be written correctly as to not treat a line of code as data. [[COS_lecture02.pdf#page=30|L2 page 30]]

### LOAD [[COS_lecture02.pdf#page=26|L2 page 26]]
Format:
- **Opcode** (bit 6-7), $R_d$ (bit 4-5), **Memory address** (bit 0-3)
- $R_d \Leftarrow \text{Mem.(adr.)}$
- We _LOAD_ from a memory address into our _register_

### STORE [[COS_lecture02.pdf#page=26|L2 page 26]]
Format:
- **Opcode** (bit 6-7), $R_d$ (bit 4-5), **Memory address** (bit 0-3)
- $\text{Mem.(adr.)}\Leftarrow R_d$
- We _STORE_ the data data from our register into out memory address

### ADDR [[COS_lecture02.pdf#page=26|L2 page 26]]
Format:
- **Opcode** (bit 6-7), $R_d$ (bit 4-5), $R_{s1}$ (bit 2-3), $R_{s2}$ (bit 0-1)
- $R_d\Leftarrow R_{s1}+R_{s2}$
- We _ADD_ $R_{s1}$ and $R_{s2}$ and _save_ it in _register_ $R_d$

### ADDM [[COS_lecture02.pdf#page=26|L2 page 26]]
Format
- **Opcode** (bit 6-7), $R_d$ (bit 4-5), **Memory address** (bit 0-3)
- $R_d\Leftarrow R_d+\text{Mem.(adr.)}$
- We _ADD_ $R_d$ and Memory address together and _save_ it in _register_ $R_d$

### Microinstructions
Microinstructions are a sequence of smaller operations performed by the _control unit_ in order to complete _one full instruction_

An example of the _LOAD_ instruction can here be seen in microinstructions [[COS_lecture02.pdf#page=31|L2 page 31]]
- PC (Program Counter) = 0 is copied to _Memory Address Register_ (**MAR**)
- _MAR_ points to the first instruction in memory (since PC=0). In this case, it is _LOAD_
	- 00 01 1101 → LOAD, Register=1, Memory=13
- The _control unit_ requests to read the contents of memory _address 0_ (first instruction) and brings the contents to _Memory Data Register_ (**MDR**). At the same time, the value of _PC_ is incremented.
- The contents of _MDR_ is copied to _Instruction Register_ (**IR**), where the instruction is decoded so $00 \Rightarrow LOAD$ 
- The _control unit_ wants to copy the 4 _LSBs_ (Least Significant Bits) from _IR_ to _MAR_ (so that is bits 1101 from our instruction)
- _MAR_ now points to memory address 1101 (address _13_)
- The _control unit_ reads the contents of address 13 and copies it to the _MDR_
- The contents of the _MDR_ is copied to register 1

This concludes the _LOAD_ operation.

Microinstructions are _less efficient_ than hardwired computers, but in return, they are _a lot_ more flexible. [[COS_lecture02.pdf#page=41|L2 page 41]]

#### Microinstruction words
When designing the _size_ of microinstructions, one _must_ think of the following [[COS_lecture02.pdf#page=42|L2 page 42]]
- _Minimize_ the size of microcode
- _Minimize_ the size of microprogram - _the length of microcode-memory_
- _Maximize_ flexibility to add and change microinstructions
- _Maximize_ parallel execution of microinstructions (thereby maximizing efficiency, since multiple microinstructions can run alongside each other.)

#### Horizontal instruction design [[COS_lecture02.pdf#page=42|L2 page 43]]
Each control signal is represented by a _single bit_ in a microinstruction.
- Means that the microinstruction is _very wide_ (many bits) because it explicitly specifies _every control signal_ needed for a particular operation

- Multiple operations can be controlled _simultaneously_ since each bit corresponds to a specific control line.
- Requires _more memory space_ since the microinstructions are _longer_
- Bigger _flexibility_
- It is possible to activate _multiple control signals_ at the same time, _possibly harming the CPU_

#### Vertical instruction design [[COS_lecture02.pdf#page=44|L2 page 44]]
Microinstructions are _shorter_ and more _compact_.
Instead of explicitly specifying every control signal, they use _encoded fields_ (like opcodes) that are _decoded into control signals_.

- **Simplicity:** Microinstructions are shorter and easier to manage, requiring _less memory_
- Operations are often executed _sequentially_ as the microinstructions may need to be decoded before control signals are generated.
- Fewer operations can be controlled simultaneously compared to horizontal design leading to _less parallelism_
- _More memory efficient_ but potentially slower du to decoding overhead
- Control signals that must not be activated simultaneously can be _grouped_ in _different decoders_.

#### Design of instructionset
When designing the instructionset of a processor it is important to consider [[COS_lecture02.pdf#page=46|L2 page 46]]
- How many instructions are necessary? (How big should the _opcode field_ be?)
	- More instructions $\Leftrightarrow$ _wider opcode field_
	- Each operation takes more _memory space_
- What operations are necessary?
- How many _operand fields_ and what type should be allowed in each instruction?

### Complex Instruction Set Computer (CISC)
A program can be written with _fewer_ and more _precise instructions_. [[COS_lecture02.pdf#page=46|L2 page 46]]
- _Complexity_ can lead to each instruction taking _more clock cycles_, but the program as a whole can possibly be _faster_ since there are _less instructions_ needed (but more available).

- Has a _wide opcode field_ $\Leftrightarrow$ more instructions
- Each operation takes _more memory space_

### Reduced Instruction Set Computer (RISC)
A program can be written with _more_ instructions, requiring more instructions to do _one_ task than CISC [[COS_lecture02.pdf#page=47|L2 page 47]]
- _Simplicity_ means that the instructions often execute in _one clock cycle_, so every instruction is _faster_ to execute

- Has a _smaller opcode field_ $\Leftrightarrow$ less instructions
- Each operation takes _less memory space_
- A program must be written with _more instructions_ to have same functionality.


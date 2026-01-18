# Topics to be covered
- [x] Mic-1
- [x] Data path
- [x] Data path timing
- [x] Control unit
- [x] Microinstructions
- [ ] Registers
- [ ] IJVM architecture
- [x] Instruction set design

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

## Instructions (Instruction Set Architecture (ISA))
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

### Choosing Instruction Set model
**CISC** [[COS_lecture02.pdf#page=48|L2 page 48]]
- Instruction in CPU
- Short access time
- _Slower_ than RISC because of _complexity_
- Smaller program
- _Larger power usage_

**RISC** [[COS_lecture02.pdf#page=48|L2 page 48]]
- Subroutine in program
- Longer access time
- _Faster_ than CISC du to _simplicity_
- Larger program (with subroutines or libraries)
- _Less power usage_

Instruction set can _vary_ from processor to processor. Most want operations that can be categorized as follows [[COS_lecture02.pdf#page=49|L2 page 49]]
- **Datatransfer:** Moving (or copying) data from one location to another
- **Arithmetic:** Simple arithmetic operations
- **Logic:** Boolean operations
- **Control:** Related to instruktion-execution e.g. SKIP, RETURN, HALT
- **System:** OS-instructions e.g. _system calls_
- **I/O:** Move data from memory to external units.

### Operand fields
The size of an operand field is usually very _limited_. It is however necessary to refer to a large amount of memory [[COS_lecture02.pdf#page=50|L2 page 50]]
This can be solved using different _address modes_. The most common are
- **Immediate** - Data
	- The data itself [[COS_lecture02.pdf#page=50|L2 page 50]]
- **Direct** - Address to data
	- A translation of data to memory address (e.g. 1111 → address 15) [[COS_lecture02.pdf#page=51|L2 page 51]]
- **Indirect** - Address to address to data
	- A translation of data to memory address, _which holds the desired memory address_(e.g. 0110 → memory address 6, which holds 1111 → memory address 15) [[COS_lecture02.pdf#page=52|L2 page 52]]
- **Displacement (indexed)** - Address to offset and local address
	- Kind of like before, where we point to a memory address, but we _also have an offset_ that points onward to the data (e.g. 0110 01 → is memory address 6 _+ 1_ so memory address 7) [[COS_lecture02.pdf#page=53|L2 page 53]]
- **Stack** - A kind of _indirect_-type
	- We have a _stack pointer_ **SP** which points to the desired memory address holding the data [[COS_lecture02.pdf#page=54|L2 page 54]]

## Micro Architecture
_Mic-1_ is on _level 1_ (Micro Architecture) (see at the top of this page). [[COS_lecture04.pdf#page=6|L4 page 6]]

Micro architecture implements the layer above, ISA (Instruction Set Architecture) [[COS_lecture04.pdf#page=7|L4 page 7]]
The design of the micro architecture is dependent upon
- The specific ISA
- Price
- Performance

- Microarchitecture consists of _fetch_-_decode_-_execute_ cycles of ISA-instructions [[COS_lecture04.pdf#page=8|L4 page 8]]
- Basically an 'endless' cycle of ISA instructions
	- **Fetch:** Find next instruction
	- Increment _PC_
	- **Decode:** decode OP code to control signal
	- **Execute:** Execute OP code

_Variables_ in a computer are called the _computers state_. [[COS_lecture04.pdf#page=9|L4 page 9]]
Register names comes from _ISA_-level.

## Mic-1
Is a _Micro Architecture_
- Has _32-bit_ registers
- Is a _microprogrammed control unit_ design for a _hypothetical CPU_
- Uses [[3 CPU architecture - Mic-1#Instructions (Instruction Set Architecture (ISA))|microcode]] to implement the CPU's instruction set.
	- Each machine instruction (e.g. ADD and LOAD) is translated into a sequence of [[3 CPU architecture - Mic-1#Microinstructions|microinstructions]] stored in a _control store_ (ROM)

Mic-1 has the following units [[COS_lecture04.pdf#page=9|L4 page 9]]
- _Memory Address Register (**MAR**)_
	- Pointer to an address
- _Memory Data Register (**MDR**)_
	- Holds data to/from memory
- _Program Counter (**PC**)_
	- Pointer to program-instruction
- _Memory Byte Register (**MBR**)_
	- Holds byte from PC
- _Stack Pointer **(SP)**_
	- Points to top of stack
- _Local Variable (**LV**)_
	- Points to local variabel in memory
- _Constant Pool Pointer(**CPP**)_
	- Points to area of memory with constants
- _Top of Stack (**TOS**)_
	- Same contents as _location_ of SP
- _Optional Program Counter (**OPC**)_
	- A register to be used as temporary data-location
- _Hold (**H**)_
	- Holds a value to be used in _next operation_
- **32-bit** _Arithmetic Logic Unit (**ALU**)_ see [[3 CPU architecture - Mic-1#ALU|ALU]]

The ALU of Mic-1 is capable of performing the usual tasks for an ALU.
To get a _32-bit_ ALU, _32 ALU's_ are coupled together.

### Data path
> The data path is the part of the CPU that contains the ALU, its inputs and outputs [[COS_lecture04.pdf#page=13|L4 page 13]]

- _Most_ registers (see Mic-1 units above) can write to the _B-bus_ [[COS_lecture04.pdf#page=14|L4 page 14]]
- The output of the ALU goes to a _shift register_
	- **SSL8:** Shifts contents _8 bit to the left_ (fills lower 8 bits with 0)
	- **SRA1:** Shifts contents _1 bit to the right_. Leaves first MSB alone
- Possible to read and write to same register _in one cycle_.

### Data path timing
_One_ clock cycle _starts_ at the falling edge of the clock pulse and _ends_ at the falling edge of the next clock pulse. [[COS_lecture04.pdf#page=15|L4 page 15]]

A clock cycle contains the following [[COS_lecture04.pdf#page=15|L4 page 15]]
- $\Delta$w: _Control signal/-bits to set up ALU_
- $\Delta$x: _Registers gets loaded onto **B-bus**_
- $\Delta$y: _ALU and shifter operates_
- $\Delta$z: _Result propagates along **C-bus** to registers_
- At _rising edge_ the results are _saved_ in the registers.

Since the parts are built up of _combinatoric logical circuits_, they run _all the time_ [[COS_lecture04.pdf#page=16|L4 page 16]]
- The clock cycle is used to limit the activity of the logical circuits to _only_ calculate, save and write the intended content.
- Therefore one must also make sure the _calculations are shorter_ than a _clock cycle_.

### Memory
Mic-1 has _two ports_ to memory [[COS_lecture04.pdf#page=18|L4 page 18]]
- _32-bit_ port controlled by
	- **MAR**: _Memory Address Register_
	- **MDR**: _Memory Data Register_
- _8-bit_ port controlled by
	- **PC**: _Program Counter_
	- **MBR**: _Memory Byte Register_

### Memory operation
The memory can be accessed through _two methods_ 
- **MAR** or **MDR** [[COS_lecture04.pdf#page=19|L4 page 19]]
	- _32-bit_ register, that accesses the memory in _word size_ (32-bit): $2^{32}=4$ GB
	- Since the _2 MSB_ (according to this example) are discarded and _0 0_ is appended, we get _1 GB addresses_
	- Can read and write 4-byte data
- **PC** or **MBR** [[COS_lecture04.pdf#page=20|L4 page 20]]
	- 32-bit registers that access memory in _byte-size_ (_8-bit_), so that is _4 G_ addresses
	- Can be read using FETCH (see structure of [[3 CPU architecture - Mic-1#Micro Instructions Register (MIR) COS_lecture04.pdf page=27 L4 page 27|MIR]])

#### MBR [[COS_lecture04.pdf#page=21|L4 page 21]]
When the 8-bit register _MBR_ is to be put onto the **B-bus**, it can be done in _two_ different ways

##### Unsigned (No extension)
**MBR** is put on the _8 LSB_ and the other 24 bits (32-8=24) are set to _0_

E.g.:
- 00000000 00000000 00000000 _MBR_

##### Signed (With extension)
**MBR** is put on the _8 LSB_ and the other 24 bits are set to either _0_ or _1_ depending on _MSB_ of MBR

E.g.:
- 00000000 00000000 00000000 _0...MBR_
- 11111111 11111111 11111111 _1...MBR_

### Data path timing in relation to MAR, MDR and MBR [[COS_lecture04.pdf#page=22|L4 page 22]]
- On falling edge (start of _cycle 1_) it is interpreted as _memory read- or write-signal_.
- On _rising_ edge of cycle 1, _MAR_ is loaded and the operation can be completed.
- On _falling edge_ (start of _cycle 2_) **MPC** (Micro Program Counter) is used to load **MIR** (Micro Instruction Register) with next microinstruction
- On _rising edge_ of cycle 2, _MDR_ OR _MBR_ is updated.
- On falling edge (start of _cycle 3_) _MDR_ or _MBR_ is ready to be used again.

### Mic-1 expanded [[COS_lecture04.pdf#page=26|L4 page 26]]
Before we focused only on the core part of Mic-1. We now expand it to hold the _microinstructions_ among other things.

- **Control store** - Is the place that holds the _micro instructions_. This is _read-only_.
- **MPC** (Micro Program Counter) - _Not_ a  real _PC_
- **MIR** (Micro Instruction Register) - Register to hold microinstructions.
	- The microinstructions are _not_ executed _in order_ - They specify the next microinstruction.
	- This is in contrast to an ISA (Instruction Set Architecture) program, where the next instruction is placed after the current.

#### Micro Instructions Register (MIR) [[COS_lecture04.pdf#page=27|L4 page 27]]
Mic-1 uses a special _intern memory_ called the _Control store_ to save microinstructions.
- These control the _flow of data_ and _ALU_-functions.
- A microinstruction of _36-bits_ is loaded _from_ Control Store _to_ MIR and thereby decides what should happen in the _Data Path_ in the _current clock_ cycle.

_MIR_ has the following structure
- **NEXT_ADDRESS** (9 bits) - Contains the address of the _next microinstruction_
- **JAM** (3 bits) - Decides how the next microinstruction is _chosen_
	- **JMPC**
	- **JAMN**
	- **JAMZ**
- **ALU** (8 bits) - _Control signals_ to the ALU and shifter
	- **SSL8** (shifter)
	- **SRA1** (shifter)
	- **F0** (ALU) - Function bit 0
	- **F1** (ALU) - Function bit 1
	- **ENA** (ALU) - Enable A
	- **ENB** (ALU) - Enable A
	- **INVA** (ALU) - Inverse A
	- **INC** (ALU) - Carry in
- **C** (9 bits) - Chooses what registers to read from **C-bus** (see [[3 CPU architecture - Mic-1#Mic-1|units]] of Mic-1)
	- **H**
	- **OPC**
	- **TOS**
	- **CPP**
	- **LV**
	- **SP**
	- **PC**
	- **MDR**
	- **MAR**
- **Mem** (3 bits) - Control-signal to access of memory
	- **WRITE**
	- **READ**
	- **FETCH**
- **B** (4 bits) - Encoder that chooses which register to write to **B-bus**
	- The registers are as follows (from the 4 bit value of **B**)
	- 0 → MDR
	- 1 → PC
	- 2 → MBR
	- 3 → **MBRU** (the upper half of the MBR (16 MSB))
	- 4 → SP
	- 5 → LV
	- 6 → CPP
	- 7 → TOS
	- 8 → OPC
	- 9 - 15 → none

## Integer Java Virtual Machine (IJVM)
- Is on _level 2_ (Instruction Set Architecture) (see top of page).

[[3 CPU architecture - Mic-1#Mic-1|Mic-1]] uses the stack for _local variables_ [[COS_lecture04.pdf#page=32|L4 page 32]]
To registers are used as _pointers_
- **LV** (Local Variable) points to the _bottom_ local variabel in the current procedure
- **SP** (Stack Pointer) points to the _top_ local variable in the current procedure

_IJVM_ is a _stack-machine_ meaning that operations happen _on the stack_.

Example:
- $a_1=a_2+a_3$
- PUSH a2 (Put variabel _a2_ on top of stack)
- PUSH a3 (Put variabel _a3_ on top of stack (thereby above _a2_))
- ADD (_adds_ the two variables _on top of stack_ and saves result on top of stack)
- POP a1 (copies (pops) the top of stack to a variabel _a1_)

### IJVM memory model
The data path contains _registers_ that describe the memory model. It has _three parts_

#### Constant pool [[COS_lecture04.pdf#page=34|L4 page 34]]
This area _cannot be written_ by a IJVM-program and contains _constants_, _strings_, and _pointers_ to other areas of the memory, which can be referred to.
**CPP** address words are _4 byte_ (32-bit)

#### Local variable frame [[COS_lecture04.pdf#page=35|L4 page 35]]
For every time a method is run, an area of memory is allocated _as long as the method is alive_.

**SP** and **LV** address words are _4 bytes_ (32-bit)

#### Method area [[COS_lecture04.pdf#page=36|L4 page 36]]
The area of memory where the _programs are stored_

**PC** addresses are _1 byte_ (8-bit)

### IJVM instruction set
IJVM has a very wide instruction set of $16^2=256$ total possible instructions.

These include among other things the ADD and POP functions seen above, and focuses on _operations within the stack_.
For a full overview of the (at least listed) operations within IJVM see [[COS_lecture04.pdf#page=39|L4 page 39]].
# Topics to be covered
- [x] Mic-2
- [x] Mic-3
- [x] Instruction Fetch Unit
- [ ] Instruction overlap
- [x] Pipeline hazards
	- [x] Structural hazards
	- [x] Data hazards
	- [x] Control hazards
- [ ] Associative mapped Cache
- [ ] Direct mapped Cache
- [ ] N-way Set associative mapped Cache
- [x] Memory interface 8-bit vs. 16-bit

# Relevant lectures
- [[L6 - Optimering af Mikroarkitekturdesign]]
- [[L3 - Hukommelse]]
- [[L1 - Kombinatoriske Logiske Kredse]]

# Relevant materials
- [[COS_lecture06.pdf]]
- [[COS_lecture03.pdf]]
- [[COS_lecture01.pdf]]

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

### Negative Bineære Tal
To represent positive numbers in binary one simply has to follow the above guide.
If we want to represent _negative_ numbers in binary, we have _four methods_.

#### Signed magnitude [[COS_lecture01.pdf#page=25|L1 page 25]]
The bit _furthest to the left_ (**MSB**) is the magnitude (_0 being +, 1 being -_)
So:
$$-N=10110010$$
$$N=00110010$$
#### Ones complement [[COS_lecture01.pdf#page=26|L1 page 26]]
Just like before, the _MSB_ is the magnitude (_0 being +, 1 being -_), but this time we _flip all other bits_
So:
$$-N=11001101$$
#### Twos complement [[COS_lecture01.pdf#page=27|L1 page 27]]
We do the same method as before, but turning a number negative requires _two steps_ this time
1. Flip all bits
2. Add 1 to the result
$$-N=11001101+01=11001110$$
#### Excess $2^{m-1}=128$ [[COS_lecture01.pdf#page=28|L1 page 28]]
We represent a number like the sum of the number itself and $2^{m-1}$ in this case, we have $m=8$ so $2^7=128$.
_Is the same as twos complement with inverted MSB_
$$-N=01001110$$

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

## Memory
Memory can be split in to _two categories_ [[COS_lecture03.pdf#page=4|L3 page 4]]
- _Volatile_ (**RAM**)
- _Non-volatile_ (**ROM**)

### Latch
A register is built up of _latches_. [[COS_lecture03.pdf#page=5|L3 page 5]]
- Constructed of two _NOR_ gates interconnected
- Has one input _D_ connected to both gates, but _NOT_'ed to one of the switches.
- Has _two outputs_ Q and NOT Q

A latch can _save 1 bit_ [[COS_lecture03.pdf#page=7|L3 page 7]]
- Can either be a _latch_ or a _D flip flop_
- _Latch_ output is _only high_ when the CLK and _input is high_.
- _D flip flop_ output can be _high_ for _one clock cycle_ and will then be whatever the input is again.

**8 D flip flops** can be arranged to construct an _8 bit register_ [[COS_lecture03.pdf#page=8|L3 page 8]]
- Then each flip flop also has a _clear_ input to presumably drop its saved value.

### 8-bit memory interface
- We have an 8-bit _data bus_ connected from both RAM and ROM to CPU [[COS_lecture03.pdf#page=13|L3 page 13]]
- The _address bus_ is 16-bit, where A8 - A15 is used for chip select (**CS**)
	- A8 - A11 is also used for address in _RAM_
- Chip Select (**CS**) is used to select what _memory chip_ is used
	- **RAM active:** When _$\overline{CS}$ is high_, which is decided from a NAND gate connected to A12 - A15 [[COS_lecture03.pdf#page=14|L3 page 14]]
		- $\overline {CS}=\overline{A_{12}\cdot A_{13}\cdot A_{14}\cdot A_{15}}$ 
	- **ROM active:** When _$\overline{CS}$ is low_, which is decided from OR gate connected to A8 - A15 [[COS_lecture03.pdf#page=15|L3 page 15]]
		- $\overline{CS}=A_{8}+A_{9}+A_{10}+A_{11}+A_{12}+A_{13}+A_{14}+A_{15}$
		- Chip is active when _all of them_ are low.
- _RAM_ is located _at the top_ of the memory space
	- **Address range:** FFFF, F000, EFFF etc.
- _ROM_ is located _at the bottom_ of the memory space
	- **Address range:** 0100, 00FF, 0000 etc.

**Read/Write signals**
- The /WR and /RD signals determine whether the memory is being _written_ or _read_ [[COS_lecture03.pdf#page=16|L3 page 16]]
- /RD is connected to _both RAM and ROM_
- /WR is connected to _only RAM_ since _ROM is read only_.

**Address Decoding**
- The CPU uses the _address bus_ A0-A15 to select an address on _either RAM or ROM_. The chips is determined from _CS_ as stated above.

**Data transfer**
- When the address and _operation_ (read/write) is selected, data is transferred to/from the CPU from/to memory over the _8-bit data line_.

### 16-bit memory interface
- We keep _in some sense_ the same setup as before, but _add another 8-bit RAM and ROM_. [[COS_lecture03.pdf#page=17|L3 page 17]]
	- The RAM and ROM from before is called _Bank 1_
	- The new RAM and ROM is called _Bank 0_
- Pin _A0_ is _unused_ in this setup.
- **CS** (Chip Select) is again used to select RAM or ROM
	- **RAM active:** when $\overline{CS}$ is high, which is decided from NAND gate connected to A13 - A15
		- $\overline {CS}=\overline{A_{13}\cdot A_{14}\cdot A_{15}}$
	- **ROM active:** when $\overline{CS}$ is _low_ which is decided from OR gate connected to A9 - A15
		- $\overline{CS}=A_{9}+A_{10}+A_{11}+A_{12}+A_{13}+A_{14}+A_{15}$
- _RAM_ is still located at the _top_ of the memory space
	- **Bank 1:** FFFF, E001, CFFF etc.
	- **Bank 0:** FFF*E*, E00*1*, CFF*E* etc.
- _ROM_ is still located at the _bottom_ of the memory space
	- **Bank 1:** 0201, 0001 etc.
	- **Bank 0:** 020*0*, 000*0* etc.

**Read/Write signals**
- We need to _select which RAM bank_ to _write_ to since they are both connected to /WR. [[COS_lecture03.pdf#page=17|L3 page 17]]
	- For this we combine /WR with _/BE0 or /BE1_ through an OR gate to select the bank.

**Address Decoding**
- Both _bank 1_ and _bank 0_ are connected to the same address lines [[COS_lecture03.pdf#page=18|L3 page 18]]
	- A1 - A12 for _RAM_
	- A1 - A8 for _ROM_
- The _last bit_ of the address is decided from _which bank_ it is in.
	- _Bank 0_ has _LSB = 0_
	- _Bank 1_ has _LSB = 1_

**Data transfer**
- We now have _16 bit data line_ [[COS_lecture03.pdf#page=17|L3 page 17]]
	- D0 - D7 is connected to _bank 0_
	- D8 - D15 is connected to _bank 1_
- From the _bank select_ operation before, we can _write_ to either bank 0 or bank 1
	- This translates to altering the _lower 8 bits_ or _higher 8 bits_ of our data
- When we _read_ we read from _both bank 0 and bank 1_ simultaneously, as they are connected to the same **CS** and address lines. [[COS_lecture03.pdf#page=17|L3 page 17]]
	- Thus we _read 16-bit data_ where bank 0 provides the _lower 8 bits_ and bank 1 provides the _higher 8 bits_

## Wait state
Some chipsets (a.k.a. memory) might need _extra time to find the data_. [[COS_lecture03.pdf#page=21|L3 page 21]]
- In these cases it is necessary to _wait_ e.g. via. a _wait-state generator-circuit_

Wait states are essentially used to _synchronize_ the CPU (Central Processing Unit) with the slower peripherals like memory (or I/O devices) by making the CPU wait for processes to complete from these slower peripherals.
- In our case, the memory is slow to transfer data to the _CPU_, so we introduce the _wait state_ as to not compute using corrupt data.

Wait states are measured in _clock cycles_.
- E.g. if a memory access requires _2 wait states_, the CPU waits _2 clock cycles_ before proceeding.

Wait states impact performance, as the _CPU is idling_
- Modern systems use techniques like _caching_, _pipelining_, and _burst mode_ to minimize or eliminate wait states.

## Address demultiplexer
Is used when different chips _use the same address-block_ (like with 16-bit memory before) [[COS_lecture03.pdf#page=23|L3 page 23]]

**3 to 8 decoder** [[COS_lecture03.pdf#page=25|L3 page 25]]
- 20 address pins A0 - A19
- A0 - A14 is used for addressing memory
- A15 - A17 is used to address the _specific chip_
	- Supports $2^3=8$ different chips
- A18 - A19 is used for **CS** for the demultiplexer. (activating demultiplexer)

**2 to 4 decoder** [[COS_lecture03.pdf#page=26|L3 page 26]]
- 16 address pins A0 - A15
- A0 - A10 is used for addressing memory
- A11 - A12 is used to address the _specific chip_
	- Supports $2^2=4$ different chips
- A13 - A15 is used for **CS** for the demultiplexer (activating demultiplexer)

### Array-logic
Address demultiplexers can be programmed using _boolean algebra._ [[COS_lecture03.pdf#page=27|L3 page 27]]
- An AND and OR gate array is constructed which will perform the algebra.

## 3 bus design
Previously, we looked at the _Mic-1_ which has a **C-bus** for output from the ALU and shifter and a **B-bus** for one of the inputs of the ALU. The other input comes from the _H_ register, which uses one microinstruction to copy from one register to the _H_ register.

To speed up our computations we _eliminate the need_ for the **H** register by _adding an A-bus_. This **A-bus** can be accessed by (almost) all registers. [[COS_lecture06.pdf#page=14|L6 page 14]]
This means, that suddenly registers can be used directly for computations instead of needing to be _held_ first. ==The H register is not removed however==

## Instruction Fetch Unit (IFU)
For every previous instruction in _microcode_ the following might occur
- The PC is passed through the ALU and incremented.
- The PC is used to fetch the next byte in the instruction stream. 
- Operands are read from memory. 
- Operands are written to memory. 
- The ALU does a computation and the results are stored back.

As an example of this, let's look at ILOAD for the _3-bus data path design_
```cpp
MAR = MBRU + LV; rd // MAR = address of local variable to push 
MAR = SP = SP + 1 // SP points to new top of stack; prepare write
PC = PC + 1; fetch; wr // Inc PC; get next opcode; write top of stack
TOS = MDR // Update TOS
PC = PC +1; fetch; goto(MBR) // MBR already holds opcode; fetch index byte
```

As we can see, the _PC is incremented_ multiple times. We also _read_ and _write_ multiple times.
We also use the PC to _fetch the next byte_ in the instruction stream.
We also update TOS (Top Of Stack) from MDR (Memory Data Register).

Much of this can be eliminated by introducing an _IFU_.
- It will be able to _independently increment PC_
- Fetch bytes from the byte stream _before they are needed_
- Can also assemble 8-bit and 16-bit operands so they are ready for immediate use whenever needed
	- As opposed to the ALU loading a register _one byte_ per clock cycle.

- IFU automatically fetches _opcodes_ in **MBR1** (8-bit) [[COS_lecture06.pdf#page=16|L6 page 16]]
- _Operands_ in **MBR2** (16-bit)
- Instruction Memory Address Register (**IMAR**) gets instructions from method-field _4 bytes_ at a time
- **PC** always points to first byte not yet used.

## Mic-2
We combine these two new methods with _mic-1_ and get **Mic-2**

Compared to Mic-1, _Mic-2_ has the following _characteristics_ [[COS_lecture06.pdf#page=19|L6 page 19]]
- No main-loop
	- The machine does not have to go to `Main1` when it is done to fetch the next instruction. This is handled by the _IFU_
- Incrementing **PC** is no longer the ALU's job
- Next instruction is _always_ ready in MBR1 (Memory Byte Register 1)
- 16-bit index/offset is generated _directly_ through MBR2 (Memory Byte Register 2)

All of this in turn _simplifies_ the microcode from Mic-1 [[COS_lecture06.pdf#page=21|L6 page 21]]

To show this lets look at ILOAD again
```cpp
MAR = LV + MBR1U; rd // Move LV + index to MAR; read operand
MAR = SP = SP + 1 // Increment SP; Move new SP to MAR
TOS = MDR; wr; goto(MBR1) // Update stack in TOS and memory
```

Much simpler as we can see, and with no need to increment PC.

## Mic-3 (pipelined model)
The _Mic-2_ is already a significant improvement over Mic-1, but is still _sequential_
- Is puts _registers onto its buses_, waits for the _ALU and shifter_ to process, and the _writes_ the results back to the registers.
- The only _parallel_ part is the **IFU**

The other way to speed up is to _reduce clock cycle_. 
Right now the clock cycle has three major parts
- The time to drive the selected registers onto the **A** and **B buses**
- The time for the ALU and shifter to do their _work_
- The time for the results to get back to the _registers and be stored_.

We can add a _latch (register)_ to each bus (**A-**, **B-**, **C-bus**) [[COS_lecture06.pdf#page=25|L6 page 25]]
- Latches get _updated every cycle_
- Clock is now _3 times as fast_ and there is _less delay_ per part
	- We _do_ have to use _three clock cycles_ to use the data path
		- Loading A and B latches
		- Running ALU and shifter and loading C latch
		- One for storing the C latch back into the registers.
	- The point of inserting the latches are however _twofold_
		- Can _speed up the clock_ because the maximum delay is now shorter
		- We can use _all parts_ of the data path during _every cycle_.

In _Mic-2_ the ALU was _idle_ in 2 out of three clock cycle steps (read and write).
- By adding latches we can use the _ALU every cycle_ getting three times as much work out of the machine.

We will call this splitting up of _microinstructions_ → _microsteps_
- 1 microinstruction = 3$\Delta$T
- One microinstruction in Mic-2 is three cycles in Mic-3.

It seems that we can start one microinstruction each cycle, but unfortunately we are limited by **RAW**-dependence (Read After Write) if we try to _read_ from a register which is _not already written_ [[COS_lecture06.pdf#page=28|L6 page 28]]
- Stopping to wait is called _stalling_.

### How does a Pipeline work?
An instruction can be split into _five phases_
1. Fetch instruction
	1. Instruction is loaded from memory in to the CPU
2. Decode instruction
	1. Instruction is decoded
	2. What type, and what operand is needed?
3. Fetch operands
	1. The operands are fetched from registers or memory
4. Execute instruction
	1. The data is _run through the data path_ and the instruction is _executed_
5. Write
	1. Save in registers

_Mic-3_ one has _four phases_, **no phase 2**. [[COS_lecture06.pdf#page=32|L6 page 32]]

> A pipeline basically has parallelism on an _instrucion-level_ as it can segment its parts. [[COS_lecture06.pdf#page=34|L6 page 34]]

#### Latency versus bandwidth
With the time for each phase being $T=2$ ns and there being _5 phases_, one instruction takes
$$T=\cdot n=2\text{ ns}\cdot 5=10\text{ ns}$$
which is the _latency_

Every phase takes _2 ns_, which means an instruction is done _every second ns_.
So the CPU's _bandwidth_ is
$$(2\text{ ns})^{-1}=\frac 1 2 10\cdot 10^9 \text{ IPs}=500 \text{ MIPS}$$
where _IPS_ is the unit _Instructions Per Second_.

### Pipeline hazards
When working with pipelines, it is possible to run in to _one of three_ of these hazards.

#### Structural hazard
Occurs at _resource-conflicts_ [[COS_lecture06.pdf#page=37|L6 page 37]]
- When the hardware cannot support certain combinations of instructions simultaneously.
- Can be necessary to perform a _pipeline-stall_

In every phase of the pipeline, different resources are used. These include [[COS_lecture06.pdf#page=38|L6 page 38]]
- **Fetching instruction:** Used resources are _PC, MAR, address- and databus_
- **Decode:** Used resources are _Decoder, intern bus, MAR, PC, address- and databus_
- **Fetching operand:** Used resources are _PC, MAR, address- and databus_
- **Execution:** Used resources are _ALU, intern bus_
- **Write:** Used resources are _Intern bus, MAR, address- and databus_

_Repeating resources create issues._

##### Solution
Duplicating resources can remedy the problem [[COS_lecture06.pdf#page=39|L6 page 39]]
- _Dual-cache_ to divide code and data with _separate busses_ and _MAR_
- _Multi-port CPU-registers_ and duplication of intern busses

#### Data hazard
Occurs when an instruction depends on the result of an earlier instruction, _if this does not exist_ because of instruction overlap [[COS_lecture06.pdf#page=37|L6 page 37]]

##### Solution
Can be remedied by adding a few _wait cycles/pipeline stall_ [[COS_lecture06.pdf#page=41|L6 page 41]]

_This does however reduce throughput and performance_

To remedy this reduce, we can fill the gap with other processes _not dependent_ on the two involved in the data hazard.
- Called _out of order execution_ [[COS_lecture06.pdf#page=42|L6 page 42]]

We can also use a __special register__ to save the result of the _execution step_ so it can be _used in another calculation_. [[COS_lecture06.pdf#page=43|L6 page 43]]

#### Control hazard
Occurs at _branches_ chancing the pipeline [[COS_lecture06.pdf#page=37|L6 page 37]]

E.g. if an instruction is a `goto`
- _Empty pipeline_- all earlier instructions already retrieved are _useless_
- _Get instructions_ from new location
- _Lower performance_

At a _conditional branch_, the new location is only known _after its execution_
Possible solutions [[COS_lecture06.pdf#page=45|L6 page 45]]
- **Branch-prediction**
	- Let the CPU attempt to guess the result of a branch.
	- Use knowledge - E.g. a branch _backwards_ will often be _chosen in favor_ of a branch _forward_
		- Think while- and for-loop
- **Branch-cache**
	- Save the first instructions in the _two separate branches_ in a _special cache_ so they can load quickly into the pipeline

## Cache
The primary memory is _much slower_ than the CPU. [[COS_lecture06.pdf#page=47|L6 page 47]]
- When the CPU requests data from memory, it may have to _wait several cycles_.
- As a **solution** we place fast _memory directly on the CPU_
	- Bigger CPU memory → Larger CPU chip → More expensive
	- Is called _**Cache**_
- We thus have a _combination_ of _fast cache_ on CPU and _slow primary memory_.

We have _multiple caches_ [[COS_lecture06.pdf#page=48|L6 page 48]]
- **L1:** One _on CPU chip_
- **L2:** One _on CPU package_
- **L3:** One _on processor board_ next to main memory
The _contents_ of each cache is _also in the higher level cache_
- L1 $\subset$ L2 $\subset$ L3
- They are a _subset_ of eachother.
- But _all content_ on higher level cache is _not on lower level_ cache.

**Main idea** [[COS_lecture06.pdf#page=50|L6 page 50]]
- The _most used words_ from memory is stored _in cache_
- CPU _looks first_ in cache when it needs a word.
- If word is _not in cache_, CPU looks in memory

**Location principle** [[COS_lecture06.pdf#page=50|L6 page 50]]
- A program does not access memory randomly.
- _The next operation_ or the next _data_ is often _nearby the current_.
- When a word is accessed, it and _some of its neighbors_ will be _moved_ from memory to _cache_
	- **Spatial locality:** Addresses with _numerical resemblance_ has _great likelihood_ of getting accessed
	- **Temporal locality:** _Great likelihood_ of accessing addresses, that have _just been accessed_.

### Cache lines [[COS_lecture06.pdf#page=53|L6 page 53]]
- Primary memory is _split into blocks_ with a _set size_.
	- These blocks are called **cache lines**
- Lines are _numerated_ after each other. Each line contains the _set byte size_
	- E.g. for _64-byte size_
	- **Line 0:** byte 0 - 63
	- **Line 1:** byte 64 - 127
	- etc.
- _Cache-controller_ checks if memory is _in cache_ or in primary memory, and _acts upon this_.

### Accesstime
The accesstime can be calculated as follows
$$\text{Accesstime}=c+(1-h)m$$
where _c_ is the time to _collect from cache_, _m_ er time to _collect from memory_, and _h_ is _hit-ratio_.
E.g.
- $c=5$ ns
- $m=60$ ns
- $h=0.9$
$$\text{Accesstime}=5\text{ ns}+(1-0.9)\cdot 60\text{ ns}=11 \text{ ns}$$
### Direct-Mapped Cache
Direct-mapped cache os the _simplest_ type of cache [[COS_lecture06.pdf#page=55|L6 page 55]]
- Each line (_entry_) holds _one cache line from memory_
	- E.g. 
	- _32-byte size_ cache lines
	- _2048 entries_
	- $\Rightarrow 2048\cdot 32\text{ bytes} = 64$ KB

**Entry** [[COS_lecture06.pdf#page=55|L6 page 55]]
- An _entry_ in direct mapped cache contains the following
- **Valid** bit - Is the data valid?
- **Tag** (16-bit) - Stores the tag portion of the memory address _for identification_
- **Data** (32 byte) - The actual data for the entry.

**Memory address** [[COS_lecture06.pdf#page=55|L6 page 55]]
- A _memory address_ used to _access specific_ data contains
- **TAG** (16 bit) - Corresponds to the _tag_ entry above
- **LINE** (11 bit) - Indicates _which entry_ (cache line) holds the data
- **WORD** (3 bit) - Indicates _which word_ is referred to within the cache line
- **BYTE** (2 bit) - Indicates what _byte_ in that word is referred to

So say we wanted to look up som data (_cache lookup_). We would send a request using _memory address_ to our _cache_
- The _LINE_ field points to a specific _cache entry_
- The _Tag_ in the cache entry is compared with the _TAG_ from our sent memory address
- If the _Valid_ bit is set and the _Tags_ match, we have _cache hit_ and the data is _retrieved from cache_
	- If not, we have a _cache miss_ and must retrieve the data from _main memory_.

#### Problem [[COS_lecture06.pdf#page=56|L6 page 56]]
- Address with a _whole_ $2^{16}$ between them
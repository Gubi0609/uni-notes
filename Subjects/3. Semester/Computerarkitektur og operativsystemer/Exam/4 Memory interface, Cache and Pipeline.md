# Topics to be covered
- [ ] Mic-2
- [ ] Mic-3
- [ ] Instruction Fetch Unit
- [ ] Instruction overlap
- [ ] Pipeline hazards
	- [ ] Structural hazards
	- [ ] Data hazards
	- [ ] Control hazards
- [ ] Associative mapped Cache
- [ ] Direct mapped Cache
- [ ] N-way Set associative mapped Cache
- [ ] Memory interface 8-bit vs. 16-bit

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
- _ROM_ is still located at the _bottom_ of the memory space

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
- We now have _16 bit data line_
	- D0 - D7 is connected to _bank 0_
	- D8 - D15 is connected to _bank 1_
- From the _bank select_ operation before, we can _write_ to either bank 0 or bank 1
	- This translates to altering the _lower 8 bits_ or _higher 8 bits_ of our data
- When we _read_ we read from _both bank 0 and bank 1_ simultaneously, as they are connected to the same **CS** and address lines.
	- 
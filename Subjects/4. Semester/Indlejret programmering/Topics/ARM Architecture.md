Short for **Acorn RISC Machine**
- Or **Advanced RISC Machine** for later chips

Uses RISC architecture (see [[3 CPU architecture - Mic-1]] for more detail).

ARM has good performance per Watt, meaning that it is **energy efficient**
- Good for mobile/embedded use

Has good price performance

# ARM Cortex-M4
Is used by the [[Tiva C Series]]

## Registers
Has registers named as `r0`, `r1`, `r2` and so on [[Lesson01_arm.pdf#page=17|L1 page 17]]

The _core registers_ can be seen here
![[Pasted image 20260202141601.png]]

## Data-types
- 32-bit words
- 16-bit halfwords
- 8-bit bytes

The data memory access is managed as _little-endian_ or _big-endian_.
Instruction memory and Private Peripheral Bus (**PPB**) accesses are always performed as _little-endian_.

---
**Date:** 2026-02-05

## Preparation

>[!TODO] HOMEWORK
>- [x] Install Vivado before lesson
>- [ ] Chapter 2 -3 of [[Free Range VHDL.pdf|the book]]

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[Lecture 1.pdf]]
[[Lab 1.pdf]]

# Topics


# Notes
An FPGA operates using _Logic Gates_.
- Compared to CPU and GPU:
	- CPU does everything _sequential_ and different cores handle different tasks
	- GPU does everything _parallel_ and handle everything together
		- High power consumption
	- FPGA are coded to perform specific tasks.

While a CPU and GPU might run while no tasks are available (idle) and consume power, an FPGA will just wait.

- CPU → Fast
- GPU → Larger tasks
- FPGA → Precise and fast

The size of a transistor (e.g. 5 nm) is defined by the size of the transistors _channel_ [[Lecture 1.pdf#page=12|L1 page 12]]. The size defines how many transistors we can pack onto a chip.

Moore's law
Every second year the number of transistors in a chip _doubles_
- Frequency also doubles
- With more transistors, we can have more functions to perform tasks
	- This however needs more management and more efficient design methods




---
#lecture 
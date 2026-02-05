
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
[[Moore's Law]]
[[K-map]]

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

Power Dissipation
Power Dissipation is a f(speed, area, technology) function.
- $E=\frac V d$
![[Pasted image 20260205132144.png]]
- Example (for welding)
	- $E=\frac {5000 V} {5000 \mu m} = 1 V/\mu m$
- Inside transistor
	- $E = \frac {0.6 V} {0.06 \mu m} = 10 V/\mu m$

---
#lecture 
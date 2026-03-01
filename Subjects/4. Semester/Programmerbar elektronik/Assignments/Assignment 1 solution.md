# Task
- Create a VHDL-based digital clock capable of displaying seconds and minutes
- The design should include appropriate sequential logic (counters, clock dividers, etc.) and any required concurrent processes.
- Perform a functional simulation of the entire clock circuit. The simulation must clearly demonstrate that the clock is counting time correctly for 2 minutes (120 clocks).

# Code
We begin by creating a counter, that will be able to count from 0 to 60, incrementing by one for each clock pulse
# Topics to be covered
- [ ] Semaphore
- [ ] Critical section
- [ ] Synchronization problems
- [ ] Monitors
- [ ] Deadlock
	- [ ] Prevention
	- [ ] Avoidance
	- [ ] Detection
- [ ] Address binding/mapping
- [ ] Contiguous memory allocation
- [ ] Paging
- [ ] Demand paging
- [ ] Page replacement
- [ ] Trashing

# Relevant lectures
- [[L9 - Process synchronization]]
- [[L10 - Deadlocks]]
- [[L11 - Memory]]
- [[L12 - Virtual memory]]

# Relevant materials
- [[COS - lecture 9 - Itslearning.pdf]]
- [[COS - lecture 10 - Itslearning.pdf]]
- [[COS - lecture 11 - Itslearning.pdf]]
- [[COS - lecture 12 - Itslearning.pdf]]

# Topics
## Process synchronization
Processes can execute concurrently or in parallel
**Concurrent**
- CPU scheduler switches rapidly between processes to provide concurrent execution.
- Processes may only _partially_ complete before being stopped in favor of another process.

**Parallel**
- Multiple instruction streams (different processes) execute _sim_
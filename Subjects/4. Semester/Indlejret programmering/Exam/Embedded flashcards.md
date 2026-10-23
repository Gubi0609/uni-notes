#flashcards/Embedded

What is a finite state machine (FSM)?::A computational model that can be in exactly one state at a time. Transitions between states are triggered by events/conditions. Can be Moore (outputs depend only on state) or Mealy (outputs depend on state AND input).

What is the difference between a Moore machine and a Mealy machine?::Moore machine: outputs depend only on the current state. Mealy machine: outputs depend on both the current state AND the current inputs.

How do you implement a state machine in C?::Use a static state variable + a switch statement. Static variables retain their value between function calls. Example: static INT8U state = STATE_IDLE; switch(state) { case STATE_IDLE: ... }

Why use static variables in state machine functions?::Static local variables retain their value between calls to the function — they are not re-initialized each time. This allows the state to persist across the super loop iterations.

What is the difference between a state machine and a task model?::A state machine describes a single thread of execution (states and transitions). A task model describes multiple parallel tasks and the information flow between them. Both can exist in the same system.

What are the elements of a state diagram?::States (circles), initial state (filled/arrow), transitions (arrows with condition/output labels), final state (double circle). Transition labels contain: events, conditions (timeouts, reset), hardware outputs, messages to other parts, timer starts.

What is RISC and how does it differ from CISC?::RISC (Reduced Instruction Set Computer): small set of simple instructions, each taking one clock cycle. CISC (Complex Instruction Set Computer): complex instructions that may take multiple cycles. ARM is RISC; Intel x86 is CISC.

What is the ARM Cortex-M4?::A 32-bit RISC processor core. Features: great performance + fast interrupt handling, low power (sleep modes), optional MPU, FPU for IEEE754 single-precision floating point, NVIC for interrupts, SysTick timer.

What are the key features of the TM4C123GH6PM microcontroller?::32-bit ARM Cortex-M4 at 80 MHz, 256 KB flash, 32 KB SRAM, 2 KB EEPROM, 43 GPIOs, 2x CAN, USB 2.0, 8x UART, 12-bit ADC, PWM, 6x 32-bit timers, 6x 64-bit timers, 2x watchdog timers.

What are the Cortex-M4 core peripherals?::NVIC (Nested Vectored Interrupt Controller), System Control Block, SysTick (24-bit countdown timer), MPU (Memory Protection Unit, up to 8 regions), FPU (IEEE754 single-precision).

What is the NVIC?::Nested Vectored Interrupt Controller — embedded interrupt controller that supports low-latency interrupt processing. Manages interrupt priorities and enables/disables individual interrupts.

What is SysTick?::A 24-bit countdown timer built into Cortex-M4. Used as the RTOS tick timer (set to 5 ms in this course). Triggers an ISR when it reaches zero.

How does SysTick-based timing work in the super loop?::SysTick ISR increments a volatile variable ticks every 5 ms. The main loop does: while(!ticks); ticks--; // then executes tasks every 5 ms.

What is the Cortex-M4 register set?::R0–R12: general purpose. R13: stack pointer (SP). R14: link register (LR, stores return address). R15: program counter (PC). xPSR: program status register.

What data types does Cortex-M4 support?::32-bit words, 16-bit halfwords, 8-bit bytes. Default byte order is little-endian (instruction memory and PPB are always little-endian).

What is an interrupt?::An asynchronous hardware event that causes the CPU to suspend current execution, save its state, and run an ISR (Interrupt Service Routine). After the ISR returns, normal execution resumes.

What is an ISR?::Interrupt Service Routine — a function that handles a specific interrupt. Should be short and fast. Must be registered in the interrupt vector table (tm4c123gh6pm_startup_ccs_gcc.c on TIVA).

What is the build process for embedded C?::Preprocessor → Compiler → Assembler → Linker → Locator → Executable. C source goes through preprocessor (expands macros/includes), compiler (to object file), linker (combines objects, resolves symbols), locator (assigns memory addresses).

What does the preprocessor do?::Handles directives starting with #: #include (copies header files), #define (replaces with defined value), #ifdef/#ifndef (conditional compilation). Also removes comments and expands macros.

What does the linker do?::Combines object files, resolves unresolved symbol references (functions/variables from other files), searches static libraries. Output is relocatable (no fixed memory addresses yet).

What does the locator do?::Transforms relocatable code into an executable binary image by assigning specific memory addresses to each piece of code and data. On embedded systems this must be done explicitly (unlike PC where the OS handles it).

What is a cross-compiler?::A compiler that runs on one platform (PC) but generates code for a different target platform (e.g. ARM Cortex-M4 TIVA). Used because the target may not have enough resources to run a compiler.

What is inline assembler in C?::Assembly code embedded directly inside a C file using the asm() keyword. Example: asm("ldr r3, [r7, #6]"); Useful for small critical sections without creating a separate .asm file.

What is linked assembler?::Separate .asm source files that are assembled into object files and linked together with C object files at build time. Separate from .c files; labels used instead of function names.

What is the ARM calling convention (ABI)?::First 4 parameters → registers R0, R1, R2, R3. Additional parameters → pushed on stack. Return value → R0. Local variables → on the stack, addressed via R7 (frame pointer). Callee must preserve R4–R11.

What are common ARM Cortex-M4 assembly instructions?::ldr (load register), str (store register), ldrb/strb (load/store byte), mov (move), add/sub, and, orr, eor (XOR), mvn (bitwise NOT), cmp (compare), b/bl (branch/branch with link).

How do you set a bit in C?::Using bitwise OR: Var |= 0x20; sets bit 5. (OR with a mask that has 1s in the bits you want to set.)

How do you clear a bit in C?::Using bitwise AND with NOT: Var &= ~(0x60); clears bits 5 and 6. (~inverts the mask so the bits to clear become 0.)

How do you toggle a bit in C?::Using bitwise XOR: Var ^= 0x02; toggles bit 1. (XOR with 1 flips the bit; XOR with 0 leaves it unchanged.)

How do you test if a bit is set in C?::if (Var & 0x04) — tests if bit 2 is set. The AND result is non-zero (true) if the bit is set.

What is the difference between logical and bitwise operators in C?::Logical operators (&&, ||, !) operate on entire values — result is 0 (false) or 1 (true). Bitwise operators (&, |, ^, ~, <<, >>) operate bit-by-bit on each bit position.

What is a task?::An independent thread of execution that competes with other tasks for CPU time. Defined by: name, unique ID, priority, Task Control Block (TCB), stack, and task routine function.

What is a Task Control Block (TCB)?::Data structure that stores all information about a task: condition/state, name/ID, current state (for state machine), current event, semaphore, timer, pointer to task function.

What criteria are used to divide an application into tasks?::Parallelism (independent functionality), Timing (different timing constraints), Priority (different urgency), Structure (one well-defined purpose per task), Coupling (loosely coupled), Periodicity (fixed-period tasks).

What is RTCS?::Run To Complete Scheduling — a simple non-preemptive (cooperative) scheduler. Each task runs until it voluntarily finishes. Tick-based scheduling. Tasks must not block. Features: tasks, state machines, events, timers, semaphores, queues.

What is non-preemptive (cooperative) scheduling?::The scheduler never forcibly interrupts a running task. Tasks voluntarily yield the CPU by completing their work. If a task runs too long, other tasks are delayed. Used in RTCS.

What is the RTCS schedule() function?::Replaces the super loop. Iterates over all tasks in the pool (POT) and calls the task function if the task is in TASK_READY state. Loops continuously.

What is the RTCS start_task() function?::Registers a task with the scheduler: start_task(TASK_NAME, task_function_pointer). Associates the task's name/ID with its callback function and sets it as ready.

What is the signature of an RTCS task callback?::void my_task(INT8U my_id, INT8U my_state, INT8U event, INT8U data) — receives its own ID, current state, current event, and data (currently unused).

What is a queue?::A FIFO (first-in, first-out) data structure used for inter-task communication. Has a unique name/ID. API: create, put/send, get/receive, full/empty/length, peek (read without removing).

What is the producer-consumer model?::A design pattern where one or more producer tasks write data into a queue, and one or more consumer tasks read from it. The queue decouples the producer and consumer.

What are the three queue implementation strategies?::1) Move data through (shift everything, like a supermarket). 2) Use head/tail pointers/indices (like a post-office ticket). 3) Linked list (dynamic, like calling the next person).

Why must queues be protected by a mutex?::A queue is a shared resource — if two tasks access it simultaneously (in preemptive scheduling), data can be corrupted. The mutex ensures only one task modifies the queue at a time.

What happens when a producer tries to put() into a full queue?::Options: throw away the new data, do something else and try later, overwrite old data, or block (wait forever or with a timeout).

What happens when a consumer tries to get() from an empty queue?::Options: do something else and try later, or block (wait forever or with a timeout).

What is a semaphore?::An integer variable for task synchronization. Only two operations: signal/V (increment, wake waiting task) and wait/P (decrement, block if result would be negative).

What are the two types of semaphores?::Binary semaphore: value 0 or 1. Counting semaphore: value 0 to N, used when N instances of a resource are available (e.g., N parking spots).

What are the two purposes of semaphores?::1) Signaling/serialization — ensure Task B's statement runs after Task A's statement. 2) Mutual exclusion (mutex) — protect a critical section so only one task accesses a shared resource at a time.

How does semaphore signaling (serialization) work?::Task A: does work → sem.signal(). Task B: sem.wait() → does work. Task B blocks until Task A signals, guaranteeing order.

What is a mutex?::A mutual exclusion semaphore. Protects a critical section — only one task may be inside at a time. Key property: can only be released by the task that acquired it (unlike a binary semaphore).

What is the key difference between a mutex and a binary semaphore?::Mutex: can only be released/given by the task that acquired/took it. Protects resources. Binary semaphore: can be released by any task. Used for signaling/serialization.

What is a critical section?::A region of code that accesses a shared resource and must not be executed by more than one task simultaneously. Protected by a mutex or by disabling interrupts/scheduler.

What is a deadlock?::A situation where two or more tasks are each waiting for a resource held by the other — neither can ever proceed. Results in a permanent system hang.

What are Coffman's 4 conditions for deadlock?::1) Mutual exclusion — resource held by at most one task. 2) Hold and wait — a task holding a resource waits for another. 3) Non-preemption — resources cannot be forcibly taken. 4) Circular wait — tasks form a cycle of resource waiting. ALL 4 must hold simultaneously.

How do you prevent deadlocks?::1) Resource ordering — always acquire mutexes in the same order in all tasks. 2) Use timeouts instead of blocking forever (portMAX_DELAY → a finite timeout). 3) Break one of Coffman's 4 conditions.

Can deadlocks occur in RTCS?::No — RTCS is non-preemptive (cooperative). Tasks run to completion without being interrupted by other tasks, so circular waiting cannot form. Deadlocks require preemptive scheduling.

What is an RTOS?::Real-Time Operating System — responds to events within a strictly defined deadline. Properties: deterministic scheduler, priority-based, processes data as it arrives. Not the same as RTCS.

What are typical RTOS applications?::Airbag deployment, air traffic control, industrial process control, closed-loop control (thermostats, AC), digital audio (MP3 decoding), military systems, robotics vision.

What does FreeRTOS provide?::Real-time scheduling (pre-emptive or co-operative), inter-task communication (queues), timing and synchronization primitives (semaphores, mutexes). It is a kernel, not a full OS.

What are the four FreeRTOS task states?::Running (using the CPU), Ready (can run but waiting for CPU), Blocked (waiting for event/time/queue/semaphore), Suspended (not available to scheduler — only via vTaskSuspend/xTaskResume).

What is context switching?::When the kernel switches from one task to another: it saves the current task's context (all registers, stack pointer, PC) to its TCB, then restores the new task's context. Each task has its own stack.

What is preemptive scheduling?::The scheduler can interrupt a running task without its cooperation and switch to a higher-priority task. The interrupted task is resumed later. Opposite: cooperative (non-preemptive) scheduling.

What is round-robin scheduling?::Equal-priority tasks each get an equal time slot (time slice) in turn. Simple and fair — all tasks at the same priority level are served. The task resumes where it left off on its next turn.

What is the FreeRTOS pre-emptive scheduling policy?::Always runs the highest-priority available task. Tasks of identical priority share CPU time via round-robin time slicing (fully pre-emptive with round-robin).

What is the FreeRTOS co-operative scheduling policy?::Context switches only occur when a task voluntarily blocks or explicitly calls taskYIELD(). The scheduler never forcibly interrupts a task.

How do you create a FreeRTOS task?::xTaskCreate(vTaskFunction, "NAME", STACK_SIZE, pvParameters, priority, &handle); The task function has signature: void vTask(void *pvParameters) with an infinite loop inside.

How do you delay a FreeRTOS task?::vTaskDelay(pdMS_TO_TICKS(500)); — blocks the task for 500 ms, allowing other tasks to run. The task transitions to Blocked state during the delay.

How do you create a FreeRTOS binary semaphore?::SemaphoreHandle_t sem = xSemaphoreCreateBinary(); Must create before use. Give: xSemaphoreGive(sem); Take: xSemaphoreTake(sem, portMAX_DELAY);

How do you create a FreeRTOS mutex?::SemaphoreHandle_t mtx = xSemaphoreCreateMutex(); Take: xSemaphoreTake(mtx, timeout); Give: xSemaphoreGive(mtx); The task that takes MUST give it back.

How do you create a FreeRTOS queue?::QueueHandle_t q = xQueueCreate(length, itemSize); Send: xQueueSendToBack(q, &data, timeout); Receive: xQueueReceive(q, &buf, timeout); Peek: xQueuePeek(q, &buf, 0);

What FreeRTOS API must be used inside an ISR?::Functions ending in FromISR, e.g. xSemaphoreGiveFromISR(). Never call blocking API (xSemaphoreTake, xQueueReceive with timeout) from within an ISR.

How do you implement a FreeRTOS critical section?::Option 1 (disable interrupts): taskENTER_CRITICAL() / taskEXIT_CRITICAL(). Option 2 (suspend scheduler): vTaskSuspendAll() / vTaskResumeAll(). Option 3: use a mutex.

What is reentrancy?::A function is reentrant if multiple instances can run simultaneously (it can be called again before a previous call returns) and each instance works correctly independently.

What are the conditions for a function to be reentrant?::1) All variables are local (not static, not global). 2) Shared resources are accessed atomically or protected by semaphores. 3) It never modifies its own code. 4) It only calls other reentrant functions.

Why are static local variables a problem for reentrancy?::Static variables are shared across all instances of a function call — they persist between calls and are not on the stack. If two instances run simultaneously, they corrupt each other's state.

Why are global variables a problem for reentrancy?::Global variables are shared across all tasks. If two tasks call the same function that uses a global, they can interfere. Solution: use local variables or protect globals with semaphores.

What is an atomic operation?::An operation that cannot be interrupted — it completes entirely or not at all. C statements are NOT atomic: foo++ compiles to 3 instructions (load, increment, store) that can be interrupted between steps.

How do you make an operation atomic in embedded C?::Disable interrupts around the critical code (short sections), or use task synchronization primitives (semaphores/mutexes) for longer sections. Disabling interrupts increases interrupt latency.

What is the difference between recursion and reentrancy?::Recursion: a function calls itself. A recursive function must be reentrant. Reentrancy: multiple instances can run simultaneously. A reentrant function does not need to be recursive.

What is the EMP coding standard rule for type names?::Use fixed-width types from emp_type.h instead of built-in C types: INT8U (unsigned char), INT8S (signed char), INT16U (unsigned short), INT16S (signed short), INT32U (unsigned long), INT32S (signed long), FP32 (float), FP64 (double).

What is the EMP rule for naming constants and macros?::Constants, type definitions, enumerations, macros, and #defines are written in UPPER_CASE. All other identifiers (variables, functions) are in lower_case. Hex numbers: 0xFF format.

What is the EMP rule for magic numbers?::Avoid numeric literals in code — use #define or const instead. Example: #define TIM_1_SEC 200 then use TIM_1_SEC instead of 200. Magic numbers become meaningless over time.

What is the EMP rule for the RETURN statement?::RETURN should only appear once — at the end of the function. This ensures single entry, single exit. Use state variables instead of multiple return statements.

What is an include guard in C?::A pattern to prevent a header file from being included more than once: #ifndef _MODULE_H / #define _MODULE_H / (content) / #endif. Prevents duplicate declarations and compile errors.

What is the file structure of an EMP .c file?::Six sections separated by comment lines: Header (module name, project, change log), Include files, Defines, Constants, Variables, Functions. All sections present even if empty.

What is the FPU on Cortex-M4?::Floating-Point Unit — provides IEEE754-compliant single-precision (32-bit) floating-point operations: add, subtract, multiply, divide, multiply-accumulate, square root. Must be explicitly enabled after reset before use.

What is SPI?::Serial Peripheral Interface — a synchronous full-duplex serial communication protocol. 4 wires: MISO (master in, slave out), MOSI (master out, slave in), SCK (serial clock), CS (chip select). Single master, multiple slaves.

How does SPI differ from UART?::UART is asynchronous (no clock, both sides agree on speed beforehand). SPI is synchronous (master provides clock). SPI is faster and full-duplex; UART is simpler for point-to-point.

How does SPI differ from I2C?::I2C is two-wire, half-duplex, synchronous, multi-master multi-slave. SPI is four-wire, full-duplex, synchronous, single master. SPI is much faster than I2C.

What debugging tools are available on the TIVA?::1) Pin/LED toggling (oscilloscope). 2) Serial port + printf (UART to terminal). 3) Assert macro (stops on failure). 4) CCS debugger via Stellaris ICDI (OCD — breakpoints, step, watch variables, registers).

What is the difference between ICE and ICD/OCD debugging?::ICE (In-Circuit Emulator): replaces the microprocessor; expensive; issues at high frequencies. ICD/OCD (In-Circuit/On-Chip Debugger): debug core built into the CPU; uses no RAM/ROM; hardware interface via JTAG.

What is JTAG?::Joint Test Action Group — IEEE standard hardware interface (4-10 pins) used for in-circuit debugging (ICD/OCD). Used by the Stellaris ICDI on the TIVA board to connect to the Cortex-M4 debug core.

What are the four queue topologies?::1) One producer, one consumer. 2) One producer, multiple consumers (all read from same queue). 3) Multiple producers, one consumer. 4) Each task has its own input queue (some OSes implement this).

What is blocking vs non-blocking queue access?::Blocking: task waits (forever or with timeout) if queue is full (put) or empty (get). Non-blocking: task immediately returns and does something else. Timeout is the middle ground — block for a limited time.

What is a software timer in RTCS?::A counter decremented each tick by swt_ctrl(). When it reaches 0, a TE_TIMEOUT event is placed into a specified event buffer. Allows time-based events without hardware timers.

What is the difference between a shared state buffer and a shared event buffer?::Shared state buffer: value persists after reading — subsequent reads return the same value (like a shared variable). Shared event buffer: value is consumed/destroyed after reading — one-shot (like a queue of length 1).

What is the super loop pattern?::The basic embedded system pattern: initialize hardware, then loop forever executing tasks. with SysTick: while(1) { while(!ticks); ticks--; // execute tasks every 5ms }

What does printf() do and what is its signature?::Prints formatted data to stdout. Signature: int printf(const char *format, ...); Format tags: %d (int), %c (char), %s (string), %x (hex), %f (float). Related: sprintf (to string), fprintf (to stream).
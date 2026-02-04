The assignment has the following requirements

- The program must implement a 0-7 counter
- The current count must be represented by a color on the on-board RGB LED
    - 0: Off
    - 1: Green
    - 2: Blue
    - 3: Cyan
    - 4: Red
    - 5: Yellow
    - 6: Magenta
    - 7: White
- The counter must be able to count up and down
- The counter should proceed on step with a button push
- The direction of the counter must change with a double button push
- The counter must enter AUTO mode when the button is held for 2 seconds or more
    - When in AUTO mode the counter must proceed one step every 200 ms
- A button push while in AUTO mode should return the counter to manual mode

The full assignment can be read in [[Subjects/4. Semester/Indlejret programmering/PDFs/Assignment1.pdf|Assignment1.pdf]].

---
This article covers the buildup of the system starting with the basics and building on top of that to lastly implement all the criteria from above. For the full code, see my [GitHub](https://github.com/Gubi0609/EMP-Assignment1).

# Basics
I'll start with the basics by implementing basic logic to change through the colors and enabling the pins correctly.

Criteria covered in this section:
The program must implement a 0-7 counter
- The current count must be represented by a color on the on-board RGB LED
    - 0: Off
    - 1: Green
    - 2: Blue
    - 3: Cyan
    - 4: Red
    - 5: Yellow
    - 6: Magenta
    - 7: White
- The counter must be able to count up ~~and down~~
- The counter should proceed on step with a button push
## Colors
The RBG LED which will be used for this can be found on port F of the GPIO. The LED pins are as follows
- Red: PF1
- Blue: PF2
- Green: PF3

We can use this to cycle through the colors by enabling the RBG pins, which will combine to the colors.
The colors, the corresponding count, and their corresponding HIGH/LOW pins can be seen in the following table.

| Counter Value | PF1 (red) | PF2 (blue) | PF3 (green) | Color   |
| ------------- | --------- | ---------- | ----------- | ------- |
| 0             | 0         | 0          | 0           | Off     |
| 1             | 0         | 0          | 1           | Green   |
| 2             | 0         | 1          | 0           | Blue    |
| 3             | 0         | 1          | 1           | Cyan    |
| 4             | 1         | 0          | 0           | Red     |
| 5             | 1         | 0          | 1           | Yellow  |
| 6             | 1         | 1          | 0           | Magenta |
| 7             | 1         | 1          | 1           | White   |

When implementing this in code, it is important to remember, that we will be setting the values for _all_ Port F pins (bit 0-7). Since we only want to set PF1 - PF3, we will leave the rest as zero.

```c
// Initialize colors {PF1, PF2, PF3} = {r, b, g}
const int off = 0x00; // 0000 0000
const int green = 0x08; // 0000 1000
const int blue = 0x04; // 0000 0100
const int cyan = 0x0C; // 0000 1100
const int red = 0x02; // 0000 0010
const int yellow = 0x0A; // 0000 1010
const int magenta = 0x06; // 0000 0110
const int white = 0x0E; // 0000 1110

// Color pointer vector to point to the colors
int colors[8] = {off, green, blue, cyan, red, yellow, magenta, white};

// Current count = current color
int cnt = 0;

// To be used in later development
bool dirUp = true;
bool autoMode = false;
```

We will use this to refer to later, to set the color on the LED.

## Pins
Next we will enable the pins

We will start by enabling power and clock control to Port F, which will be the one we are using.

Next a dummy is used to implement a few dummy cycles in order to give Port F time to initialize.

The _direction_ of the Port F pins are set as either output or input depending on their bit value.

A pull-up resistor is enabled for the switch, meaning it will be HIGH when not pressed an LOW when pressed.

Lastly digital function is enabled for Port F 1 - Port F 4 (**PF1 - PF4**) meaning we can actually code with them.

```c
int dummy; // Dummy to do a few cycles

// Enable GPIO port F (used for RBG and switch) by turning on power to the port
SYSCTL_RCGC2_R = SYSCTL_RCGC2_GPIOF; // System Control Run-Mode Clock Gating Control

// Do a dummy read to insert a few cycles after enabling the peripheral
dummy = SYSCTL_RCGC2_R;

// Enable RGB (PF1 - PF3) as output and switch (PF4) as input
GPIO_PORTF_DIR_R = 0x0E; // 0000 1110 - Bit 1 is output, bit 0 is input

// Enable pull-up resister for switch (PF4)
GPIO_PORTF_PUR_R = 0x10; // 0001 0000

// Enable digital function for PF1 - PF4
GPIO_PORTF_DEN_R = 0x1E;
```

## While loop
Lastly, we implement an infinite while loop, that reads the value of PF4 and increments cnt if PF4 is pressed.

It will also display the current count on the RBG LED

```c
// Loop forever
while(1){
// Check if switch is pressed (active LOW with pull-up)
	if (!(GPIO_PORTF_DATA_R & 0x10)) {
		cnt = (cnt + 1) % 8; // Cycle through 0-7
		
	// Wait for button release as to not increment indefinitely
	while(!(GPIO_PORTF_DATA_R & 0x10));
	}

	// Set LED color (clear LED bits and set new color)
	GPIO_PORTF_DATA_R = (GPIO_PORTF_DATA_R & ~0x0E) | colors[cnt];
}
```

### If statement
We check if the data register from Port F has the switch enabled. This done by performing an AND operation on PORTF_DATA and 0001 0000, where the _1_ represents PF4 (being the 5th bit from the right (0, 1, 2, 3, 4)).

If the button is pressed, cnt is incremented, and we perform modulus division on it to keep it within 0-7

A while loop is implemented again, which just runs and blocks indefinitely while the button is pressed.

### Setting LED
The LED is set from the [[Assignment 1 solution#Colors|colors]] defined before.
- We start by _clearing_ the LEDs by performing an AND operation on PORTF_DATA and `~0x0E` which is 0000 1110 inverted (so 1111 0001). By doing this, we turn off PF1 - PF3.
- Next we perform an OR operation on this, and the color of our choice (decided by the count).
- This effectively sets the bits of the PF1 - PF3 to the ones of the color.

# ISR
We now want to move the button logic to an Interrupt Service Routine (**ISR**).
This requires a few steps and changing in the startup file for the specific chip (TM4C123GH6PM). This is provided by the CCS program.

Criteria covered in this section:
The program must implement a 0-7 counter
- The current count must be represented by a color on the on-board RGB LED
    - 0: Off
    - 1: Green
    - 2: Blue
    - 3: Cyan
    - 4: Red
    - 5: Yellow
    - 6: Magenta
    - 7: White
- The counter must be able to count up ~~and down~~
- The counter should proceed on step with a button push

So in short: The same criteria as [[Assignment 1 solution#Basics|before]], but now with smarter logic.

## Setting switch
We want to activate the ISR at a falling edge of our switch (being pushed).
```c
// Set switch (PF4) as edge-sensitive
GPIO_PORTF_IS_R = 0x00;

// Trigger controlled by IEV
GPIO_PORTF_IBE_R = 0x00;

// Falling Edge Trigger
GPIO_PORTF_IEV_R = 0x00;

// Clear any Prior Interrupts
GPIO_PORTF_ICR_R = 0x10;

// Unmask interrupts for PF4
GPIO_PORTF_IM_R = 0x10;
```

By setting the IS_R value for PF4 to 0 (including the rest, as they are not used for this), we set it to edge-sensitive instead of level-sensitive (HIGH/LOW).

We next set _IBE_ of PF4 to 0, meaning that we disable _Interrupt Both Edges_.

Instead we enable _IEV_ on falling edge by setting the value for PF4 to 0.
- If we set it to 1, we would be detecting on _rising edge_.

We clear any pending interrupts on PF4 _before_ enabling the pin for Interrupts. This is done by setting _ICR_ of PF4 to 1.

Lastly, PF4 is enabled - or _unmasked_ - by setting the _IM_ value of PF4 to 1 (enable).

## Enable interrupts from Port F in NVIC
To actually _use_ the interrupts from port F, we will need to enable interrupt signals from this in the NVIC (Nested Vector Interrupt Controller).

_NVIC_ is used by the ARM Cortex-M4 for interrupt management hardware. It manages the following:
- Prioritizes and manages all peripheral interrupts
- Automatically saves/restores processor context when entering/leaving an ISR
- Supports _nested interrupts_ (higher priority can preempt lower priority)

```c
NVIC_EN0_R |= (1 << (INT_GPIOF - INT_GPIOA));
```

We enable interrupts in NVIC from port F from this simple line.

`NVIC_EN0_R` is a 32-bit (0 - 31) hardware register that enables interrupts in the processor. By setting a bit to _1_ we enable that interrupt.

Interrupt assignments start from _16_ with `INT_GPIOA`. If we want to find `INT_GPIOF`'s placement in NVIC, we will need to subtract `INT_GPIOA` from the placement of `INT_GPIOF`. Since GPIO Port A is _16_ and GPIO Port F is _46_ the result will be _30_.

Since we want to now enable NVIC _30_ we will need to shift bit 1 _left_ by 30 bits.
- Remember LSB is to the right, and MSB is to the left.

We now perform an OR operation on `NVIC_EN0_R` to _enable_ bit 30, and activate Port F.
- Sidenote: If a bit _higher_ than 31 needs to be activated, `NVIC_EN1_R` can be used and so on for higher bits.
	- `NVIC_EN1_R`: 32-63
	- `NVIC_EN2_R`: 64-95
	- And so on.

## Interrupt Service Routine (ISR)
Now that we have set up alle the basics for enabling ISR, we will need to define _what to do_.

Before defining our ISR, we will need to let the system know, that it should be used for interrupts from port F.

For this, we navigate to `tm4c123gh6pm_startup_ccs.c` which is a startup file created by Code Composer Studio (CCS).

```c
void ResetISR(void);
static void NmiSR(void);
static void FaultISR(void);
static void IntDefaultHandler(void);

// Custom ISR handler
void GPIOF_Handler(void);
```

We can see her the _declaration_ of a bunch of default fault handlers.
- We add the declaration of our custom interrupt handler to this.
- We will NOT define it just yet.


We next need to let the system know to use this on port F.
We navigate further down the file to find the _vector table_ that defines what interrupts from parts of the system will use to handle the interrupt.

```c
#pragma DATA_SECTION(g_pfnVectors, ".intvecs")
void (* const g_pfnVectors[])(void) =
{
	(void (*)(void))((uint32_t)&__STACK_TOP),
	
	// The initial stack pointer
	
	ResetISR, // The reset handler
	
	NmiSR, // The NMI handler
	
	FaultISR, // The hard fault handler
	
	IntDefaultHandler, // The MPU fault handler
	
	IntDefaultHandler, // The bus fault handler
	
	IntDefaultHandler, // The usage fault handler
	
	0, // Reserved
	
	// ...
	
	IntDefaultHandler, // System Control (PLL, OSC, BO)
	IntDefaultHandler, // FLASH Control
	
	// Custom handler
	GPIOF_Handler, // GPIO Port F
	
	IntDefaultHandler, // GPIO Port G
	IntDefaultHandler, // GPIO Port H
	
	// ...

};
```

We can see a section of the vector here with examples of how it is defined.

As we can see, a lot of the interrupts, including the Ports use the default interrupt handler, `IntDefaultHandler`.
- We change the handler of GPIO Port F to our custom handler, `GPIOF_Handler`.


We now go back to `main.c` to _define_ our ISR
```c
// The Interrupt Service Routine (ISR)
void GPIOF_Handler(void) {
	
	// For debounce
	volatile int i;
	
	// Clear the interrupt flag for PF4 (must be done first)
	GPIO_PORTF_ICR_R = 0x10;
	
	// Increment counter to cycle through colors
	cnt = (cnt + 1) % 8; // Cycle through 0-7
	
	// Simple debounce delay
	for(i = 0; i < 100000; i++);
	
	// Wait for button release as to not increment indefinitely
	while(!(GPIO_PORTF_DATA_R & 0x10));
}
```

This is relatively simple. We first define a volatile integer `i` to be used for a simple debounce delay later on.

The interrupt flag for PF4 will need to be done first, as to make room for future interrupts.

Next we increment cnt. We will however need to keep it within 0-7. This is simply done be performing _modulus_ division. The clever reader will notice that this step is the same as [[Assignment 1 solution#If statement|before]] when we covered the basics.

Lastly we implement the debounce delay by blocking the processor for a short time by increment `i` from 0 to 100.000.

To add to this, we also wait for the button to be released. This is not essential, and will be removed later on to make room for further functionality.

## New while loop
The while loop from [[Assignment 1 solution#While loop|before]] can now be shortened to only include LED control
```c
// Loop forever
while(1) {
	// Set LED color (clear LED bits and set new color)	
	GPIO_PORTF_DATA_R = (GPIO_PORTF_DATA_R & ~0x0E) | colors[cnt];
}
```

And the system will now react as before, but now with the button logic handled by an Interrupt Service Routine.
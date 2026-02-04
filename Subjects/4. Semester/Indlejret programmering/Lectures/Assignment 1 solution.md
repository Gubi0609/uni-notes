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

# Basics
I'll start with the basics by implementing basic logic to change through the colors and enabling the pins correctly.

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
```

We will use this to refer to later, to set the color on the LED.

## Pins
Next we will enable the pins

We will start by enabling power and clock control to Port F, which will be the one we are using.

Next a dummy is used to implement a few dummy cycles in order to give Port F time to initialize.

The _direction_ of the Port F pins are set as either output or input depending on their bit value.

A pull-up resistor is enabled for the switch, meaning it will be HIGH when not pressed an LOW when pressed.

Lastly digital function is enabled for PF1 - PF4 meaning we can actually code with them.

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
Husk at du har ændret i startup filen. og nogle værdier i headerfilen bruges til reference.
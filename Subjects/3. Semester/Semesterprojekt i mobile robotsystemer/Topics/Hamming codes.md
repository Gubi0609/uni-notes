
## What are Hamming Codes?
Hamming codes are a way to detect a 1 bit flip error. That is to say, when a single bit in a message is flipped, hamming codes can be used to correct the flipped bit.

# How do they work?

## Control bits
In a table of eg. 16 bits, 4 bits are used to control, that the data is correct, 11 bits are used to store data, and 1 bit is unused.
![[Pasted image 20251005130328.png|500]]
Position 0 is unused
Position 1, 2, 4 & 8 are used as control bits.
The rest (position 3, 5-7, 9-11, 12-15) are used to store data.

Notice, that the control bits are all placed in a position, that is a power of 2 ($2^0 = 1$, $2^1 = 2$ and so on)
That pattern will continue, if the hamming code is scaled to contain more data.

That also means, that the control bits will take up less percentile space, if the hamming code is scaled to a larger size, as the subset of positions that are equal to a power of 2 does not increase linearly with all possible positions.

## Parity checks
With the control bits in place, parity checks can be performed to narrow down the position of a potentially flipped bit

Parity checks work by checking if the number of 1's in an area is even or odd. We want it to be even, to maintain no errors.
![[Pasted image 20251005131011.png|500]]

In the above image, the control bits are used to perform parity checks in the blue areas, and then combine the results of these (eg. using AND) to narrow down the position of a single bit error.



---
#data-communication #error-detection
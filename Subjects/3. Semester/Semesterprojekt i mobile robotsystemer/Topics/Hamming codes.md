
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

The table above is called a (15, 11) Hamming Code, as 11 of the 15 used bits store data.

## Parity checks
With the control bits in place, parity checks can be performed to narrow down the position of a potentially flipped bit

Parity checks work by checking if the number of 1's in an area is even or odd. We want it to be even, to maintain no errors.
![[Pasted image 20251005131011.png|500]]

In the above image, the control bits are used to perform parity checks in the blue areas, and then combine the results of these (eg. using AND) to narrow down the position of a single bit error.

When encoding the hamming code, the parity checks are used to determine whether the control bit should be a 0 or 1. If the data in the blue area belonging to the control bit already has an even number of 1's, the control bit is set to 0. Else it is set to 1.

For a larger size of hamming code (eg. 256 bits) the parity checks might look like this:
![[Pasted image 20251005132025.png|500]]
## Extended Hamming Codes
The above works fine for detecting a single bit error. But what if we have more than one?
Using Extended Hamming Codes, we utilize the unused bit in a parity check for the whole table.

We count up the number of 1's in the whole table, and just like before we want the number of 1's to be even. If it is even, the extended hamming bit is set to 0. Else it is set to 1.

In that way, we can detect if we have an even or odd number of errors. We can still only correct for one error, but at least we can now _detect_ more than one error.
That can be used to request a bit block from the sender again. Say for example, that you have some data of 30 bits blocks, each split up into 16 bit extended hamming codes. If there is an error in one of the blocks, that can't be corrected by the receiver, that specific block can be requested again instead of all 30 blocks.

## Positions represented by bits
If each of the parity checks are made, so that NO_ERROR = 0 and ERROR = 1, these results can be combined to the bit-value of the position, where the flipped bit is.

See this:
![[Pasted image 20251005132245.png|300]]

Here Q1, Q2, Q3 all produce an error, and so their result is set to 1. Q4 doesn't produce an error, and so its value is set to 0.
Then these results can be combined with Q4 being MSB (Most Significant Bit) and Q1 being LSB (Least Significant Bit) in to the bit value of the flipped bit's position:
### $$0111_2 = 7_{10}$$
This can be extended, if we represent all the positions using binary instead of decimal:
![[Pasted image 20251005132640.png|400]]

Then we can also see, why the control bits are placed in positions, that are a pos

---
#data-communication #error-detection
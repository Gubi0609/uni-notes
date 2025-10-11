# What is it?
CRC (Cyclic Redundancy Check) is a form of error detection, that can detects upward of **99%** of all errors in a bit string.
It works a bit like a checksum, where it performs some binary math, and checks if it ends with the expected value (000..). If it does not, it knows that there is an error in the data-block.

Unlike a checksum CRC can be used for smaller bits of data, meaning that you could have your data split up in to blocks (eg. blocks of 12 bits) and then append your CRC check to that data -block alone. Do this for all data blocks and you have a quick and easy method of checking for errors in each part of your data. This means, that you could potentially detect an error in block 7, 9, 13, and 15, and then request those blocks alone instead of requesting _ALL_ the data like with checksum.

# How does it work?
CRC works a bit like polynomial division. You have a numerator (your data) and a denominator (your control key).

## How to select a control key
Say, that you want a control key of 5 bits. You would then set up a fourth-order polynomial like so
## $$ x^4+0x^3+0x^2+x^1+x^0=x^4+x+1$$
This would translate into a binary control key like this (10011) where each bit is tied to the value of each part of the polynomial. MSB (Most significant bit) is in this case tied to $x^4$ and LSB (Least Significant Bit) is tied to $x^0$.
Thus, we in this example end with **10011** as our control key.

## Preparing data
Before performing our polynomial division, we want to prepare our binary data string. This is done by appending $n = length(control\quad key)-1$ number of 0's. In this case, our control key is 5 bits long, so we would append $5-1=4$ 0's to our data.

**Data string (before preparation):** 101100101101 (12 bits)
**Data string (after preparation):** 101100101101*0000* (16 bits)

And so, our data is ready for polynomial division.
**It is important to note, that _you_ can decide what length your final "encoded" block should be, by choosing the length of your actual data (in this case 12 bits) and the length of your polynomial. I have chosen the two, so that we end up with an encoded CRC block of 16 bits.**

## Polynomial division
Polynomial division works just like an XOR operation, when we're performing it on bit-level

![[Pasted image 20251011115003.png]]

We start from the MSB in our prepared data block, and perform an XOR operation on each bit. In this case we end with **00101** as the result of that XOR.

![[Pasted image 20251011120109.png]]

We ignore the otherwise MSB of our result, and therefore we do not write it.
Next we move the next bit in our prepared data block to sit as the LSB of the next XOR operation.

Now, we can se that the MSB of our next operation is a 0. In this case, something interesting happens.

![[Pasted image 20251011120349.png]]

Since our MSB is 0, we perform the next XOR operation with _all 0's_. This ensures that we ignore the 0 (for the next XOR operation), and just like before we move the next bit in our prepared data string to be the LSB of the next XOR operation.

![[Pasted image 20251011120648.png]]

Now the MSB is not 0, and so we use our control key for the XOR operation again.

![[Pasted image 20251011121744.png]]

We continue like this, and end up with our remainder, when we have no more bits in our prepared data string to append. **The remainder for this calculation is in the red box.**
We now append this remainder to our data string _instead of_ the 0's we put there before, and end up with the following:

**Data string (before preparation):** 101100101101 (12 bits)
**Data string (after preparation):** 101100101101*0000* (16 bits)
**Data string (after encoding):** 101100101101*1101* (16 bits)

Finally we have the bit string 1011001011011101, that we send of into our communication channel.

## Receiver end
On the receiver end, we receive the bit string 1011001011011101, and now want to check if the data, we received is correct.
This is done in the same way as when encoding (by polynomial division).
We want to end up with a remainder of 0000. If we end up with _anything else_, we know, the data has been corrupted.

![[Pasted image 20251011122535.png]]

Here, we can see, that we end up with a remainder of 0000, and we then know, that the data is correct.

### Example of corrupted data
In this example, I have changed one single bit to be incorrect.

![[Pasted image 20251011122742.png]]

We can see, that we end up with a non-zero remainder, and we then know, that the data block is corrupted.
We can then choose to request this single block from the sender again, and check if this new block is corrupted.

**In the meantime, we can buffer the rest of the data, until we receive the corrected version of this block. In that way, the sender can send eg. 30 blocks of data, we request 4 corrupted blocks again while buffering the rest, and afterwards we decode all 30 blocks, while only 4 blocks had to be send again, instead of all 30.**

# Code implementation
I will now explain how the above explanation is implemented in code.

## Encoding
``` cpp
vector<uint16_t> CRC::encode1216(vector<uint16_t> splitBinaryData) {
    
    vector<uint16_t> encodedData;

    // Generator polynomial for class denominator
    const uint16_t generator = vec2bin(denominator);

    for(int i = 0; i < splitBinaryData.size(); i++) {
        // We only use 12 bits of data
        splitBinaryData[i] &= 0x0FFF;

        // Append 4 zeros (shift left by 4 bits)
        uint16_t shifted = splitBinaryData[i] << 4;

        // Perform modulo-2 division
        for (int i = 15; i >= 4; --i) { // from MSB to bit 4
            if (shifted & (1 << i)) {
                shifted ^= generator << (i - 4);
            }
        }

        // Remainder is in the lowest 4 bits
        uint16_t crc = shifted & 0xF;

        // Encoded 16-bit word: data (12 bits) + crc (4 bits)
        encodedData.push_back((splitBinaryData[i] << 4) | crc);

    }

    return encodedData;

}
```

We first define our result vector called _encodedData_. We can see, that it contains objects of _uint16_t_. This means "Unsigned Int" (16 bit). More precisely it means "Unsigned Short".
Next, our control key is defined. This is in my code defined as a class attribute. When defining it, it is defined as a vector of 1's and 0's, and we now only redefine it as an uint16_t.

Next, we go through our vector of 12 bit data, that needs to be encoded.

We first check, if the data really only _is_ 12 bits by applying a mask `0x0FFF` 
	The first part of the mask `0x`means, that we are writing a hexidecimal number. 
	The next part `0FFF`is a hexidecimal, and in binary it is written `0b 0000 1111 1111 1111`. Meaning that 12 bits of it is 1's.
This results in only using the 12 first bits of our data block (remember, that LSB is the last bit in our bit string).
	The operation `&=`really means, that we are performing a bitwise AND operation, and storing it in `splitBinaryData[i]`.

---
## Recourses
https://en.wikipedia.org/wiki/Cyclic_redundancy_check
https://www.geeksforgeeks.org/dsa/modulo-2-binary-division/
https://youtu.be/A9g6rTMblz4
https://youtu.be/wQGwfBS3gpk

---
#error-detection #data-communication 
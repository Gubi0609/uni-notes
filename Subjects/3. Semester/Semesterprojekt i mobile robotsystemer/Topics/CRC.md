
# What is it?
CRC (Cyclic Redundancy Check) is a form of error detection, that can detects upward of **99%** of all errors in a bit string.
It works a bit like a checksum, where it performs some binary math, and checks if it ends with the expected value (000..). If it does not, it knows that there is an error in the data-block.

Unlike a checksum CRC can be used for smaller bits of data, meaning that you could have your data split up in to blocks (eg. blocks of 12 bits) and then append your CRC check to that data -block alone. Do this for all data blocks and you have a quick and easy method of checking for errors in each part of your data. This means, that you could potentially detect an error in block 7, 9, 13, and 15, and then request those blocks alone instead of requesting _ALL_ the data like with checksum.

# How does it work?
CRC works a bit like polynomial division. You have a numerator (your data) and a denominator (your control key).

## How to select a control key
Say, that you want a control key of 5 bits. You would then set up a fourth-order polynomial like so
## $$ x^4+0x^3+0x^2+x^1+x^0=x^4+x+1$$
This would translate into a binary control key like this (10011) where each bit is tied to the value of 

# Code implementation


---
## Recourses
https://en.wikipedia.org/wiki/Cyclic_redundancy_check
https://www.geeksforgeeks.org/dsa/modulo-2-binary-division/
https://youtu.be/A9g6rTMblz4
https://youtu.be/wQGwfBS3gpk

---
#error-detection #data-communication 
A K-map can be used to shorten down a logic system

## Example
![[Pasted image 20260205135729.png]]
The above truth table can be plotted in to a K-map to find its circuit/boolean equation

|     | AB  | AB  | AB  | AB  |
| --- | --- | --- | --- | --- |
|     | 00  | 01  | 10  | 11  |
| 0   | 0   | 0   | 1   | 1   |
| 1   | 0   | 1   | 0   | 1   |
We can see that the output is 1 when A and Select is high, or B and NotSelect is high.
$Output = A*Sel + B*NOTSel$
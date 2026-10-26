# Opgave 1
kriv en rekursiv algoritme, som har et naturligt tal som parameter og returnerer summen af de ulige tals
kvadrater fra 1 til N.

Eksempel: kaldt med parameteren 8 returneres 84 ($1^2+3^2 +5^2 + 7`2$).

Det er vigtigt at optimere algoritmen, så overflødige rekursive kald undgås.

### Kode
```cpp
#include <iostream>

int sumOfOddSquared(int limitNum) {

    // Bottom limit reached, square of 1 is 1, so return it and stop recursion.
    if (limitNum <= 1) return 1;

    // Ensure that number is odd by checking if it is divisible by 2
    if (limitNum % 2 == 0) limitNum -= 1;

    // Recursively square and sum up
    return (limitNum * limitNum) + sumOfOddSquared(limitNum - 2);

}


int main() {
    int testNum = 8;

    std::cout << "The sum of odd numbers squared up until " << testNum << " is: " << sumOfOddSquared(testNum) << std::endl;

    return 0;
}
```

## Output
```
The sum of odd numbers squared up until 8 is: 84
```

# Opgave 2
Hvad er Store-O tidskompleksiteten for nedenstående algoritme. Begrund dit svar.
```java
public static int myMethod( int N )
{
	int x = 0; int y = 0;
	for (int i = 0; i < N; i++)
	{
		for (int j = 0; j < N; j++)
		{
			for (int k = 0; k < N*Math.sqrt(N); k++)
			//square root; C++: #include <math.h>
			{
				x++;
			}
			j *= 2;
		}
		i += i;
}

for (int i = 0; i < N*N; i++)
	y++;
return x+y;
}
```

## Svar
- Yderste for loop er O(n), men fordi man i for loopet har linjen `i += i` bliver det $O(\log n)$.
- For loop nummer 2 er O(n), men fordi man har linjen `j *= 2`, bliver det også $O(\log n)$.
- For loop nummer 3 har kompleksitet $O(n * \sqrt(n))$, hvilket nemt kan aflæses i for loopets start.
- For loop nummer 4 i bunden har kompleksitet $O(n^2)$.

Samlet set er det
$$O(\log(N))\cdot O(\log(N))\cdot O(N\cdot \sqrt N)+O(N^2)=O(\log^2(N)\cdot N^{3/2}+N^2)=\boxed{O(N^2)}$$

Siden $O(N^2)$ var størst i den sidste, har den størst indflydelse, og er derfor det endelige resultat.


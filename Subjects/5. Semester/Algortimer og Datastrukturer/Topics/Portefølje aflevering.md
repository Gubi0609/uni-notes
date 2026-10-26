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


# Opgave 3
Skriv en rekursiv algoritme med følgende signatur:
$$\texttt{bool additive(String s)}$$
Parameteren indeholder en streng bestående af cifre, fx. “82842605”.

Algoritmen returnerer true, hvis parameteren indeholder en substring af tre på hinanden efterfølgende tal,
hvor det tredje ciffer er lig med summen af de to forrige.

I ovenstående eksempel returneres true, fordi indeks 5 (6) er summen af indeks 3 og 4 (4 plus 2).

Tip: ASCII-værdien af karakteren ‘7’ er 55.

## Kode
```cpp
#include <iostream>
#include <string>

bool additive(std::string s) {

    if (s.size() < 3) return false;

    // Sum together the first and second and convert to int by subtracting
    // ASCII value of '0'
    int sum = (s[0] - 48) + (s[1] - 48);

    bool result = (s[2] - 48) == sum;

    // Remove first character
    s.erase(0,1);

    return result + additive(s);

}



int main() {

    std::string testString = "82842605";

    std::string result = additive(testString) ? "contains an additive string" : "does not contain an additive string";

    std::cout << "The string \"" << testString << "\" " << result << std::endl;

    return 0;
}
```

## Output
```
The string "82842605" contains an additive string
```

# Opgave 4
Skriv en algoritme, der har et array af usorterede, entydige naturlige tal som input og find de tre tal i
arrayet, hvis sum er tættest på en potens af 2. Det samme tal kan må bruges én gang.

Algoritmens returværdi skal være et heltalsarray, som først indeholder de tre tal og dernæst den tilhørende
potens af to (fx 512).

Kaldt med arrayet {23,56,22,11,65,89,3,44,87,910,45,35,98}, returneres de tre tal 89, 3, 35 og potensen af
2: 128.

Hvad er Store-O tidskompleksiteten af din algoritme? Begrund dit svar og diskuter mulighederne for at
optimere din løsning yderligere.
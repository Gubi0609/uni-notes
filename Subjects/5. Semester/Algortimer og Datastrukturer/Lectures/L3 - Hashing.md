
---
**Date:** 2026-09-21

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[03 - Kapitel 5 - hashing.pdf]]
[[Øvelser i hashing.pdf]]
[[MIT Hopscotch Hashing.pdf]]
[[Pagh Cuckoo Hashing.pdf]]

# Topics


# Notes

# Exercises

## Exercise 1
En hashtabel har plads til 16 elementer. Indsæt fem elementer, som alle hasher til samme position i tabellen med quadratic probing.

### Step 1: Empty table
| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  | 13  | 14  | 15  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
### Step 2: Insert element **20**
| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  | 13  | 14  | 15  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20  |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
### Step 3: Insert element **30**
- Also hashes to index _0_. So use **Quadratic probing:** $\text{hash}(x)+i^2=\text{new hash}$
	- $0+1^2=1$: New hash is _1_ since it is unoccupied

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  | 13  | 14  | 15  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20  | 30  |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
### Step 4: Insert element **40**
- Also hashes to index _0_. So use **Quadratic probing**
	- $0+1^2=1$: Already occupied, continue iteration
	- $0+2^2=4$: New hash is _4_ since it is unoccupied

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  | 13  | 14  | 15  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20  | 30  |     |     | 40  |     |     |     |     |     |     |     |     |     |     |     |
### Step 5: Insert element **50**
- Also hashes to index _0_. **Quadratic probing** used
	- $0+1^2=1$: Occupied, continue
	- $0+2^2=4$: Occupied, continue
	- $0+3^2=9$: Unoccupied!

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  | 13  | 14  | 15  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20  | 30  |     |     | 40  |     |     |     |     | 50  |     |     |     |     |     |     |
### Step 6: Insert element **60**
- Hashes to index _0_. Use Quadratic probing
	- $0+1^2=1$: Occupied
	- $0+2^2=4$: Occupied
	- $0+3^2=9$: Occupied
	- $0+4^2=16$: Unoccupied, but not within reach!

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  | 13  | 14  | 15  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 20  | 30  |     |     | 40  |     |     |     |     | 50  |     |     |     |     |     |     |
- Even with wrap around using `mod table_size`, we get the same slots already occupied...

## Exercise 2
En hashtabel har plads til 11 elementer. Indsæt seks elementer, som alle hasher til samme position i tabellen med quadratic probing.

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |     |     |     |     |     |     |     |

### Step 1: Insert element **10**
- Hashes to _0_

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10  |     |     |     |     |     |     |     |     |     |     |
### Step 2: Insert element **20**
- Hashes to _0_. Occupied, so use **Quadratic probing**
	- $0+1^2=1$

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10  | 20  |     |     |     |     |     |     |     |     |     |
### Step 3: Insert element **30**
- Hashes to _0_. Occupied
	- $0+1^2=1$: Occupied
	- $0+2^2=4$: Unoccupied

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10  | 20  |     |     | 30  |     |     |     |     |     |     |

### Step 4: Insert element **40**
- Hashes to _0_. Occupied
	- $0+1^2=1$: Occupied
	- $0+2^2=4$: Occupied
	- $0+3^2=9$: Unccoupied

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10  | 20  |     |     | 30  |     |     |     |     | 40  |     |
### Step 5: Insert element **50**
- Hashes to _0_
	- $0+1^2=1$
	- $0+2^2=4$
	- $0+3^2=9$
	- $0+4^2=16$: Out of range! Wrap around with `mod table_size`
		- $16\%11=5$: Unoccupied

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10  | 20  |     |     | 30  | 50  |     |     |     | 40  |     |
### Step 6: Insert element **60**
- Hashes to _0_
	- $0+1^2=1$
	- $0+2^2=4$
	- $0+3^2=9$
	- $0+4^2=16$: Out of range! Wrap around with `mod table_size`
		- $16\%11=5$: Occupied
	- $0+5^2=25$: Out of range! Wrap around
		- $25\%11=3$: Unoccupied!

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10  | 20  |     | 60  | 30  | 50  |     |     |     | 40  |     |

## Exercise 3
Hvordan skal man håndtere sletninger, hvis der anvendes probing/open addressing?
- Til lookup ved disse metoder, bruger man en form for search and probe metode, hvor man egentlig kører samme iteration som oppe ovenover (eller hvilken anden metode man nu implementerer) og stopper når man støder på et _empty slot_, da det må betyde at det man leder efter ikke er der.
	- Det betyder at hvis man via quadratic probing har placeret noget på $\text{hash}+3^2$ og $\text{hash}+4^2$ og derefter sletter det på $\text{hash}+3^2$, vil man aldrig mere kunne tilgå det på $\text{hash}+4^2$, da søge-funktionen stopper inden da.

# Exercises from exam
## Exercise 1
![[Pasted image 20260921152200.png|652]]

Vi starter med at tjekke at de nuværende elementer er indsat rigtigt
- $22\%11=0$. Correct
- $5\%11=5$. Correct
- $16\%11=5$
	- $5+1^2=6$ Correct
- $27\%11=5$
	- $5+1^2=6$
	- $5+2²=5+9=15$ Out of range! Wrap around with `mod`
		- $15\%11=4$ _Incorrect!_ 27 should be placed at index **4**


| 0   | 1   | 2   | 3   | 4      | 5   | 6   | 7   | 8   | 9   | 10  |
| --- | --- | --- | --- | ------ | --- | --- | --- | --- | --- | --- |
| 22  |     |     |     | **27** | 5   | 16  |     |     |     |     |

Indsæt dernæst **1**, **12**, **23**, min alder (**22**), mit eksamens nummer (**566211937**)
- $1\%11=1$ _Unoccupied_
- $12\%11=1$
	- $1+1^2=2$ _Unoccupied_
- $23\%11=1$
	- $1+1^2=2$
	- $1+2^2=5$
	- $1+3^2=10$ _Unoccupied_
- Min alder **22** er allerede indsat. Vi indsætter en arbitrær alder, **24** i stedet: $24\%11=2$
	- $2+1^2=3$ _Unoccupied_
- $566211937\%11=5$
	- $5+1^2=6$
	- $5+2^2=9$ _Unoccupied_

| 0   | 1   | 2   | 3   | 4      | 5   | 6   | 7   | 8   | 9         | 10  |
| --- | --- | --- | --- | ------ | --- | --- | --- | --- | --------- | --- |
| 22  | 1   | 12  | 24  | **27** | 5   | 16  |     |     | 566211937 | 23  |

## Exercise 2
![[Pasted image 20260921153304.png]]

Jeg valgte at gøre dette udelukkende i python, fordi fuck da at gøre det i hånden. Resultat er her:
### Source code
```python
hash1 = [None] * 16 # Empty list with size 16
hash2 = [None] * 16 # Empty list with size 16

alphabet = ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"]

keys1 = ["D", "E", "M", "O", "C", "R", "A", "T"]
keys2 = ["R", "E", "P", "U", "B", "L", "I", "C", "A", "N"]

def hashFunc(alphIndex):
    val = (11*alphIndex) % 11
    return val

def linProb(index, iteration, arrSize):
    val = (index + iteration) % arrSize
    return val

def quadProb(index, iteration, arrSize):
    val = (index + iteration*iteration) % arrSize
    return val

def fillHash1():
    for letter in keys1:
        val = hashFunc(alphabet.index(letter) + 1)
        if hash1[val]:
            iteration = 1
            while hash1[val] is not None:
                val = linProb(val, iteration, len(hash1))
                iteration += 1
            hash1[val] = letter
            print("{} was indexed to {} after linear probing. Iteration: {}".format(letter, val, iteration))
        else:
            hash1[val] = letter
            print("{} was indexed to {} directly!".format(letter, val))
    print(hash1)

def fillHash2():
    for letter in keys2:
        val = hashFunc(alphabet.index(letter) + 1)
        if hash2[val]:
            iteration = 1
            while hash2[val] is not None:
                val = linProb(val, iteration, len(hash2))
                iteration += 1
            hash2[val] = letter
            print("{} was indexed to {} after linear probing. Iteration: {}".format(letter, val, iteration))
        else:
            hash2[val] = letter
            print("{} was indexed to {} directly!".format(letter, val))
    print(hash2)

def main():
    print("Filling hashtable 1\n")
    fillHash1()

    print("\n Filling hashtable 2\n")
    fillHash2()

if __name__ == "__main__":
    main()
```

### Output
```bash
Filling hashtable 1

D was indexed to 0 directly!
E was indexed to 1 after linear probing. Iteration: 2
M was indexed to 3 after linear probing. Iteration: 3
O was indexed to 6 after linear probing. Iteration: 4
C was indexed to 10 after linear probing. Iteration: 5
R was indexed to 15 after linear probing. Iteration: 6
A was indexed to 5 after linear probing. Iteration: 7
T was indexed to 12 after linear probing. Iteration: 8
['D', 'E', None, 'M', None, 'A', 'O', None, None, None, 'C', None, 'T', None, None, 'R']

 Filling hashtable 2

R was indexed to 0 directly!
E was indexed to 1 after linear probing. Iteration: 2
P was indexed to 3 after linear probing. Iteration: 3
U was indexed to 6 after linear probing. Iteration: 4
B was indexed to 10 after linear probing. Iteration: 5
L was indexed to 15 after linear probing. Iteration: 6
I was indexed to 5 after linear probing. Iteration: 7
C was indexed to 12 after linear probing. Iteration: 8
A was indexed to 4 after linear probing. Iteration: 9
N was indexed to 13 after linear probing. Iteration: 10
['R', 'E', None, 'P', 'A', 'I', 'U', None, None, None, 'B', None, 'C', 'N', None, 'L']
```

---
#lecture 
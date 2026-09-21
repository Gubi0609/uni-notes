
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
	- Det betyder at hvis man via quadratic probing har placeret noget på $\text{hash}+3^2$ og $\text{hash}+4^2$ og derefter sletter det på $\text{hash}+3^2$, vil man aldrig mere kunne tilgå det på $\text{hash}+4^2$


---
#lecture 
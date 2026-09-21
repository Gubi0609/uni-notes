
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


---
#lecture 
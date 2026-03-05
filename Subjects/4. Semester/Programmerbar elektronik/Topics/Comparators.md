Compares two or more inputs using one or multiple different comparisons.
![[Pasted image 20260305132255.png]]

When the given relationship(s) is true, an output signal is given (logic 0 or 1).
# Modelling
![[Pasted image 20260305132322.png]]

Comparators are only modeled using **if** with an **else** clause, and _no_ **else-if** clauses.

Only two data objects can be compared at once, so for example, **`if(a=b=c)`** can not be used.
	Can use multiple logical operators instead **`if((a=b) and (a=c))`**

# Complex comparator
- std_logic_vector type does not indicate a value of the bus. To compare two buses, unsigned or signed types are used as comparison must be preformed between signals or variables that have a defined values.
- Example:
	- a,b,c,d,e,f are unsigned
![[Pasted image 20260305132416.png]]
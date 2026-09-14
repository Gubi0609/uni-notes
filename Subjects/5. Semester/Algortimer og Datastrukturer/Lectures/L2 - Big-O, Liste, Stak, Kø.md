
---
**Date:** 2026-09-14

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[02 - Kapitel 1, 2 og 3.pdf]]

# Topics


# Notes

# Opgaver om Big O
## Opgave 1
Hvad er Store O tidskompleksiteten af nedenstående metode. Begrund dit svar.
```cs
public static int myMethod( int[] arr )
{
	int x = 0;
	for (int i = 0; i < arr.length; i++)
		for (int j = 0; j < arr.length/2; j++)
			for (int k = 0; k < arr.length; k++)
			{
				x++;
				if (k==1)
					break;
			}
	return x;
}
```

- Yderste for-loop er `O(n)`
- Nr. 2 for-loop er `O(n)`
- Inderste for-loop er `O(2)`, da den kun går fra `k=0` til `k=1` før den breaker.
- **Samlet set: `O(n)*O(n)*O(2) = O(n^2)`** da vi ikke må skrive konstanter såsom `O(2)`

## Opgave 2
Hvad er Store O tidskompleksiteten af nedenstående metode. Begrund dit svar.
```cs
public static int myMethod1( int[] arr )
{
	int x = 0;
	for (int i = 0; i < arr.length/2; i++)
		for (int j = 0; j < arr.length; j++)
			for (int k = 0; k < arr.length; k++)
			{
				x++;
				if (k==arr.length/2)
					break;
			}
	return x;
}
```

- Yderste for-loop er `O(n)`
- Nr. 2 for-loop er `O(n)`
- Inderste for-loop er `O(n/2)`, da den kun kører til `n/2`.
- **Samlet set: `O(n)*O(n)*O(n/2) = O(n^3)`** da vi ikke må skrive konstanter såsom `O(1/2)`

## Opgave 3
Hvad er Store O tidskompleksiteten af metoden `func1`. Begrund dit svar.
```cs
public static int func2(int N)
{
	int res = 0;
	for (int i = 0; i < N; i++)
		res = res + 1;
	return res;
}

public static int func1(int N)
{
	int x = 0;
	for (int i = 0; i < N; i++)
		x = x + func2(N);
	return x;
}
```

- `func2` er `O(n)`
- `func1` for-loop er i sig selv `O(n)`
- **For-loop i `func1` kalder `func2` en gang pr loop. Dette gør det til et nested for-loop, altså `O(n) * O(n) = O(n^2)`**  


---
#lecture 
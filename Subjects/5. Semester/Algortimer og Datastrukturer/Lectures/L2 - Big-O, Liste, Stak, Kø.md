
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




---
#lecture 
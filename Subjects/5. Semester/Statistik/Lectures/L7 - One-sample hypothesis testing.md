
---
**Date:** 2026-10-23

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 9.2.2, 9.2.3, 9.2.4, 9.2.6a, 9.2.7, 9.3.1, 9.3.7, 9.4.1, 9.4.3, 9.5.2

---

# Relevant documents
[[Agenda lecture 07.pdf]]
[[Lektion 7 slides.pdf]]
[[Solutions lecture 07 v3.pdf]]

# Topics


# Notes
![[Pasted image 20261023102927.png]]

Signifikans niveau: $\alpha$
$H_0:\quad \mu=5$
$H_1:\quad \mu<5$

Ud fra vores hypoteser, kan vi opstille områderne

$$C:\quad z_0 < z_\alpha \Rightarrow \text{forkast }H_0$$
$$A:\quad z_0= z_\alpha \Rightarrow \text{accepter }H_0$$
Hvor
$$z_\alpha\rightarrow \text{norminv}(\alpha)$$

Dette kan vi gøre da $\sigma^2$ er _kendt_, hvilket betyder at $Z_0$ følger normalfordelingen. Derfor kan vi løse problemet ved at bruge _standard normal fordelingen_. Ud fra hypotesen kan vi se at det er en _lower one-sided test_ altså kan vi opstille de områder vi har gjort ovenfor.

```
>> norminv(0.01)

ans =

   -2.3263

>> norminv(0.05)

ans =

   -1.6449

>> norminv(0.10)

ans =

   -1.2816
```


![[Pasted image 20261023102942.png]]

![[Pasted image 20261023102955.png]]

![[Pasted image 20261023103006.png]]

![[Pasted image 20261023103014.png]]

![[Pasted image 20261023103028.png]]

![[Pasted image 20261023103048.png]]
![[Pasted image 20261023103059.png]]

![[Pasted image 20261023103112.png]]

![[Pasted image 20261023103124.png]]
![[Pasted image 20261023103136.png]]

![[Pasted image 20261023103157.png]]

---
#lecture 
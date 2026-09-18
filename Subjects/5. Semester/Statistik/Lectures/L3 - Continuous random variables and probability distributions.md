
---
**Date:** 2026-09-18

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 4.1.2, 4.2.4, 4.3.1, 4.4.1, 4.5.1, 4.5.4, 4.5.13, 4.6.1, 4.7.13

---
# Relevant documents
[[Agenda lecture 03.pdf]]
[[Lektion 3 slides.pdf]]
[[Solutions lecture 03 v3.pdf]]

# Topics


# Notes

Ligesom [[Diskrete stokastiske variable & fordelinger]] har vi et sample space $S$ og et sæt af stokastiske variable $X$.
$$X: S\rightarrow I\subseteq \mathbb R$$

# Probability *Density* Function, PDF
På dansk kunne man kalde det en sandsynligheds-*tætheds* funktion

Skrevet $f_X(x)$ ligesom [[Diskrete stokastiske variable & fordelinger#Probability mass function, PMF|PMF]].
![[Pasted image 20260918082149.png|284]]

$$f_X(x):=\frac {P(X\in[x,x+dx])}{dx}$$
![[Pasted image 20260918082328.png|309]]
$$P(a\leq X\leq b)=\int_a^b f_X(x)dx$$

$f_X(x)$ er _likelihood_.

Der gælder
$$\int_{-\infty}^\infty f_X(x)dx=1\quad [P(s)=1]$$
$$f_X(x)\geq 0$$

Da vi bruger integraler her, gælder der også
$$P(X=x)=0$$
Da arealet for et specifikt x-punkt er 0.

# Cumulative Probability Density Function, CDF
På dansk: fordelingsfunktion

Skrevet $F_X(x)$.
$$F_X(x):=F(X\leq x)=\int_{-\infty}^xf_X(u)du$$
![[Pasted image 20260918083233.png|323]]

_Svagt monoton_, stiger langsomt. Starter i 0, og stiger til 1.

Vi kan finde $f_X(x)$ fra $F_X(x)$
$$f_X(x)=\frac {dF_X(x)}{dx}\geq 0$$

$$\lim_{x\rightarrow -\infty}F_X(x)=0$$
$$\lim_{x\rightarrow \infty}F_X(x)=1$$


---
#lecture 
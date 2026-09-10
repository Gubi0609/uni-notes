
---
**Date:** 2026-09-10

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[Passino - FLC.pdf]]
[[2026-09-10 - Fuzzy Logic Control 1.pdf]]
[[Fuzzy control 1 - Exercises.pdf]]

# Topics


# Notes

- Fuzzy logic control er brugbart i situationer hvor man ikke har et fuldt overblik over systemet==????==
	- E.g. et bremsesystem. Hvis du opdeler det i distancer for hvor meget du skal bremse (5-10 m, 10-15 m, ...). Så har du overgange hvor du skifter brat i mellem hvor meget du bremser (tænk Schmitt controller).
	- Hvis vi opsætter på en x-y-koordinatsystem, kan vi ud af x-aksen have distance og op af y-aksen have _"degree of membership"_ [[2026-09-10 - Fuzzy Logic Control 1.pdf#page=17|slides]]
- **Ligesom med bilen ovenover, er mange ting i virkeligheden ikke enten-eller, men _flydende_** [[2026-09-10 - Fuzzy Logic Control 1.pdf#page=22|slides]]
- I stedet for `if else`, beskriver vi logikken med _termer_ (**regel-base**)
	- **if** premise/antecedent **then** consequence/action
![[Pasted image 20260910130822.png]]

## Fuzzy set operations
- **Cardinality**
	- $|A| = \sum_X \mu_A(x)$ - Kan bruges til at finde samlet størrelse af vores _fuzzy subset_ [[2026-09-10 - Fuzzy Logic Control 1.pdf#page=38|slides]]
- **Union**
	- $\mu_{A\cup B} = \max(\mu_A, \mu_B)$
- **Intersection**
	- $\mu_{A\cap B} = \min(\mu_A, \mu_B)$
- **Complement**
	- $\mu_{\bar A} = 1-\mu_A$

# Exercises
## Artificial intelligence introduction
- **What is a rational agent?**
	- An agent that _thinks_ and _behaves_ rationally. Uses axioms like Platon (Socrates is a man; Men are mortal; Therefore Socrates is mortal)
- **In the context of AI agents, how can an environment be characterized?**
	- _Accessible/inaccessible_
		- Describes whether the agent has access to the _complete state_ of the enviroment
	- _Deterministic/non deterministic (stochastic)_
		- Describes whether the same action will always produce the same output
	- _Episodic/sequential (non episodic)_
		- Describes whether the agents performance is a result of a series of independent, one-shot actions (episodic) or whether an action has consequences for future (sequential)
			- **Basically: Are actions and their consequences isolated or not?**
	- _Static/dynamic_
		- Does the environment change independent of the agent's actions?
	- _Discrete/continuous_
		- Is the state space of the enviroment discrete (e.g. all **natural numbes** $\mathbb{N}$) or continuous (like all **real numbers** $\mathbb R$)
- **What is a reactive agent and how does it differ from a deliberative agent?**
	- A reactive agent has _no memory_ while a deliberate agent does.


---
#lecture 
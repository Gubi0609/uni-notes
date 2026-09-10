
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
		- I _assume_ that the memory can be used to learn from the consequences of the agents output/action
- **Which are some of the main topics in AI research?**
	- Search - Like binary tree in chess computing
	- Knowledge representation - _How is knowledge represented?_ (Like do I represent the chessboard as a matrix or using bitboards)
		- **Declarative knowledge** - Deals with factoid questions (like "what is the capital of Denmark?")
		- **Procedural knowledge** - Deals with _how_ (like "how do you ride a bike?")
	- Planning - _Given a set of goals, construct a sequence of actions that achieves those goals_ (Like in chess computing. We want to win, so we _search_ to find a sequence of moves, that achieves that goal)
	- Learning - _How do we learn from existing data; How do we generate new facts from old; How do we generate new concepts; How do we learn to distinguish different situations in new environments?_
		- **Supervised**
		- **Unsupervised**
		- **Reinforcement**
	- Natural language processing
	- Expert systems
	- Robotics
- **What is the difference between supervised, unsupervised, and reinforcement learning?**
	- _Supervised learning:_ Given a set of inputs, the output is compared against an expected, known output (E.g. cats/dogs. We know beforehand whether the image shows a cat or dog, and we compare the computers output against this)
	- _Unsupervised learning:_ Learning patterns in the input when no specific output values are supplied.
	- _Reinforcement learning:_ The learner (agent) is rewarded or punished depending on the correctness of the output/action

## Fuzzy control
- **What is fuzzy control – namely, how does it differ from conventional control, and based on what is a fuzzy control system designed?**
	- Fuzzy control is based on the premise, that we do not have crisp (**true or false**) values, but rather fluid values between 0 and 1, that describe the _degree of membership_ of a specific set. Thus our action/output can also be more fluid instead of **true/false**.
- **What is a fuzzy set and what is a membership function?**
	- A fuzzy set is a set of values assigned to a specific set, and a membership function is a specific value within that set, that lies between 0 and 1 (continuously) - $\mu_A(x)¸\rightarrow [0, 1]$. Can also be drawn [[2026-09-10 - Fuzzy Logic Control 1.pdf#page=24|slides]]
- **Draw a membership function (and hence define a fuzzy set) that quantifies the set of all people of medium height.**
	- 
- **Draw a membership function that quantifies the set of all small properties.**
- **Draw a membership function that quantifies the set of all big properties.**
- **Draw a membership function that quantifies the statement “the number x is near 10."**
- **Draw a membership function that quantifies the statement “the number x is less than 10.”**
- **Draw a membership function that quantifies the statement “the number x is greater than 10.”**
- **Suppose that X = {a, b, c, d, e} and that $\mu_A(a)=0.5, \mu_A(b)=0, \mu_A(c)=0.2, \mu_A(d)=0, \mu_A(e)=1$**
	- **Compute the cardinality of A**
	- **Compute the complement of A, namely $\bar A$**
	- **Compute $A\cup \bar A$**
	- **Compute $A\cap \bar A$**
- **What is a linguistic variable?**
- **What is a linguistic value?**
- **What is a rule and a rule-base?**
- **Specify linguistic variables, linguistic values, and a fuzzy rule-base for the “Level Controller” (LC) in the system shown below. Your input is the water level provided by the “Level Transmitter” (LT). The goal is to maintain the water level in the tank at around 75% of total capacity and you can regulate the influx of water by opening and closing the “Level Control Valve**
![[Pasted image 20260910143834.png|489]]


---
#lecture 
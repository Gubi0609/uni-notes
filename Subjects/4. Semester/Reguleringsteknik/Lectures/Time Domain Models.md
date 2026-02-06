There are two types of linear time-domain models

# Continuous time state space
This is based on _differential equations_
![[Pasted image 20260206085202.png]]

Is a system of first order differential equations and an output equation.
![[Pasted image 20260206085304.png]]

## Transformation to State Space Form
When we have an $n^{th}$ order differential equation, we will need to reformulate it to a system of first order differential equations [[Time Domain Models#Continuous time state space|Continuous time state]].
![[Pasted image 20260206085613.png]]
![[Pasted image 20260206085805.png]]

So basically:
- Isolate the variables in the $\dot x$ matrix/vector one by one in the nth order differential equation and insert the constants associated with each variable in the corresponding field in the matrix (either A or B)
	- It's really quite easy. The _row_ of a matrix defines the $\dot x$ variable we want to find and the _column_ of the matrix defines what variable in either the $x$ or $u(t)$ vector will be multiplied with the matrices' constant.

> [!example]- Mass-Spring-Damper system
> ![[Pasted image 20260206090456.png]]

> [!help]- Matlab Simulation
> ![[Pasted image 20260206093154.png]]
> ![[Pasted image 20260206093211.png]]

# Discrete time state space
This is based on _difference equations_
![[Pasted image 20260206085226.png]]


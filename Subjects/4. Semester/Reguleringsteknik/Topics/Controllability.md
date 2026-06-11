## Continuous time system
A continuous time system
## $$\dot x(t)=Ax(t)+Bu(t),\quad x(0)=0$$
is said to be _controllable_ **iff** for any state $\xi \in \mathbb{R}^n$ there exists $u(t)$ such that for some $T>0$, $x(T)=\xi$.
So that is to say, that there exists an input $u$ for any state $\xi$ such that for the time $T$, the state vector is equal to the state $\xi$.

## Discrete time system
A discrete time system
## $$x_{k+1}=\Phi x_k+\Gamma u_k, \quad x_0=0$$
where $\Phi$ and $\Gamma$ are the equivalent matrices of $A$ and $B$.
is said to be controllable **iff** for any $\xi\in\mathbb{R}^n$ there exists a sequence $(u_0,u_1,...)$ such that for some $N>0$, $x_N=\xi$.
So exactly the same as continuous time systems, but instead of having a time dependent system, we have a sequence of data points.

# Condition for Controllability
We consider the discrete time system
## $$x_{k+1}=\Phi x_k+\Gamma u_k, \quad x_0=0$$
and iterate, starting at $x_1$ and observing the development as we iterate
## $$x_1=\Phi x_0+\Gamma u_0=0+\Gamma u_0=\Gamma u_0$$ $$x_2=\Phi x_1+\Gamma u_1=\Phi \Gamma u_0+\Gamma u_1$$ $$x_3=\Phi x_2+\Gamma u_2=\Phi^2\Gamma u_0+\Phi\Gamma u_1 +\Gamma u_2$$ $$x_n=\Phi^{n-1}\Gamma u_0+...+\Phi\Gamma u_{n-2}+\Gamma u_{n-1}$$
We notice, that by continuously using the previous output, we can iterate to get the current output

Writing the above equation in matrix form, we obtain
## $$x_n=\left[\begin{array}[cccc] & \Gamma & \Phi\Gamma & ... & \Phi^{n-1}\Gamma\end{array}\right]\left[\begin{array}[c] & u_{n-1} \\ u_\end{array}\right]$$
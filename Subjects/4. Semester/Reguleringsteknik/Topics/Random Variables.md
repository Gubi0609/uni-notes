We have a noisy sample, that we want to measure on. For this, we need to differentiate the measurement from the noise.

![[Pasted image 20260508082604.png]]

Noise often has a high frequency. Thus we can apply a low-pass filter, to filter out the high frequency noise.
This however introduces a phase. This in practice delays our signal, which is not optimal for time-dependent systems.

The solution is a ***Kalman filter*** that relies on a stochastic model, and noisy measurements.

# Discrete Random Variables
To introduce uncertainty and noise in the considered system models, we introduce **random variables**

> [!help]
> Let $X$ be a random variable describing the outcome of rollign a fair dice. The fair dice is characterized by
> - It has 6 different outcomes $[1 ; 6]$
> - The probability of getting each of the six outcomes is the same. i.e., $Pr(X=4)=1/6$
> - The outcome of each roll of the dice is independent.
> 
> To descirbe this mathematically, we use a **probability mass function** $p_X$. This is associated to $X$ that determines the probability that $X$ equals $x$
> $$p_X(x)=Pr(\{X=x\})$$
> ![[Pasted image 20260508083229.png]]

The **expected value*** of a random variable $X$ with $n$ outcomes can be determined from the probability mass function $p_X$ as
## $$E[X]=\sum_{i=1}^n x_iP_X(x_i)$$

The **variance** quantifies how much a random variable is varying around the mean value
## $$Var(X)=E[(X-\mu)^2]$$
where $\mu=E(X)$ (mean value)

# Continuous Random Variable
If we have a continuous variable that lies between $0$ and $1$, then the probability of getting any specific of the numbers in that range using the above method is $1/\infty=0$. Thus we adjust it for continuous signals.

We now have the **probability density function** $f_X$
## $$Pr(\{a\leq X\leq b\})=\int_a^bf_X(x)dx$$
This calculates the probability of the random value being in a particular range $[a;b]$.
The integral should always be equal to $1$. If it isn't, then it isn't a probability density function.

We now have the **expected value**
## $$E[X]=\int_{-\infty}^\infty xf_X(x)dx$$

And the **variance** as
## $$Var(X)=E[(X-\mu)^2]$$
where $\mu=E(X)$ (mean value)

# Normal distribution
![[Pasted image 20260508084145.png]]




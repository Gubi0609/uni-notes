We have a noisy sample, that we want to measure on. For this, we need to differentiate the measurement from the noise.

![[Pasted image 20260508082604.png]]

Noise often has a high frequency. Thus we can apply a low-pass filter, to filter out the high frequency noise.
This however introduces a phase. This in practice delays our signal, which is not optimal for time-dependent systems.

The solution is a ***Kalman filter*** that relies on a stochastic model, and noisy measurements.

## Random Variables
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

The **expected value*** of a random variable


We have a noisy sample, that we want to measure on. For this, we need to differentiate the measurement from the noise.
![[Pasted image 20260508082604.png]]

Noise often has a high frequency. Thus we can apply a low-pass filter, to filter out the high frequency noise.
This however introduces a phase. This in practice delays our signal, which is not optimal for time-dependent systems.

The solution is a ***Kalman filter*** that relies on a stochastic model, and noisy measurements.
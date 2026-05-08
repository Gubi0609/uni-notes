![[Pasted image 20260508090200.png]]

We want to find an **unbiased state estimate** $\hat x_k$ of $x_k$ ($E[x_k-\hat x_k]=0$) with **minimal variance** by exploiting
- A model of the system
- A noise model

The **Kalman Filter** is similar to the observer introduced in [[L10 - Observer Design]], but the observer did not take into account the process noise $w_k$ and the measurement noise $v_k$.

The Kalman Filter consists of two stages
![[Pasted image 20260508090623.png]]

# Principle of the Kalman Filter
![[Subjects/4. Semester/Reguleringsteknik/PDFs/Lecture 12 - The KalmanFilter.pdf#page=53]]

The last pages of the above pdf, describe the principles.


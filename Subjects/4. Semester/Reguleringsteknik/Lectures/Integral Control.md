Considering a state space system of the form
## $$\dot x=Ax+Bu$$ $$y=Cx$$
for which we wish to design a feedback law
## $$u(t)=Fx(t)+F_Ix_I(t)$$
The $I$ denotes an _integrator term_. Thus
## $$x_I(t)=\int_0^ty(\tau)-r(\tau)d\tau$$
Differentiating this yields
## $$\dot x_I(t)=y(t)-r(t)$$

We now have the equations
## $$\dot x=Ax+By$$ $$\dot x_I=y-r$$ $$y=Cx$$

Can then be combined into an extended state model
## $$\left[\\right]
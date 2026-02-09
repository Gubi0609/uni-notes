
Da vi ikke har uendelig forstærkning (som ved [[Den ideelle Op Amp]]) kommer der til at være en kurve i stedet for en step funktion
![[Pasted image 20260209082331.png]]

For den ideelle Op Amp havde vi at output spændingen er
## $$V_o=A_{OL}\cdot V_{id}$$
hvor $A_{OL}$ er _gain open loop_

For den ikke ideelle op amp må vi have

## $$V_{id}=V_{in}\cdot\alpha-V_{id}\cdot A_{OL}\cdot\beta$$

Vi har nogle lidt lange udtryk i det ovenstående. Vi kan formulere nogle nye formler fra disse
## $$V_s=\alpha\cdot V_{in}$$ $$V_f=V_o\cdot\beta$$

Og _closed loop gain_ bliver så (efter lidt forkortelse)

## $$A_{CL}=\frac {V_o}{V_{in}}=\frac \alpha\beta\cdot \frac {A_{Ol}}{\frac 1\beta+A_{OL}}$$
hvor **fejlen** er
## $$\text{Error}=1-\frac {A_{Ol}}{\frac 1\beta+A_{OL}}$$
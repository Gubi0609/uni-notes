A parallel register is simply a bank of [[D- Type Flip-Flop|D-type flip-flops]], its implementation has the same structure as for one flip-flop but with extended inputs and outputs.
![[Pasted image 20260226130506.png]]

# Modelling
![[Pasted image 20260226130515.png]]

It is basically the same as the [[D-Type Flip-Flop#Modeling|modelling]] for [[D- Type Flip-Flop]], but with input and output as _busses_.

## With enable
![[Pasted image 20260226130605.png]]

Notice the use of `others`. It is used if we have another value.


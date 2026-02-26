A parallel register is simply a bank of [[D- Type Flip-Flop|D-type flip-flops]], its implementation has the same structure as for one flip-flop but with extended inputs and outputs.
![[Pasted image 20260226130506.png]]

# Modelling
![[Pasted image 20260226130515.png]]

It is basically the same as the [[D-Type Flip-Flop#Modeling|modelling]] for [[D- Type Flip-Flop]], but with input and output as _busses_.

## With enable
![[Pasted image 20260226130605.png]]

Notice the use of `others`. It is used if we have another value.

# Shift registers
![[Pasted image 20260226131131.png]]

Has _1 input_

- Shift registers are registers with added features that enable them to shift their contents in either directions.
- A typical parallel shift register that has added controls to achieve these features; signals shift_left and shift_ right.
- These signals control whether the register is to shift its contents to left or right.
- Depending on the usage of the register, the empty place appears after shifting is filled whether with ‘0’, or ‘1’, or the shifted bit from the other side of the register (barrel shifters)
- Signals are simply a bank of D-type flip-flops, its implementation
- has the same structure as for one flip-flop but with extended
- inputs and outputs

## Modelling
![[Pasted image 20260226131241.png]]

See the use of `&`. By using this we combine several steps into one line.
- Mapping from `reg_temp` to signal needs to be done _outside_ the `process`.
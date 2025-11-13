
## Monolithic structure
![[Pasted image 20251107084924.png]]

The example shown here is UNIX.

If you want to develop further, this structure can be difficult to develop further.

## Monolithic plus modular structure
![[Pasted image 20251107084957.png]]

The example shown here is Linux.

Here we have the same structure as above, but the modules aren't as interconnected, making it easier to develop further.

## Layered structure
![[Pasted image 20251107085048.png]]

The example shown here is MULTICS

This approach creates _one_ layer for each module, making a layered structure kind of like Data-communication.
But if you need to communicate between layer 1 and 10, you need to travel through layer 2-9, instead of directly.

## Microkernel structure
![[Pasted image 20251107085342.png]]

The example shown here is MACH (MacOS is partially built on MACH)

This is still modular, but removes the need to travel through all other layers like in Layered structure.

## Star structure
![[Pasted image 20251107085454.png]]

The example shown here is Solaris.

- Each component is independent
- Each component communicates with others over known interfaces
- Each component can be started within the kernel as needed.
- This is similar to layered architecture, but is more flexible
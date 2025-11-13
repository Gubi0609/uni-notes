Links and Loaders are used when we compile eg a C or C++ program.

> [!info]- **Good video on compilers**
> ![](https://youtu.be/XJC5WB2Bwrc?)

![[Pasted image 20251107083958.png]]

If we have the parameter `-c` when compiling with gcc, we get the output after compilation. This is before _linking_ and _loading_.
If we use the `-o` parameter, we get the output executable file.

Once the code is compiled and linked together into a program, it is often the case that this program can only run on a specific OS. But …
- The source code and thus the program can be ported to another OS if there is a compiler for this platform.
- The program can run on multiple OS if there is a virtual machine for the OS.  A virtual machine is a layer that lies between the program and the OS. Here, the program's commands (API) are translated (interpreted) into target OS commands (system calls) through the virtual machine.
# Introduction to Return Oriented Programming

#### Data Execution Prevention (DEP)

Idea: Execute Code, not Data.

Data areas are marked non-executable. (Stack and Heap)

#### Extended Instruction Pointer (EIP)

Can only land in executable regions, not to heap or stack.

## How to Defeat DEP?

By borrowing bits and pieces of code that exist in executable regions of the process. Then creating a sequence of operation to be carried out as an attack.

This can be by using a library that the code holds or using functions not intended as they were.

So complex code can be transformed into a sequence of primitive operations (functions) present in the executable regions. These operations are called Gadgets.

This idea of sequencing code is call Return Oriented Programming (ROP).

## Ret2LibC

First idea of executing existing code was through the Ret2LibC technique.

By having the EIPointer return to "an existing function" after a stack overflow. So by manipulating the EIpointer, we could have it "return" to system("/bin/sh"). Thus giving the us control.

Normally, this process would be done through overwriting the return address with a attacker controlled value; through a stack overflow. Then when the function returns, the EIPointer can be set to an arbitrary address resulting in hijacking the program But, this way doesn't work as if the stack is non-executable.

So instead, by placing a fake frame into the stack memory, its possible to invoke arbitrary functions. It is also possible to retain EIPointer control after this function returns.

## Creating a Fake Frame

Creating a buffer overflow payload may look like...

    $ ./main AAAAAA...AAAAA <address of function> <return address> <parameter1>...

    $ ./main AAAAAA...AAAAA 080484bd 42424242 01010101...

With AAA...AAA being the distance to EIPointer.
Address of function, return address, and other parameters being in hex.

This sequence would overflow the buffer using AAA...AAA and have the next sequence be the function we would want.

## Chaining Functions

So then how would we chain the frames?

Use: the address of "POP/RET" ("pops" an elements and continues execution by "returning")

    $ ./main AAAAAA...AAAAA 080484bd <address of POP/RET> 01010101 080484bd 02020202


## Overall Ideas of ROP

- Series of returns to functions
- Chained frames
- Transform EIP based primitives into gadgets and can be "returned int"
- Run arbitrary code execution by using frames on the stack

# Introduction to Language Based Security

## What is Software Security?

Software security is the idea of engineering software so that it continues to function correctly under malicious attacks.

It is not firewalls, intrusion detection, or encryption. (It is not security software)

## Sources of Software Insecurity

- Complexity and change
- Incorrect or changing assumptions
- Poor implementation
- Inadequate software security techniques 
- Absent or minimum consideration of security during all lifecycle phases

## Pointer and Arrays

Fundamental operations with Pointers:
- Assignment
- Dereferencing

In C, assignment can look like:

    int x = 24;
    int *ptr;
    ptr = &x;

While dereferencing can look like:

    // Continuing off from the code above
    int j;
    j = *ptr;

### Problems with Pointers and Arrays

Pointer arithmetic can happen and lead to accessing other areas of memory. This can lead to unexpected results.

Dangling pointers, pointer which points to a heap-dynamic variable that has already been de-allocated, are also dangerous.

Memory leakage, allocated heap-dynamic variable that is not accessible anymore, can also happen with pointers.

For C, it also does not check array bounds, which means that it would write into the next piece of memory or segfault. In Java, this does not happen as it checks array bounds.

## Type Checking

Type checking ensures that operands of an operator are compatible types. Compatible type is one that is either legal for the operator or is allowed under language rules to be implicitly converted, by compiler generated code, to a legal type. (Coercion)

### Classification of Type Systems

- Static, done at compile time
- Dynamic, done at run time

### Type Binding

Takes place...
- Static, by either explicit or implicit declaration
- Dynamic, when specified by an assignment statement when executed

Explicit declaration
- Program statement used to declaring types of variables

    int count;
    int x,y,z;

Implicit Declaration
- Default mechanism for specifying types of variables

    var count = 0;
    var x, y, z = 0.0;

### Types of Type Checking
- Weakly typed has looser typing rules, but may produce unpredictable results at run time
- Strongly typed has stricter rules and type errors are always detected

## Type Safety
- A language is type safe if the only operations that are performed on the data are those by the type of data.
- Done at compile or run time
- So weakly typed languages, would be unsafe

## Call Stacks and Program Function Calls

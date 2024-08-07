# Prevention of Buffer Overflow Attacks

1. Array Bounds Checking
2. Non-executable stack/heap
3. Safe C library
4. Compiler solutions (StackGuard, RAD)
5. Type safe languages
6. Static source code analysis
7. Anomaly Detection (through system calls)
8. Randomization of executable Code
9. Memory Address Obfuscation (ASLR)

## Non-Executable Memory

The program counter should point to code segment; not to heap, stack, or data segments. This makes these segments non-executable, making it impossible for attackers to execute their own malicious code on the stack or heap buffer.

Does not block from buffer overflows, but prevents shellcode from being executed.

## Safe C Library

Some string related C library such as strcpy or strcat do not check buffer boundaries of destination buffers. Replacing these function with strncpy or strncat can help.

## Compiler Solutions

### StackGuard

The idea is to put a canary word before each return address in each stack frame. So, that before the function returns it checks to see if the canary has been overwritten by a buffer overflow. Although, it only works if the canary is not known by the attacker. One way to work around this is to choose a random string at the program startup, so that the string would be different every run of the program. Although, this idea is not compatible with some programs.

### Return Address Defender (RAD)

The idea is when a function is called, a copy of the return address is saved in RAD. This area is very hard to corrupt. So once the function finshes, the callee checks with the return address is the same as its caller through RAD.

## Type Safe Language

These languages will perform array bound checking but majority of programs are not written in these languages.

## Static Source Code Analysis

Analyze source code to find potential program statements that could result in buffer overflow vulnerabilities. Problems with this may be false positives or false negatives.

## Anomaly Detection

Based on the idea that most malicious code that is run on a target system will make system calls to access certain system resources. Problems with this may be false positives and false negatives.

## Randomization of Executable Code

This method involves the randomization of code that will be executed. Encrypts instructions and decrypts when they are executed. Because attackers do not know the key to encrypt their code, injected code cannot be decrypted correctly. The problem with this assumes that most attacks are by code injection attacks and performance of the program.

## Memory Address Obfuscation or Address Space Layout Randomization (ASLR)

Randomizes the layout of the process components in main memory. So attacks can only guess where the addresses are making it much harder to create a working injection. Problems with this is complexity of debugging a program like this and change in run-time memory layout.

### Various Techniques of Address Obfuscation

The first technique is randomization of base addresses. Randomization of bases addresses of the stack, heap, and starting address of dynamically linked libraries.

The second technique includes permuting the order of variables and functions.

The third technique is adding in padding or random lengths of gap in between stack frames, malloc allocation or code segments.


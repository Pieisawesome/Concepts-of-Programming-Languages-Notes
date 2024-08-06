# Language Based Security in Java

## Some Components of Java
- Compiled and interpreted
- Has dynamic linking
- Strongly typed
- No pointers
- Garbage collection
- No operator overloading

### Java Virtual Machine (JVM)
Class Loader
- Locates and loads classes into JVM

Native Method Loader
- Needed to access some underlying operating system functions

Heap
- Memory used to store objects during execution

Execution Engine
- Virtual processor that executes bytecode
- Has virtual registers, stack, etc.
- Performs memory and thread management, calls native methods

Security Manager
- Enforces access control at run-time

Just in Time Compiler (JIT)
- Translate bytecode into native code

## Need for Security in Java
While code mobility can be useful, downloaded executable content can be dangerous.

- Could modify, destroy, or read data in your file system
- Install other programs on your system

### Sandbox Model
The Java security model is based on a customizable "sandbox". Allows Java programs to run safely without potential risk to the filesystem.

Trusted Code
- Applets that orginate from a trusted source that could be trusted
- Signed Applets, contains a signature that the browser can verify by a authority server

### Fine Grained Access Control
- A protection domain, established by the classloader, gives permissions to code sources specified by the policy file
- Policy file, configuration file used by Java Runtime Environment (JRE), used to determine granted permissions
- Idea is that all code has access to the system resources on what is defined in the policy file

### Pillars of Java Security
- Security Manager
    - Ensures that the permission in the policy file are not overridden
- Class Loaders
    - Separate name spaces
        - Classes in one name space cannot access a class in another name space
    - Establish the protection domain
- Bytecode Verifer
    - Checks loads classes to ensure:
        - Variables are initialized before use
        - Rules for private data and method are not violated
        - Runtime stack does not overflow
        - No illegal data conversions

## Java Security APIs
- In later JDK version, separate packages are included to help maintain security
    - JCE (Cryptography)
    - JSSE (Secure Sockets)
    - JAAS (Authentication and Authorization Services)
    - etc.
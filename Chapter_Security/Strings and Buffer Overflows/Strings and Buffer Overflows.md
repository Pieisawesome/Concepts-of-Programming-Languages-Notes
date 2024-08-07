# Strings and Buffer Overflows

In C and C++, there are many problems with input strings and array bounds at runtime. There have been solutions to check array bounds during runtime, yet C or C++ have not adopted this solution. So buffer overflows can happen often in these languages.

## String Manipulation Functions

Using "char buf[20];"...

gets(buf)
- Reads user input until first EoL or EoF character
- Use fgets(buf, size, stdin) instead
    - Reads data until newline or exceeds specified buffer length

Using "char dest[20];" and "string src;"...

strcpy(dest, src)
- Copies src to dest
- Problem: assumes dest is long enough to hold everything in src, assumes src is null terminated
- Use strncpy(dest, src, size)
    - "strncpy(dest, src, sizeof(dest) - 1); 
    - dest[sizeof(dest) - 1] = '\0';"
    - Makes sure that dest is null-terminated

Using "char *buf; int i, len;" and fd is file descriptor

read(fd, &len, sizeof(len))
buf = malloc(len);
read(fd, buf, len);
- Reads sizeof(int) bytes and stores them in len 
- Problem: len may become negative (integer overflow) which affects rest of the program

### Format String Vulnerability
A string can be passed as an argument to printf (or other related functions) and result in writes to arbitrary memory addresses.

    #include <stdio.h>
    int main(int argc, char* argv[])
    { if (argc > 1)
    printf(argv[1]);
    return 0;
    }

This code can be abused using format string attacks. It could result in a buffer overflow attack.

To prevent this, we can specify a format string as part of the program, not as an input. So replace printf(buf) with printf("%s", buf).



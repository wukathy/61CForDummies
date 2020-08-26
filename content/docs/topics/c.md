# C

```sizeof()```: tells you the size in **bytes** of the variable type that you pass in
- Characters are _always_ one byte in every system, **everthing else can vary**
	- short <= int <= long <= long long
- Pointers are always the same size, depends on architecture

Pointer arithmetic: increment in sizeof(type_pointing_to), not bytes!

Example: assume sizeof(int) == 4
```
int x = 5;
int *y = &x;		// y = 0x4000
y = y + 2;		// y = 0x4008
char* z = "bears!";    // z = 0x2000
z = z + 2;		// z = 0x2002
```
## Memory

![Memory](/images/memory.png)

- Stack: function local variables, strings allocated as **arrays**, pointers
	- String literals put in read-only memory is feature of compiler not language
- Heap: dynamically allocated memory (with malloc etc)
- Static: global variables, statically allocated strings
- Code: machine instructions

## Bitwise & Logical Operations
- Bitwise XOR: useful to find differences
- Bitwise AND: useful to find shared bits
- Bitwise OR: useful to find either-or relationships
- Bitwise NOT: ~
- Logical NOT: !
- Logical OR: ||
- Logical AND: &&


# How to write x86_64 Assembly Language in your Mac?
## For any people who need to write Assembly Language in your Mac, please refer to this post!
Assembly Language in Mac is formmated differently from Windows. In my case, I had an assignment to write a simple gcd assembly code in the language. 
However, the examples that professor showed were all written in Windows; so copying directly from his codes didn't help at all. 
Follwing hacks are somethings I found with 5 days of Googling. I hope this post can help you!

### Before we start, most of the codes are similar to Windows. For example, `push %rbp` means push base pointer to stack in Windows. In Mac, it is`pushq %rbp`. 
### So, basic syntax is very similar! But, we just need to add a little bit. 

1. write a short c program(ex. hello.c) and convert to asm file using `gcc -S -c -O0 -fverbose-asm filename.c` command. This command will generate Assembly file(ex. hello.asm) for this C file. 
```
#include <stdio.h>

int main()
{
	printf("hello, %d, %d\n", 123, 456);
}
```

2. In your converted .asm file, you will see some complex codes on the top and bottom of the assembly file. For mine, it was 
```
	.section   __TEXT,__text,regular,pure_instructions
    .build_version macos, 10, 15    sdk_version 10, 15
    .globl    _gcd
    .p2align    4, 0x90
_gcd:
	pushq %rbp
  .
  .
  .
  (same assembly codes with Windows following)

	.section __TEXT,__cstring,cstring_literals
.fmt:
    .asciz "calling gcd(%d, %d)\n"
```
Copy codes like this into the assembly file you need to create. 

3. To call or state any function, underscore(_) is necessary. call `_gcd` or `call _printf` for example.

4. For strings in `.rodata section`(Windows), initialize them in `.asciz “hello”`, not `.string “hello”`.

5. Include `operation suffixes (b, s, w, l, q, etc)` in every operation. push -> pushq or pushl for example. 

6. gcc command of `-no-pie` may not work in your terminal. Don’t care about it!

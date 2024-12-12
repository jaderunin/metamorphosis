# Description: 
For what argument does this program print `win` with variables 79, 7 and 3? 

File: `chall_1.S` 

Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

The file provided is:
```
		.arch armv8-a
	.file	"chall.c"
	.text
	.align	2
	.global	func1
	.type	func1, %function
func1:
	sub	sp, sp, #16
	str	w0, [sp, 12]
	str	w1, [sp, 8]
	ldr	w1, [sp, 12]
	ldr	w0, [sp, 8]
	cmp	w1, w0
	bls	.L2
	ldr	w0, [sp, 12]
	b	.L3
.L2:
	ldr	w0, [sp, 8]
.L3:
	add	sp, sp, 16
	ret
	.size	func1, .-func1
	.section	.rodata
	.align	3
.LC0:
	.string	"Result: %ld\n"
	.text
	.align	2
	.global	main
	.type	main, %function
main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	x19, [sp, 16]
	str	w0, [x29, 44]
	str	x1, [x29, 32]
	ldr	x0, [x29, 32]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi
	mov	w19, w0
	ldr	x0, [x29, 32]
	add	x0, x0, 16
	ldr	x0, [x0]
	bl	atoi
	mov	w1, w0
	mov	w0, w19
	bl	func1
	mov	w1, w0
	adrp	x0, .LC0
	add	x0, x0, :lo12:.LC0
	bl	printf
	mov	w0, 0
	ldr	x19, [sp, 16]
	ldp	x29, x30, [sp], 48
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits

```
# Solution:
ran a program to convert the assembly code to C
```
#include <stdio.h>
#include <stdlib.h>

int func(int a) {
    int b = 79;
    int c = 7;
    int d = 3;
    int result;

    result = b << c; // Equivalent to lsl
    result = result / d; // Equivalent to sdiv
    result = result - a; // Equivalent to sub

    return result;
}

int main(int argc, char *argv[]) {
    int a;

    if (argc > 1) {
        a = atoi(argv[1]);
    } else {
        a = 0; // Default value if no argument is provided
    }

    int result = func(a);
    
    if (result == 0) {
        puts("You win!");
    } else {
        puts("You Lose :(");
    }

    return 0;
}
```
The program only outputs 'You win' when the value of func is 0. 
on running the program, Condition for "win": is when 3370-a=0 so a=3370.
3370 in hexadecimal = 0x00000D2A
# flag:
picoCTF{00000d2a}



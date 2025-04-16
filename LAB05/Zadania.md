1. Napisz program który obliczy wzór: a+b+c
```Assembly
org 100h

mov AX, [a]
add AX, [b]
add AX, [c]

mov [y], AX

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```

2. Napisz program obliczający wzór: 𝑎∗𝑏+𝑐
```Assembly
org 100h

mov AX, [a]
mov BX, [b]
mul BX
add AX, [c]

mov [y], AX

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```

3. Napisz program obliczający wzór: 2𝑎+2𝑏−2𝑐
```Assembly
org 100h

mov AX, [a]
mov BX, 2
mul BX

mov CX, 00h
mov CX, AX

mov AX, [b]
mul BX

add CX, AX

mov AX, [c]
mul BX

sub CX, AX

mov [y], CX

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```

4. Napisz program obliczający wzór: (a/b)+𝑐
```Assembly
org 100h

mov AX, [a]
add BX, [b]
div BX
mov BX, [c]
add AX, BX

mov [y], AX

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```

5. Napisz program obliczający wzór: a/(b+c)
```Assembly
org 100h

mov AX, [a]
add BX, [b]
mov CX, 00h
mov CX, [c]

add BX, CX
mov DX, 00h
div BX

mov [y], AX

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```

6. Napisz program obliczający wzór: a*(b/c)
```Assembly
org 100h

mov AX, [b]
mov BX, [c]

mov DX, 00h
div BX

mov BX, AX
mov AX, [a]

mul BX

mov [y], AX

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```

7. Napisz program obliczający wzór: a^2+2b+c
```Assembly
org 100h

mov AX, [a]
mul AX

mov BX, AX

mov AX, [b]
mov CX, 00h
mov CX, 2

mul CX

add AX, BX
add AX, [c]

mov [y], AX

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```

8. Napisz program obliczający wzór: 2a*(b/2c)
```Assembly
org 100h

mov AX, [c]
mov CX, 00h
mov CX, 2

mul CX

mov BX, AX
mov AX, [b]
mov DX, 00h

div BX
mov BX, AX

mov AX, [a]
mul CX

mul BX

mov [y], AX

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```

9. Napisz program obliczający wzór: a*(b+a/c)
```Assembly
org 100h

mov AX, [b]
add AX, [a]
mov BX, [c]
mov DX, 00h

div BX

mov BX, [a]
mul BX

mov [y], AX

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```

10. Napisz program obliczający wzór: a/2+b/3+c/4
```Assembly
org 100h

mov AX, [a]
mov BL, 2

div BL
mov CX, 00h
mov CX, AX ; CX = a/2

mov AX, [b]
mov BL, 3

div BL
mov DX, AX ; DX = b/3

mov AX, [c]
mov BL, 4

div BL ; AX = c/4

add AX, CX
add AX, DX

mov [y], AX

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```
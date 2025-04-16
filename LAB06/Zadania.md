1. Napisz program obliczający wzór (skorzystaj z notacji postfiksowej): `a * b + c`

Postfix: a b * c +

```Assembly
org 100h

push word [a]
push word [b]

pop AX
pop DX
mul DL
push AX

push word [c]

pop AX
pop DX
add AX, DX
push AX

push word [y]

mov AH, 00h
int 21h

a dw 2
b dw 6
c dw 4
y dw 0
```

2. Napisz program obliczający wzór (skorzystaj z notacji postfiksowej): `2𝑎 + 2𝑏 − 2𝑐`

Postfix: 2 a * 2 b * + 2 c * -

```Assembly
org 100h

mov BX, 2

push BX
push word [a]

pop AX 
pop DX
mul DL
push AX

push BX
push word [b]

pop AX 
pop DX
mul DL
push AX

pop AX 
pop DX
add AX, DX
push AX

push BX
push word [c]

pop AX 
pop DX
mul DL
push AX

pop AX
pop DX
sub AX, DX
push AX

push word [y]

mov AH, 00h
int 21h

a dw 2
b dw 6
c dw 4
y dw 0
```

3. Napisz program obliczający wzór (skorzystaj z notacji postfiksowej): `a / b + c`

Postfix: a b / c +

```Assembly
org 100h

push word [a]
push word [b]

pop AX 
pop CX
mov DX, 00h
div CX
push AX

push word [c]

pop AX 
pop DX
add AX, DX
push AX

push word [y]

mov AH, 00h
int 21h

a dw 2
b dw 6
c dw 4
y dw 0
```

4. Napisz program obliczający wzór (skorzystaj z notacji postfiksowej): `a / (b + c)`

Postfix:  a b c + /

```Assembly
org 100h 

push word [a]
push word [b]
push word [c]

pop AX 
pop DX
add AX, DX
push AX

pop AX 
pop CX
mov DX, 00h
div CX
push AX

push word [y]

mov AH, 00h
int 21h

a dw 2
b dw 6
c dw 4
y dw 0
```

5. Napisz program obliczający wzór (skorzystaj z notacji postfiksowej): `a * b / c`

Postfix: a b * c /

```Assembly
org 100h 

push word [a]
push word [b]

pop AX 
pop DX
mul DL
push AX

push word [c]

pop AX 
pop CX
mov DX, 00h
div CX
push AX

push word [y]

mov AH, 00h
int 21h

a dw 2
b dw 6
c dw 4
y dw 0
```

6. Napisz program obliczający wzór (skorzystaj z notacji postfiksowej): `a^2 + 2b + c`

Postfix:  a a * 2 b * + c +

```Assembly
org 100h 

mov BX, 2

push word [a]
push word [a]

pop AX 
pop DX
mul DL
push AX

push BX
push word [b]

pop AX 
pop DX
mul DL
push AX

pop AX 
pop DX
add AX, DX
push AX

push word [c]

pop AX 
pop DX
add AX, DX
push AX

push word [y]

mov AH, 00h
int 21h

a dw 2
b dw 6
c dw 4
y dw 0
```

7. Napisz program obliczający wzór (skorzystaj z notacji postfiksowej): `2a * b + 2c`

Postfix: 2 a * b * 2 c * +

```Assembly
org 100h 

mov BX, 2

push BX
push word [a]

pop AX 
pop DX
mul DL
push AX

push word [b]

pop AX 
pop DX
mul DL
push AX

push BX
push word [c]

pop AX 
pop DX
mul DL
push AX

pop AX 
pop DX
add AX, DX
push AX

push word [y]

mov AH, 00h
int 21h

a dw 2
b dw 6
c dw 4
y dw 0
```
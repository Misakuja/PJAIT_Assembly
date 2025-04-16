Credit: [mhyla.com](https://mhyla.com/wia2-4/)

jmp - skok do jakiegoś miejsca w kodzie

```
org 100h

mov AL, 10
jmp koniec


etykieta:
mov AH, 00h
int 21h
```


`cmp` - compare two values, ex:
```
cmp AL, 5
```

jump if *greater than/less than...*
```
jg ; >
jl ; <
jge ; >=
jle ; <=
je ; ==
jne ; !=
```


* zawsze trzeba wyjsc z jmp; to nie funkcja:
```
org 100h

mov AH, 21h
mov AL, 11h
cmp AL, AH

JL mniejsze
JG koniec

mniejsze:
mov AH, 02h
mov DL, '<'
int 21h
jmp koniec

koniec:
mov AH, 00h
int 21h

```

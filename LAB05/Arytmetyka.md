[mhyla.com](https://mhyla.com/wia2-5/)

Setup:
```Assembly
org 100h
mov AH, 05h

; increment/decriment/add/sub/mul/div instructions

mov AH, 00h
int 21h

a dw 5h
b dw 4h
c dw 2h
y dw 0h
```


Dodawanie:
```Assembly
add AH, 05 ; cel : co dodać (AH + 05h)
```

Odejmowanie:
```Assembly
sub AH, 05h ; cel : co odjąć (AH - 05h)
```

Mnożenie:
```Assembly
mul DH ; one argument - 8bit or 16bit
```

For 8bit:
- Multiplies `AL` • provided argument = `AX`

For 16bit:
- Multiplies `AX` • provided argument = `DXAX`

Dzielenie:
```Assembly
DIV BL ; one argument
```

For 8 bit:
$$\frac{AX}{BL} = AL,\ \ reszta\ w\ AH$$


For 16 bit:
$$\frac{DXAX}{BX} = AX,\ \ reszta\ w\ DX$$


---


1. Napisz programik, który wydrukuje jedną pod drugą 12 literek H.
```Assembly
org 100h

mov CX, 12

print:
    mov AH, 02h
    mov DL, 'H'
    int 21h
    
    mov AH, 09h
    mov DX, newline
    int 21h
loop print
    
mov AH, 00h
int 21h

newline db 0Ah, 0Dh, '$'
```

2. Napisz program, który wczyta ciąg znaków za pomocą przerwania 21h i wypisze go na ekranie, także za pomocą przerwania 21h.
```Assembly
org 100h

mov BX, 80h
mov CX, 15

mov AH, 01h
getInput:
    int 21h
    cmp AL, 13 ; 13 - enter char
    je endInput
    
    mov [BX], AL
    inc BX
loop getInput

endInput:
mov byte [BX], '$'

mov AH, 09h
mov DX, 80h ;80h works, some random stack overflow guy said its a 'safe address', this doesnt work with BX set to 00h so ig he spoke facts
int 21h

mov AH, 00h
int 21h
```

3. Zmodyfikuj poprzedni program tak, aby wypisywał tekst od 10 znaku.
```Assembly
org 100h

mov BX, 80h
mov CX, 15

mov AH, 01h
getInput:
    int 21h
    cmp AL, 13
    je endInput
    
    mov [BX], AL
    inc BX
loop getInput

endInput:
mov byte [BX], '$'

    mov AH, 09h
    mov DX, newline
    int 21h

mov AH, 09h
mov DX, 80h ;same as task 2
add DX, 9
int 21h

mov AH, 00h
int 21h

newline db 0Ah, 0Dh, '$'
```

4. Korzystając z pamięci karty graficznej wyświetl w prawym dolnym rogu ostatnią cyfrę z twojego numeru indeksu. Jest 80 znaków w wierszu, oraz jest 25 wierszy.
```Assembly
org 100h

mov AH, 02h
mov DH, 24 ; row
mov DL, 79 ; column
int 10h

mov AH, 09h
mov AL, '4'
mov BL, 0x0F ; colour (white on black): 0 - black, 7 - white
int 10h

mov AH, 00h
int 21h
```


5. Korzystając z pamięci karty graficznej wyświetl
    - na samym środku ekranu czerwone serduszko na białym tle
    - u góry ekranu, na środku, czerwony trefl na czarnym tle
    - na dole ekranu, na środku, czarny pik na białym tle.
```Assembly
org 100h

mov AH, 02h
mov DH, 1 ; row
mov DL, 40 ; column
int 10h

mov AH, 09h
mov AL, 0x05 ; ascii club symbol (CP437 - extended ASCII)
mov BL, 0x04 ; colour (red on black)
mov CX, 1
int 10h

mov AH, 02h
mov DH, 12 ; row
mov DL, 40 ; column
int 10h

mov AH, 09h
mov AL, 0x03 ; ascii heart symbol (CP437 - extended ASCII)
mov BL, 0xF4 ; colour (red on white)
mov CX, 1
int 10h

mov AH, 02h
mov DH, 24 ; row
mov DL, 40 ; column
int 10h

mov AH, 09h
mov AL, 0x06 ; ascii spades symbol (CP437 - extended ASCII)
mov BL, 0x0F ; colour (black on white)
mov CX, 1
int 10h

mov AH, 00h
int 21h
```
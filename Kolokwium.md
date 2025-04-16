1. Napisz programik, którego zadaniem będzie szyfrowanie znaków. Program ma odczytać z konsoli znak, a następnie wydrukować go w formie zakodowanej. Odczytany znak ma zostać zmieniony o: +10(dec) pozycji dla zakresu 0x20 - 0x3F, +7(dec) pozycji dla zakresu 0x40-0x5F, -12(dec) pozycji dla zakresu 0x60-7E.

Dla przykładu: podanie znaku $ powinno skutkować wydrukowaniem kropki (.), podanie litery ‘K’ da nam ‘R’, a ‘p’ da nam d.

Nadprogramowymi punktami nagrodzę, jeśli program będzie w stanie przyjmować w ten sposób wiele znaków bez zamykania się. Na wszelki wypadek, jakby nie udało się zrobić jakiegoś zadania a to akurat tak.
```Assembly
org 100h

start:
    mov AH, 08h
    int 21h
    mov [input_char], AL

    mov AL, [input_char]
    cmp AL, 0x20         
    jb end               
    cmp AL, 0x3F
    jbe range_1          ; 0x20-0x3F
    cmp AL, 0x40
    jb end
    cmp AL, 0x5F
    jbe range_2          ; 0x40-0x5F
    cmp AL, 0x60
    jb end
    cmp AL, 0x7E
    jbe range_3          ; 0x60-0x7E
    jmp end

range_1:
    add AL, 10
    jmp save_result

range_2:
    add AL, 7
    jmp save_result

range_3:
    sub AL, 12
    jmp save_result

save_result:
    mov [output_char], AL
    mov AH, 02h
    mov DL, [output_char]
    int 21h
    jmp start

end:
    mov AH, 00h
    int 21h

input_char db 0
output_char db 0
```

2. Napisz program, który wczyta pojedynczy znak z klawiatury. Jeśli będzie to wielka litera, wtedy niech wypisze w lewym górnym rogu tekst “wielka litera”. Jeśli jest to mała litera, wtedy niech wypisze “mała litera” w jakimś określonym miejscu (ale możecie sobie wybrać gdzie).

Jeśli wprowadzone zostanie cokolwiek innego to program wydrukuje error i się zakończy
```Assembly
org 100h

mov AH, 01h
int 21h

mov AH, 41h ;dolna granica
cmp AL, AH

JL not_letter  ;mniejsze

mov AH, 7Ah ;gorna granica
cmp AL, AH

JG not_letter

mov AH, 5Bh
cmp AL, AH

JL uppercase

mov AH, 60h
cmp AL, AH

JG lowercase
jmp not_letter

lowercase:
mov AH, 02h
mov DH, 05h
mov DL, 05h
int 10h

mov AH, 09h
mov DX, lowercase_letter
int 21h
jmp end

uppercase:
mov AH, 02h ;lewy gorny rog
mov DH, 00h
mov DL, 00h
int 10h

mov AH, 09h
mov DX, upercase_letter
int 21h
jmp end

not_letter:
mov AH, 09h
mov DX, error_msg
int 21h
jmp end

end:
mov AH, 00h
int 21h

lowercase_letter db "mala litera", '$'
upercase_letter db "wielka litera", '$'
error_msg db "error", '$'
```

3. Napisz programik, który wczyta od użytkownika stringa, a w następnej linii wydrukuje połowę tego stringa. Np:
```
MICHAŁ HYLA JEST NAJPIEKNIEJSZY
MICHAŁ HYLA JE
```

```Assembly
org 100h

mov AH, 0Ah
mov DX, inputText
int 21h

mov AX, 00h
mov DX, 00h
mov BX, inputText + 2
mov AL, [inputText + 1] ; Get length of the entered string
mov CX, 2   
div CX 
add BX, AX

mov byte [BX], '$'

mov AH, 09h
mov DX, newline
int 21h

mov AH, 09h
mov DX, inputText + 2
int 21h

mov AH, 00h
int 21h

newline db 0Dh, 0Ah, '$'
inputText db 50
```

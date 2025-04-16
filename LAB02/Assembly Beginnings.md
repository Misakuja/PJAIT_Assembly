Credit: [mhyla.com](https://mhyla.com/wia2-2/)

DIR - Directory view
CD - Change directory
CLS - Clear screen

---


nasm - kompilator

type - show file content

```Assembler
nasm filename.ext -o example.com
```

to run:
```Assembler
example.com
```

---

Always at beginning:
```
org 100h
```

---

Instructions:
1. Transfer:
    1. MOV - instrukcja przyjmująca 2 argumenty. Pierwszy z nich będzie miejscem docelowym, drugi źródłowym
    2. PUSH - instrukcja zapisująca podany argument na stosie
    3. POP - instrukcja zdejmująca podany argument ze stosu
2. Arytmetyczne
    1. ADD
    2. SUB
    3. MUL
    4. DIV
3. Pozostałe:
    1. INT - wywołuje podane jako argument przerwanie

INT Types:
[10h](https://www.ctyme.com/intr/int-10.htm) - wyświetlanie pikseli, znaków, kursora etc.
[16h](https://www.ctyme.com/intr/int-16.htm) - odczyty klawiszy etc.
[21h](https://www.ctyme.com/intr/int-21.htm) - procedury systemowe; wyświetlanie/odczytywanie znaków i stringów, tworzenie katalogów etc.

Szesnastkowy system: 0x*Number* (ex. 0xFFFF) / *number*h (ex. 2137h)

---
\
`insight` - uruchomienie programu w debuggerze

---

##### *Przerwania*:
mov AH, 00h
int 21h
- nie zablokuje terminala
---

Drukowanie literki
mov AH, 02h
mod DL, 'a'
int 21h

---


;/ <- comment

;/-text

1. Za pomocą przerwania [int 21h/AH=0Ah](http://www.ctyme.com/intr/rb-2563.htm) wczytaj ciąg znaków, a następnie wydrukuj trzeci znak tego stringa. _To przerwanie w momencie wywołania odczytuje z pamięci 1 bajt z podanego adresu i pozwala na wprowadzenie tylu znaków, jaką wartość tam znajdzie. Po wprowadzeniu stringa na drugim bajcie znajdzie się długość wprowadzonego ciągu znaków, pierwsza litera tego ciągu będzie dopiero na bajcie trzecim_
```Assembly
org 100h

mov AH, 0Ah
mov DX, string
int 21h

mov AH, 09h
mov DX, newline
int 21h

mov AH, 02h
mov DL, [string+4]
int 21h

mov AH, 00h
int 21h

newline db 0Ah, 0Dh, '$'
string db 9
```

2. Wydrukuj stringa (może być zdefiniowany w kodzie), znak nowej linii (0A0Dh), oraz tego samego stringa, ale do trzeciego znaku. _Przerwanie [int 21h/AH=09h](http://www.ctyme.com/intr/rb-2562.htm) drukuje stringa zaczynając od umieszczonego w DX adresu aż do napotkania znaku ‘$’, czyli wystarczy po trzecim znaku umieścić w pamięci $ i załatwione._
```Assembly
org 100h

mov AH, 09h
mov DX, string
int 21h

mov AH, 09h
mov DX, newline
int 21h

mov AH, 09h
mov byte [string+3], '$'
mov DX, string
int 21h

mov AH, 00h
int 21h

newline db 0Ah, 0Dh, '$'
string db "pain$", 0  
```

3. Napisz program, który przyjmie stringa od użytkownika (int 21h/AH=0Ah), przesunie gdzieś kursor albo wydrukuje nową linię i wydrukuje tego stringa na terminalu. Program ma wykryć, jak długi był przyjęty od użytkownika string i postawić na jego końcu ‘$’
```Assembly
org 100h

mov AH, 0Ah
mov DX, string
int 21h

mov AH, 09h
mov DX, newline
int 21h

mov AH, 00h
mov AX, string+2
mov BL, [string+1]
add BX, AX
mov byte [BX], '$'

mov AH, 09h
mov DX, string+2
int 21h

mov AH, 00h 
int 21h

newline db 0Ah, 0Dh, '$'
string db 9
```


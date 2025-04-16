1. Napisz program, który wyświetli na terminalu literkę ‘A’ oraz ‘g’. - 21h/AH=02h
```Assembly
org 100h

mov AH, 02h
mov DL, 'A'
int 21h
mov DL, 'g'
int 21h

mov AH, 00h
int 21h
```

2. Napisz program, który wypisze na terminalu twoje imię i nazwisko - 21h/AH=09h
```Assembly
org 100h

mov AH, 09h
mov DX, tekst
int 21h

mov AH, 00h
int 21h

tekst db "Anna Turowska$"
```


3. Napisz program, który ustawi kursor w lewym górnym rogu ekranu i napisze tam literkę ‘A’ - 10h/AH=02h i 21h/AH=02h. W 10h ustawiamy pozycję w rejestrach DH i DL, nie ruszamy BH.
```Assembly
org 100h

mov AH, 02h
mov DH, 00h
mov DL, 00h
int 10h

mov AH, 02h
mov DL, 'A'
int 21h

mov AH, 00h
int 21h
```


4. Napisz program, który odczyta znak, a następnie go wydrukuje - int 21h/AH=01h - proponuję przed wydrukowaniem odczytanego znaku wydrukować jeszcze np. spację
```Assembly
org 100h

mov AH, 01h
int 21h

mov AH, 02h
int 21h

mov AH, 00h
int 21h
```

5. Napisz program, który wyświetli pośrodku ekranu literę “C”
```Assembly
org 100h

mov AH, 02h
mov DH, 12
mov DL, 40
int 10h

mov AH, 02h
mov DL, 'C'
int 21h

mov AH, 00h
int 21h
```
Credit: [mhyla.com](https://mhyla.com/wia2-3/)

INT 21h/AH=09h - Przerwanie do wydruku stringa.

- adresowanie bezpośrednie - przeniesie do wskazanego miejsca zawartość ze wskazanego adresu.
```
mov AL, [0x1000]
```
- adresowanie pośrednie - polega na podaniu adresu przechowywanego w rejestrze:
```
mov AL, [BX]
```
- adresowanie z przesunięciem - umożliwia odniesienie się do adresu przesuniętego względem rejestru:
```
mov AL, [BX+3]
```

każdy rejestr ma dwa registry. Na przykład rejestr AX składa się z dwóch registrów AH i AL.

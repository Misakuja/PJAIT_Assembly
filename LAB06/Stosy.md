Credit: [mhyla.com](https://mhyla.com/wia2-6/)

Prefix | Infix | Postfix
## Postfix - Odwrotna notacja polska

- znak po operandach

## Stos

<img width="470" alt="Stos" src="https://github.com/user-attachments/assets/067e0362-e10b-4f77-ab50-a6d457368cf6" />

**LIFO** - Last in, first out

---

# Algorytmy

|Operator|Priorytet|
|---|---|
|(|0|
|**+ - )**|1|
|*** /**|2|
|**^**|3|

## Infix -> Postfix

Wczytujemy dane po kolei. Jeżeli wczytany element jest:

1. **Zmienną (stałą)**
    - Przesyłamy go na output
2. **(**
    - Przesyłamy go na stos
3. **)**
    - Odczytujemy ze stosu i przepisujemy na wyjście wszystkie operatory aż do (, którego nie przepisujemy
4. **+, -, \*, /, ^**
    - Jeżeli priorytet operatora wczytywanego jest wyższy od priorytetu tego na wierzchu stosu (lub stos jest pusty), dopisujemy na stos.
    - Jeżeli priorytet operatora wczytywanego jest mniejszy lub równy od tego na wierzchu stosu, odczytujemy i przepisujemy na wyjście kolejne operatory z wierzchu stosu, dopóki ich priorytet jest >= wczytanego, po czym wpisujemy na stos operator.

Dla przykładu: `(12 + 8) − 2 * 6`

|step|input|stack|output|
|---|---|---|---|
|1|(|(||
|2|12|(|12|
|3|+|( +|12|
|4|8|( +|12 8|
|5|)||12 8 +|
|6|-|-|12 8 +|
|7|2|-|12 8 + 2|
|8|*|- *|12 8 + 2|
|9|6|- *|12 8 + 2 6|
|10|||12 8 + 2 6 * -|

## Postfix -> Wynik

- Jeżeli wczytany symbol jest liczbą, wkładamy go na stos
- Jeżeli jest operatorem, to:
    - Ze stosu zdejmujemy jeden element (a)
    - Ze stosu zdejmujemy drugi element (b)
    - Na stosie umieszczamy wynik b operator a Po wykonaniu dla wszystkich symboli w ONP na stosie pozostanie nam wynik wyrażenia. Dla przykładu, na poprzednim przykładzie, czyli  
        `12 8 + 2 6 * -`:

| step | input | stack  |
| ---- | ----- | ------ |
| 1    | 12    | 12     |
| 2    | 8     | 12 8   |
| 3    | +     | 20     |
| 4    | 2     | 20 2   |
| 5    | 6     | 20 2 6 |
| 6    | *     | 20 12  |
| 7    | -     | 8      |

---

# Stos w ASM

- Rośnie w dół, ale działa tak samo
- SP: domyślnie FFFE

Push:
```Assembly
push 0xDEAD

push AX ; tylko rejestry 16-bitowe

push word [a] 

pusha ; wrzuca wszystkie rejestry do stosu (AX, BX, CX...)


a dw 2 ; na stosie - wszystko jako 'dw'
```

Pop:
```Assembly
pop AX ; pop do rejestru (tylko 16-bitowe)

pop word [y] ; pop do wartości

popa ; pop all do rejestrów
```

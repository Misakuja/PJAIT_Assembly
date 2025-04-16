Basic Paint written in ASM.

```Assembly
org 100h

mov AH, 00h 
mov AL, 12h
int 10h ; graphics mode

mov AH, 0Ch
mov AL, 0xF
mov CX, 0
mov DX, 0
bg_col_loop:
	bg_row_loop:
		int 10h
		inc CX
		dec word [bg_col_counter]
		cmp word [bg_col_counter], 0
		jne bg_row_loop
		mov CX, 0
		inc DX
		mov word [bg_col_counter], 640
		cmp DX, 480
		jne bg_col_loop

mov AX, 1h
int 33h ; 'turns on the cursor'

main_loop:
    mov AX, 03h
    int 33h ; find cursor position
    
    cmp BX, 1h ; draw only if left mouse button is pressed
        je draw_pixel
    
    mov AH, 01h
    int 16h
    cmp AL, 'q'
        je koniec ; end if q is pressed 
    cmp AL, 'c'
        je change_colour ;change colour if c pressed
    cmp AL, 'z'
        je brush_inc ; inc brush size if z
    cmp AL, 'x'
        je check_brush_size ; dec brush size if x + if its greater than 0
	cmp AL, 'e'
		je eraser
jmp main_loop

koniec:
    mov AH, 00h
    int 16h ; makes sure the program doesnt throw 'q' on exit

    mov AX, 2h
    int 33h

    mov AH, 0h
    int 21h
    
draw_pixel:
    mov AH, 0Ch
    mov AL, [colour]
    mov byte [loop_counter], 0h
    inc DX
    sub CX, [brush_size]
    dec byte [loop_counter]
    outer_loop:
        dec DX
        add CX, [brush_size]
        inc byte [loop_counter]
        mov BL, [brush_size]
        cmp [loop_counter], BL
            je main_loop
        inner_loop:
            int 10h
            dec BL
            dec CX
            cmp BL, 0
                je outer_loop
                jne inner_loop

    jmp outer_loop        
jmp main_loop

eraser:
	mov AH, 00h
	int 16h
	mov word [colour], 0xF
	jmp main_loop

change_colour:
    mov AH, 00h
    int 16h
    inc byte [colour]
    
    call draw_pixel_in_corner
    
    jmp main_loop
    
brush_inc:
    mov AH, 00h
    int 16h
    inc byte [brush_size]
    
    call draw_pixel_in_corner
    
    jmp main_loop
    
check_brush_size:
    mov AH, 00h
    int 16h
    
    mov AL, [brush_size]
    cmp AL, 1
        je main_loop
        jg brush_dec
    
    jmp main_loop 

brush_dec:
    mov AH, 00h
    int 16h
    
	call draw_black_pixel_in_corner
	
    dec byte [brush_size]
    
    call draw_pixel_in_corner

    jmp main_loop

draw_pixel_in_corner:
    mov AH, 0Ch
    mov CX, 79 ; column
    mov DX, 24 ; row
    int 10h
     
    call draw_pixel
ret

draw_black_pixel_in_corner:
    mov AH, 0Ch
    mov AL, 0xF    ; black color
    mov CX, 79   ; column
    mov DX, 24   ; row
    
    mov byte [loop_counter], 0h
    inc DX
    sub CX, [brush_size]
    dec byte [loop_counter]
    black_outer_loop:
        dec DX
        add CX, [brush_size]
        inc byte [loop_counter]
        mov BL, [brush_size]
        cmp [loop_counter], BL
            je black_done
        black_inner_loop:
            int 10h
            dec BL
            dec CX
            cmp BL, 0
                je black_outer_loop
                jne black_inner_loop
    
black_done:
	ret
	
colour dw 1
brush_size dw 3h
loop_counter db 0
bg_col_counter dw 640
```

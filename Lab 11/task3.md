    
    TITLE Task 3: Move AX[0] into BX[15] (Manual and SHRD)
    
    INCLUDE Irvine32.inc
    
    .data
    msg1 BYTE "Manual Method - BX after BX[15] = AX[0]: ", 0
    msg2 BYTE "SHRD Method  - BX after BX[15] = AX[0]: ", 0
    
    .code
    main PROC
        ; -------------------------------
        ; Manual Method (no SHRD)
        ; -------------------------------
        mov ax, 1              ; AX = 0001h, bit 0 is 1
        mov bx, 1234h          ; BX has some initial value
    
        mov cx, ax             ; Copy AX to CX
        and cx, 1              ; Isolate bit 0
        shl cx, 15             ; Shift into bit 15 position
    
        and bx, 7FFFh          ; Clear bit 15 of BX
        or bx, cx              ; Set BX[15] = AX[0]
    
        ; Output result
        call Crlf
        mov edx, OFFSET msg1
        call WriteString
        movzx eax, bx
        call WriteHex
    
        ; -------------------------------
        ; SHRD Method
        ; -------------------------------
        call Crlf
        mov ax, 1              ; Reset AX = 0001h
        mov bx, 0              ; Clear BX for fresh test
        mov cx, 15             ; Shift count = 15
        shrd bx, ax, cl        ; Shift AX[0] into BX[15]
    
        ; Output result
        call Crlf
        mov edx, OFFSET msg2
        call WriteString
        movzx eax, bx
        call WriteHex
    
        call Crlf
        exit
    main ENDP
    
    END main






![image](https://github.com/user-attachments/assets/69a34c35-cf0f-4637-bcb0-4ab4ac695a94)

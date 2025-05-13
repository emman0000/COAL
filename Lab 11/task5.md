    
    TITLE Extended 64-bit Addition
    
    INCLUDE Irvine32.inc
    
    .data
    ; 64-bit values
    operand1Low   DWORD 0FFFFFFFFh     ; Lower 32 bits of operand 1
    operand1High  DWORD 00000001h      ; Upper 32 bits of operand 1
    operand2Low   DWORD 00000001h      ; Lower 32 bits of operand 2
    operand2High  DWORD 00000000h      ; Upper 32 bits of operand 2
    
    resultLow     DWORD ?              ; Result lower 32 bits
    resultHigh    DWORD ?              ; Result upper 32 bits
    
    msg1          BYTE "64-bit addition result (high:low) = ", 0
    
    .code
    
    Extended_Add PROC
        ; Add low 32 bits
        mov eax, operand1Low
        add eax, operand2Low
        mov resultLow, eax
    
        ; Add high 32 bits with carry
        mov eax, operand1High
        adc eax, operand2High
        mov resultHigh, eax
    
        ret
    Extended_Add ENDP
    
    main PROC
        call Extended_Add
    
        ; Display result
        call Crlf
        mov edx, OFFSET msg1
        call WriteString
    
        mov eax, resultHigh
        call WriteHex
        mov eax, resultLow
        call WriteHex
    
        call Crlf
        exit
    main ENDP
    
    END main




![image](https://github.com/user-attachments/assets/a52d05fd-ce59-415b-bd6b-2cdd6b4d0ea9)

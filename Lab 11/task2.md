    
    
    INCLUDE Irvine32.inc
    
    .data
    msg1 BYTE "Initial 16-bit value (AX): ", 0
    msg2 BYTE "Sign-extended 32-bit value (EAX): ", 0
    
    .code
    main PROC
      
        mov ax, -128         ; AX = FF80h
    
      
        xor eax, eax         ; Clear EAX to avoid garbage in upper bits
        mov ax, -128         ; Reload to make sure upper bits are clean
    
    
        shl eax, 16          ; Move AX content into high word (EAX = 0xFF800000)
        sar eax, 16          ; Arithmetic shift right to sign-extend to 32-bit
    
     
        call Crlf
        mov edx, OFFSET msg1
        call WriteString
        movzx eax, ax        ; Zero-extend AX just for display
        call WriteInt
    
     
        call Crlf
        mov edx, OFFSET msg2
        call WriteString
        call WriteInt        ; EAX already contains the sign-extended result
    
        call Crlf
        exit
    main ENDP
    
    END main








![image](https://github.com/user-attachments/assets/f70b8bfc-bfee-42a1-a547-5bb997e2b051)

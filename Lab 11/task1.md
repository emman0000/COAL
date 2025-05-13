
    
    INCLUDE Irvine32.inc
    
    .data
    promptMsg    BYTE "Enter a number to multiply by 21: ", 0
    resultMsg    BYTE "Result (EAX * 21) = ", 0
    
    .code
    main PROC
        ; Prompt user to enter a number
        mov edx, OFFSET promptMsg
        call WriteString
        call ReadInt             ; Read integer input into EAX
    
        ; Copy original value for reuse
        mov ebx, eax             ; EBX = original EAX
    
        ; Calculate EAX * 21 using: (EAX << 4) + (EAX << 2) + EAX
        shl eax, 4               ; EAX = EAX * 16
        mov ecx, ebx             ; ECX = original EAX
        shl ecx, 2               ; ECX = EAX * 4
        add eax, ecx             ; EAX = 16*EAX + 4*EAX
        add eax, ebx             ; EAX = (16 + 4 + 1) * EAX = 21 * EAX
    
        ; Display result
        call Crlf
        mov edx, OFFSET resultMsg
        call WriteString
        call WriteInt            ; Display the result in EAX
    
        call Crlf
        exit
    main ENDP
    
    END main






![image](https://github.com/user-attachments/assets/bac7087c-f1d6-47f6-bacf-c35268aed655)


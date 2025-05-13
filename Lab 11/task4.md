    
    INCLUDE Irvine32.inc
    
    .data
    val1   SDWORD 100
    val2   SDWORD 20
    val3   SDWORD 5
    
    msg1   BYTE "Result (val1) = ", 0
    
    .code
    main PROC
        ; Compute (val2 / val3)
        mov eax, val2       ; EAX = val2
        cdq                 
        idiv val3           
        mov ebx, eax       
    
        ; Compute (val1 / val2)
        mov eax, val1       ; EAX = val1
        cdq                 
        idiv val2           
        mov ecx, eax        
    
        ; Multiply: val1 = (val2 / val3) * (val1 / val2)
        mov eax, ebx        ; EAX = val2 / val3
        imul ecx            
        mov val1, eax       
    
        call Crlf
        mov edx, OFFSET msg1
        call WriteString
        mov eax, val1
        call WriteInt
    
        call Crlf
        exit
    main ENDP
    
    END main





![image](https://github.com/user-attachments/assets/27d08480-0692-4aa8-9eea-dd7583f84327)

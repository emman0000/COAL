    INCLUDE Irvine32.inc
    
    .data
    string1 BYTE "Enter a number N: ", 0
    string2 BYTE "Output: ", 0
    
    .code
    main PROC
    mov eax, 0
    
    mov edx, OFFSET string1
    call WriteString
    call ReadInt
    mov ecx, eax
    mov eax, 0
    
    sumloop:
    add eax,ecx
    dec ecx
    jnz sumloop
    
    mov edx, OFFSET string2
    call WriteString
    call WriteDec
    call Crlf
    
    exit
    main ENDP
    END main
  
  ![image](https://github.com/user-attachments/assets/c91a2fb4-a772-4d8a-963f-ad33bdfe1311)


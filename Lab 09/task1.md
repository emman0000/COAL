    Include Irvine32.inc
    .data
    n1 DWORD 2
    n2 DWORD 3
    n3 DWORD 4
    
    .code
    main PROC
    ;Push Value in reverse order 
    
    push n3 ;top of the stack
    push n2
    push n1
    
    call ThreeProd
    exit
    main ENDP

    ThreeProd PROC
    push ebp
    mov ebp, esp
    
    mov eax, [ebp+12]
    mov ebx, [ebp+8]
    imul eax, ebx
    
    mov ecx, [ebp+16]
    imul eax, ecx
    
    call WriteInt 
    call Crlf
    
    pop ebp
    ret 
    ThreeProd ENDP
    
    END main






![image](https://github.com/user-attachments/assets/86d48709-a75f-4374-8149-8d5f011cbe27)

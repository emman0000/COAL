    INCLUDE Irvine32.inc
    
    .data
    ; Variable declarations
    var DWORD 0          ; var initialized to 0
    
    ; Strings to print
    helloStr BYTE "Hello", 0
    worldStr BYTE "World", 0
    counterMsg BYTE "var = ", 0
    completeMsg BYTE "Loop completed.", 0
    
    .code
    main PROC
        ; Implement the while loop
        ; while (var <= 10)
    WhileStart:
        ; Check while condition (var <= 10)
        mov eax, var
        cmp eax, 10
        jg WhileEnd       ; Jump if var > 10 (exit loop)
        
        ; Display current value of var
        mov edx, OFFSET counterMsg
        call WriteString
        mov eax, var
        call WriteDec
        mov al, ':'
        call WriteChar
        mov al, ' '
        call WriteChar
        
        ; if (var < 5)
        mov eax, var
        cmp eax, 5
        jge ElsePart      ; Jump to else part if var >= 5
        
        ; Print "Hello"
        mov edx, OFFSET helloStr
        call WriteString
        call Crlf
        jmp IfEnd
        
    ElsePart:
        ; Print "World"
        mov edx, OFFSET worldStr
        call WriteString
        call Crlf
        
    IfEnd:
        ; var = var + 1
        mov eax, var
        inc eax
        mov var, eax
        
        ; Loop back to while condition
        jmp WhileStart
        
    WhileEnd:
        ; Display completion message
        mov edx, OFFSET completeMsg
        call WriteString
        call Crlf
        
        exit
    main ENDP
    
    END main
    
    
    
    
  ![image](https://github.com/user-attachments/assets/9c1dc276-9daa-48a8-b028-699ee5ce295b)

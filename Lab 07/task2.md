    INCLUDE Irvine32.inc
    
    .DATA
    num1 DWORD 5
    num2 DWORD 10
    num3 DWORD 15
    result DWORD ?
    newline BYTE 10, 13, 0
    
    .CODE
    main PROC
        ; Push numbers onto stack
        PUSH num1
        PUSH num2
        PUSH num3
    
        ; Pop and sum the numbers
        POP EAX    ; Pop first number into EAX
        POP EBX    ; Pop second number into EBX
        ADD EAX, EBX  ; EAX = num1 + num2
    
        POP ECX    ; Pop third number into ECX
        ADD EAX, ECX  ; EAX = (num1 + num2) + num3
    
        ; Store the result in memory
        MOV result, EAX
        PUSH EAX  ; Push the sum back onto the stack
    
        ; Print the result
        CALL Clrscr
        MOV EAX, result  ;  Fixed instruction
        CALL WriteDec    ; Print sum
        CALL Crlf        ; Print newline
    
        EXIT
    main ENDP
    END main

  ![Screenshot 2025-03-27 072030](https://github.com/user-attachments/assets/b723ad84-adbf-4ca0-9474-b3d7ae762a57)


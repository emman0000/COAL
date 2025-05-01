    INCLUDE Irvine32.inc
    
    .data
    promptMsg1 BYTE "Enter the first integer: ", 0
    promptMsg2 BYTE "Enter the second integer: ", 0
    promptMsg3 BYTE "Enter the third integer: ", 0
    promptMsg4 BYTE "Enter the fourth integer: ", 0
    equalMsg BYTE "All four integers are equal.", 0
    notEqualMsg BYTE "The integers are not all equal.", 0
    
    ; Variables to store the four integers
    int1 SDWORD ?
    int2 SDWORD ?
    int3 SDWORD ?
    int4 SDWORD ?
    
    .code
    main PROC
        call Clrscr
        
        ; Get the first integer
        mov edx, OFFSET promptMsg1
        call WriteString
        call ReadInt
        mov int1, eax
        
        ; Get the second integer
        mov edx, OFFSET promptMsg2
        call WriteString
        call ReadInt
        mov int2, eax
        
        ; Get the third integer
        mov edx, OFFSET promptMsg3
        call WriteString
        call ReadInt
        mov int3, eax
        
        ; Get the fourth integer
        mov edx, OFFSET promptMsg4
        call WriteString
        call ReadInt
        mov int4, eax
        
        ; Compare the integers
        call CompareIntegers
        
        exit
    main ENDP
    
    ;-------------------------------------------------
    ; CompareIntegers - Compares four integers and displays result
    ; Receives: Nothing (uses global variables)
    ; Returns: Nothing, displays message on console
    ;-------------------------------------------------
    CompareIntegers PROC
        ; Compare first with second
        mov eax, int1
        cmp eax, int2
        jne NotEqual
        
        ; Compare first with third
        cmp eax, int3
        jne NotEqual
        
        ; Compare first with fourth
        cmp eax, int4
        jne NotEqual
        
        ; If we get here, all are equal
        mov edx, OFFSET equalMsg
        call WriteString
        call Crlf
        jmp Done
        
    NotEqual:
        ; At least one integer is different
        mov edx, OFFSET notEqualMsg
        call WriteString
        call Crlf
        
    Done:
        ret
    CompareIntegers ENDP
    
    END main
    
  ![image](https://github.com/user-attachments/assets/41e8ce5b-363c-48ca-b0cb-9e9cb730a5d0)
    
  ![image](https://github.com/user-attachments/assets/8d5630f8-6916-4f56-b9a0-8480cc64d29a)
    

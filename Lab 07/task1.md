    INCLUDE Irvine32.inc
    
    .DATA
        st1 WORD 1, 2, 3, 4, 5, 6, 7, 8, 9, 0   ; Original array
        st2 WORD 10 DUP (?)  ; Empty array for popped values
        newline BYTE 10, 13, 0   ; Newline characters (LF + CR)
    
    .CODE 
    main PROC
        MOV ECX, 10       ; Loop counter for 10 elements
        LEA ESI, st1      ; Load address of st1
    
    PUSH_LOOP:
        MOV AX, [ESI]     ; Load value from st1 into AX (16-bit move)
        PUSH EAX          ; Push AX onto the stack (zero-extended to 32-bit)
        ADD ESI, 2        ; Move to next word
        LOOP PUSH_LOOP    ; Repeat for all elements
    
        MOV ECX, 10       ; Reset loop counter
        LEA ESI, st2      ; Load address of st2
    
    POP_LOOP:
        POP EAX           ; Pop value from stack into EAX
        MOV [ESI], AX     ; Store only the lower 16-bit of EAX into st2
        ADD ESI, 2        ; Move to next word
        LOOP POP_LOOP     ; Repeat for all elements
    
        ; PRINTING THE REVERSED ARRAY
        MOV ECX, 10       ; Loop counter for 10 elements
        LEA ESI, st2      ; Load address of st2
    
    PRINT_LOOP:
        MOV AX, [ESI]     ; Load value from st2 into AX
        MOVZX EAX, AX     ; Zero extend AX to EAX (so WriteInt works)
        CALL WriteDec    ; Print integer
        MOV EDX, OFFSET newline  ; Print space after each number
        CALL WriteString  
        ADD ESI, 2        ; Move to next word
        LOOP PRINT_LOOP   ; Repeat for all elements
    
        EXIT
    main ENDP
    END main


![Screenshot 2025-03-27 070958](https://github.com/user-attachments/assets/5d7c21f7-0f2a-4fd3-a284-b253668df7fd)


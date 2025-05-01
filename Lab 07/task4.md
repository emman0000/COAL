    INCLUDE Irvine32.inc

    .data
    promptMsg BYTE "Enter number of columns for the pattern: ", 0
    asterisk BYTE "*", 0

    ; Variable to store the number of columns
    numColumns DWORD ?
    
    .code
    main PROC
    call Clrscr
    
    ; Prompt user for number of columns
    mov edx, OFFSET promptMsg
    call WriteString
    call ReadInt
    
    ; Store the user input in numColumns
    mov numColumns, eax
    
    ; Call the function to print the pattern
    ; Pass the number of columns in ECX
    mov ecx, numColumns
    call PrintPattern
    
        exit
    main ENDP
    
    ;-------------------------------------------------
    ; PrintPattern - Prints a pattern of asterisks
    ; Receives: ECX = number of columns (max asterisks in a row)
    ; Returns: Nothing, displays pattern on console
    ;-------------------------------------------------
    PrintPattern PROC
        push ecx          ; Save the original column count
        mov ebx, 1        ; Start with 1 asterisk per row
        
    RowLoop:
        push ecx          ; Save outer loop counter
        
        ; For each row, print ebx asterisks
        mov ecx, ebx      ; Set inner loop counter to current row number
        
    AsteriskLoop:
        mov edx, OFFSET asterisk
        call WriteString
        loop AsteriskLoop
        
        call Crlf         ; Move to the next line
        inc ebx           ; Increment asterisks for next row
        
        pop ecx           ; Restore outer loop counter
        loop RowLoop
        
        pop ecx           ; Restore the original value
        ret
    PrintPattern ENDP
    
    END main
  ![image](https://github.com/user-attachments/assets/94822448-8abd-4597-b3a8-2dbee187042e)

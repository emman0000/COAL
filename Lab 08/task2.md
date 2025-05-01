    INCLUDE Irvine32.inc
    
    .data
    ; The array to search through
    intArr SWORD 0, 0, 0, 150, 120, 35, -12, 66, 4, 0
    
    ; Messages for output
    foundMsg BYTE "First non-zero value found: ", 0
    positionMsg BYTE "Position in array: ", 0
    notFoundMsg BYTE "No non-zero values found in the array.", 0
    
    ; Variables to store results
    firstNonZero SWORD ?
    position DWORD ?
    
    .code
    main PROC
        call Clrscr
        
        ; Call procedure to find the first non-zero value
        call FindFirstNonZero
        
        exit
    main ENDP
    
    ;-------------------------------------------------
    ; FindFirstNonZero - Searches for the first non-zero value in the array
    ; Receives: Nothing (uses global array)
    ; Returns: Nothing, displays results on console
    ;-------------------------------------------------
    FindFirstNonZero PROC
        ; Initialize index and pointer
        mov esi, OFFSET intArr   ; ESI points to the array
        mov ecx, LENGTHOF intArr ; ECX has the array length
        mov ebx, 0               ; EBX will track the current position
        
    SearchLoop:
        ; Compare current element with zero
        cmp WORD PTR [esi], 0
        jne FoundNonZero         ; Jump if not equal to zero
        
        ; Move to next element
        add esi, TYPE intArr     ; Move pointer to next element
        inc ebx                  ; Increment position counter
        loop SearchLoop          ; Decrement ECX and loop if not zero
        
        ; If we get here, no non-zero value was found
        mov edx, OFFSET notFoundMsg
        call WriteString
        call Crlf
        jmp Done
        
    FoundNonZero:
        ; Store the non-zero value and its position
        movsx eax, WORD PTR [esi]  ; Move and sign-extend the value to EAX
        mov firstNonZero, ax       ; Store the value
        mov position, ebx          ; Store the position
        
        ; Display the results
        mov edx, OFFSET foundMsg
        call WriteString
        movsx eax, firstNonZero
        call WriteInt
        call Crlf
        
        mov edx, OFFSET positionMsg
        call WriteString
        mov eax, position
        call WriteDec
        call Crlf
        
    Done:
        ret
    FindFirstNonZero ENDP
    
    END main
    
    
  ![image](https://github.com/user-attachments/assets/081141ce-d8da-4a48-b35d-d6f33fcff307)

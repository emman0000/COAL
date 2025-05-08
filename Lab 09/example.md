    INCLUDE Irvine32.inc
    
    .data
    prompt BYTE "Enter a number: ", 0
    resultMsg BYTE "Result = ", 0
    array DWORD 10 DUP(?)
    
    .code
    main PROC
        ; ---- Example: Pass by value ----
        mov eax, 5
        push eax
        call SquareValue       ; eax will now have eax^2
        call ShowResult
    
        ; ---- Example: Pass by reference ----
        push OFFSET array
        push 10
        call FillArray         ; Fill array with values [0, 1, ..., 9]
    
        ; ---- Call advanced procedure with local variable ----
        call LocalExample
    
        exit
    main ENDP
    
    ; ---------------------------------------------------------
    ; Procedure: SquareValue (pass-by-value)
    ; Receives one integer on stack and returns square in eax
    SquareValue PROC
        push ebp
        mov ebp, esp
    
        mov eax, [ebp + 8]      ; get parameter
        imul eax, eax           ; square it
    
        pop ebp
        ret 4                   ; clean 1 argument
    SquareValue ENDP
    
    ; ---------------------------------------------------------
    ; Procedure: FillArray (pass-by-reference + multiple params)
    ; Arguments: [ebp+8] = count, [ebp+12] = array address
    FillArray PROC
        push ebp
        mov ebp, esp
        pushad
    
        mov ecx, [ebp + 8]      ; count
        mov edi, [ebp + 12]     ; array address
    
        xor eax, eax            ; counter value
    
    FillLoop:
        mov [edi], eax
        add edi, 4
        inc eax
        loop FillLoop
    
        popad
        pop ebp
        ret 8                   ; clean 2 arguments
    FillArray ENDP
    
    ; ---------------------------------------------------------
    ; Procedure: LocalExample
    ; Demonstrates use of ENTER/LEAVE and a local variable
    LocalExample PROC
        enter 4, 0              ; reserve 4 bytes for one DWORD local
                                ; [ebp - 4] is local var
    
        mov edx, OFFSET prompt
        call WriteString
        call ReadInt
    
        mov [ebp - 4], eax      ; store input in local var
        mov eax, [ebp - 4]
        imul eax, 2             ; multiply input by 2
    
        mov edx, OFFSET resultMsg
        call WriteString
        call WriteDec
        call Crlf
    
        leave
        ret
    LocalExample ENDP
    
    ; ---------------------------------------------------------
    ; Utility Procedure: ShowResult (just prints value in eax)
    ShowResult PROC
        mov edx, OFFSET resultMsg
        call WriteString
        call WriteDec
        call Crlf
        ret
    ShowResult ENDP
    
    END main

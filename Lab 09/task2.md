    INCLUDE Irvine32.inc
    
    .data
    arr DWORD 20, 5, 9, 2, 12, 7, 15, 1, 8, 10, 6, 3, 11, 19, 4, 13, 14, 17, 18, 16
    msgMin BYTE "Minimum = ", 0
    msgMax BYTE "Maximum = ", 0
    
    .code
    main PROC
        push OFFSET arr
        call MinMaxArray
        exit
    main ENDP
    
    MinMaxArray PROC
        push ebp
        mov ebp, esp
        pushad
    
        mov esi, [ebp+8]     ; esi = address of array
        mov ecx, 20          ; loop counter
    
        ; First element
        mov eax, [esi]       ; eax = first element
        mov ebx, eax         ; ebx = min
        mov edx, eax         ; edx = max
        add esi, 4           ; move to next element
        dec ecx              ; already used 1 element
    
    NextElement:
        mov eax, [esi]       ; get current element
    
        cmp eax, ebx
        jl SetNewMin         ; if eax < min, update min
    
        cmp eax, edx
        jg SetNewMax         ; if eax > max, update max
    
    ContinueLoop:
        add esi, 4
        loop NextElement
        jmp ShowResults
    
    SetNewMin:
        mov ebx, eax
        jmp ContinueLoop
    
    SetNewMax:
        mov edx, eax
        jmp ContinueLoop
    
    ShowResults:
        ; Display minimum
        mov edx, OFFSET msgMin
        call WriteString
        mov eax, ebx
        call WriteDec
        call Crlf
    
        ; Display maximum
        mov edx, OFFSET msgMax
        call WriteString
        mov eax, edx
        call WriteDec
        call Crlf
    
        popad
        pop ebp
        ret 4
    MinMaxArray ENDP
    
    END main

![Screenshot 2025-05-08 030207](https://github.com/user-attachments/assets/7bf0cca9-90db-480f-bb17-aab96db1075e)
    

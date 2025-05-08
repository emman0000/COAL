    INCLUDE Irvine32.inc
    
    .data
    Str1 BYTE "127&j~3#^&*#*#45^", 0
    msg BYTE "Found at index: ", 0
    
    .code
    main PROC
        call Scan_String
        exit
    main ENDP
    
    Scan_String PROC
        cld
        mov edi, OFFSET Str1      ; point to string
        mov ecx, LENGTHOF Str1    ; set counter
        mov al, '#'               ; char to find
    
        repne scasb               ; scan until found or end
        jnz NotFound              ; if not found, skip
    
        ; Found! Calculate index = (EDI - OFFSET Str1 - 1)
        sub edi, OFFSET Str1
        dec edi                   ; point to actual position
        mov eax, edi
    
        mov edx, OFFSET msg
        call WriteString
        call WriteDec
        call Crlf
        ret
    
    NotFound:
        mov edx, OFFSET msg
        call WriteString
        mov eax, -1
        call WriteInt
        call Crlf
        ret
    Scan_String ENDP
    END main


![image](https://github.com/user-attachments/assets/8e511fda-ce1f-4690-9c49-7cca928e6ce8)


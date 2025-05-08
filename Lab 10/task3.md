    
    INCLUDE Irvine32.inc
    
    .data
    s1 BYTE "hello", 0
    s2 BYTE "hello", 0
    equalMsg BYTE "Strings are equal", 0
    notEqualMsg BYTE "Strings are NOT equal", 0
    
    .code
    main PROC
        INVOKE Str_compare, ADDR s1, ADDR s2  ; Compare strings
        jz Equal                              ; ZF set = equal
    
        mov edx, OFFSET notEqualMsg
        call WriteString
        call Crlf
        jmp Done
    
    Equal:
        mov edx, OFFSET equalMsg
        call WriteString
        call Crlf
    
    Done:
        exit
    main ENDP
    END main
    
    









![image](https://github.com/user-attachments/assets/558bf448-b4b2-4507-9f78-102e949283d0)


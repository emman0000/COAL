    
    INCLUDE Irvine32.inc
    
    .data
    prompt BYTE "Enter a number = ", 0
    result BYTE "Square = ", 0
    
    .code
    main PROC
     call LocalSquare
     exit
     main ENDP
    
     LocalSquare PROC
      enter 4, 0 ; reserve 4 bytes for 1 loacl DWORD
    
      mov edx, OFFSET prompt
      call WriteString
      call ReadInt
    
      mov[ebp-4], eax ; local variable 
    
    
      mov eax, [ebp - 4]
        imul eax, eax
    
      mov edx, OFFSET result
      call WriteString
      call WriteDec
      call Crlf 
    
      leave
      ret
      LocalSquare ENDP
    END main
    






![image](https://github.com/user-attachments/assets/eeeca156-8004-4b99-a660-7823b556acc1)

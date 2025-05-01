    INCLUDE Irvine32.inc
    
    .data
    promptMsg BYTE "Enter a number (n): ", 0
    resultMsg BYTE "The sum of numbers 1 to ", 0
    isMsg BYTE " is: ", 0
    
    ; Variable to store the user input number and the sum
    userNumber DWORD ?
    sum DWORD ?
    
    .code
    main PROC
        call Clrscr
        
        ; Call the function to get input and calculate sum
        call CalculateSum
        
        exit
    main ENDP
    
    ;-------------------------------------------------
    ; CalculateSum - Asks for a number and calculates sum from 1 to n
    ; Receives: Nothing
    ; Returns: Nothing, displays the sum on console
    ;-------------------------------------------------
    CalculateSum PROC
        ; Prompt user for a number
        mov edx, OFFSET promptMsg
        call WriteString
        call ReadInt
        
        ; Store the number
        mov userNumber, eax
        
        ; Initialize registers for summation
        mov ecx, eax    ; Set loop counter to n
        mov eax, 0      ; Initialize sum to 0
        
    SumLoop:
        add eax, ecx    ; Add current number to sum
        loop SumLoop    ; Decrement ECX and loop if not zero
        
        ; Store the final sum
        mov sum, eax
        
        ; Display the result
        mov edx, OFFSET resultMsg
        call WriteString
        
        mov eax, userNumber
        call WriteDec
        
        mov edx, OFFSET isMsg
        call WriteString
        
        mov eax, sum
        call WriteDec
        call Crlf
        
        ret
    CalculateSum ENDP
    
    END main
    
    
   ![image](https://github.com/user-attachments/assets/e5b9f58d-02d8-4cd9-93eb-e6ee2e117fdb)

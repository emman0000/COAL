    INCLUDE Irvine32.inc
    
    .data
    msgPrompt BYTE "Enter a number: ", 0
    msgNotPrime BYTE "Not all numbers are prime.", 0
    msgLargest BYTE "Largest prime number is: ", 0
    numbers DWORD 4 DUP(?)       ; array to store 4 user inputs
    
    .code
    main PROC
        mov esi, OFFSET numbers  ; ESI will point to numbers array
        mov ecx, 4               ; input count
    
    ReadLoop:
        mov edx, OFFSET msgPrompt
        call WriteString
        call ReadInt             ; result in EAX
        mov [esi], eax           ; store input in array
        add esi, 4               ; move to next dword
        loop ReadLoop
    
        ; Now check all numbers for primality
        mov esi, OFFSET numbers
        mov ecx, 4
        mov ebx, 0               ; EBX will count how many are NOT prime
    
    CheckLoop:
        mov eax, [esi]
        push eax
        call CheckPrime
        add esi, 4
        cmp eax, 0               ; if not prime
        jne Next                 ; if prime, continue
        inc ebx                  ; count non-primes
    
    Next:
        loop CheckLoop
    
        cmp ebx, 0               ; any non-prime?
        jne NotAllPrime          ; if yes, skip LargestPrime
    
        ; All are prime, find largest
        call LargestPrime
        jmp EndProgram
    
    NotAllPrime:
        mov edx, OFFSET msgNotPrime
        call WriteString
        call Crlf
    
    EndProgram:
        exit
    main ENDP
    
    ; -----------------------------
    ; CheckPrime: receives number in stack
    ; Returns 1 in EAX if prime, 0 if not
    CheckPrime PROC
        push ebp
        mov ebp, esp
    
        mov eax, [ebp + 8]   ; number to check
        cmp eax, 2
        jl NotPrime          ; if < 2 → not prime
        mov ecx, 2
    
    LoopCheck:
        mov edx, 0
        div ecx              ; EAX / ECX → EAX quotient, EDX remainder
        cmp edx, 0
        je NotPrime          ; divisible → not prime
        inc ecx
        mov eax, [ebp + 8]
        cmp ecx, eax
        jl LoopCheck
    
        mov eax, 1           ; it's prime
        jmp DoneCheck
    
    NotPrime:
        mov eax, 0
    
    DoneCheck:
        pop ebp
        ret 4                ; clean one argument
    CheckPrime ENDP
    
    ; -----------------------------
    LargestPrime PROC
        mov esi, OFFSET numbers
        mov eax, [esi]       ; first number
        add esi, 4
    
        mov ecx, 3           ; check remaining 3
    CompareLoop:
        mov ebx, [esi]
        cmp ebx, eax
        jle SkipUpdate
        mov eax, ebx         ; update max
    
    SkipUpdate:
        add esi, 4
        loop CompareLoop
    
        mov edx, OFFSET msgLargest
        call WriteString
        call WriteDec
        call Crlf
    
        ret
    LargestPrime ENDP
    
    END main
    



![image](https://github.com/user-attachments/assets/3809b01d-bc3f-4171-946b-d77af6726105)

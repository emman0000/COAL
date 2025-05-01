      INCLUDE Irvine32.inc
      
      .data
      ; The array from the previous task
      intArr SWORD 0, 0, 0, 150, 120, 35, -12, 66, 4, 0
      
      ; Variable declarations
      var DWORD 5          ; var = 5 
      edxValue DWORD ?     ; Will store var+1 (6)
      x DWORD ?            ; Result of the conditional logic
      
      ; Messages for output
      resultMsg BYTE "The value of x is: ", 0
      varMsg BYTE "var = ", 0
      edxMsg BYTE "edx = ", 0
      ecxMsg BYTE "ecx (counter) = ", 0
      
      .code
      main PROC
          call Clrscr
          
          ; Initialize edx to var+1
          mov eax, var
          add eax, 1
          mov edxValue, eax
          
          ; Find first non-zero value and get the counter
          call FindFirstNonZero
          
          ; Implement the conditional logic
          call ImplementConditional
          
          ; Display the results
          call DisplayResults
          
          exit
      main ENDP
      
      ;-------------------------------------------------
      ; FindFirstNonZero - Searches for the first non-zero value in the array
      ; Receives: Nothing (uses global array)
      ; Returns: ECX will contain the counter value (position found)
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
          ; Default to position 0
          mov ecx, 0
          jmp Done
          
      FoundNonZero:
          ; Store the position in ECX
          mov ecx, ebx
          
      Done:
          ret
      FindFirstNonZero ENDP
      
      ;-------------------------------------------------
      ; ImplementConditional - Implements the conditional logic
      ; Receives: ECX = counter value
      ;           var = 5
      ;           edxValue = var+1 (6)
      ; Returns: Sets x to 0 or 1 based on the condition
      ;-------------------------------------------------
      ImplementConditional PROC
          ; Implement: if (var < ecx) AND (ecx >= edxValue) then x = 0 else x = 1
          
          ; First check: var < ecx
          mov eax, var
          cmp eax, ecx
          jge SetXToOne    ; If var >= ecx, the condition is false
          
          ; Second check: ecx >= edxValue
          mov eax, edxValue
          cmp ecx, eax
          jl SetXToOne     ; If ecx < edxValue, the condition is false
          
          ; If we get here, both conditions are true
          mov x, 0
          jmp Done
          
      SetXToOne:
          ; At least one condition is false
          mov x, 1
          
      Done:
          ret
      ImplementConditional ENDP
      
      ;-------------------------------------------------
      ; DisplayResults - Shows the values and result
      ; Receives: Nothing (uses global variables)
      ; Returns: Nothing, displays results on console
      ;-------------------------------------------------
      DisplayResults PROC
          ; Display var value
          mov edx, OFFSET varMsg
          call WriteString
          mov eax, var
          call WriteDec
          call Crlf
          
          ; Display edx value
          mov edx, OFFSET edxMsg
          call WriteString
          mov eax, edxValue
          call WriteDec
          call Crlf
          
          ; Display ecx value
          mov edx, OFFSET ecxMsg
          call WriteString
          mov eax, ecx
          call WriteDec
          call Crlf
          
          ; Display result
          mov edx, OFFSET resultMsg
          call WriteString
          mov eax, x
          call WriteDec
          call Crlf
          
          ret
      DisplayResults ENDP
      
      END main
      
      
   ![image](https://github.com/user-attachments/assets/c62026c3-f322-4b8d-bec4-138351c99c03)

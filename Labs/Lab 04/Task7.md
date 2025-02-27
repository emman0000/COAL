## Code

```
TITLE Test Program (Test.asm)
INCLUDE Irvine32.inc

.data
val1 BYTE  10h
val2 WORD  8000h
val3 DWORD 0FFFFh
val4 WORD  7FFFh

.code
main PROC
    mov ax, val2      ; Load val2 into AX (16-bit)
    inc ax            ; Increment val2 by 1
    mov val2, ax      ; Store back the updated value
    movzx eax, ax     ; Move into EAX for printing (zero-extend)
    call WriteDec     ; Print updated val2
    call Crlf         ; New line

    mov eax, val3     ; Load val3 into EAX
    sub eax, val3     ; Subtract val3 from EAX (EAX will now be 0)
    call WriteDec     ; Print result
    call Crlf         ; New line

    mov ax, val2      ; Load val2 into AX again
    sub ax, val4      ; Subtract val4 from val2
    mov val2, ax      ; Store the result back in val2
    movsx eax, ax     ; Move into EAX for printing (sign-extend)
    call WriteDec     ; Print the final value of val2
    call Crlf         ; New line

    call DumpRegs     ; Show register values for debugging
    exit
main ENDP
END main

```
## Screen Shot
![Screenshot 2025-02-27 095800](https://github.com/user-attachments/assets/457fa789-0be3-4ae2-8eb7-e5d270974da0)

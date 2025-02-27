## Code

```
TITLE Test Program (Test.asm)
INCLUDE Irvine32.inc

.data
Val1 DWORD 25h
Val2 BYTE 36o
Val3 WORD 20d

.code
main PROC
    mov eax, 0
    mov eax, 89        ; Load 89 into EAX
    add eax, 075Fh     ; Add 75Fh (1887 decimal)
    sub eax, 046o      ; Subtract 46o (38 decimal)
    sub eax, 28        ; Subtract 28 decimal
    add eax, 1101b     ; Add 1101b (13 decimal)
    
    ; At this point, EAX = 1923

    call DumpRegs           
    call WriteDec

    exit
main ENDP
END main
```

## Screen Shot

![Screenshot 2025-02-27 093512](https://github.com/user-attachments/assets/ce0865f2-cbf1-46ef-bc30-58c2db0e151e)


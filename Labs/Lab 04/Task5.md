## Code 
```
TITLE Test Program (Test.asm)
INCLUDE Irvine32.inc

   ; Define symbolic constant using '=' directive
SecondsInDay = 24 * 60 * 60   ; 86400 seconds

.code
main PROC
    mov eax, SecondsInDay 

    call DumpRegs           
    call WriteDec

    exit
main ENDP
END main
```

## Screen Shot

![Screenshot 2025-02-27 094651](https://github.com/user-attachments/assets/978c81bc-5f7b-48ad-9f84-301fbe178614)

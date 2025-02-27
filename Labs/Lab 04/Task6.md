## Code
```
TITLE Test Program (Test.asm)
INCLUDE Irvine32.inc

.data
A WORD 0FF10h   ; Define A
B WORD 0E10Bh   ; Define B

.code
main PROC
    mov ax, A   ; Store A in ax
    mov cx, B   ; Store B in cx
    mov A, cx   ; Move B into a
    mov B, ax   ;  

    call DumpRegs           
    call WriteDec

    exit
main ENDP
END main
```
![Screenshot 2025-02-27 095027](https://github.com/user-attachments/assets/ef3626e1-3768-4cdb-a74c-087f08fcb8c9)

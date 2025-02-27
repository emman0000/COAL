## Code 
TITLE Test Program (Test.asm)
INCLUDE Irvine32.inc

.code
main PROC
mov ax, 0
mov bx, 0
mov ax, 'Em'
mov bx, 'm'
call DumpRegs

exit
main ENDP
END main



### Screen Shot
![Screenshot 2025-02-27 090252](https://github.com/user-attachments/assets/20284245-c1de-4b84-9e8d-d0ff5ac9c429)

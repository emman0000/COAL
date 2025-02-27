## code 
TITLE Test Program (Test.asm)
INCLUDE Irvine32.inc

.data
varB BYTE +10
varW WORD -150
varD DWORD 600

.code
main PROC
    mov eax, 0
    mov ebx, 0
    mov ecx, 0

    movzx eax, varB         ; Zero-extend BYTE to EAX
    movsx ebx, varW         ; Sign-extend WORD to EBX
    mov ecx, varD           ; Directly move DWORD into ECX

    call DumpRegs           

    exit
main ENDP
END main


## screen shot 

![Screenshot 2025-02-27 092340](https://github.com/user-attachments/assets/c15efb3b-da0c-4b74-b09a-e0292da364b4)

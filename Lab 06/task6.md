                INCLUDE Irvine32.inc
                
                .data
                array DWORD 8,5,1,2,6
                arraySize EQU LENGTHOF array
                sorted BYTE "SORTED ARRAY: ", 0
                
                .code
                main PROC
                
                mov ecx, arraySize
                
                Outerloop:
                dec ecx
                mov esi, OFFSET array
                mov edi, 0
                
                Innerloop: 
                mov eax, [esi]
                mov ebx, [esi+4]
                cmp eax, ebx
                jle NoSwap
                
                ;swap elements
                mov[esi], ebx
                mov [esi+4], eax

                        NoSwap:
                add esi, 4
                add edi, 1
                cmp edi, ecx
                jl Innerloop
                
                cmp ecx,0
                jg Outerloop
                
                call Crlf
                mov edx, OFFSET sorted
                call WriteString
                call Crlf
                
                mov ecx, arraySize
                mov esi, OFFSET array
                
                Printloop:
                mov eax, [esi]
                call WriteDec
                call Crlf
                add esi, 4
                loop Printloop
                
                exit
                main ENDP
                END main
        
        
![Screenshot 2025-03-19 145955](https://github.com/user-attachments/assets/e1322fb6-df43-4597-87ce-f0396bd04a91)



        

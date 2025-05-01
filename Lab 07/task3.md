    INCLUDE Irvine32.inc

 
    ; Get values for the first array
    mov edx, OFFSET promptArray1
    call WriteString
    call Crlf
    mov esi, OFFSET array1
    mov ecx, ARRAY_SIZE
    call GetArrayValues
    
    ; Get values for the second array
    call Crlf
    mov edx, OFFSET promptArray2
    call WriteString
    call Crlf
    mov esi, OFFSET array2
    mov ecx, ARRAY_SIZE
    call GetArrayValues
    
    ; Calculate sum of first array
    mov esi, OFFSET array1
    call SumArray1
    
    ; Calculate sum of second array
    mov esi, OFFSET array2
    call SumArray2
    
    ; Add both sums
    call AddTotalSum
    
    ; Display results
    call DisplayResults
    
    exit
  


![image](https://github.com/user-attachments/assets/59630a29-cf8c-4527-98cd-620c2d20915e)


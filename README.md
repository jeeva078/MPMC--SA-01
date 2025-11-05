skill-assesment1
Write an assembly language program in 8086 to count the number of even and odd numbers in an array of 10 elements and display the counts.
Aim
To write an assembly language program in 8086 to count the number of even and odd numbers in an array of 10 elements and display the counts.

Algorithm
Step 1: Start
Initialize the data segment and code segment.

Step 2: Initialize registers
Set up the data segment.

Load the starting address of the array into a register (e.g., SI).

Load the number of elements (10) into a counter register (e.g., CX = 10).

Initialize two registers to zero for counting:

EVEN_COUNT = 0

ODD_COUNT = 0

Step 3: Access each array element
Read one element from the array using [SI].

Step 4: Check if the number is even or odd
Perform AND AL, 01H operation.

If the result = 0 → number is even

Else → number is odd

Step 5: Update counters
If even → increment EVEN_COUNT.

Else → increment ODD_COUNT.

Step 6: Move to next element
Increment SI to point to the next byte (or +2 if elements are words).

Decrement CX.

Repeat Steps 3–6 until CX = 0.

Step 7: Display the counts
Display the final values of EVEN_COUNT and ODD_COUNT using INT 21H (DOS interrupt).

Step 8: Stop
End the program using INT 21H (Function 4CH).

PROGRAM:
DATA SEGMENT
    ARR DB 07,08,05,04
    EVEN_COUNT DB 0
    ODD_COUNT  DB 0
    MSG1 DB 13,10,'Number of Even Numbers = $'
    MSG2 DB 13,10,'Number of Odd Numbers  = $'
DATA ENDS

CODE SEGMENT
ASSUME DS:DATA, CS:CODE

START:
    MOV AX, DATA
    MOV DS, AX

    MOV SI, OFFSET ARR
    MOV CX, 10

NEXT_NUM:
    MOV AL, [SI]
    MOV BL, AL
    AND BL, 01H
    CMP BL, 00H
    JZ EVEN_LABEL

ODD_LABEL:
    INC ODD_COUNT
    JMP CONTINUE

EVEN_LABEL:
    INC EVEN_COUNT

CONTINUE:
    INC SI
    LOOP NEXT_NUM

    ; ----- Display results -----
    MOV AH, 09H
    LEA DX, MSG1
    INT 21H

    MOV AL, EVEN_COUNT
    CALL DISP_NUM

    MOV AH, 09H
    LEA DX, MSG2
    INT 21H

    MOV AL, ODD_COUNT
    CALL DISP_NUM

    MOV AH, 4CH
    INT 21H

; ===== Subroutine to display number in AL =====
DISP_NUM PROC
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H
    RET
DISP_NUM ENDP

CODE ENDS
END 
output:

<img width="642" height="433" alt="Screenshot 2025-11-05 094822" src="https://github.com/user-attachments/assets/a81efc2c-7a6e-46ae-91d3-4035e9bc71e0" />


Result:
Hence the assembly language program in 8086 to count the number of even and odd numbers in an array of 10 elements and display the counts were verified.

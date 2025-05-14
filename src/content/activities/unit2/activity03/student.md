``` asm
@16 
M=1 
@17 
M=0 
@16 
D=M 
@100 
D=D-A 
@18 
D;JGT 
@16 
D=M 
@17 
M=D+M 
@16 
M=M+1
@4 
0;JMP
@18 
0;JMP
0;JMP
```
- En el ciclo while y for se aplica la misma estructura traducida a ensamblador 

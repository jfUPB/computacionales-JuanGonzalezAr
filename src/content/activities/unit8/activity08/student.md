``` asm
@5 
M=A 
D=M 
@10 
D=D-A 
@7 
D;JLT 
@1 
D=A 
@7 
M=D
```
Caso 1
``` asm
@5 
M=A 
D=M 
@10 
D=D-A 
@7 
D;JGE 
@1 
D=A 
@7 
M=D
```

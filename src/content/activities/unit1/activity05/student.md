# **Análisis del Ciclo Fetch-Decode-Execute en un Programa Hack**

## **Introducción**
Este documento detalla el ciclo **Fetch-Decode-Execute** para el programa en ensamblador Hack que **suma los números del 1 al 5** y almacena el resultado en la dirección de memoria `RAM[12]`.

---

## **Código en ensamblador Hack**  
```assembly
// Inicialización
@1  
M=A      // RAM[1] = 1  
@12  
M=0      // RAM[12] = 0  

// Inicio del ciclo
(LOOP)
@1  
D=M  
@5  
D=D-A  
@18  
D;JGT    // Si D > 0, salta a la línea 18 (finaliza)

@1  
D=M  
@12  
M=D+M    // RAM[12] = RAM[12] + RAM[1]  

@1  
M=M+1    // RAM[1] = RAM[1] + 1  
@4  
0;JMP    // Vuelve al inicio del ciclo  

// Fin del programa (bucle infinito)
(END)
@18  
0;JMP  
```

---

## **Tabla Fetch-Decode-Execute**  

| **Ciclo** | **PC (Contador de Programa)** | **Instrucción buscada** | **Decodificación** | **Ejecución** | **Valores finales (A, D, M)** |
|-----------|------------------------------|-------------------------|---------------------|---------------|------------------------------|
| 1         | 0                            | `@1`                    | A = 1              | Carga 1 en `A` | A = 1, D = ?, M = ?          |
| 2         | 1                            | `M=A`                   | RAM[1] = A         | RAM[1] = 1    | A = 1, D = ?, M[1] = 1       |
| 3         | 2                            | `@12`                   | A = 12             | Carga 12 en `A` | A = 12, D = ?, M[1] = 1     |
| 4         | 3                            | `M=0`                   | RAM[12] = 0        | Inicializa suma en RAM[12] | A = 12, D = ?, M[12] = 0 |
| 5         | 4                            | `@1`                    | A = 1              | Carga 1 en `A` | A = 1, D = ?, M[1] = 1       |
| 6         | 5                            | `D=M`                   | D = RAM[1]         | D = 1         | A = 1, D = 1, M[1] = 1       |
| 7         | 6                            | `@5`                    | A = 5              | Carga 5 en `A` | A = 5, D = 1, M[1] = 1       |
| 8         | 7                            | `D=D-A`                 | D = D - A          | D = 1 - 5 = -4 | A = 5, D = -4, M[1] = 1      |
| 9         | 8                            | `@18`                   | A = 18             | Carga 18 en `A` | A = 18, D = -4, M[1] = 1     |
| 10        | 9                            | `D;JGT`                 | Salta si D > 0     | No salta (D ≤ 0) | A = 18, D = -4, M[1] = 1    |
| 11        | 10                           | `@1`                    | A = 1              | Carga 1 en `A` | A = 1, D = -4, M[1] = 1      |
| 12        | 11                           | `D=M`                   | D = RAM[1]         | D = 1         | A = 1, D = 1, M[1] = 1       |
| 13        | 12                           | `@12`                   | A = 12             | Carga 12 en `A` | A = 12, D = 1, M[1] = 1      |
| 14        | 13                           | `M=D+M`                 | RAM[12] = D + M    | RAM[12] = 1   | A = 12, D = 1, M[12] = 1     |
| 15        | 14                           | `@1`                    | A = 1              | Carga 1 en `A` | A = 1, D = 1, M[12] = 1      |
| 16        | 15                           | `M=M+1`                 | RAM[1] = RAM[1] + 1 | RAM[1] = 2    | A = 1, D = 1, M[1] = 2       |
| 17        | 16                           | `@4`                    | A = 4              | Carga 4 en `A` | A = 4, D = 1, M[1] = 2       |
| 18        | 17                           | `0;JMP`                 | Salto incondicional | Salta a 4     | A = 4, D = 1, M[1] = 2       |

---

## **Resultado Final**  
El programa suma los números del **1 al 5** y almacena el resultado **15** en `RAM[12]`.  

### **Conclusión**  
- Se usa un **bucle** para sumar los valores del 1 al 5 y guardarlos en `RAM[12]`.  
- Una vez que `RAM[1] > 5`, el programa **termina** saltando a la dirección `@18`.  



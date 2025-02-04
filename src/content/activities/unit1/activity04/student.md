# **Tipos de Instrucciones en el Lenguaje Ensamblador Hack**  

## **1. ¿Cuál es la función de cada tipo de instrucción?**  

El lenguaje ensamblador Hack tiene **dos tipos de instrucciones**:  

### **A-instructions (Instrucciones de tipo A)**  
- Se usan para **cargar direcciones o valores numéricos en el registro A**.  
- Representan una dirección de memoria o un valor constante.  
- Su formato es: `@valor` (donde `valor` es un número o una etiqueta).  
- **Ejemplo:**  
  ```assembly
  @5  // Almacena el número 5 en el registro A
### **C-instructions (Instrucciones de tipo C)**  
Las C-instructions se usan para realizar **operaciones aritméticas, lógicas, almacenar valores o saltar a otra instrucción**.  

Contienen tres partes:  
- **comp (cálculo):** La operación que se ejecuta.  
- **dest (destino):** Dónde se guarda el resultado.  
- **jump (salto):** Opcional, indica si se debe saltar a otra línea del código.  
## **2. ¿Cómo se representa cada tipo de instrucción en binario?**

### **A-instruction:**
- Siempre comienza con `0`, seguido por un número binario de **15 bits** que representa la dirección o el valor.

#### **Formato en binario:**
0vvvvvvvvvvvvvvv
(donde `vvvvvvvvvvvvvvv` es el número en binario).

#### **Ejemplo:**
```assembly
@5  // Carga 5 en el registro A
```
- Binario: 0000000000000101
## **2. ¿Cómo se representa cada tipo de instrucción en binario?**

### **A-instruction:**
- Siempre comienza con `0`, seguido por un número binario de **15 bits** que representa la dirección o el valor.
#### **Formato en binario:**
0vvvvvvvvvvvvvvv
(donde `vvvvvvvvvvvvvvv` es el número en binario).
#### **Ejemplo:**
```assembly
@5  // Carga 5 en el registro A
Binario: 0000000000000101
```
### C-instruction:
- Siempre comienza con 111, seguido de los bits que representan la operación, destino y salto.
##### Formato en binario
**111accccccdddjjj**
- a → Define si el cálculo usa el registro A (0) o la memoria (1).
- ccccc → Código de la operación (comp).
- ddd → Código del destino (dest).
- jjj → Código del salto (jump).
## 3.Ejemplos:
- **A instructions:**
- @10 A=10 Binario: 0000000000001010
- @SCREEN A=16384 Binario: 0100000000000000
- @40 A=40 Binario: 101000
- **C instructions:**
- D=M  // D = RAM[A] Cargar en D el valor de la memoria apuntada por A
- D=D+A  // D = D + A Sumar D con A y almacenar el resultado en D
- D;JGT  // Si D > 0, saltar a la dirección A


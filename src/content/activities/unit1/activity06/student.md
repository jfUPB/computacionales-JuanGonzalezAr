### **Respuestas a las preguntas sobre memoria y direccionamiento en el computador Hack**

#### **1. ¿Qué es el direccionamiento directo? ¿Cómo se usa en el lenguaje ensamblador Hack?**  
El **direccionamiento directo** es un modo de acceso a la memoria en el que se especifica **directamente** la dirección de memoria a la que queremos acceder o modificar.
En el lenguaje ensamblador Hack, se utiliza la instrucción `@n` para acceder a la dirección `n` de la memoria RAM o ROM.  

#### **2. ¿Qué significa `M=D` en lenguaje ensamblador Hack? ¿Y `D=M`?**  

- **`M=D`**: Guarda el valor del registro `D` en la dirección de memoria apuntada por `A`.  
  - **Ejemplo:**  
    ```asm
    @12
    M=D  // Guarda en RAM[12] el valor actual de D
    ```
  - Si `D` tenía el valor `5`, ahora `RAM[12]` contendrá `5`.

- **`D=M`**: Carga en `D` el valor almacenado en la dirección de memoria apuntada por `A`.  
  - **Ejemplo:**  
    ```asm
    @20
    D=M  // Carga en D el valor almacenado en RAM[20]
    ```
  - Si `RAM[20]` tenía `8`, ahora `D` también tendrá `8`.
#### **3.Puntero**
Un puntero es una variable que almacena una dirección de memoria en lugar de un valor directo.
Esto significa que en lugar de guardar un número,
el puntero almacena dónde encontrar un número en la memoria.
En el computador Hack, podemos usar un puntero almacenando una dirección en una celda de memoria
y luego usándola para acceder dinámicamente a otras ubicaciones.
``` asm
@20
D=A   
@10
M=D
```

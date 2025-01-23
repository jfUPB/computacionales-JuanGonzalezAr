```
@1
D=A
@2
D=D+A
@16
M=D
@6
0;JMP
```
- Este es el primer codigo
- Este es el codigo con los cambios realizados
```
@60
D=A
@9
D=D+A
@6
M=D
@0
0;JMP
```
### **Cambios respecto al primer código:**

1. **Constantes diferentes:**
   - Se utilizan las constantes `60` y `9` en lugar de `1` y `2`. Esto cambia la operación de suma.  
     - **Primera suma:** `1 + 2 = 3` → **Nueva suma:** `60 + 9 = 69`.

2. **Cambio en posición de memoria:**
   - El resultado de la suma ahora se guarda en la posición de memoria `6` (antes se guardaba en la posición `16`).  
     - **Primera posición:** `RAM[16] = 3` → **Nueva posición:** `RAM[6] = 69`.

3. **Salto a dirección diferente:**
   - El salto incondicional (`0;JMP`) ahora redirige a la dirección `0` en lugar de la dirección `6`.  
     - **Primer salto:** va a `@6` → **Nuevo salto:** va a `@0`.

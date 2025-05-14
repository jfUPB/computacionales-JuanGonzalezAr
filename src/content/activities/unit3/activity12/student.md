## ✅ Act 12
### 🔹 ¿Compila?
- No, el primer código no compila porque pBloque2 se declara dentro de unas llaves {}, lo que significa que solo existe dentro de ese bloque.

- Cuando intentas usar pBloque2 después de que se cerró ese bloque, ya no es reconocida por el compilador, porque está fuera de su alcance (scope).

### 🔹 ¿Por qué pBloque se destruye al salir del bloque y pBloque2 no?
- pBloque es un objeto creado normalmente (no con puntero). Por eso, cuando el programa sale del bloque en el que fue declarado, se destruye automáticamente. Esto es porque está en la memoria de la pila (stack).

- En cambio, pBloque2 es un puntero que apunta a un objeto que fue creado con new. Aunque el puntero pBloque2 se elimina al salir del bloque (porque también está en el stack), el objeto que apuntaba sigue existiendo en la memoria dinámica (heap).

- Como fue creado con new, el objeto no se elimina solo. Es necesario usar delete pBloque2; para liberar esa memoria y evitar fugas.

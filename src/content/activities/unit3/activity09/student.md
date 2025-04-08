
# 🧠 Comparación de Copia de Objetos en C++ y C#

## 🔍 ¿Qué ocurre al copiar un objeto en C++?

En C++, cuando haces una copia de un objeto como:

```cpp
Punto copia = original;
```
Se crea una copia independiente del objeto. Esto se conoce como copia por valor. Los atributos como x, y y name se duplican en una nueva instancia de la clase Punto.
Modificar copia no afecta al objeto original, y viceversa.

✅ Resultado: La copia es completamente independiente.

🔍 ¿Qué ocurre al copiar un objeto en C#?
En C#, cuando haces una copia de un objeto con:

```c#

Punto copia = original;
```
Lo que está haciendo es copiar la referencia, no el objeto.
Es decir, tanto original como copia apuntan al mismo objeto en memoria. Si modificas uno, estás modificando el otro.

⚠️ Resultado: La "copia" no es una copia real del contenido, sino una referencia compartida al mismo objeto.

🧪 Conclusión

En C++, al copiar un objeto se genera una nueva instancia independiente, por lo que los cambios en la copia no afectan al original.

En C#, al copiar un objeto de una clase se comparte la referencia, por lo tanto cualquier cambio se ve reflejado también en el original.


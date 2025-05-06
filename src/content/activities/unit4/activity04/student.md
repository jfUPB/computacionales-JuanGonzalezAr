# 🎯 Actividad 4: Implementación de una Cola (FIFO)

## 🧠 Explicación Sencilla de una Cola (FIFO)

Imagina que estás en una fila para comprar boletos en el cine. El primero en llegar es el primero en ser atendido, y quienes llegan después se ubican al final.  
En programación, una **cola** funciona igual: se basa en el principio **FIFO** (First In, First Out), es decir, el primer elemento en entrar es el primero en salir.

---

## 🛠️ ¿Cómo Implementar una Cola Manualmente?

Una cola se puede construir usando **nodos** conectados entre sí, donde cada nodo contiene información y una referencia (puntero) al siguiente nodo.

---

## ➕ Agregar un Elemento al Final

Cuando se inserta un nuevo nodo en la cola:

- Se crea un nuevo nodo con los datos.
- Si la cola está vacía, este nodo se convierte en el `front` y también en el `rear`.
- Si la cola ya contiene nodos, el nuevo nodo se enlaza al final (`rear`) y se actualiza la referencia.

---

## ➖ Eliminar el Primer Elemento

Cuando se elimina un elemento:

- Se elimina el nodo ubicado en `front`, que es el más antiguo.
- Luego, `front` se actualiza para apuntar al siguiente nodo.
- Si la cola queda vacía, tanto `front` como `rear` deben pasar a ser `nullptr`.

---

## ⚠️ Error Común: Pérdida de Referencia (Memory Leak)

Un error frecuente al implementar colas es:

- Olvidar actualizar `front` después de eliminar un nodo.
- No liberar la memoria ocupada por el nodo eliminado.

---

## ✅ Cómo Evitarlo

Para evitar errores de memoria:

1. Guarda una referencia temporal al nodo que vas a eliminar.
2. Actualiza `front` para que apunte al siguiente nodo.
3. Libera correctamente la memoria del nodo anterior usando `delete`.

```cpp
Node* temp = front;
front = front->next;
delete temp;

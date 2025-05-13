# ACTIVIDAD 4

## Propósito del patrón State

El patrón State permite que un objeto cambie su comportamiento dependiendo de su estado interno, sin necesidad de usar muchos `if` o `switch`.  
Es útil cuando un objeto puede tener varios modos de funcionamiento que pueden cambiar en tiempo de ejecución.

En este caso, las partículas cambian su movimiento según el estado en el que estén: normal, atracción, repulsión o detenido.

---

## Diagrama explicado en palabras simples

La clase `Particle` es como una burbuja que puede estar en uno de estos cuatro estados:

- Normal
- Attract
- Repel
- Stop

Las transiciones entre estos estados se hacen al presionar teclas:

- Presionar `n` cambia al estado **Normal**
- Presionar `a` cambia al estado **Attract**
- Presionar `r` cambia al estado **Repel**
- Presionar `s` cambia al estado **Stop**

Cada estado es como un nodo en un diagrama, y las teclas son los disparadores que hacen que la partícula cambie de estado.

---

## Ventajas del patrón State frente a if/switch

- El código queda más limpio y fácil de entender.
- Cada estado tiene su propia clase y lógica, lo que mejora la organización.
- Es más fácil agregar nuevos estados sin modificar el código ya existente, lo cual sigue el principio abierto/cerrado.

Por ejemplo, si quiero agregar un estado llamado "Explode", solo debo crear una nueva clase sin tocar la clase `Particle`.

---

## Rol de onEnter y onExit

- `onEnter()` se ejecuta cuando una partícula entra a un nuevo estado. Se puede usar para preparar animaciones o guardar datos.
- `onExit()` se ejecuta al salir del estado. Se puede usar para limpiar variables o reiniciar configuraciones.

Aunque en este ejemplo no se usan mucho, son útiles para manejar transiciones entre estados de forma ordenada.

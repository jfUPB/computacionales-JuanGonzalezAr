


🔄 ¿Qué ocurre después de llamar a la función cambiarNombre?
Después de llamar a la función cambiarNombre (cuando recibe el parámetro por valor):

Se imprime el mensaje:

```css
Destructor: Punto cambiado(70, 80) destruido.
```
- Este mensaje indica que se ha destruido una copia del objeto original, no el original.

- ¿Por qué original sigue existiendo luego de llamar a cambiarNombre?
Porque la función cambiarNombre recibe su parámetro por valor.

- Esto significa que:

- Se crea una copia temporal del objeto original, llamada p.

- El atributo name de p se modifica.

- Pero no afecta al objeto original en main.

- Al terminar la función:

- La copia p es eliminada del stack.

- Se ejecuta su destructor, de ahí el mensaje de destrucción.

🧠 ¿En qué parte del mapa de memoria se encuentran original y p?
- 🟩 original
. Se encuentra en el stack de main(), ya que es una variable local.
- Sus atributos (name, x, y) también están en el stack.

- 🟨 p (en cambiarNombre)
- Es una copia de original.

- Sus atributos también están en el stack, pero son independientes.

- Cuando cambiarNombre termina:

- p se elimina.

- Se llama al destructor de p.

- ➡️ Por lo tanto, original y p no son el mismo objeto. Son objetos distintos con valores similares, pero completamente independientes en memoria.

- 🛠️ Cambio de la función cambiarNombre (uso de referencia)
- Si modificamos la función para que reciba una referencia:

```cpp
void cambiarNombre(Punto& p) {
    p.name = "cambiado";
}
```
- Ahora sí se modifica original:
- p ya no es una copia.

- En su lugar, almacena una referencia al objeto original.

- Modificar p.name equivale a modificar original.name.

- 🧪 Cambio en el main y el efecto de la nueva función
```cpp
Punto original("original", 70, 80);
cambiarNombre(original);
```
- ¿Qué ocurre ahora?
- p apunta a la misma dirección de memoria que original.

- Cuando cambiamos p.name, se está modificando directamente el objeto en main.

- Por eso, al imprimir original, su nombre ya es "cambiado".


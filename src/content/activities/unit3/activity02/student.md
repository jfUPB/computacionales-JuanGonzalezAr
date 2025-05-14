```c++
#include <iostream>

using namespace std;

// Función que modifica el parámetro pasado por valor
void swapPorValor(int a, int b) {
    cout << "Dentro de swapPorValor, valor inicial de a: " << a << "\nDentro de swapPorValor, valor inicial de b:" << b << endl;
    int c = a;
    a = b;
    b = c;
    cout << "Dentro de swapPorValor, valor modificado: " << a << "\nDentro de swapPorValor, valor modificado de b: " << b << endl;

}

// Función que modifica el parámetro pasado por referencia
void swapPorReferencia(int& a, int& b) {
    cout << "Dentro de swapPorReferencia, valor inicial: " << a << "\nDentro de swapPorReferencia, valor inicial: " << b << endl;
    int c = a;
    a = b;
    b = c;
    cout << "Dentro de swapPorReferencia, valor modificado: " << b << "\nDentro de swapPorReferencia, valor modificado: " << a << endl;
}

// Función que modifica el parámetro utilizando punteros
void swapPorPuntero(int* a, int* b) {
    cout << "Dentro de swapPorPuntero, valor inicial: " << *a << "\nDentro de swapPorPuntero, valor inicial: " << *b << endl;
    int c = *a;
    *a = *b;
    *b = c;
    cout << "Dentro de swapPorPuntero, valor modificado: " << *a << "\nDentro de swapPorPuntero, valor modificado: " << *b << endl;


}

int main() {
    int x = 5;
    int y = 10;

    cout << "\n### Prueba con swapPorValor ###" << endl;
    cout << "Valores iniciales: x = " << x << ", y = " << y << endl;
    swapPorValor(x, y);
    cout << "Después de swapPorValor en main: x = " << x << ", y = " << y << " (sin cambios)" << endl;

    // Reiniciar valores
    x = 5;
    y = 10;

    cout << "\n### Prueba con swapPorReferencia ###" << endl;
    cout << "Valores iniciales: x = " << x << ", y = " << y << endl;
    swapPorReferencia(x, y);
    cout << "Después de swapPorReferencia en main: x = " << x << ", y = " << y << " (intercambiados)" << endl;

    // Reiniciar valores
    x = 5;
    y = 10;

    cout << "\n### Prueba con swapPorPuntero ###" << endl;
    cout << "Valores iniciales: x = " << x << ", y = " << y << endl;
    swapPorPuntero(&x, &y);
    cout << "Después de swapPorPuntero en main: x = " << x << ", y = " << y << " (intercambiados)" << endl;

    return 0;
}
```
# 📌 Preguntas y Respuestas sobre `swapPorValor`, `swapPorReferencia` y `swapPorPuntero`

## **1️⃣ ¿Por qué la versión de `swapPorValor` no logra intercambiar los valores de `x` e `y` en `main()`?**
La función `swapPorValor(int a, int b)` recibe **copias** de `x` e `y` en `main()`.  
Esto significa que cualquier modificación dentro de la función **solo afecta a las copias** y no a las variables originales.  


---

## **2️⃣ ¿Cómo y por qué logran `swapPorReferencia` y `swapPorPuntero` modificar las variables originales?**

### 🔹 **`swapPorReferencia(int &a, int &b)`**
- Recibe `a` y `b` como **referencias** a `x` e `y`.
- Cualquier modificación en `a` y `b` **afecta directamente** a `x` e `y` en `main()`, ya que no se crean copias.
- Al salir de la función, los valores intercambiados **se mantienen**.

### 🔹 **`swapPorPuntero(int *a, int *b)`**
- Recibe **punteros** a `x` e `y`, es decir, las **direcciones de memoria** de estas variables.
- Se usa `*a` y `*b` para modificar los valores en la memoria original.
- Al salir de la función, los cambios se **mantienen en `x` e `y`**.


---

## **3️⃣ Ventajas y Consideraciones de Usar Referencias vs. Punteros**

| **Característica**        | **Referencias (`&`)** | **Punteros (`*`)** |
|--------------------------|------------------|------------------|
| **Facilidad de uso**      | Más simple y seguro | Más complejo pero flexible |
| **Obligación de inicializar** | Siempre debe inicializarse | Puede ser `nullptr` si no se asigna |
| **Modificabilidad**       | Modifica la variable original | Puede cambiar la dirección a la que apunta |
| **Sintaxis**             | Más limpia y fácil de leer | Requiere `*` y `&` para acceder a los valores |
| **Uso en memoria dinámica** | No se usa con `new` y `delete` | Es necesario para manejar memoria dinámica |



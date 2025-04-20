## Solution
```cpp
#include <iostream>
using namespace std;

class Personaje {
public:
    string nombre;
    int salud;
    static int totalPersonajes;

    // Constructor
    Personaje(string _nombre, int _salud) : nombre(_nombre), salud(_salud) {
        totalPersonajes++;
        cout << "Constructor: " << nombre << " creado con " << salud << " de salud." << endl;
    }

    // Destructor
    ~Personaje() {
        totalPersonajes--;
        cout << "Destructor: " << nombre << " destruido." << endl;
    }

    // Método
    void mostrar() {
        cout << "Personaje " << nombre << ", salud: " << salud << endl;
    }

    // Método que modifica salud por referencia
    void curar(Personaje& otro) {
        otro.salud += 10;
        cout << nombre << " ha curado a " << otro.nombre << endl;
    }

    // Método que no afecta al original (paso por valor)
    void daniar(Personaje enemigo) {
        enemigo.salud -= 10;
        cout << nombre << " ha dañado a una copia de " << enemigo.nombre << endl;
    }
};

// Inicialización de variable estática
int Personaje::totalPersonajes = 0;

int main() {
    // Objeto en el stack
    Personaje p1("Guerrero", 100);
    p1.mostrar();

    // Objeto en el heap
    Personaje* p2 = new Personaje("Hechicero", 80);
    p2->mostrar();

    // Paso por referencia (modifica)
    p1.curar(*p2);
    p2->mostrar();

    // Paso por valor (no modifica)
    p1.daniar(*p2);
    p2->mostrar();

    cout << "Total de personajes vivos: " << Personaje::totalPersonajes << endl;

    delete p2; // liberar heap
    cout << "Total de personajes vivos: " << Personaje::totalPersonajes << endl;

    return 0;
}
```
## Explicacion:
### 🧠 ¿Cómo se aplicó cada concepto?
- **Clases y objetos:** Se usa la clase Personaje con atributos y métodos. Se crean dos objetos: p1 y p2.

- **Paso de parámetros por valor y referencia:**

   - curar() recibe un objeto por referencia y lo modifica.

   - daniar() recibe una copia (por valor) y no modifica el original.

### Constructores y destructores:

- Se imprime un mensaje al crear y al destruir cada objeto.

### Métodos y atributos:

- mostrar(), curar() y daniar() son métodos que usan y modifican atributos.

### Objetos en stack y heap:

- p1 se crea en el stack.

- p2 se crea con new en el heap.

### Punteros y referencias:

- p2 es un puntero. Se usa *p2 para pasar la referencia.

### Variables estáticas:

- totalPersonajes cuenta cuántos personajes hay vivos.

### Depuración:

- Puedes usar breakpoints en cada constructor y destructor para seguir la vida de los objetos.

### 🧩 Análisis de memoria (explicado con palabras)
En este programa, el objeto p1 se crea directamente dentro del main, así que se almacena en la pila (stack). Eso significa que cuando el programa salga del main, p1 se eliminará automáticamente y se llamará a su destructor.

El objeto p2 se crea usando new, lo que quiere decir que vive en la memoria dinámica (heap). En este caso, p2 es solo un puntero que está en la pila, pero el objeto real al que apunta está en el heap. Como fue creado con new, no se destruye solo: por eso, usamos delete p2; para liberarlo manualmente.

La variable totalPersonajes es una variable estática, lo que significa que se guarda en una zona especial de memoria llamada data segment y solo existe una copia durante todo el programa, sin importar cuántos objetos de la clase Personaje se creen.

Cuando se llaman funciones como curar() o daniar(), los parámetros que se pasan (como el objeto otro) también se guardan temporalmente en el stack, ya que es ahí donde se guarda todo lo que se necesita durante una llamada a función.

Finalmente, los atributos como nombre y salud de cada personaje se almacenan junto con el objeto: si el objeto está en el stack, sus atributos también; si está en el heap, los atributos viven allí también.


![Img1](../../../../assets/Und5Act2(1).png)
- Un vector llamado particles almacenará punteros (Particle*) que apuntan a objetos creados dinámicamente, ya sean del tipo RisingParticle o de los distintos tipos de ExplosionParticle.

- A lo largo de la ejecución del programa, este vector irá creciendo al generarse nuevas partículas (por ejemplo, tras una explosión) y decreciendo cuando se eliminen las que ya no son necesarias.
---
### 🔍¿Qué puedes observar? ¿Qué información te proporciona el depurador? ¿Qué puedes concluir?
- Al usar el depurador, se puede observar que aunque un puntero esté declarado con el tipo de la clase base, el depurador identifica correctamente el tipo real (dinámico) del objeto al que apunta. Esto permite confirmar que se está ejecutando la versión adecuada del método, según la clase derivada correspondiente.
- ![Img1](../../../../assets/Und5Act2(2).png)
---
### ✅ ¿Qué puedes observar en la memoria? ¿Qué información te proporciona el depurador? ¿Qué puedes concluir?
- En la vista de memoria del depurador, es posible ver cómo están representados en binario los atributos internos de un objeto, como las direcciones de memoria, los datos de color, la posición, entre otros. También se puede identificar la dirección del puntero a la tabla virtual (vtable), que se usa para realizar llamadas dinámicas a métodos. Esta herramienta permite observar cómo se estructura un objeto en memoria, incluyendo tanto los atributos heredados de la clase base como los definidos en la clase derivada. Además, se puede comprobar que la organización en memoria respeta la jerarquía de herencia, empezando por los atributos de la clase base.
- ![Img1](../../../../assets/Und5Act2(2.).png)
- ![Img1](../../../../assets/Und5Act2(3).png)
---

### 🔍 Observa de nuevo ambas tablas y compara. ¿Qué puedes ver? ¿Qué puedes concluir? ¿Qué relación existe entre la tabla de funciones y los métodos virtuales?

Al revisar las tablas nuevamente, noto que cada clase (como `RisingParticle` o `StarExplosion`) posee su propia tabla de funciones virtuales (vtable), con direcciones únicas. Esto indica que cada tipo de objeto redefine sus métodos virtuales de forma particular.  
Cada subclase crea su propia vtable que apunta directamente a sus versiones sobrescritas de los métodos, permitiendo que el comportamiento se adapte al tipo específico de objeto.

**Conclusión:**  
Existe una conexión directa entre la vtable y los métodos virtuales. Son los métodos virtuales los que permiten que ocurra el polimorfismo en tiempo de ejecución.

---

### 🧩 Relación entre Métodos Virtuales y Polimorfismo

Los métodos virtuales son esenciales para que el polimorfismo funcione en lenguajes como C++ y C#.  
Gracias a ellos, podemos manejar varios objetos diferentes a través de un mismo puntero o referencia a la clase base. Aunque el tipo aparente sea el mismo, el comportamiento final depende del tipo real del objeto, lo que permite que cada uno responda con su versión particular del método.

---

### ⚠️ ¿Qué sucede?

Ocurren errores al intentar acceder directamente a ciertos atributos de objetos, especialmente si estos están protegidos o privados. Esto muestra que el lenguaje impone límites de acceso para proteger los datos.

---

### ✅ ¿Qué puedo concluir?

El **encapsulamiento** actúa como un mecanismo de protección para los datos internos de una clase.  
Esto permite:
- Evitar modificaciones accidentales desde fuera.
- Ocultar detalles innecesarios o delicados.
- Obligar a acceder a los datos a través de métodos públicos (como getters y setters).

Una buena analogía sería imaginar la clase como una caja fuerte:
- Lo público es accesible directamente.
- Lo protegido solo lo pueden ver las clases que heredan.
- Lo privado está completamente fuera del alcance externo.

---

## ⚙️ ¿Qué pasa al compilar y ejecutar?

El programa compila sin errores y funciona correctamente al imprimir los valores de los atributos privados.

**Importante:**  
El compilador bloquea el acceso directo a los campos privados durante la compilación. Sin embargo, mediante técnicas como `reinterpret_cast` y el uso de punteros, es posible llegar a esos datos en tiempo de ejecución.

Esto demuestra que el encapsulamiento en C++ es una **protección lógica**, no una barrera física en memoria.

---

## 🔐 ¿Qué es el encapsulamiento?

El **encapsulamiento** es uno de los pilares de la programación orientada a objetos.  
Consiste en ocultar la lógica interna de una clase y permitir el acceso solo a lo necesario a través de una interfaz pública.  
Se logra usando modificadores de acceso como `private`, `protected` y `public`.

---

## 🧬 ¿Cómo se implementa la herencia en C++?

La herencia en C++ permite que una clase (llamada derivada o hija) herede las propiedades y comportamientos de otra clase (llamada base o padre).  
Esto hace posible reutilizar código, especializar comportamientos y estructurar relaciones jerárquicas entre objetos.

---

## 🔄 ¿Qué relación hay entre métodos virtuales y polimorfismo?

Los métodos virtuales son lo que permite que el polimorfismo funcione.  
Cuando se define un método como `virtual`, el programa puede decidir en tiempo de ejecución cuál versión del método debe usar, dependiendo del tipo real del objeto.  
Esto es lo que permite que un mismo código se adapte y funcione con diferentes tipos de objetos de forma flexible.

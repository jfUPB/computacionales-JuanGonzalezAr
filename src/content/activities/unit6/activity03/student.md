# 🧩 ACTIVIDAD 3

## 🎯 Propósito del patrón Factory Method

El **Factory Method** permite centralizar la creación de objetos, separando ese proceso del resto del programa.  
🔧 **Problema que resuelve**: evita tener múltiples llamadas a `new` distribuidas por todo el código, lo que mejora el mantenimiento y la legibilidad.

---

## ✅ Ventajas de usar `ParticleFactory` en `ofApp::setup`

Utilizar `ParticleFactory` hace que el código en `ofApp` sea más limpio y enfocado.  
`ofApp` solo se encarga de **usar** las partículas, no de **crearlas ni configurarlas**, cumpliendo con el **principio de responsabilidad única (SRP)**.

Esto permite:
- Mejor organización del código.
- Facilidad para agregar nuevos tipos de partículas sin modificar `ofApp`.
- Reutilizar la fábrica desde otras partes del programa.

---

## ➕ Añadir el tipo de partícula `black_hole`

Para agregar una partícula llamada `black_hole`, solo se necesita modificar `ParticleFactory::createParticle`, agregando una condición para este nuevo tipo (por ejemplo, color negro, tamaño grande y velocidad lenta).

✅ **No es necesario tocar `ofApp::setup`**, ya que simplemente se solicita el nuevo tipo desde la fábrica.  
Esto demuestra la **flexibilidad del patrón Factory**, que permite extender funcionalidades sin modificar el código principal.

---

## ⚠️ Implicaciones de que `createParticle` sea estático

Hacer que `createParticle` sea un **método estático** es práctico porque se puede llamar sin crear una instancia de `ParticleFactory`.

🔽 **Ventajas**:
- Simplicidad en el uso.
- No requiere instancias.

🔼 **Desventajas**:
- No se puede heredar o sobreescribir fácilmente.
- No puede mantener estado interno (por ejemplo, contadores, configuraciones).

📌 Si se desea más flexibilidad o varias fábricas diferentes, es recomendable usar un **método de instancia** en lugar de uno estático.

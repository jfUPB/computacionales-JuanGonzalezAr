# 🧩 ACTIVIDAD 2

## ¿Para qué sirve el patrón Observer?

El patrón Observer permite que varios objetos reaccionen automáticamente a un evento, sin que el emisor necesite saber qué hacen.  
**🔧 Problema que resuelve**: evita el acoplamiento fuerte entre clases y hace que el programa sea más flexible y fácil de extender.

---

## ¿Quién es quién?

| Rol         | Descripción                                                                 |
|-------------|------------------------------------------------------------------------------|
| **Observer**        | Interfaz que define `onNotify()`                                                   |
| **Particle**        | Es un *ConcreteObserver*, implementa `onNotify()` y reacciona al evento            |
| **Subject**         | Tiene la lista de observadores y el método `notify()`                              |
| **ofApp**           | Es el *ConcreteSubject*, quien invoca `notify()` cuando ocurre un evento           |

```
       +-------------+
       |   Subject   |  <--- Clase base
       +-------------+
       | notify()    |
       | addObserver |
       +------^------+
              |
      Inheritance
              |
          +--------+
          | ofApp  |  <--- Emite eventos
          +--------+

              |
         notify("r")
              ↓
      +----------------+
      |   Observer     |  <--- Interfaz
      +----------------+
      | onNotify() = 0 |
              ↑
      Inheritance
              |
        +------------+
        | Particle   |  <--- Reacciona al evento
        +------------+
        | setState() |
```
---

## ¿Qué pasa cuando presiono `r`?

1. Se presiona la tecla `'r'`.
2. `ofApp::keyPressed()` llama a `notify("repel")`.
3. `notify()` ejecuta `onNotify("repel")` en cada `Particle`.
4. Cada partícula cambia su estado a `RepelState`.
5. En cada `update()`, las partículas se alejan del mouse con `RepelState::update()`.

---

## ✅ Ventajas del patrón Observer en este proyecto

- Organiza el código de forma más limpia.
- Es fácil agregar o quitar partículas.
- Permite manejar eventos sin depender directamente de los objetos.

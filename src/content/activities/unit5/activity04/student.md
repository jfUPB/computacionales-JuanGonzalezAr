# 🎯 Actividad 4:

### 🔐 Encapsulamiento
Se agrupan atributos y métodos dentro de cada clase y se protege el acceso directo desde fuera.  
**Ejemplo:**  
```cpp
class RisingParticle : public Particle {
protected:
    glm::vec2 position;
};
```
### 🧬 Herencia
Permite crear nuevas clases a partir de otras, reutilizando código y especializando comportamientos.
Ejemplo:

```cpp

class CircularExplosion : public ExplosionParticle { };
```
### 🌀 Polimorfismo
Permite usar punteros a la clase base para manejar distintos tipos de partículas y ejecutar sus métodos automáticamente.
Ejemplo:

```cpp

particles[i]->update(dt);
```
### 🧱 Objeto y Clase
Una clase es una plantilla; un objeto es una instancia real creada en memoria.
Ejemplo:

```cpp

particles.push_back(new RisingParticle(...));
```
### 🧠 Objeto con Herencia en Memoria
Un objeto derivado almacena primero los atributos de la clase base, luego los suyos, y puede incluir un puntero a la vtable.
```cpp
class CircularExplosion : public ExplosionParticle { };
```

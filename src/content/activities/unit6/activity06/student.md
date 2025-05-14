# Reflexión sobre el Proyecto: Uso de Patrones de Diseño

## Patrón Observer

- **Sujeto (Subject):**  
  Implementado en la clase `ofApp` con el método `notify` que envía eventos a las partículas.

```cpp
  void ofApp::notify(const std::string& event) {
      for (auto& p : particles) {
          p.onNotify(event);
      }
  }
```
### Observador (Observer):
- La clase Particle implementa el método onNotify para reaccionar a eventos.
### Eventos notificados:
- "attract", "stop", "normal" para cambiar el estado de las partículas.
- Se usó Observer para desacoplar el emisor (ofApp) de los receptores (partículas).

### Uso del patrón:
notify se llama en keyPressed, las partículas reaccionan en onNotify.
## Patrón Factory Method
### Método Factory:
- Tipos creados:
Partículas rápidas ("fast") y lentas ("slow") con diferentes velocidades y colores.

- Beneficios:
Centraliza la creación de partículas, facilita añadir nuevos tipos sin modificar ofApp.
## Patrón State
### Contexto:
- La clase Particle guarda el estado actual en currentState (string).

### Estados concretos:
- "normal" (movimiento libre) y "attract" (movimiento hacia mouse), "stop" (sin movimiento).

### Transiciones:
Ocurren en onNotify cuando Particle recibe eventos para cambiar estado.

### Justificación:
State permite separar comportamientos limpios sin condicionales dispersos.
Alternativa: muchos if en update(), más difícil de mantener.

### Definiciones Post-Experiencia
#### Clase:
- Plantilla o molde que define atributos y comportamientos de un tipo de objeto.

### Objeto:
- Instancia concreta de una clase con valores y estado propios.

### Beneficios Estructurales
- El uso de Observer, Factory y State ayudó a:

- Mantener el código modular y organizado.

- Facilitar la extensión (nuevos estados o tipos de partículas).

- Reducir el acoplamiento entre componentes.

- Mejorar la legibilidad y mantenimiento del proyecto

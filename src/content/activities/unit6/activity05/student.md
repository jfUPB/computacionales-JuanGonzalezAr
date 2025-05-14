### ofapp.h
```cpp
#pragma once
#include "ofMain.h"


class Observer {
public:
    virtual void onNotify(const std::string& event) = 0;
};


class Particle : public Observer {
public:
    ofVec2f pos, vel;
    ofColor color;
    std::string currentState;

    Particle();
    void update();
    void draw();
    void onNotify(const std::string& event) override;
};


class ParticleFactory {
public:
    static Particle createParticle(const std::string& type);
};

class ofApp : public ofBaseApp {
public:
    std::vector<Particle> particles;
    std::vector<Observer*> observers;

    void setup();
    void update();
    void draw();
    void keyPressed(int key);

    void notify(const std::string& event);
};

```
### ofApp.cpp
``` cpp
#include "ofApp.h"


Particle::Particle() {
    pos.set(ofRandomWidth(), ofRandomHeight());
    vel.set(ofRandom(-2, 2), ofRandom(-2, 2));
    color = ofColor::white;
    currentState = "normal";
}

void Particle::update() {
    if (currentState == "attract") {
        ofVec2f dir = ofVec2f(ofGetMouseX(), ofGetMouseY()) - pos;
        vel += dir.getNormalized() * 0.5;
        vel.limit(4);
    } else if (currentState == "stop") {
        vel.set(0, 0);
    }
    pos += vel;
}

void Particle::draw() {
    ofSetColor(color);
    ofDrawCircle(pos, 5);
}

void Particle::onNotify(const std::string& event) {
    currentState = event;
    if (event == "attract") color = ofColor::red;
    else if (event == "stop") color = ofColor::blue;
    else color = ofColor::white;
}


Particle ParticleFactory::createParticle(const std::string& type) {
    Particle p;
    if (type == "fast") {
        p.vel *= 2;
        p.color = ofColor::yellow;
    } else if (type == "slow") {
        p.vel *= 0.5;
        p.color = ofColor::green;
    }
    return p;
}


void ofApp::setup() {
    for (int i = 0; i < 50; i++) {
        Particle p = ParticleFactory::createParticle("fast");
        observers.push_back(&p);
        particles.push_back(p);
    }
}

void ofApp::update() {
    for (auto& p : particles) {
        p.update();
    }
}

void ofApp::draw() {
    for (auto& p : particles) {
        p.draw();
    }
}

void ofApp::keyPressed(int key) {
    if (key == 'a') notify("attract");
    else if (key == 's') notify("stop");
    else if (key == 'n') notify("normal");
}

void ofApp::notify(const std::string& event) {
    for (auto& p : particles) {
        p.onNotify(event);
    }
}
```

# Proyecto de Arte Generativo Interactivo en openFrameworks

## Descripción del Proyecto

Este proyecto crea un sistema simple de partículas que cambian su comportamiento dinámicamente según el estado seleccionado por el usuario a través del teclado. Las partículas pueden:

- Moverse libremente (estado *normal*).
- Ser atraídas hacia el cursor del mouse (estado *attract*).
- Detenerse completamente (estado *stop*).

Se implementan los patrones de diseño **Observer**, **Factory Method** y **State** para estructurar el código y permitir escalabilidad y mantenimiento.

---

## Patrones Implementados

### 1. Patrón Observer

- **Rol Sujeto (Subject)**: La clase `ofApp` actúa como sujeto notificando eventos.
- **Rol Observador (Observer)**: Cada partícula implementa la interfaz `Observer` y reacciona a cambios de estado con el método `onNotify`.
- **Eventos Notificados**: Cambios de estado global como `"attract"`, `"stop"` y `"normal"`.
- **Ventaja**: Permite desacoplar la lógica de notificación y reacción, facilitando que múltiples partículas respondan independientemente.

### 2. Patrón Factory Method

- **Factory**: `ParticleFactory` genera partículas con diferentes propiedades (velocidad rápida o lenta, color distinto).
- **Beneficio**: Centraliza la creación de objetos, mejorando la legibilidad y facilitando la extensión del código sin modificar las partes que usan las partículas.
- **Uso**: En `setup()`, se crean partículas usando la fábrica para inicializar la colección de partículas.

### 3. Patrón State

- **Contexto**: Cada `Particle` mantiene su estado actual como una cadena (`currentState`).
- **Estados Concretos**: `"normal"`, `"attract"` y `"stop"`.
- **Transiciones**: Desencadenadas por eventos de teclado, modificando el comportamiento de movimiento y color de las partículas.
- **Ventaja**: Facilita modificar el comportamiento dinámicamente sin saturar el código con condicionales complejos.

---

## Integración

- La clase `ofApp` maneja la colección de partículas y distribuye eventos usando `notify`.
- Las partículas reciben estas notificaciones y cambian su comportamiento (estado).
- El patrón Factory se usa para crear partículas iniciales con diferentes características.
- El patrón State regula cómo se comporta cada partícula en cada ciclo de actualización.

---

## Desafíos y Consideraciones

- **Sincronización**: Mantener la lista de observadores actualizada con la lista de partículas es clave para evitar errores.
- **Escalabilidad**: Aunque el proyecto es simple, al crecer la cantidad y tipos de partículas, la implementación actual puede requerir separación en múltiples archivos y clases.
- **Estado representado como cadena**: Usar strings es sencillo pero menos eficiente que usar clases de estado, lo cual sería una mejora futura.
- **Depuración**: Verificar que las partículas reaccionan correctamente a las notificaciones fue fundamental para asegurar la correcta integración del patrón Observer.

---

## Conclusión

Este proyecto demuestra cómo los patrones de diseño pueden organizar código para un sistema interactivo complejo, facilitando la extensión y mantenimiento. El uso de Observer, Factory y State permitió manejar eventos globales, crear objetos flexibles y adaptar comportamientos en tiempo real con claridad y eficiencia.

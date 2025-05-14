### ofapp.h
```cpp
#pragma once
#include "ofMain.h"

class ofApp : public ofBaseApp {
public:
    std::vector<ofVec2f> positions;
    std::vector<ofVec2f> velocities;
    std::vector<ofColor> colors;
    std::string currentState;

    void setup();
    void update();
    void draw();
    void keyPressed(int key);

    void changeState(const std::string& state);
};
```
### ofApp.cpp
``` cpp
#include "ofApp.h"

void ofApp::setup() {
    for (int i = 0; i < 50; i++) {
        positions.push_back(ofVec2f(ofRandomWidth(), ofRandomHeight()));
        velocities.push_back(ofVec2f(ofRandom(-2, 2), ofRandom(-2, 2)));
        colors.push_back(ofColor::white);
    }
    currentState = "normal";
}

void ofApp::update() {
    for (size_t i = 0; i < positions.size(); i++) {
        if (currentState == "normal") {
            // Movimiento libre
        } else if (currentState == "attract") {
            ofVec2f dir = ofVec2f(ofGetMouseX(), ofGetMouseY()) - positions[i];
            velocities[i] += dir.getNormalized() * 0.5;
            velocities[i].limit(4);
        } else if (currentState == "stop") {
            velocities[i].set(0, 0);
        }
        positions[i] += velocities[i];
    }
}

void ofApp::draw() {
    for (size_t i = 0; i < positions.size(); i++) {
        ofSetColor(colors[i]);
        ofDrawCircle(positions[i], 5);
    }
}

void ofApp::keyPressed(int key) {
    if (key == 'a') changeState("attract");
    else if (key == 's') changeState("stop");
    else if (key == 'n') changeState("normal");
}

void ofApp::changeState(const std::string& state) {
    currentState = state;
    if (state == "attract") {
        for (auto& c : colors) c = ofColor::red;
    } else if (state == "stop") {
        for (auto& c : colors) c = ofColor::blue;
    } else {
        for (auto& c : colors) c = ofColor::white;
    }
}
```

# Proyecto de Arte Generativo con Partículas en openFrameworks

##  Descripción general

Este proyecto consiste en un sistema de partículas que cambian su comportamiento dinámicamente según el estado seleccionado mediante teclado. Las partículas pueden moverse libremente, ser atraídas al cursor o detenerse por completo. Todo se desarrolla usando únicamente dos archivos (`ofApp.h` y `ofApp.cpp`), ideal para prototipado rápido.

##  Patrones implementados

### 1. **Patrón State (Estado)**
- Las partículas cambian su comportamiento dinámicamente dependiendo del estado actual: `"normal"`, `"attract"`, o `"stop"`.
- El estado se almacena como una cadena (`currentState`) y se usa para modificar la lógica de movimiento y color en `update()` y `changeState()`.



---

## Integración de conceptos

- Todo el proyecto está centralizado en la clase `ofApp`, que contiene el estado actual, la lógica de entrada, actualización y renderizado.
- Al presionar teclas:
  - `'a'` cambia el estado a **attract**, donde las partículas se mueven hacia el mouse.
  - `'s'` cambia el estado a **stop**, donde las partículas se detienen.
  - `'n'` regresa al estado **normal**, con movimiento libre.
- Los colores de las partículas se actualizan según el estado, dando retroalimentación visual inmediata.

---

##  Objetivos de aprendizaje

- Aplicar programación orientada a objetos básica.
- Simular estados dinámicos sin usar estructuras complejas.
- Trabajar con vectores de posición, velocidad y color.
- Implementar control de estado con interacción del teclado.

---

##  Posibles desafíos

| Desafío                         | Descripción                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| Manejo de vectores dinámicos     | Es necesario mantener sincronía entre `positions`, `velocities` y `colors`. |
| Comprensión del ciclo update/draw| El flujo de `update()` y `draw()` en openFrameworks puede confundir al inicio. |
| Implementar cambios suaves       | Cambiar entre estados abruptamente puede generar movimientos bruscos.       |


---

## 💡 Idea de extensión

- Añadir más estados como "explosión", "rebote", etc.
- Integrar una interfaz gráfica con `ofxGui` para cambiar de estado visualmente.
- Guardar trazos para crear arte generativo más complejo.


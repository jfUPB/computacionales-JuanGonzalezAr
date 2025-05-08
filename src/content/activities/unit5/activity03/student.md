### ofapp.cpp
```cpp
#include "ofApp.h"

// --------------------------------------------------------------
void ofApp::setup() {
    ofSetFrameRate(60);
    ofBackground(0);
}

// --------------------------------------------------------------
void ofApp::update() {
    float dt = ofGetLastFrameTime();

    // Actualiza todas las partículas
    for (int i = 0; i < particles.size(); i++) {
        particles[i]->update(dt);
    }

    // Procesa las partículas (iteración en reversa para facilitar eliminación)
    for (int i = particles.size() - 1; i >= 0; i--) {
        // Si la partícula debe explotar, generamos nuevas explosiones
        if (particles[i]->shouldExplode()) {
            int explosionType = (int)ofRandom(4); // 0: Circular, 1: Random, 2: Star, 3: Spiral
            int numParticles = (int)ofRandom(20, 30);
            for (int j = 0; j < numParticles; j++) {
                if (explosionType == 0) {
                    particles.push_back(new CircularExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
                else if (explosionType == 1) {
                    particles.push_back(new RandomExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
                else if (explosionType == 2) {
                    particles.push_back(new StarExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
                else {
                    particles.push_back(new SpiralExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
            }
            delete particles[i];
            particles.erase(particles.begin() + i);
        }
        else if (particles[i]->isDead()) {
            delete particles[i];
            particles.erase(particles.begin() + i);
        }
    }
}

// --------------------------------------------------------------
void ofApp::draw() {
    for (int i = 0; i < particles.size(); i++) {
        particles[i]->draw();
    }
}

// --------------------------------------------------------------
void ofApp::createRisingParticle() {
    float minX = ofGetWidth() * 0.35;
    float maxX = ofGetWidth() * 0.65;
    float spawnX = ofRandom(minX, maxX);
    glm::vec2 pos(spawnX, ofGetHeight());
    glm::vec2 target(ofGetWidth() / 2 + ofRandom(-300, 300), ofGetHeight() * 0.10 + ofRandom(-30, 30));
    glm::vec2 direction = glm::normalize(target - pos);
    glm::vec2 vel = direction * ofRandom(250, 350);
    ofColor col;
    col.setHsb(ofRandom(255), 220, 255);
    float lifetime = ofRandom(1.5, 3.5);
    particles.push_back(new RisingParticle(pos, vel, col, lifetime));
}

void ofApp::createFallingParticle() {
    float spawnX = ofRandom(0, ofGetWidth());
    glm::vec2 pos(spawnX, 0);  // Nace en la parte superior
    glm::vec2 vel(0, ofRandom(150, 300));  // Caída vertical
    ofColor col;
    col.setHsb(ofRandom(255), 220, 255);
    float lifetime = ofRandom(1.5, 3.5);
    particles.push_back(new FallingParticle(pos, vel, col, lifetime));
}

void ofApp::createHorizontalParticle() {
    float spawnY = ofRandom(0, ofGetHeight());
    glm::vec2 pos(0, spawnY);  // Nace en el lado izquierdo
    glm::vec2 vel(ofRandom(150, 300), 0);  // Movimiento horizontal
    ofColor col;
    col.setHsb(ofRandom(255), 220, 255);
    float lifetime = ofRandom(1.5, 3.5);
    particles.push_back(new HorizontalParticle(pos, vel, col, lifetime));
}

// --------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button) {
    createRisingParticle();
}

// --------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == ' ') {
        for (int i = 0; i < 1000; i++) {
            createRisingParticle();
        }
    }
    if (key == 'f') {
        createFallingParticle();
    }
    if (key == 'h') {
        createHorizontalParticle();
    }
    if (key == 's') {
        ofSaveScreen("screenshot_" + ofToString(ofGetFrameNum()) + ".png");
    }
}

// --------------------------------------------------------------
ofApp::~ofApp() {
    for (int i = 0; i < particles.size(); i++) {
        delete particles[i];
    }
    particles.clear();
}
```
### ofapp.h
```cpp
#include "ofApp.h"

// --------------------------------------------------------------
void ofApp::setup() {
    ofSetFrameRate(60);
    ofBackground(0);
}

// --------------------------------------------------------------
void ofApp::update() {
    float dt = ofGetLastFrameTime();

    // Actualiza todas las partículas
    for (int i = 0; i < particles.size(); i++) {
        particles[i]->update(dt);
    }

    // Procesa las partículas (iteración en reversa para facilitar eliminación)
    for (int i = particles.size() - 1; i >= 0; i--) {
        // Si la partícula debe explotar, generamos nuevas explosiones
        if (particles[i]->shouldExplode()) {
            int explosionType = (int)ofRandom(4); // 0: Circular, 1: Random, 2: Star, 3: Spiral
            int numParticles = (int)ofRandom(20, 30);
            for (int j = 0; j < numParticles; j++) {
                if (explosionType == 0) {
                    particles.push_back(new CircularExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
                else if (explosionType == 1) {
                    particles.push_back(new RandomExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
                else if (explosionType == 2) {
                    particles.push_back(new StarExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
                else {
                    particles.push_back(new SpiralExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
            }
            delete particles[i];
            particles.erase(particles.begin() + i);
        }
        else if (particles[i]->isDead()) {
            delete particles[i];
            particles.erase(particles.begin() + i);
        }
    }
}

// --------------------------------------------------------------
void ofApp::draw() {
    for (int i = 0; i < particles.size(); i++) {
        particles[i]->draw();
    }
}

// --------------------------------------------------------------
void ofApp::createRisingParticle() {
    float minX = ofGetWidth() * 0.35;
    float maxX = ofGetWidth() * 0.65;
    float spawnX = ofRandom(minX, maxX);
    glm::vec2 pos(spawnX, ofGetHeight());
    glm::vec2 target(ofGetWidth() / 2 + ofRandom(-300, 300), ofGetHeight() * 0.10 + ofRandom(-30, 30));
    glm::vec2 direction = glm::normalize(target - pos);
    glm::vec2 vel = direction * ofRandom(250, 350);
    ofColor col;
    col.setHsb(ofRandom(255), 220, 255);
    float lifetime = ofRandom(1.5, 3.5);
    particles.push_back(new RisingParticle(pos, vel, col, lifetime));
}

void ofApp::createFallingParticle() {
    float spawnX = ofRandom(0, ofGetWidth());
    glm::vec2 pos(spawnX, 0);  // Nace en la parte superior
    glm::vec2 vel(0, ofRandom(150, 300));  // Caída vertical
    ofColor col;
    col.setHsb(ofRandom(255), 220, 255);
    float lifetime = ofRandom(1.5, 3.5);
    particles.push_back(new FallingParticle(pos, vel, col, lifetime));
}

void ofApp::createHorizontalParticle() {
    float spawnY = ofRandom(0, ofGetHeight());
    glm::vec2 pos(0, spawnY);  // Nace en el lado izquierdo
    glm::vec2 vel(ofRandom(150, 300), 0);  // Movimiento horizontal
    ofColor col;
    col.setHsb(ofRandom(255), 220, 255);
    float lifetime = ofRandom(1.5, 3.5);
    particles.push_back(new HorizontalParticle(pos, vel, col, lifetime));
}

// --------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button) {
    createRisingParticle();
}

// --------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == ' ') {
        for (int i = 0; i < 1000; i++) {
            createRisingParticle();
        }
    }
    if (key == 'f') {
        createFallingParticle();
    }
    if (key == 'h') {
        createHorizontalParticle();
    }
    if (key == 's') {
        ofSaveScreen("screenshot_" + ofToString(ofGetFrameNum()) + ".png");
    }
}

// --------------------------------------------------------------
ofApp::~ofApp() {
    for (int i = 0; i < particles.size(); i++) {
        delete particles[i];
    }
    particles.clear();
}
```
### Capturas de pantalla





# ✅ Registro de pruebas de simulación de partículas

## 🔹 Prueba 1: Movimiento según tipo de partícula

**🔸 Lo que quería verificar:**  
Quería confirmar que cada tipo de partícula se moviera como corresponde: ascendiendo, cayendo o desplazándose en horizontal.

**🔸 Resultado esperado:**  
Esperaba que las partículas se comportaran según su tipo y que se eliminaran automáticamente al finalizar su ciclo de vida o salir de la pantalla.

**🔸 Resultado obtenido:**  
Todo funcionó como esperaba: la `RisingParticle` subió, la `FallingParticle` bajó, y la `HorizontalParticle` se movió lateralmente. Las partículas desaparecieron correctamente cuando correspondía.

**🔸 Correcciones necesarias:**  
No fue necesario hacer ajustes, el comportamiento fue el esperado desde el inicio.

---

## 🔹 Prueba 2: Explosión en espiral (SpiralExplosion)

**🔸 Lo que quería verificar:**  
Quería observar que las partículas de la explosión en espiral siguieran una trayectoria curva y coherente, alejándose del centro de forma fluida.

**🔸 Resultado esperado:**  
Esperaba un patrón de movimiento en espiral con desplazamiento continuo desde el centro de la explosión.

**🔸 Resultado obtenido:**  
El comportamiento fue correcto: las partículas se desplazaron en una espiral clara y coherente.

**🔸 Correcciones necesarias:**  
No fue necesario realizar cambios, funcionó como se planeó.

---

## 🔹 Prueba 3: Eliminación de partículas tras la explosión

**🔸 Lo que quería verificar:**  
Quería asegurarme de que las partículas se eliminaran automáticamente cuando finalizara su vida útil o después de una explosión.

**🔸 Resultado esperado:**  
Esperaba que las partículas se eliminaran solas sin necesidad de intervención manual.

**🔸 Resultado obtenido:**  
Las partículas se eliminaron correctamente al terminar su ciclo de vida o al explotar, como se esperaba.

**🔸 Correcciones necesarias:**  
No fue necesario hacer ninguna corrección.

---

## 🔹 Prueba 4: Generación de partículas con teclas

**🔸 Lo que quería verificar:**  
Probé que las teclas asignadas funcionaran correctamente para generar distintos tipos de partículas (`f`, `h` y barra espaciadora).

**🔸 Resultado esperado:**  
Esperaba que cada tecla generara la partícula adecuada: caída, horizontal o ascendente.

**🔸 Resultado obtenido:**  
Las teclas funcionaron sin problemas: `f` generó partículas en caída, `h` las horizontales, y la barra espaciadora generó partículas que subían.

**🔸 Correcciones necesarias:**  
Todo funcionó correctamente, no fue necesario modificar nada.

---

## 🔹 Prueba 5: Uso del depurador para inspección

**🔸 Lo que quería verificar:**  
Quería confirmar que el depurador de Visual Studio me permitiera inspeccionar las propiedades internas de las partículas durante la ejecución.

**🔸 Resultado esperado:**  
Esperaba poder detener la simulación y revisar detalles como posición, velocidad, color y vida útil de cada partícula.

**🔸 Resultado obtenido:**  
El depurador funcionó perfectamente: pude observar los valores internos de cada partícula y comprobar que se actualizaban y eliminaban como debía ser.

**🔸 Correcciones necesarias:**  
Ninguna corrección fue necesaria; el depurador cumplió con su función.


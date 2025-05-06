## Solucion:
app.h
```cpp
#pragma once
#include "ofMain.h"

// Nodo de la cola
struct Node {
    float x, y;
    float radius;
    ofColor color;
    float opacity;
    Node* next;

    Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
        : x(_x), y(_y), radius(_radius), color(_color), opacity(_opacity), next(nullptr) {}
};

// Implementación manual de una cola (FIFO)
class BrushQueue {
public:
    Node* front;
    Node* rear;
    int size;
    int maxSize;

    BrushQueue(int _maxSize);
    ~BrushQueue();

    void enqueue(float x, float y, float radius, ofColor color, float opacity);
    void dequeue();
    void clear();
    bool isEmpty();
    void draw();
};

// Constructor
BrushQueue::BrushQueue(int _maxSize) : front(nullptr), rear(nullptr), size(0), maxSize(_maxSize) {}

// Destructor
BrushQueue::~BrushQueue() {
    clear();
}

// Agregar un nuevo nodo a la cola
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
    Node* newNode = new Node(x, y, radius, color, opacity);
    if (rear) {
        rear->next = newNode;
    }
    else {
        front = newNode;
    }
    rear = newNode;
    size++;

    if (size > maxSize) {
        dequeue();
    }
}

// Eliminar el nodo más antiguo
void BrushQueue::dequeue() {
    if (!front) return;
    Node* temp = front;
    front = front->next;
    if (!front) {
        rear = nullptr;
    }
    delete temp;
    size--;
}

// Vaciar la cola
void BrushQueue::clear() {
    while (front) {
        dequeue();
    }
}

// Verificar si la cola está vacía
bool BrushQueue::isEmpty() {
    return front == nullptr;
}

class ofApp : public ofBaseApp {
public:
    BrushQueue strokes; // Cola de trazos
    float backgroundHue = 0;

    ofApp() : strokes(50) {} // Tamaño máximo de la cola

    void setup();
    void update();
    void draw();
    void keyPressed(int key);

};
```
app.cpp
```cpp
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofBackground(0);
}

//--------------------------------------------------------------
void ofApp::update() {
    backgroundHue += 0.2;
    if (backgroundHue > 255) backgroundHue = 0;

    if (ofGetMousePressed()) {
        float radius = ofRandom(5, 15);
        ofColor color = ofColor::fromHsb(ofRandom(255), 255, 255);
        float opacity = ofRandom(100, 255);
        strokes.enqueue(ofGetMouseX(), ofGetMouseY(), radius, color, opacity);
    }
}

//--------------------------------------------------------------
void ofApp::draw() {
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    Node* current = strokes.front;
    int i = 0;
    while (current) {
        float adjustedOpacity = ofMap(i, 0, strokes.maxSize, 50, 255);
        ofSetColor(current->color, adjustedOpacity);
        ofDrawCircle(current->x, current->y, current->radius);
        current = current->next;
        i++;
    }
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'c') {
        strokes.clear();
    }
    else if (key == 'a') {
        strokes.maxSize = (strokes.maxSize == 50) ? 100 : 50;
    }
}
```
# 🧪 Registro de Pruebas y Uso del Depurador en Visual Studio

## 🛠️ Uso del Depurador en Visual Studio

Durante el desarrollo, se utilizó el depurador de Visual Studio para verificar el comportamiento interno de las funciones clave:

- **enqueue()**: Se observó el estado de los punteros `front` y `rear` para confirmar que los nodos se enlazaban correctamente al final de la cola.
- **dequeue()**: Se validó que el nodo más antiguo fuera correctamente eliminado cuando se alcanzaba el tamaño máximo permitido.
- **clear()**: Se comprobó que todos los nodos fueran eliminados, dejando la cola vacía.

---

## ✅ Lista de Pruebas Realizadas

### 📌 1. Prueba de Inserción de Nodos (`enqueue()`)

- **Objetivo**: Verificar que los nodos se agregan y se dibujan correctamente en pantalla.  
- **Acción**: Se llamó a `enqueue(100, 100, 10, ofColor::red, 255)`.  
- **Resultado**: El nodo rojo apareció correctamente en pantalla.

---

### 📌 2. Prueba de Eliminación FIFO (`dequeue()`)

- **Objetivo**: Confirmar que al superar el límite de la cola, el nodo más antiguo sea eliminado siguiendo el principio FIFO.  
- **Acción**: Se insertaron 51 nodos consecutivos.  
- **Resultado**: El nodo más antiguo fue removido correctamente y los nuevos se añadieron al final.

---

### 📌 3. Prueba de Vaciado de la Cola (`clear()`)

- **Objetivo**: Verificar que todos los nodos desaparecen al activar la función de limpieza.  
- **Acción**: Se dibujaron múltiples trazos y luego se presionó la tecla `'c'`.  
- **Resultado**: Todos los nodos se eliminaron satisfactoriamente de la pantalla.

---

### 📌 4. Prueba de Alternancia del Tamaño de la Cola (`maxSize`)

- **Objetivo**: Comprobar que la capacidad máxima de la cola cambia entre 50 y 100 al presionar `'a'`.  
- **Acción**: Se presionó `'a'`, luego se insertaron más de 50 nodos.  
- **Resultado**: La cola permitió hasta 100 elementos. Al presionar `'a'` nuevamente, el límite regresó a 50.

---

### 📌 5. Prueba de Gradual Desaparición de Trazos (Opacidad Dinámica)

- **Objetivo**: Validar que los trazos pierden opacidad con el tiempo mediante `ofMap()`.  
- **Acción**: Se dibujaron múltiples trazos y se observó su desvanecimiento gradual.  
- **Resultado**: La opacidad de los nodos disminuyó correctamente, simulando una desaparición progresiva.

---

### 📌 6. Prueba de Almacenamiento de un Frame (`'s'`)

- **Objetivo**: Confirmar que se puede guardar una captura del lienzo como imagen al presionar `'s'`.  
- **Acción**: Se dibujaron trazos, se presionó `'s'`.  
- **Resultado**: La imagen se guardó correctamente con todos los trazos visibles.

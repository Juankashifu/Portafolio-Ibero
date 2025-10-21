# 📚 Práctica 3: "Blink" (Parpadeo Básico de LED)

> El "Hola, Mundo" del hardware. Este proyecto es el primer paso esencial para verificar que el microcontrolador (ESP32) puede ejecutar código y controlar un actuador simple.

---

## 1) Resumen

- **Autor:** Juan Carlos Valdés Pérez
- **Asignatura:** Introducción a la Mecatrónica
- **Fecha:** 12/09/2025
- **Plataforma:** ESP32
- **Descripción breve:** Programa básico que hace parpadear un LED (encender y apagar) a intervalos de un segundo para demostrar el control de un pin de salida digital y el uso de temporizadores (`delay`).

---

## 2) Objetivo del Proyecto

El objetivo es dominar los tres comandos más fundamentales de la programación de microcontroladores:

1.  **`pinMode(PIN, OUTPUT)`:** Establecer un pin específico como una salida de voltaje.
2.  **`digitalWrite(PIN, HIGH/LOW)`:** Enviar voltaje (encender el LED) o quitarlo (apagar el LED).
3.  **`delay(ms)`:** Crear pausas en la ejecución del programa para controlar el tiempo del parpadeo.

---

## 3) Componentes y Requisitos

**Hardware**
- Microcontrolador ESP32
- 1 LED (cualquier color)
- 1 Resistencia de 220 Ohms (para proteger el LED)
- Protoboard y Jumpers (cables)

**Software**
- Arduino IDE
- Lenguaje de programación: C++

---

## 4) Desafíos Clave y Aprendizajes

**Desafío:**
Aunque es un programa simple, el desafío inicial es asegurarse de que el LED esté conectado en la polaridad correcta (la "pata" larga o ánodo al pin digital, y la corta o cátodo a tierra/GND) y que la resistencia sea la adecuada para no quemar el LED.

**Aprendizaje:**
Este proyecto solidifica la comprensión del **"flujo de control"** de un programa. Entendí que el código dentro del `void loop()` se ejecuta en secuencia (línea por línea) y se repite infinitamente.

Mi aprendizaje más importante fue entender que **`delay()` es una función "bloqueante"**: mientras el `delay(1000)` está activo, el ESP32 se detiene por completo y no puede hacer nada más (como leer un botón) durante ese segundo. Esto es crucial para entender por qué en proyectos más avanzados se deben usar otros métodos de temporización.

---

## 5) Código Clave

Este es el código completo que se carga en el ESP32 para lograr el parpadeo.

```bash
// Define el pin donde está conectado el LED
// (Puedes cambiar '12' al pin que hayas usado, ej: 2, 4, 13, etc.)
byte ledPin = 12; 

void setup() {
  // Configura el pin del LED como una SALIDA
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // 1. Enciende el LED (pone el pin en ALTO)
  digitalWrite(ledPin, HIGH);
  
  // 2. Espera 1 segundo (1000 milisegundos)
  delay(1000);
  
  // 3. Apaga el LED (pone el pin en BAJO)
  digitalWrite(ledPin, LOW);
  
  // 4. Espera 1 segundo
  delay(1000);
  
  // (El loop se repite desde el inicio)
}


```

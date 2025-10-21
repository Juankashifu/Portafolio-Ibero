# 📚 Actividad1: ESP32 - Control de Salida Digital (LED Blink)

## 1) Resumen

-   **Nombre del proyecto:** `ESP32 - Control de Salida Digital (Blink)`
-   **Autor:** _(Tu Nombre)_
-   **Asignatura:** _(Tu Asignatura, ej: Taller de Introducción a la Mecatrónica)_
-   **Fecha:** _(Fecha de Hoy)_
-   **Descripción breve:** Un programa básico que hace parpadear un LED conectado a un pin digital del ESP32. Es la prueba inicial para verificar que el entorno de desarrollo y el hardware funcionan correctamente.

---

## 2) Objetivos

-   **General:** Comprender el funcionamiento de los pines de Salida Digital (GPIO) del ESP32.
-   **Específicos:**
    -   Configurar correctamente el IDE de Arduino para la placa ESP32.
    -   Declarar y configurar un pin digital como `OUTPUT`.
    -   Enviar señales eléctricas (HIGH y LOW) para encender y apagar un LED.
    -   Utilizar la función `delay()` para controlar el tiempo del parpadeo.

---

## 3) Alcance y Exclusiones

-   **Incluye:** El parpadeo de un solo LED a una frecuencia constante (1 segundo encendido, 1 segundo apagado).
-   **No incluye:** Control de brillo (PWM), lectura de botones, o cualquier tipo de comunicación inalámbrica.

---

## 4) Requisitos

**Software**
-   Arduino IDE (con el gestor de tarjetas ESP32 instalado).
-   Controladores USB (CH340 o CP210x, dependiendo de tu placa).

**Hardware**
-   1x Placa de desarrollo ESP32.
-   1x LED (cualquier color).
-   1x Resistencia de 220 $\Omega$ o 330 $\Omega$ (¡importante para no quemar el LED!).
-   1x Protoboard.
-   2x Cables Jumper (macho-macho).

**Conocimientos previos**
-   Ninguno. Este es el punto de partida.

---

## 5) Código e Instalación

Aquí tienes el código completo. Este código usa el **Pin GPIO 2**, que en muchas placas ESP32 es el LED azul que ya viene integrado (`LED_BUILTIN`).

```cpp
/*
 * PROYECTO 1: LED BLINK
 * Descripción: Hace parpadear un LED conectado al GPIO 2.
 * Autor: (Tu Nombre)
 * Fecha: (Fecha de Hoy)
 */

// Definimos una constante para el pin del LED.
// El pin 2 es comúnmente el LED integrado en la placa (LED_BUILTIN)
const int LED_PIN = 2; 

void setup() {
  // 1. Configurar el pin del LED como una SALIDA (OUTPUT)
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  // 2. Encender el LED (enviar señal ALTA)
  digitalWrite(LED_PIN, HIGH);
  
  // 3. Esperar 1 segundo (1000 milisegundos)
  delay(1000); 
  
  // 4. Apagar el LED (enviar señal BAJA)
  digitalWrite(LED_PIN, LOW);
  
  // 5. Esperar otro segundo
  delay(1000);
}

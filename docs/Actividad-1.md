# 📚 Proyecto 1: "Hola Mundo" del Hardware (LED Blink)

> Este es el proyecto fundamental de la mecatrónica. Demuestra que tienes control sobre el microcontrolador y puedes enviar una señal al mundo físico.

---

## 1) Resumen

-   **Nombre del proyecto:** `ESP32 - Control de Salida Digital (Blink)`
-   **Autor:** _(Tu Nombre)_
-   **Asignatura:** _(Tu Asignatura)_
-   **Fecha:** _(Fecha de Hoy)_
-   **Descripción breve:** Un programa básico que hace parpadear un LED conectado a un pin digital del ESP32.

> **🤖 Consejo de RepoMentor:**
> ¡Este proyecto es tu "Hola, Mundo!" del hardware! Nunca lo subestimes. Demuestra que sabes configurar tu entorno, compilar código y energizar un actuador básico.

---

## 📸 Demostración del Proyecto

(¡Aquí pones una foto, o mejor, un GIF animado de tu circuito parpadeando!)

![Demo del LED Parpadeando](Blink-Demo.gif)

---

## 2) Objetivos

-   **General:** Comprender el funcionamiento de los pines de Salida Digital (GPIO) del ESP32.
-   **Específicos:**
    -   Configurar correctamente el IDE de Arduino para la placa ESP32.
    -   Declarar y configurar un pin digital como `OUTPUT`.
    -   Enviar señales eléctricas (HIGH y LOW) para encender y apagar un LED.
    -   Utilizar la función `delay()` para controlar el tiempo del parpadeo.

## 3) Alcance y Exclusiones

-   **Incluye:** El parpadeo de un solo LED a una frecuencia constante.
-   **No incluye:** Control de brillo (PWM), lectura de botones, o cualquier tipo de comunicación.

---

## 4) Requisitos

**Software**
1.  Arduino IDE (con el gestor de tarjetas ESP32 instalado).
2.  Controladores USB (CH340 o CP210x, dependiendo de tu placa).

**Hardware (Lista de Materiales)**
1.  Placa de desarrollo ESP32 (x1)
2.  LED de 5mm (x1)
3.  Resistencia de 220 $\Omega$ o 330 $\Omega$ (x1)
4.  Protoboard (x1)
5.  Cables Jumper (x2)

**Conocimientos previos**
-   Ninguno. Este es el punto de partida.

---

## 5) Código e Instalación

### El Código

El `pin 2` es comúnmente el LED azul que ya viene integrado en la placa (`LED_BUILTIN`).

```arduino
/*
 * PROYECTO 1: LED BLINK
 * Descripción: Hace parpadear un LED conectado al GPIO 2.
 * Autor: (Tu Nombre)
 * Fecha: (Fecha de Hoy)
 */

// Definimos una constante para el pin del LED.
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

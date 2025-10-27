# 📚 Práctica 5: Aceleración Suave con ESP32 y Puente H

> Este proyecto avanza del control ON/OFF al control analógico. Se implementa una señal de **Modulación por Ancho de Pulso (PWM)** para controlar la velocidad de un motoreductor DC, logrando una aceleración y desaceleración fluida.

---

## 1) Resumen

- **Autor:** Juan Carlos Valdés Pérez
- **Asignatura:** Introducción a la Mecatrónica
- **Fecha:** 19/09/2025
- **Placa:** ESP32 (Controlador LEDC PWM)
- **Descripción breve:** Se programa un ESP32 para generar una señal PWM que alimenta el pin "Enable" de un Puente H L293D. El código incrementa y disminuye el ciclo de trabajo (duty cycle) progresivamente para hacer que un motoreductor DC acelere y frene suavemente.

---

## 2) Objetivo del Proyecto

Aprender el concepto fundamental de **PWM (Modulación por Ancho de Pulso)** y cómo utilizar las funciones específicas del ESP32 (`ledcAttach` y `ledcWrite`) para controlar con precisión la **potencia** entregada a un motor.

---

## 3) Componentes y Requisitos

**Hardware**
- Microcontrolador ESP32
- 1 Motoreductor DC (amarillo, con caja reductora)
- 1 Driver Puente H (Modelo: **L293D**)
- Fuente de alimentación externa
- Protoboard y Jumpers

**Software**
- Arduino IDE
- Lenguaje de programación: C++ (utilizando las funciones del controlador **LEDC** del ESP32)

---

## 4) Desafíos Clave y Aprendizajes

**Desafío:**
El desafío principal fue el **código para la fluidez**. En las primeras pruebas, el motor cambiaba de velocidad, pero lo hacía de forma brusca y a "saltos". El reto fue encontrar la lógica correcta en el programa para que el incremento de potencia fuera gradual. Esto se solucionó implementando bucles `for` que modifican el valor del PWM paso a paso (de 0 a 255 y viceversa), logrando el efecto de "rampa" deseado.

**Aprendizaje:**
Tuve dos aprendizajes clave en esta práctica:

1.  **Conceptual (Qué es PWM):** Entendí que el PWM no "baja el voltaje" mágicamente. Es una técnica digital que **enciende y apaga la energía a muy alta frecuencia** (en este caso, 1000 veces por segundo). Al cambiar el *ancho* de esos pulsos (el "ciclo de trabajo"), se controla la potencia promedio que recibe el motor, simulando un voltaje analógico.

2.  **Técnico (PWM en ESP32):** Aprendí que el ESP32 es más avanzado que un Arduino Uno. No usa la función `analogWrite()`. En su lugar, tiene controladores **LEDC** dedicados. Se debe primero "configurar un canal" de PWM (con `ledcAttach`) y luego "escribir" el valor de potencia en ese canal (con `ledcWrite`).

---

## 5) Código Clave

Este es el código principal cargado en el ESP32. Se definen los pines de dirección (`in1`, `in2`) y un pin para la señal PWM (`pwm`). Los bucles `for` se encargan de aumentar y disminuir el ciclo de trabajo de 0 a 255.

```bash

// --- Pines de Control ---
// Pines para la DIRECCIÓN del motor
#define in1 25
#define in2 26
// Pin para la VELOCIDAD (conectado al 'Enable' del Puente H)
#define pwm 27

// --- Configuración del Canal PWM ---
// Frecuencia de la señal PWM (1000 Hz)
int frecuenciaPWM = 1000;
// Canal PWM que usaremos (de 0 a 15)
int canalPWM = 0;
// Resolución en bits (8 bits = 0 a 255)
int resolucion = 8;


void setup() {
  // Configurar pines de dirección como SALIDA
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  
  // Configurar el canal PWM con ledcAttach
  // (canal, frecuencia, resolución)
  ledcAttach(canalPWM, frecuenciaPWM, resolucion);
  
  // Vincular el pin 'pwm' (27) al canal que configuramos
  ledcAttachPin(pwm, canalPWM);
}

void loop() {
  // --- Bucle de Aceleración ---
  // Incrementa 'i' desde 0 (0% potencia) hasta 255 (100% potencia)
  for (int i = 0; i <= 255; i++) {
    // Escribe el valor actual de 'i' en el canal PWM
    ledcWrite(canalPWM, i);
    // Fija la dirección (ej. "adelante")
    digitalWrite(in1, 1);
    digitalWrite(in2, 0);
    // Pequeña pausa para ver el efecto
    delay(10);
  }

  // --- Bucle de Desaceleración ---
  // Decrementa 'i' desde 255 (100% potencia) hasta 0 (0% potencia)
  for (int i = 255; i >= 0; i--) {
    // Escribe el valor actual de 'i' en el canal PWM
    ledcWrite(canalPWM, i);
    // Mantiene la dirección
    digitalWrite(in1, 1);
    digitalWrite(in2, 0);
    // Pequeña pausa
    delay(10);
  }
}

```
---
## 6) Galería y Demostración

<iframe width="315" height="560" src="https://youtube.com/shorts/584IOEMMXvE?si=ndIf3D5sHl23OS1G>" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


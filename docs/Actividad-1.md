# Práctica 1: Entradas Digitales y Comunicación Bluetooth con ESP32

Este proyecto es una introducción fundamental al control de hardware con el microcontrolador ESP32. El objetivo es controlar el encendido y apagado de un LED de dos maneras: primero, usando una entrada digital (un pulsador físico) y, segundo, de forma inalámbrica mediante comunicación Bluetooth desde una app en un teléfono Android.

## 🎯 Objetivo

El propósito principal fue aprender a configurar los pines del ESP32 como **entrada** (para leer el estado de un botón) y como **salida** (para escribir un estado en un LED). Además, sirvió como introducción a los conceptos básicos de la **comunicación serial por Bluetooth**, enviando comandos simples ('1' y '0') desde un dispositivo móvil para controlar el hardware.

## 🛠️ Tecnologías Utilizadas

### Hardware
* Microcontrolador ESP32
* LED rojo
* Resistencia de 220 Ohms (para proteger el LED)
* Pulsador (push button)
* Protoboard y Jumpers

### Software
* **Lenguaje:** C++ (en el Entorno de Desarrollo de Arduino)
* **App Móvil:** Serial Bluetooth Terminal (Android)

## 💡 Desafíos y Aprendizajes

El principal desafío fue la compatibilidad de software, ya que mi teléfono personal (iOS) no era compatible con la app "Serial Bluetooth Terminal". Esto se resolvió exitosamente **trabajando en equipo**, utilizando el dispositivo Android de mi compañero para realizar las pruebas de conexión y envío de datos.

Mi mayor aprendizaje fue descubrir el potencial de las terminales seriales por Bluetooth. A diferencia de plataformas más cerradas como Arduino Cloud (que había usado en el pasado), una terminal directa ofrece **mucha más flexibilidad y menos restricciones**. Comprendí que esto abre más posibilidades para futuros proyectos de control inalámbrico más complejos.

## 📸 Galería del Proyecto

(Aquí es donde pones tus fotos y videos)

![Foto del circuito en protoboard](foto-circuito-led.jpg)
![Circuito con el pulsador añadido](foto-circuito-boton.jpg)
![Demostración con la app Bluetooth](foto-app-terminal.jpg)

[Ver video del proyecto en acción](demo-bluetooth.mp4)

# 📚 Práctica 4: Control de Giro de Motor DC con Puente H

> Este proyecto es una introducción fundamental a la robótica móvil. Se implementa el control de la dirección de giro de un motor DC utilizando un driver L293D (Puente H) y un microcontrolador ESP32.

---

## 1) Resumen

- **Autor:** Juan Carlos Valdés Pérez
- **Asignatura:** Introducción a la Mecatrónica
- **Fecha:** 19/09/2025 
- **Placa:** ESP32
- **Descripción breve:** Se programa un ESP32 para enviar señales lógicas a un driver L293D, el cual invierte la polaridad del voltaje suministrado a un motor DC para hacerlo girar en ambas direcciones.

---

## 2) Objetivo del Proyecto

El objetivo fue aprender a usar el driver **Puente H L293D** y entender su principio de funcionamiento: cómo utiliza una lógica de control de bajo voltaje (del ESP32) para **invertir la polaridad** de una fuente de alimentación de mayor voltaje (para el motor) y así controlar la dirección del giro.

---

## 3) Componentes y Requisitos

**Hardware**
- Microcontrolador ESP32
- 1 Motor DC (tipo "pager" o similar)
- 1 Driver Puente H (Modelo: **L293D**)
- Fuente de alimentación variable de laboratorio (para V\_motor del Puente H)
- Protoboard y Jumpers

**Software**
- Arduino IDE
- Lenguaje de programación: C++

---

## 4) Desafíos Clave y Aprendizajes

**Desafío:**
El mayor desafío durante el ensamblaje fue la **depuración de conexiones físicas**. En varias ocasiones, el circuito no funcionaba como se esperaba y, tras revisar el código y las conexiones lógicas, descubrí que el problema eran *jumpers* (cables) defectuosos que "falseaban" o no hacían buen contacto. Esto me enseñó a no asumir que el hardware nuevo funciona perfectamente y a tener un método para probar la continuidad de los cables.

**Aprendizaje:**
Mi principal aprendizaje fue sobre la **gestión de energía** del L293D. Analizando el componente, descubrí que tiene una salida de 5V (V\_logic) que puede usarse para alimentar al propio ESP32. Esto es útil porque permite que el microcontrolador y el driver compartan alimentación desde una misma fuente (como una batería).

Sin embargo, también entendí la desventaja: esta configuración le "quita" potencia a los motores (ya que la potencia total se divide) y puede agotar la batería más rápidamente.

---

## 5) Código Clave

Este fragmento de código muestra la lógica básica para controlar el giro. Se usan dos pines del ESP32 (`in1` e `in2`) para dictar la dirección del motor.

```bash
#define in1 18
#define in2 19
#define pwm 21
 
 
void setup() {
  // put your setup code here, to run once:
pinMode(in1,OUTPUT);
pinMode(in2,OUTPUT);
ledcAttach(pwm,1000,8);
}
 
void loop() {
  // put your main code here, to run repeatedly:
for(int i=0; i <= 255; i++){
  ledcWrite(pwm,i);;
}
 
digitalWrite(in1,1);
digitalWrite(in2,0);
delay(400);
digitalWrite(in1,0);
digitalWrite(in1,0);
delay(200);
digitalWrite(in1,0);
digitalWrite(in1,1);
delay(400);
}

```
---
## 6) Galería y Demostración

<iframe width="315" height="560" src="https://youtube.com/embed/SabS0YZtHZ4?si=QsEjBLbeXFIf0Hi8>" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

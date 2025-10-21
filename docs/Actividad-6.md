# 📚 Práctica 6: Control de Posición con Servomotor SG90

> Este proyecto completa la trilogía de control de actuadores. Se implementa el control de **posición angular** de un servomotor SG90, ordenándole moverse a ángulos específicos entre 0° y 180°.

---

## 1) Resumen

- **Autor:** Juan Carlos Valdés Pérez
- **Asignatura:** Introducción a la Mecatrónica
- **Fecha:** 26/09/2025
- **Placa:** ESP32 (Controlador LEDC PWM)
- **Descripción breve:** Se programa un ESP32 para generar una señal PWM muy específica (50Hz) que le ordena a un servomotor SG90 moverse progresivamente en pasos de 10 grados, realizando un barrido de 0° a 180°.

---

## 2) Objetivo del Proyecto

- Aprender a controlar el **ángulo (posición)** de un servomotor.
- Entender cómo una señal PWM de **frecuencia fija (50Hz)** se utiliza para enviar comandos posicionales, a diferencia del PWM de alta frecuencia usado para controlar la *velocidad* de un motor DC.

---

## 3) Componentes y Requisitos

**Hardware**
- Microcontrolador ESP32
- 1 Servomotor SG90 (azul)
- Protoboard y Jumpers

**Software**
- Arduino IDE
- Lenguaje de programación: C++ (utilizando las funciones del controlador **LEDC** del ESP32)

---

## 4) Desafíos Clave y Aprendizajes

**Desafío:**
El desafío principal fue conceptual: **entender por qué se usa una frecuencia de 50Hz y no otra**. A diferencia del PWM para motores DC (donde 1000Hz o más es común para evitar zumbidos), los servomotores son un estándar industrial. Aprendí que 50Hz (lo que equivale a un pulso cada 20 milisegundos) es la norma que estos motores "esperan" para interpretar la señal. Enviar una frecuencia incorrecta (como 1000Hz) simplemente no funciona, ya que el servo no puede entender los comandos.

**Aprendizaje:**
Tuve dos aprendizajes clave que resumen estas últimas prácticas:

1.  **Conceptual (Servos vs. Motor DC):** Entendí que un motor DC y un servomotor son fundamentalmente diferentes, aunque ambos giran. Un motor DC es para **velocidad y giro continuo** (controlas la potencia con PWM). Un servomotor es para **posición y giro limitado** (controlas el ángulo con el *ancho del pulso* en una frecuencia fija).
2.  **Técnico (Función `map()`):** Aprendí a usar la función `map()` de Arduino. Es una herramienta increíblemente útil para escalar (o "mapear") un rango de números a otro. En este caso, fue perfecta para convertir mi rango de ángulos (0° a 180°) al rango de "duty cycle" que el servo entiende (que calculamos ser de 205 a 410).

---

## 5) Código Clave

Este es el código principal. La parte más importante es el cálculo matemático: un servo se controla con un pulso de 1ms (0°) a 2ms (180°). A 50Hz y 12 bits de resolución (4096 pasos), 1ms es ~5% (valor 205) y 2ms es ~10% (valor 410).

```bash
/*Control de 1 solo servomotor*/
#define pwmPin 12  //Pin del ESP32 a la señal del servo

// --- Valores Clave para el Servo ---
// Frecuencia estándar para servos
int frecuenciaPWM = 50;  // 50 Hz (o un pulso cada 20ms)
// Canal PWM que usaremos (de 0 a 15)
int canalPWM = 0;
// Resolución de 12 bits (0 a 4095)
int resolucion = 12;

// Valores de "Duty Cycle" calculados
// 0°   = 1ms de pulso = 5% de 20ms = 5% de 4096 = 205
int minDuty = 205; 
// 180° = 2ms de pulso = 10% de 20ms = 10% de 4096 = 410
int maxDuty = 410;

void setup() {
  Serial.begin(115200);
  
  /*Configuracion de canal PWM 
    - Frecuencia de 50hz
    - Resolucion de 12 bit (0-4095)
    - Canal 0
  */
  ledcSetup(canalPWM, frecuenciaPWM, resolucion);
  
  // Asignar el pin (12) al canal (0)
  ledcAttachPin(pwmPin, canalPWM);
}

void loop() {
  Serial.println("Iniciando barrido progresivo (0 -> 180)...");

  // Bucle para ir de 0 a 180 grados, en pasos de 10
  for (int angulo = 0; angulo <= 180; angulo += 10) {
    
    // Mapear el ángulo (0-180) al valor de duty cycle (205-410)
    int duty = map(angulo, 0, 180, minDuty, maxDuty);
    
    Serial.print("Angulo: ");
    Serial.print(angulo);
    Serial.print(" - Duty Cycle: ");
    Serial.println(duty);
    
    // Enviar el pulso al servo
    ledcWrite(canalPWM, duty);
    
    // Pausa de medio segundo antes del siguiente paso
    delay(500);
  }
  
  // Pausa de 2 segundos al llegar a 180
  delay(2000); 

  // (Aquí se podría agregar un 'for' loop para regresar de 180 a 0)
}
```

¡Claro! Aquí tienes la tercera parte de la presentación para enseñar a niños a usar Arduino de forma básica y avanzar en proyectos más complejos.

---

### Slide 20: Proyecto 11 - Estación Meteorológica Básica
- **Conexión de Sensores de Temperatura y Humedad (DHT11)**
  - Cómo conectar el sensor DHT11 a la placa Arduino
- **Escribir el Código**
  - Explicación del código para leer datos de temperatura y humedad y mostrarlos en el monitor serie
  - Ejemplo de código:
    ```cpp
    #include "DHT.h"

    #define DHTPIN 2      // Pin donde se conecta el sensor DHT
    #define DHTTYPE DHT11 // Tipo de sensor DHT

    DHT dht(DHTPIN, DHTTYPE);

    void setup() {
      Serial.begin(9600);
      dht.begin();
    }

    void loop() {
      float h = dht.readHumidity();
      float t = dht.readTemperature();
      float f = dht.readTemperature(true);

      if (isnan(h) || isnan(t) || isnan(f)) {
        Serial.println("Failed to read from DHT sensor!");
        return;
      }

      Serial.print("Humidity: ");
      Serial.print(h);
      Serial.print(" %\t");
      Serial.print("Temperature: ");
      Serial.print(t);
      Serial.print(" *C ");
      Serial.print(f);
      Serial.println(" *F");
      delay(2000);
    }
    ```

---

### Slide 21: Proyecto 12 - Sistema de Riego Automático
- **Conexión del Sensor de Humedad del Suelo**
  - Cómo conectar un sensor de humedad del suelo y una bomba de agua a la placa Arduino
- **Escribir el Código**
  - Explicación del código para activar la bomba de agua según el nivel de humedad del suelo
  - Ejemplo de código:
    ```cpp
    int sensorPin = A0; // Pin analógico donde se conecta el sensor de humedad
    int pumpPin = 7;    // Pin digital donde se conecta la bomba de agua
    int sensorValue = 0;

    void setup() {
      Serial.begin(9600);
      pinMode(pumpPin, OUTPUT);
    }

    void loop() {
      sensorValue = analogRead(sensorPin); // Leer el valor del sensor de humedad
      Serial.println(sensorValue);
      if (sensorValue < 300) {             // Si el valor es menor que 300, encender la bomba
        digitalWrite(pumpPin, HIGH);
      } else {
        digitalWrite(pumpPin, LOW);        // De lo contrario, apagar la bomba
      }
      delay(1000);
    }
    ```

---

### Slide 22: Proyecto 13 - Robot Seguidor de Línea
- **Conexión de Sensores de Infrarrojos**
  - Cómo conectar sensores de infrarrojos y motores a la placa Arduino
- **Escribir el Código**
  - Explicación del código para controlar los motores basados en la detección de línea
  - Ejemplo de código:
    ```cpp
    int sensorEsq = 2; // Sensor de infrarrojos izquierdo
    int sensorDir = 3; // Sensor de infrarrojos derecho
    int motorEsq1 = 5; // Motor izquierdo pin 1
    int motorEsq2 = 6; // Motor izquierdo pin 2
    int motorDir1 = 9; // Motor derecho pin 1
    int motorDir2 = 10; // Motor derecho pin 2

    void setup() {
      pinMode(sensorEsq, INPUT);
      pinMode(sensorDir, INPUT);
      pinMode(motorEsq1, OUTPUT);
      pinMode(motorEsq2, OUTPUT);
      pinMode(motorDir1, OUTPUT);
      pinMode(motorDir2, OUTPUT);
    }

    void loop() {
      int esq = digitalRead(sensorEsq);
      int dir = digitalRead(sensorDir);

      if (esq == HIGH && dir == HIGH) {
        // Avanzar
        digitalWrite(motorEsq1, HIGH);
        digitalWrite(motorEsq2, LOW);
        digitalWrite(motorDir1, HIGH);
        digitalWrite(motorDir2, LOW);
      } else if (esq == LOW && dir == HIGH) {
        // Girar a la izquierda
        digitalWrite(motorEsq1, LOW);
        digitalWrite(motorEsq2, LOW);
        digitalWrite(motorDir1, HIGH);
        digitalWrite(motorDir2, LOW);
      } else if (esq == HIGH && dir == LOW) {
        // Girar a la derecha
        digitalWrite(motorEsq1, HIGH);
        digitalWrite(motorEsq2, LOW);
        digitalWrite(motorDir1, LOW);
        digitalWrite(motorDir2, LOW);
      } else {
        // Detener
        digitalWrite(motorEsq1, LOW);
        digitalWrite(motorEsq2, LOW);
        digitalWrite(motorDir1, LOW);
        digitalWrite(motorDir2, LOW);
      }
    }
    ```

---

### Slide 23: Proyecto 14 - Alarma de Seguridad con Sensor Ultrasónico
- **Conexión del Sensor Ultrasónico (HC-SR04)**
  - Cómo conectar un sensor ultrasónico y una alarma (zumbador) a la placa Arduino
- **Escribir el Código**
  - Explicación del código para activar una alarma cuando se detecta movimiento a cierta distancia
  - Ejemplo de código:
    ```cpp
    #define trigPin 9
    #define echoPin 10
    #define buzzer 11

    void setup() {
      pinMode(trigPin, OUTPUT);
      pinMode(echoPin, INPUT);
      pinMode(buzzer, OUTPUT);
      Serial.begin(9600);
    }

    void loop() {
      long duration, distance;
      digitalWrite(trigPin, LOW);
      delayMicroseconds(2);
      digitalWrite(trigPin, HIGH);
      delayMicroseconds(10);
      digitalWrite(trigPin, LOW);

      duration = pulseIn(echoPin, HIGH);
      distance = (duration / 2) / 29.1;

      if (distance <= 10) {
        digitalWrite(buzzer, HIGH); // Activar el zumbador si la distancia es menor o igual a 10 cm
      } else {
        digitalWrite(buzzer, LOW);  // De lo contrario, apagar el zumbador
      }
      Serial.print(distance);
      Serial.println(" cm");
      delay(500);
    }
    ```

---

### Slide 24: Proyecto 15 - Control de Luces con Sensores de Luz (LDR)
- **Conexión del Sensor de Luz (LDR)**
  - Cómo conectar un LDR y un LED a la placa Arduino
- **Escribir el Código**
  - Explicación del código para encender o apagar un LED basado en el nivel de luz
  - Ejemplo de código:
    ```cpp
    int sensorLuz = A0; // Pin analógico donde se conecta el LDR
    int led = 13;       // Pin digital donde se conecta el LED
    int valorLuz = 0;

    void setup() {
      pinMode(led, OUTPUT);
      Serial.begin(9600);
    }

    void loop() {
      valorLuz = analogRead(sensorLuz); // Leer el valor del sensor de luz
      Serial.println(valorLuz);
      if (valorLuz < 500) {
        digitalWrite(led, HIGH); // Encender el LED si el valor es menor que 500
      } else {
        digitalWrite(led, LOW);  // Apagar el LED de lo contrario
      }
      delay(1000);
    }
    ```

---

### Slide 25: Proyecto 16 - Sistema de Alarma de Gas
- **Conexión del Sensor de Gas (MQ-2)**
  - Cómo conectar un sensor MQ-2 a la placa Arduino
- **Escribir el Código**
  - Explicación del código para activar una alarma cuando se detecta gas
  - Ejemplo de código:
    ```cpp
    int gasPin = A0; // Pin analógico donde se conecta el sensor de gas
    int buzzer = 9;  // Pin digital donde se conecta el zumbador

    void setup() {
      pinMode(buzzer, OUTPUT);
      Serial.begin(9600);
    }

    void loop() {
      int gasLevel = analogRead(gasPin); // Leer el nivel de gas
      Serial.println(gasLevel);
      if (gasLevel > 300) {              // Si el nivel de gas es mayor que 300, activar el zumbador
        digitalWrite(buzzer, HIGH);
      } else {
        digitalWrite(buzzer, LOW);       // De lo contrario, apagar el zumbador
      }
      delay(1000);
    }
    ```

---

### Slide 26: Recapitulación y Recursos Adicionales
- **Resumen de Proyectos Realizados**
  - Resumen de los proyectos y conceptos clave aprendidos en el taller
- **Próximos Pasos y Proyectos**
  - Ideas para proyectos más avanzados y desafiantes
  - Cómo continuar aprendiendo y explorando el mundo de Arduino
- **Recursos Adicionales**
  - Libros, tutoriales en línea, comunidades y foros recomendados

---

### Slide 27: Evaluación

 y Retroalimentación
- **Evaluación del Taller**
  - Solicitar a los participantes que compartan sus opiniones y sugerencias
  - Formularios de evaluación y encuestas
- **Agradecimientos**
  - Agradecimiento a los participantes por su entusiasmo y dedicación

---

### Slide 28: Información de Contacto y Cierre
- **Información de Contacto**
  - Correo electrónico del instructor
  - Redes sociales y otros medios de contacto
- **Cierre**
  - Mensaje de despedida y motivación para seguir aprendiendo

---

Espero que esta tercera parte complemente bien la presentación inicial y ayude a mantener a los niños interesados y comprometidos mientras aprenden sobre Arduino. Si necesitas más detalles o algún ajuste, ¡házmelo saber! 😊
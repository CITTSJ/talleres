¡Claro! Aquí tienes la segunda parte de la presentación para enseñar a niños a usar Arduino de forma básica. Esta parte se enfocará en proyectos adicionales y conceptos más avanzados para mantener el interés y fomentar la creatividad de los niños.

---

### Slide 11: Proyecto 5 - Control de Brillo de un LED con Potenciómetro
- **Conexión del Potenciómetro**
  - Cómo conectar un potenciómetro y un LED a la placa Arduino
- **Escribir el Código**
  - Explicación del código para controlar el brillo del LED usando el potenciómetro
  - Ejemplo de código:
    ```cpp
    int potPin = A0;  // Pin analógico donde se conecta el potenciómetro
    int ledPin = 9;   // Pin digital PWM donde se conecta el LED
    int potValue = 0; // Variable para almacenar el valor leído del potenciómetro

    void setup() {
      pinMode(ledPin, OUTPUT);
    }

    void loop() {
      potValue = analogRead(potPin);            // Leer el valor del potenciómetro
      int brightness = map(potValue, 0, 1023, 0, 255); // Mapear el valor a un rango de 0 a 255
      analogWrite(ledPin, brightness);          // Ajustar el brillo del LED
      delay(10);
    }
    ```

---

### Slide 12: Proyecto 6 - Sensor de Temperatura
- **Conexión del Sensor de Temperatura (LM35)**
  - Cómo conectar un sensor de temperatura LM35 a la placa Arduino
- **Escribir el Código**
  - Explicación del código para leer la temperatura y mostrarla en el monitor serie
  - Ejemplo de código:
    ```cpp
    int sensorPin = A0; // Pin analógico donde se conecta el sensor de temperatura
    float temp;         // Variable para almacenar la temperatura

    void setup() {
      Serial.begin(9600);
    }

    void loop() {
      int reading = analogRead(sensorPin);      // Leer el valor del sensor
      temp = reading * 0.48828125;              // Convertir el valor a temperatura en grados Celsius
      Serial.print("Temperatura: ");
      Serial.print(temp);
      Serial.println(" C");
      delay(1000);
    }
    ```

---

### Slide 13: Proyecto 7 - Alarma de Movimiento
- **Conexión del Sensor de Movimiento (PIR)**
  - Cómo conectar un sensor PIR y un zumbador a la placa Arduino
- **Escribir el Código**
  - Explicación del código para activar una alarma cuando se detecte movimiento
  - Ejemplo de código:
    ```cpp
    int pirPin = 2;    // Pin digital donde se conecta el sensor PIR
    int buzzerPin = 3; // Pin digital donde se conecta el zumbador
    int pirState = LOW;

    void setup() {
      pinMode(pirPin, INPUT);
      pinMode(buzzerPin, OUTPUT);
      Serial.begin(9600);
    }

    void loop() {
      pirState = digitalRead(pirPin); // Leer el estado del sensor PIR
      if (pirState == HIGH) {
        digitalWrite(buzzerPin, HIGH); // Activar el zumbador
        Serial.println("Movimiento detectado");
        delay(1000);
      } else {
        digitalWrite(buzzerPin, LOW);  // Desactivar el zumbador
      }
    }
    ```

---

### Slide 14: Proyecto 8 - Control de Motores
- **Conexión de un Motor y un L293D**
  - Cómo conectar un motor y un controlador de motor L293D a la placa Arduino
- **Escribir el Código**
  - Explicación del código para controlar la dirección y velocidad del motor
  - Ejemplo de código:
    ```cpp
    int motorPin1 = 5;
    int motorPin2 = 6;
    int enablePin = 9;

    void setup() {
      pinMode(motorPin1, OUTPUT);
      pinMode(motorPin2, OUTPUT);
      pinMode(enablePin, OUTPUT);
      digitalWrite(enablePin, HIGH);
    }

    void loop() {
      digitalWrite(motorPin1, HIGH); // Girar en una dirección
      digitalWrite(motorPin2, LOW);
      delay(2000);
      digitalWrite(motorPin1, LOW);  // Parar el motor
      digitalWrite(motorPin2, LOW);
      delay(2000);
      digitalWrite(motorPin1, LOW);  // Girar en la otra dirección
      digitalWrite(motorPin2, HIGH);
      delay(2000);
      digitalWrite(motorPin1, LOW);  // Parar el motor
      digitalWrite(motorPin2, LOW);
      delay(2000);
    }
    ```

---

### Slide 15: Proyecto 9 - Display LCD
- **Conexión de un Display LCD**
  - Cómo conectar un display LCD 16x2 a la placa Arduino
- **Escribir el Código**
  - Explicación del código para mostrar mensajes en el LCD
  - Ejemplo de código:
    ```cpp
    #include <LiquidCrystal.h>

    LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

    void setup() {
      lcd.begin(16, 2);
      lcd.print("Hola, Mundo!");
    }

    void loop() {
      lcd.setCursor(0, 1);
      lcd.print(millis() / 1000);
      delay(1000);
    }
    ```

---

### Slide 16: Proyecto 10 - Control de Luces con Bluetooth
- **Conexión del Módulo Bluetooth (HC-05)**
  - Cómo conectar un módulo Bluetooth y un LED a la placa Arduino
- **Escribir el Código**
  - Explicación del código para controlar un LED desde un dispositivo Bluetooth
  - Ejemplo de código:
    ```cpp
    #include <SoftwareSerial.h>

    SoftwareSerial BTSerial(10, 11); // RX, TX
    int ledPin = 9;
    char data;

    void setup() {
      pinMode(ledPin, OUTPUT);
      BTSerial.begin(9600);
      Serial.begin(9600);
    }

    void loop() {
      if (BTSerial.available()) {
        data = BTSerial.read();
        if (data == '1') {
          digitalWrite(ledPin, HIGH);
        } else if (data == '0') {
          digitalWrite(ledPin, LOW);
        }
      }
    }
    ```

---

### Slide 17: Recursos Adicionales y Comunidades
- **Sitios Web y Tutoriales**
  - Arduino Project Hub
  - Instructables
  - Hackster.io
- **Libros Recomendados**
  - "Arduino for Kids" de Priya Kuber
  - "Arduino Project Handbook" de Mark Geddes
- **Comunidades y Foros**
  - Reddit: r/arduino
  - Stack Overflow: Arduino tag

---

### Slide 18: Próximos Pasos
- **Proyectos Más Avanzados**
  - Crear un robot seguidor de línea
  - Sistema de riego automático
  - Estación meteorológica con sensores múltiples
- **Continuar Aprendiendo**
  - Participar en hackathons y competiciones
  - Unirse a clubs de robótica y tecnología
  - Seguir cursos en línea sobre electrónica y programación

---

### Slide 19: Agradecimientos y Contacto
- **Agradecimientos**
  - Agradecimiento a los participantes por su atención y entusiasmo
- **Información de Contacto**
  - Correo electrónico del instructor
  - Redes sociales y otros medios de contacto

---

Espero que esta segunda parte complemente bien la presentación inicial y ayude a mantener a los niños interesados y comprometidos mientras aprenden sobre Arduino. Si necesitas más detalles o algún ajuste, ¡házmelo saber! 😊
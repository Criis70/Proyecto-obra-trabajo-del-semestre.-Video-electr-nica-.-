# Encargo 8

Generar una animación, afiche, video o pieza de imagen-movimiento en Processing basada en la interacción con un encoder. Este debe incluir palabras, y utilizar también el switch del encoder. Puntos extra si la obra está buena (si es coherente con mi práctica habitual o dialoga con el gesto de girar un encoder)

### Video registro Encargo N°8

- Link: <https://drive.google.com/file/d/1--pQXz38RC870zCp9B_hcwcbTZMSShdV/view?usp=sharing>

## Encargo bonus:
#### Controlar la velocidad y dirección del paso a paso con un encoder

### Diagrama del Encoder

<img width="1888" height="866" alt="Sin-título" src="https://github.com/user-attachments/assets/3ce0f5a4-ac45-4274-8773-ad694e5bf4e3" />

### Manos a la obra: 

Primero que hice fue cambiar el codigo que nos dieron en la clase del encoder. 

Agregué un 
```
#define PIN_STIWCH 4
```
Para definir el switch en el pin 4

Luego dentro del codigo agregué un el loop un 
```
 if (pos != newPos) {
    pos = newPos;
    Serial.println(" Posición: ");
      Serial.println(pos);
  }

  static bool lastButtonState = HIGH;
  bool buttonState = digitalRead(PIN_SWITCH);

  if (buttonState == LOW && lastButtonState == HIGH) {
    
    if (digitalRead(PIN_SWITCH) == LOW){
      encoder.setPosition(0);
      pos = 0;
      Serial.println(" Valor reiniciado a 0 ");
    }
    
  }
```
Para que cada que se presione el switch los valores entregados se reinicien en "0". 

### Codigo N°1 Encoder + Switch 
```
#include <RotaryEncoder.h>

#define ARDUINO_AVR_UNO

int valorAEnviar = 0;

#if defined(ARDUINO_AVR_UNO) || defined(ARDUINO_AVR_NANO_EVERY)

#define PIN_IN1 2
#define PIN_IN2 3
#define PIN_SWITCH 4

#elif defined(ESP8266)
#define PIN_IN1 D5
#define PIN_IN2 D6

#endif
RotaryEncoder encoder(PIN_IN1, PIN_IN2, RotaryEncoder::LatchMode::TWO03);


void setup() { 

Serial.begin(9600);
  pinMode(PIN_SWITCH, INPUT_PULLUP);
  Serial.println(" Encoder Listo. ");
}


void loop() {

  static int pos = 0;
  encoder.tick();

  int newPos = encoder.getPosition();

  if (pos != newPos) {
    pos = newPos;
    Serial.println(" Posición: ");
      Serial.println(pos);
  }

  static bool lastButtonState = HIGH;
  bool buttonState = digitalRead(PIN_SWITCH);

  if (buttonState == LOW && lastButtonState == HIGH) {
    
    if (digitalRead(PIN_SWITCH) == LOW){
      encoder.setPosition(0);
      pos = 0;
      Serial.println(" Valor reiniciado a 0 ");
    }
  }

  lastButtonState = buttonState;
}
```
A partir de este punto para poder concretar el encargo, utilicé la IA ChatGPT para que me ayudase con los proximos codigos, ya que mi intención era realizar una animación en 3D en Processing, y que este comunicado con el Encoder. 

### Codigo N°2 para comunicar con Processing

```
#include <RotaryEncoder.h>

#define PIN_IN1 2
#define PIN_IN2 3
#define PIN_SWITCH 4

RotaryEncoder encoder(PIN_IN1, PIN_IN2, RotaryEncoder::LatchMode::TWO03);

void setup() {
  Serial.begin(9600);
  pinMode(PIN_SWITCH, INPUT_PULLUP);
}

void loop() {
  encoder.tick();
  int pos = encoder.getPosition();

  // Leer el switch
  static bool lastButtonState = HIGH;
  bool buttonState = digitalRead(PIN_SWITCH);
  bool switchPressed = false;

  if (buttonState == LOW && lastButtonState == HIGH) {
    delay(50); // debounce
    if (digitalRead(PIN_SWITCH) == LOW) {
      switchPressed = true;
    }
  }
  lastButtonState = buttonState;

  // Enviar datos a Processing: "pos,switch"
  Serial.print(pos);
  Serial.print(",");
  Serial.println(switchPressed ? 1 : 0);

  delay(10);
}

```

Todo esto es para crear una animación en Processing donde pueda controlar el movimiento "X" (horizontal) girando el encoder - se presiona el Switch - cambia el control de movimiento al "Y" (vertical). 

### Codigo para Processing (clean)

```
import processing.serial.*;

Serial myPort;

PImage fondo;
PImage[] caras = new PImage[6];

float angleX = 0;          // Ángulo vertical
float angleY = 0;          // Ángulo horizontal
boolean verticalMode = false; // false = controla Y, true = controla X
int lastEncoderPos = 0;    // Posición anterior del encoder

void setup() {
  size(600, 600, P3D);
  smooth(8);

  // --- Carga de fondo y texturas ---
  fondo = loadImage("fondo.JPG");
  caras[0] = loadImage("front.jpg");
  caras[1] = loadImage("back.jpg");
  caras[2] = loadImage("left.jpg");
  caras[3] = loadImage("right.jpg");
  caras[4] = loadImage("top.jpg");
  caras[5] = loadImage("bottom.jpg");

  hint(DISABLE_TEXTURE_MIPMAPS);
  textureMode(NORMAL);
  textureWrap(CLAMP);
  rectMode(CENTER);

  // --- Puerto Serial manual ---
  myPort = new Serial(this, "COM10", 9600); // <--- reemplaza con tu puerto real
  myPort.bufferUntil('\n');
}

void draw() {
  background(0);

  // --- Fondo ---
  hint(DISABLE_DEPTH_TEST);
  image(fondo, 0, 0, width, height);
  hint(ENABLE_DEPTH_TEST);

  // --- Cubo 3D ---
  pushMatrix();
  translate(width/2, height/2, 0);
  rotateX(angleX);
  rotateY(angleY);
  noStroke();
  drawBoxTextured(150, 200, 50);
  popMatrix();
}

// --- Lectura del encoder desde Arduino ---
void serialEvent(Serial p) {
  String line = p.readStringUntil('\n');
  if (line == null) return;
  line = trim(line);
  if (line.length() == 0) return;

  String[] parts = split(line, ',');
  if (parts.length != 2) return;

  try {
    int pos = int(parts[0]);
    int sw = int(parts[1]);

    // Cambiar eje si se presionó switch
    if (sw == 1) verticalMode = !verticalMode;

    // --- Delta acumulativo ---
    int delta = pos - lastEncoderPos;
    lastEncoderPos = pos;

    float sensitivity = 0.10; // Ajusta velocidad de giro
    if (!verticalMode) {
      angleY += delta * sensitivity;
    } else {
      angleX += delta * sensitivity;
    }

  } catch(Exception e) {
    println("Error leyendo Serial: " + line);
  }
}

// --- Función para dibujar cubo con texturas ---
void drawBoxTextured(float w, float h, float d) {
  float x = w/2;
  float y = h/2;
  float z = d/2;

  // Frente
  beginShape(QUADS);
  texture(caras[0]);
  vertex(-x, -y,  z, 0, 0);
  vertex( x, -y,  z, 1, 0);
  vertex( x,  y,  z, 1, 1);
  vertex(-x,  y,  z, 0, 1);
  endShape();

  // Atrás
  beginShape(QUADS);
  texture(caras[1]);
  vertex( x, -y, -z, 0, 0);
  vertex(-x, -y, -z, 1, 0);
  vertex(-x,  y, -z, 1, 1);
  vertex( x,  y, -z, 0, 1);
  endShape();

  // Izquierda
  beginShape(QUADS);
  texture(caras[2]);
  vertex(-x, -y, -z, 0, 0);
  vertex(-x, -y,  z, 1, 0);
  vertex(-x,  y,  z, 1, 1);
  vertex(-x,  y, -z, 0, 1);
  endShape();

  // Derecha
  beginShape(QUADS);
  texture(caras[3]);
  vertex( x, -y,  z, 0, 0);
  vertex( x, -y, -z, 1, 0);
  vertex( x,  y, -z, 1, 1);
  vertex( x,  y,  z, 0, 1);
  endShape();

  // Arriba
  beginShape(QUADS);
  texture(caras[4]);
  vertex(-x, -y, -z, 0, 0);
  vertex( x, -y, -z, 1, 0);
  vertex( x, -y,  z, 1, 1);
  vertex(-x, -y,  z, 0, 1);
  endShape();

  // Abajo
  beginShape(QUADS);
  texture(caras[5]);
  vertex(-x,  y,  z, 0, 0);
  vertex( x,  y,  z, 1, 0);
  vertex( x,  y, -z, 1, 1);
  vertex(-x,  y, -z, 0, 1);
  endShape();
}
```


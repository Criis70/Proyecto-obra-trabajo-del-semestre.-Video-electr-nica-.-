Clase nro 3: 

Cosas de github: 

- branches - una variante, luego se inserta al codigo principal.

- fork: una deriva temporal, hacer un clon, una modifiación, una copia en tu pc.

Para subir imágenes:
- Subcarpeta ''imágenes'' dentro de la clase 3
- ![texto alternativo](ubicación de foto.jpg)  


## Arduino
ATMEGA328P/, tambien de forma virtual esta el tinkercad.com/ Autodesk. 

Wiring - Facilitar el acceso a un microcontrolador - AFEL / MCI electronics. 
Las placas chinas se necesita descargar un crack / driver para que el PC lo detecte - driver CH340.

El arduino: 
inputs - outputs. 
- Inputs: Sensonres - LDR, botón, perillas, potenciadores.
- Outputs: Luz (pantallas, led) - motores - sonidos.
  
Digital y Análogico. 

Digital: pixeles - discreto, de uno separado de otro - Si quiero digitalizar el mundo, tengo que cortarlo (samples). 
- Digital in: 1 o 0 - on off - high low.
  
Analógico: continuo - todo es fluido, es contorno - el tiempo. 
- Analog: Rango.

USB: 
- Universal Serial Bus
- Seriales: cadena de datos en serie.

Tiene 4 patitas: 
- VCC 5V
- Data + >
- Data - <
- GND

Se pueden subir un código, siempre se queda con el último código - se puede conectar a una fuente externa luego de subir el codigo desde el pc. 

TX: Transxmite.

RX: Recibe.

```
int ledPin = 13;
int tiempoPunto = 100;
int separador = 50;
int tiempoRaya = 500;
int finCaracter = 100;

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(ledPin, HIGH);
  Serial.println(" punto ");

  delay(tiempoPunto);
  digitalWrite(ledPin, LOW);

  delay(separador);
//
  digitalWrite(ledPin, HIGH);
  Serial.println(" raya ");

  delay(tiempoRaya);
  digitalWrite(ledPin, LOW);

  delay(finCaracter);
}
```

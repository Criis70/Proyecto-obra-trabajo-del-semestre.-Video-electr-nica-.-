# Primeros circuitos. 

Primer uso de los materiales: 
- Resistencia de 1k Ohm
- Potenciométro
- Protoboard
- Led
En arduino, se usan casi 3 valores, 1k, ... etc

Que significa LED: Light Emiter Diodo. 
Resistencias variables. - Potenciómetro 
-  https://docs.arduino.cc/language-reference/ (BUSCAR Y APRENDER).

```
int potPin= A0;
int ledPin=8;
int valorPot = 0;
int potMapeado=0; 
int tiempoParpadeo=100;
  
void setup(){
  pinMode(ledPin,OUTPUT);
Serial.begin(9600);
  
}
void loop(){
  
  valorPot= analogRead(potPin);
    potMapeado= map(valorPot,0,1023,100,2000);
  
  tiempoParpadeo=potMapeado;
  
  digitalWrite(ledPin, HIGH);
  delay(tiempoParpadeo);
digitalWrite(ledPin,LOW);
  delay(tiempoParpadeo);
  
  Serial.println(tiempoParpadeo);
}
```
```
int ledPin=8;
  int potPin=A0;
int intervalo=1000;
bool estadoLed=0;

int tiempoParpadeo=100;
  
  
unsigned long tiempoActual=0;
unsigned long tiempoAnterior=0; 

void setup()
{
pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
  
}
void loop(){
  
tiempoActual= millis();
valorPot= analogRead(potPin);

  potMapeado= map(valorPot,0,1023,100,2000);
  intervalo= potMapeado;
  if (tiempoActual - tiempoAnterior > intervalo);{
  estadoLed=!estadoLed;
    Serial.println("Se cumplió la condición");
    
    tiempoAnterior = tiempoActual;
  }
  digitalWrite(ledPin, estadoLed);
  Serial.println("");
  
  
}
```
(este codigo tiene un error, no pude descifrar cual era, pronto a revisarlo). 

```
int ledPin=9;
int potPin=A0;
int valorPot=0;
bool estadoLed=0;
int potMapeado=0;

int tiempoParpadeo=100;
  int intensidadLuz=0;

void setup()
{
pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
  
}

void loop(){
  
valorPot= analogRead(potPin);
  
  if(valorPot <100 ){
    intensidadLuz= 255;
  }else if (valorPot<200){
      intensidadLuz=30;
    } 
  
  
  potMapeado= map(valorPot,0,1023,0,255);
  intensidadLuz = potMapeado;
 
  analogWrite(ledPin, intensidadLuz);
  Serial.println(intensidadLuz);
  
  
}
```
(este codigo tiene un error, no pude descifrar cual era, pronto a revisarlo). 

## Encargo 5: 

- Van a usar una estructura if para alterar el brillo led a otros comportamientos. Por ejenplo, si el potenciométro mide hasta 100, ....

## Encargo 6: 
comprar una pantalla LCD 

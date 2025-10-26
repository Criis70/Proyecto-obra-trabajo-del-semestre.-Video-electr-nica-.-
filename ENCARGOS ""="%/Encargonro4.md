# Encargo nro 4. 

Escribir una frase en código morse, en processing

## frase escogida. 

" la distracción nos impide el desarrollo de un pensamiento crítico"

video registro: 
- link: <https://drive.google.com/file/d/1oVhGwNzduKx-09VPSKmdZMdOjyQZsOBm/view?usp=sharing>

codigo en Arduino 

```
int ledPin = 13;

// tiempos
int tiempoPunto = 100;
int separador = 50;
int tiempoRaya = 500;
// int finCaracter = 100;
int espacio = 500;
int finPalabra =1000; 

void setup() {
    pinMode(ledPin, OUTPUT);
    Serial.begin(9600);
}

void loop() {
    // La distracción nos impide el desarrollo de un pensamiento crítico
    l(); delay(espacio);
    a(); delay(espacio);
    delay(finPalabra);

    d(); delay(espacio);
    i(); delay(espacio);
    s(); delay(espacio);
    t(); delay(espacio);
    r(); delay(espacio);
    a(); delay(espacio);
    c(); delay(espacio);
    c(); delay(espacio);
    i(); delay(espacio);
    o(); delay(espacio);
    n(); delay(espacio); 
    delay(finPalabra);

    n(); delay(espacio);
    o(); delay(espacio);
    s(); delay(espacio);
    delay(finPalabra);

    i(); delay(espacio);
    m(); delay(espacio);
    p(); delay(espacio);
    i(); delay(espacio);
    d(); delay(espacio);
    e(); delay(espacio);
    delay(finPalabra);

    e(); delay(espacio);
    l(); delay(espacio);
    delay(finPalabra);

    d(); delay(espacio);
    e(); delay(espacio);
    s(); delay(espacio);
    a(); delay(espacio);
    r(); delay(espacio); 
    r(); delay(espacio);
    o(); delay(espacio);
    l(); delay(espacio);
    l(); delay(espacio);
    o(); delay(espacio);
    delay(finPalabra);

    d(); delay(espacio);
    e(); delay(espacio);
    delay(finPalabra);

    u(); delay(espacio);
    n(); delay(espacio);
    delay(finPalabra); 

    p(); delay(espacio);
    e(); delay(espacio);
    n(); delay(espacio);
    s(); delay(espacio),
    a(); delay(espacio);
    m(); delay(espacio);
    i(); delay(espacio);
    e(); delay(espacio);
    n(); delay(espacio);
    t(); delay(espacio);
    o(); delay(espacio);
    delay(finPalabra);

    c(); delay(espacio);
    r(); delay(espacio);
    i(); delay(espacio);
    t(); delay(espacio);
    i(); delay(espacio);
    c(); delay(espacio);
    o(); delay(espacio);
    delay(finPalabra);

    Serial.println("Fin de la frase");
    delay(2000); // Espera antes de repetir
}

void punto() {
    digitalWrite(ledPin, HIGH);
    Serial.println("punto");
    delay(tiempoPunto);
    digitalWrite(ledPin, LOW);
    delay(separador);
}

void raya() {
    digitalWrite(ledPin, HIGH);
    Serial.println("raya");
    delay(tiempoRaya);
    digitalWrite(ledPin, LOW);
    delay(separador);
}

// Letras
// l - a - d - i - s - t - r - c - o - n -  m - p - e - u

void l(){
    punto(); raya(); punto(); punto();
}

void a() {
    punto(); raya();
}

void d(){
    raya(); punto(); punto(); 
}

void i (){
    punto(); punto();
}

void s(){
    punto(); punto(); punto();
}

void t(){
    raya();
}

void r(){
    punto(); raya(); punto();
}

void c(){
    raya(); punto(); raya(); punto();
}

void o() {
    raya(); raya(); raya();
}

void n() {
    raya(); punto();
}

void m() {
    raya(); raya(); 
}

void p() {
    punto(); raya(); raya(); punto();
}

void e(){
    punto();
}

void u(){
    punto(); punto(); raya(); 
}
```
##Encargo bonus 

Luego de terminar el encargo posterior el nro 5, salí al balcón de mi apartamento a pensar sobre las posibilidades entre la luz emitida en morse y otro receptor que pueda traducir la luz para luego transcribirlo en algun lado, esto pensando en el referente que nos dió en la clase del día 23 de octubre, donde nos mostró un proyecto en donde se "complejiza" demasiado el lenguaje, por medio de un morse, sensores, impresión sobre boleta y audio, no recuerdo muy bien el referente. 


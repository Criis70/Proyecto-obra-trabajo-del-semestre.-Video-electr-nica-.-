# Encargo nro 4

Escribir una frase en código morse, en processing

## Frase escogida : 

### " la distracción nos impide el desarrollo de un pensamiento crítico"

video registro: 
- link: <https://drive.google.com/file/d/1M9P8A1wMuI9F3_0ywYArsC2ciJIFxdlG/view?usp=sharing>
- link (bonus): <https://drive.google.com/file/d/1oT6W6VgpmfoWofINjeUBWDC1c_CY_Gds/view?usp=sharing>
  
## Bonus

Luego de terminar el encargo posterior el nro 5 salí al balcón de mi apartamento a pensar sobre las posibilidades entre la luz emitida en morse y un receptor que pueda traducir la luz para luego transcribirlo en algun lado.

Esto pensando en el referente que nos dió en la clase del día 23 de octubre, donde nos mostró un proyecto en donde se "complejiza" demasiado el lenguaje, por medio de un morse, sensores, impresión sobre boleta y audio, no recuerdo muy bien el nombre del referente.

Por lo tanto lo que pensé fue un LDR que "lea" la frase en morse emitida por el LED, y que luego lo transcriba en el serial. Para lograr esto ocupe ChatGpt para que me ayude con los codigos y además de que me explicara cada linea del codigo. 

### Codigo en Arduino (Encargo 4) 

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
### Codigo LED - Bonus

```
int ledPin = 13;

// Tiempos en milisegundos
const int TIEMPO_PUNTO = 150;
const int TIEMPO_RAYA  = TIEMPO_PUNTO * 3;
const int SEPARADOR    = TIEMPO_PUNTO;
const int FIN_LETRA    = TIEMPO_PUNTO * 3;
const int FIN_PALABRA  = TIEMPO_PUNTO * 7;

// Frase a transmitir
String frase = "LA DISTRACCION NOS IMPIDE EL DESARROLLO DE UN PENSAMIENTO CRITICO";

// Tabla Morse
struct Morse {
  char letra;
  const char* codigo;
};

Morse morseTable[] = {
  {'A', ".-"},   {'B', "-..."}, {'C', "-.-."}, {'D', "-.."},
  {'E', "."},    {'F', "..-."}, {'G', "--."},  {'H', "...."},
  {'I', ".."},   {'J', ".---"}, {'K', "-.-"},  {'L', ".-.."},
  {'M', "--"},   {'N', "-."},   {'O', "---"},  {'P', ".--."},
  {'Q', "--.-"}, {'R', ".-."},  {'S', "..."},  {'T', "-"},
  {'U', "..-"},  {'V', "...-"}, {'W', ".--"},  {'X', "-..-"},
  {'Y', "-.--"}, {'Z', "--.."}
};

void setup() {
  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, LOW);
  Serial.begin(9600);
  Serial.println("Emisor Morse listo...");
}

void loop() {
  transmitirFrase(frase);
  Serial.println("\n--- Frase completa transmitida ---\n");
  delay(4000); // espera antes de repetir
}

// Enviar punto
void punto() {
  digitalWrite(ledPin, HIGH);
  delay(TIEMPO_PUNTO);
  digitalWrite(ledPin, LOW);
  delay(SEPARADOR);
}

// Enviar raya
void raya() {
  digitalWrite(ledPin, HIGH);
  delay(TIEMPO_RAYA);
  digitalWrite(ledPin, LOW);
  delay(SEPARADOR);
}

// Transmitir letra en Morse
void transmitirLetra(char letra) {
  if (letra == ' ') {
    delay(FIN_PALABRA);
    return;
  }

  letra = toupper(letra);
  const char* codigo = "";
  for (int i = 0; i < sizeof(morseTable)/sizeof(Morse); i++) {
    if (morseTable[i].letra == letra) {
      codigo = morseTable[i].codigo;
      break;
    }
  }

  for (int i = 0; codigo[i] != '\0'; i++) {
    if (codigo[i] == '.') punto();
    else if (codigo[i] == '-') raya();
  }

  delay(FIN_LETRA);
}

// Transmitir frase completa
void transmitirFrase(String texto) {
  for (int i = 0; i < texto.length(); i++) {
    transmitirLetra(texto.charAt(i));
  }
}

```

### Codigo LDR - Bonus

```
// Pin donde está conectado el LDR
int ldrPin = A0;

// Umbral de luz (ajusta según tu LED y ambiente)
int umbralLuz = 600;

// Estado anterior de luz (HIGH = LED encendido, LOW = LED apagado)
int estadoLuz = LOW;

// Variables de tiempo
unsigned long tiempoCambio = 0;

// Guarda los símbolos (punto y raya) de una letra
String simbolo = "";

// Tabla Morse simplificada (solo letras A–Z)
String morse[][2] = {
  {".-", "A"}, {"-...", "B"}, {"-.-.", "C"}, {"-..", "D"},
  {".", "E"}, {"..-.", "F"}, {"--.", "G"}, {"....", "H"},
  {"..", "I"}, {".---", "J"}, {"-.-", "K"}, {".-..", "L"},
  {"--", "M"}, {"-.", "N"}, {"---", "O"}, {".--.", "P"},
  {"--.-", "Q"}, {".-.", "R"}, {"...", "S"}, {"-", "T"},
  {"..-", "U"}, {"...-", "V"}, {".--", "W"}, {"-..-", "X"},
  {"-.--", "Y"}, {"--..", "Z"}
};

void setup() {
  Serial.begin(9600);
  Serial.println("Receptor Morse listo...");
  tiempoCambio = millis();
}

void loop() {
  int valorLuz = analogRead(ldrPin);
  unsigned long ahora = millis();

  // Detectar si hay luz o no
  int nuevaLuz = (valorLuz > umbralLuz) ? HIGH : LOW;

  // Detecta cambio de estado
  if (nuevaLuz != estadoLuz) {
    unsigned long duracion = ahora - tiempoCambio;
    tiempoCambio = ahora;

    if (nuevaLuz == HIGH) {
      // Luz encendida → terminó una pausa
      if (duracion > 600 && duracion < 1200) {
        // fin de letra
        decodificarLetra();
        simbolo = "";
      } else if (duracion >= 1200) {
        // fin de palabra
        decodificarLetra();
        Serial.print(" "); // espacio entre palabras
        simbolo = "";
      }
    } else {
      // Luz apagada → terminó una emisión (punto o raya)
      if (duracion < 300) {
        simbolo += ".";
      } else if (duracion >= 300 && duracion < 900) {
        simbolo += "-";
      }
    }
    estadoLuz = nuevaLuz;
  }
}

// Función para decodificar una letra en Morse
void decodificarLetra() {
  if (simbolo.length() == 0) return;

  for (int i = 0; i < 26; i++) {
    if (morse[i][0] == simbolo) {
      Serial.print(morse[i][1]);
      return;
    }
  }
  Serial.print("?"); // letra no reconocida
}


```



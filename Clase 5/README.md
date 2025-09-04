# Clase 5

Raspberry - Micro procesador, serve para hacer juegos o "cosas" arcade, tiene un sistema operativo, tiene entradas usb, hdmi, wifi. 
- Se le pueden conectar hasta dos pantallas !!!! (Raspberry 4 Model B). 
- Es linux, es más económico usar la barra de programación.
- Tiene patitas similares a las de arduino.
- Lo malo, hay que programarlo desde la terminal.
- Idea, correr un juego (minecraft) y ponerle un sensor a las raspi y que cambie algo del juego, que lo modifique, que haga cosas, que interfiera. nose

### Pantalla oled 0,96. 
Vamos a aprender a usar el ciclo "for". 
Repaso: 
- Variable (una cajita para guardar números), por ejemplo: una variable para cada uno de un grupo de personas:

"" 
String
Estudiante 1=0 Gato; 
String
Estudiante 1= Angel; 
""

Para estos cachos se utiliza una "array", es un arreglo, es una cajonera llena de variables, donde puedes encontrar la variable por medio de un índice. Solo se crea una pura estructura, donde entre cada variable, "una fila dentro de excel". "otro ladrillo del muro". 

#### ¿como se usa un "array"?
Lost numeros: 4, 8, 15, 16, 23, 42.

Como se declara: 
```
int numerosLost [] = {4,8,15,16,23,42};

String lineasPoema [] =
 {
"HOLA HOLA HOLA HOLA",
"hola",
};


void setup (){
Serial.begin(9600);  
//Serial.println(numerosLost [0]);
//Serial.println(numerosLost [1]);
//Serial.println(numerosLost [2]);
//Serial.println(numerosLost [3]);
//Serial.println(numerosLost [4]);
//Serial.println(numerosLost [5]);
// evitamos este cacho, con un ciclo "for" . 
// para un ciclo for, hay que saber: 
// - donde inicia.
// - donde terminar.
// - que se varia. 

Serial.println("empezamdo ciclo for");
for (int i =0; i <=5; i ++){
  
Serial.println(numerosLost [i]);
delay(1000);
}
Serial.println ("sali del ciclo for");


};

void loop (){

Serial.println("empezamdo ciclo for");
for (int i =0; i <=2; i ++){
  
Serial.println(lineasPoema [i]);
delay(1000);
}
Serial.println ("sali del ciclo for");

};
```






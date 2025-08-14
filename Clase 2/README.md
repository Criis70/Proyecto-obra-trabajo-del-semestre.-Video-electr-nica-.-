#Clase 2
## 14/08/2025
Processing y cosas, todo esta en el processing guardado(?)
// comenterios 
// los comentarios la pc se los salta
// (doble //) 
// ¿que es print?, es una función. 
// todas la funciones en processing se escribe asi ; Función (argumento)
// x es el argumento de la función, cuando esta en '' comillas'' es una palabra a impri-
// mir. 

// variables, son numeros o datos. 
// se crean definiendo siempre el tipo de variable.
// una varible guarda una información. 
char letra= 'a';
//no sirven para los numeros
//int para numero enteros
// el int se declara solo una vez

int a = 10; 
int b = 45;
int lasuma = 0; // es lo que ocupa, es nada 
lasuma= a + b; // el print te dice un momento de la variable

print (lasuma);
println(" Lasmas"); //salto de linea facil
print ("\n"); // salto de linea dificil

// otro tipo de variable, un numero de punto flotante
float notaAki= 6.9;
//uno puede convertir float en int
TODO ESTO LO ESCRIBI EN PROCESSING

Para hacer una linea en processing, hay que escribir la función ''line()''. donde debo decir la coordenadas, x o y (x,y) y la coordenada del otro. 
se declara //line(x1,y1,x2,y2);
line(10,20,30,40);
para ajustar el tamaño se ocupa el size();, tamaño del lienzo
size (400,600)
para definir el color de fondo. Se usa background();
background(200);
para que aparezcan las lineas, crearlas despues de pintar al fondo

Para incluir texto en el canvas, se utiliza la función text(); . Cuyos argumentos son texto, posicionX y posiciónY.
text(hola 50,50); 
Para el tamaño del texto textSize();
Para rellenar el texto fill();

Ahora para que tenga vida 

void setup(){
//aqui ocurren cosas. 
}
void draw(){
//y aqui ocurren otras cosas. 
}

Librerias, para complejizar aun más funciones del processing, el void draw() es un loop, siempre repite lo que esta escrito en el codigo. 
Las variables se suelen crear, antes del setup, una declaración de la variable. si se declara fuera del setup, se considera una variable global. 

Escribir alguna frase en processing. 

Entrega 3

Frase + variaciones de movimiento + constructivismo ruso. Un afiche en movimiento. 

investigar variables de tipo "String"






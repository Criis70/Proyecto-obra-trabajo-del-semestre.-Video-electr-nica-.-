# Encargo 5

Van a usar la estructura if para alterar el brillo del led a otros comportamientos. Por ejemplo, si el potenciometro mide hasta 100, que la intensidad sea maxima, si mide entre 100 y 500, que sea intensidad media, etc.

video registro: 
- link: <https://drive.google.com/file/d/1t6iPN7M8L6_HDIloO7FyQH9b4cj3lbEY/view?usp=sharing>

Codigo del encargo: 

```
 else if (valorPot >= 50 && valorPot < 150){
    intensidadLed= 0;
  }
  else if (valorPot >= 150 && valorPot < 200) {
    intensidadLed = 255;           // brillo bajo
  } 
   else if (valorPot >= 200 && valorPot < 250) {
    intensidadLed = 20;           // brillo bajo
  } 
   else if (valorPot >= 250 && valorPot <300) {
    intensidadLed = 255;           // brillo bajo
  } 
   else if (valorPot >= 300 && valorPot <350) {
    intensidadLed = 40;           // brillo bajo
  }
```

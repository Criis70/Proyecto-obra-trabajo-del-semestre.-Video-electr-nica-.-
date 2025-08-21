# Encargo Nro 3 

Processing, texto + construcctivismo ruso. 

```
int cantidad = 0;

void setup() {
  colorMode(HSB);
  size(600, 600);
  background(255);
  stroke(0);
  strokeWeight(2);
  noFill();
  frameRate(1000);
}
void draw() {
  background(frameRate, 0, 0);
  fill(255);
  rect(150, 80, 300, 450);

  line(150, 130, 230, 180); //1
  line(230, 180, 450, 110); //2

  fill(150, 250, 100); // 1 y 2
  beginShape();
  vertex(150, 80);
  vertex(150, 130);
  vertex(230, 180);
  vertex(450, 110);
  vertex(450, 80);
  endShape(CLOSE);

  line(150, 200, 450, 200);
  //line(150, 320, 450, 320);
  //line(150, 500, 450, 500);
  fill(0, 255, 20);
  rect(160, 320, 280, 200); //grande

  fill(255, 10, 240);
  rect(170, 470, 260, 40); //chico

  fill(150, 250, 100);
  rect(180, 260, 240, 20); // r1

  fill(150, 250, 100);
  rect(180, 220, 240, 3);// r2

  fill(5, 255, 200);
  textAlign(CENTER, CENTER);
  textSize(50);
  text("CARNIVAL", 300, 240);

  fill(255, 0, 255);
  textAlign(CENTER, CENTER);
  textSize(20);
  text("EL ALGORITMO DEL SUFRIMIENTO", 300, 350);

  fill(255, 0, 255);
  textAlign(CENTER, CENTER);
  textSize(17);
  text("Las mentes acostumbras a sufrir", 300, 380);
  fill(255, 0, 255);
  textAlign(CENTER, CENTER);
  textSize(17);
  text("abrazan la dependencia al conflicto,", 300, 400);
  fill(255, 0, 255);
  textAlign(CENTER, CENTER);
  textSize(17);
  text("al dolor, como rutina, como ritual,", 300, 420);
  fill(255, 0, 255);
  textAlign(CENTER, CENTER);
  textSize(17);
  text("como necesidad de sentirse vivos.", 300, 440);

cantidad= cantidad +10;

  fill(0);
  textAlign(CENTER, CENTER);
  textSize(20);
  text("TE QUEDAN " +  cantidad  + " DÍAS DE VIDA", 300, 490);
  text(frameCount,30,50);
}
```

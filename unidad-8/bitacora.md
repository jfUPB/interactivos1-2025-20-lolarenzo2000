
# Evidencias de la unidad 8

## Actividad 01
* **Documenta los referentes visuales que te inspiren**  
* **Define el concepto de las visuales que quieres crear**  
  En la pantalla del computador se verian particulas fluir de alguna parte de la pantalla (definida por el Tilt del Micro:Bit), que cambian de tamaño con el cambio de desibeles de la musica, y que rebotan con la parte contraria de la ventana hasta salir de la pantalla.
* **Explica cómo el móvil y el micro:bit controlarán las visuales**  
  En microbit se utilizaria el acelerometro para ver de donde caen las particulas, en el mobil se verian sliders con los que se podrian cambiar el tamaño, color y cantidad de particulas
* **Haz un bocetos de todas las interfaces del sistema**  
* **Haz un diagrama que explique cómo se comunicarán los diferentes componentes del sistema**  
## Actividad 02
```
let socket;
let tps;
let particulas = [];
const port = 3000;

class particle{
    constructor(x,xVelocity,y,yVelocity,size,color){
        this.x = x;
        this.xVelocity = xVelocity;
        this.y = y;
        this.yVelocity = yVelocity;
        this.size = size;
        this.color = color;
    }

    Move(){
        this.x += this.xVelocity;
        this.y += this.yVelocity;
        this.yVelocity += 0.5;
        if (this.y >= height-this.size/2 && this.yVelocity > 0){
            this.yVelocity *= -0.8;
        }
        if (this.y <= 0+this.size/2 && this.yVelocity < 0){
            this.yVelocity *= -0.8;
        }
        if (this.x <= 0+this.size/2 && this.xVelocity < 0){
            this.xVelocity *= -0.8;
        }
        if (this.x >= width-this.size/2 && this.xVelocity > 0){
            this.xVelocity *= -0.8;
        }
    }
}

function setup() {
    tps = 0;
    createCanvas(300, 400);
    background(220);
    for (let i=0; i < 10 ; i++){
      particulas.push(new particle(width/2,Math.random()*(5-1)+1,height/2,Math.random()*(5-1)+1,Math.random()*(50-20)+20,"blue"));
    }
}

function draw() {
    if (millis()-tps > 500){
        particulas.push(new particle(width/2,Math.random()*(5-1)+1,0,Math.random()*(5-1)+1,Math.random()*(50-20)+20,"blue"));
        tps = millis();
    }
    background(220);
    fill(255, 0, 0);
    for (let i = 0; i < particulas.length;i++){
      ellipse(particulas[i].x,particulas[i].y,particulas[i].size,particulas[i].size)
      particulas[i].Move();
    }
}

function rand(Min,Max){
    return Math.random()*(Max-Min)+Min;
}
```


# Evidencias de la unidad 8

## Actividad 01
* **Documenta los referentes visuales que te inspiren**  
  <img width="540" height="360" alt="image" src="https://github.com/user-attachments/assets/ec91353b-4a12-46aa-a9b6-777be8a58216" />
  <img width="168" height="300" alt="image" src="https://github.com/user-attachments/assets/d6163149-c9e5-4468-a5a3-8c9cf45b0b20" />  
  <img width="1024" height="415" alt="image" src="https://github.com/user-attachments/assets/396b4f0d-e36b-4256-9d67-153dbabde3f0" />
* **Define el concepto de las visuales que quieres crear**  
  En la pantalla del computador se verian particulas fluir de alguna parte de la pantalla (definida por el Tilt del Micro:Bit), que cambian de tamaño con el cambio de desibeles de la musica, y que rebotan con la parte contraria de la ventana hasta salir de la pantalla.
* **Explica cómo el móvil y el micro:bit controlarán las visuales**  
  En microbit se utilizaria el acelerometro para ver de donde caen las particulas, en el mobil se verian sliders con los que se podrian cambiar el tamaño, color y cantidad de particulas
* **Haz un bocetos de todas las interfaces del sistema**  
  <img width="1010" height="538" alt="image" src="https://github.com/user-attachments/assets/605becf2-0029-467f-80aa-048fc6aefaba" />
  <img width="309" height="409" alt="image" src="https://github.com/user-attachments/assets/137cffbe-b1a3-48f0-8fc6-b8946008b1c4" />

* **Haz un diagrama que explique cómo se comunicarán los diferentes componentes del sistema**
  <img width="584" height="606" alt="image" src="https://github.com/user-attachments/assets/3d84e171-992e-42f8-bd87-5a41c14accaf" />

## Actividad 02
dektop ``sketch.js``
``` js
class particle{
    constructor(x,xVelocity,y,yVelocity,size,color){
        this.x = x;
        this.xVelocity = xVelocity;
        this.y = y;
        this.yVelocity = yVelocity;
        this.size = size;
        this.OGSize = size;
        this.color = color;
    }

    Move(){
        this.x += this.xVelocity;
        this.y += this.yVelocity;
        
        switch(gravDir){
            case 0:
                break;
            case 1:
                this.yVelocity += gr;
                break;
            case 2:
                this.yVelocity -= gr;
                break;
            case 3:
                this.xVelocity += gr;
                break;
            case 4:
                this.xVelocity -= gr;
                break
        }
        if (this.y >= height-this.size/2 && this.yVelocity > 0){
            this.yVelocity *= amtg;
        }
        if (this.y <= 0+this.size/2 && this.yVelocity < 0){
            this.yVelocity *= amtg;
        }
        if (this.x <= 0+this.size/2 && this.xVelocity < 0){
            this.xVelocity *= amtg;
        }
        if (this.x >= width-this.size/2 && this.xVelocity > 0){
            this.xVelocity *= amtg;
        }
    }
}

function rand(Min,Max){
    return Math.random()*(Max-Min)+Min;
}

let incomingColor = { r: 0, g: 0, b: 255 };

let port;
let connectBtn;
let connectionInitialized = false;
let microBitConnected = false;
const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAITMICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};
let appState = STATES.WAIT_MICROBIT_CONNECTION;
let microBitX = 0;
let microBitY = 0;

let pColor;

let gravDir = 0;

let socket;
let particulas = [];
let amtg = -1;
let gr = 0.1;


let mySound;
let amplitude;

function preload() {
    soundFormats('mp3', 'ogg');
    mySound = loadSound('14_What if (The Alters Song).mp3');
    
}

function setup() {
    port = createSerial();

    amplitude = new p5.Amplitude();
    background(220);
    let cnv = createCanvas(windowWidth/2, windowHeight/2);
    cnv.mousePressed(canvasPressed); 

    // Button to connect/disconnect
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(0, 0);
    connectBtn.mousePressed(connectBtnClick);

    //Particulas
    for (let i=0; i < 10 ; i++){
        particulas.push(new particle(width/2,rand(-5,5),height/2,rand(-5,5),rand(150,200),"blue"));
    }

    socket = io("http://localhost:3000");

    socket.on("connect", () => {
        console.log("Connected to socket server:", socket.id);
    });

    socket.on("message", (msg) => {
        console.log("Message from server:", msg);
        if (data.r !== undefined && data.g !== undefined && data.b !== undefined) {
            incomingColor.r = data.r;
            incomingColor.g = data.g;
            incomingColor.b = data.b;
        }
    });
}

function draw() {
    if (!port.opened()) {
        connectBtn.html("Connect to micro:bit");
        microBitConnected = false;
    } else {
        microBitConnected = true;
        connectBtn.html("Disconnect");
        if (port.opened() && !connectionInitialized) {
            port.clear();
            connectionInitialized = true;
        }
    }
    switch (appState) {
        case STATES.WAIT_MICROBIT_CONNECTION:
            if (microBitConnected === true) {
                print("Microbit ready");
                noCursor();
                appState = STATES.RUNNING;
            }
        break;

        case STATES.RUNNING:
            if (microBitConnected === false) {
                print("Waiting microbit connection");
                cursor();
                appState = STATES.WAIT_MICROBIT_CONNECTION;
            }
            if(microBitConnected === true){
                serialRead();
                if (microBitY > 500){
                    gravDir = 1;
                } else if (microBitY < -500){
                    gravDir = 2;
                }
                else if (microBitX > 500){
                    gravDir = 3;
                }
                else if (microBitX < -500){
                    gravDir = 4;
                }
            }
        break;
    }
    background(220);
    // Get the current volume (0 → 1)
    let level = amplitude.getLevel();
    // Convert to decibels
    let dB = 20 * Math.log10(level || 0.0001); // avoid log(0)
    fill(255);
    textSize(18);
    text('Volume (dB): ' + dB.toFixed(2), 20, 50);

    // Optionally visualize it
    let size = map(level, 0, 1, 10, 400);
    ellipse(width / 2, height / 2, size, size);

    noStroke();
    for (let i = 0; i < particulas.length;i++){
        particulas[i].color = color(incomingColor.r,incomingColor.g,incomingColor.b)
        fill(particulas[i].color);
        particulas[i].size = particulas[i].OGSize + dB;
        let size = particulas[i].size;
        ellipse(particulas[i].x,particulas[i].y,size,size);
        particulas[i].Move();
    }
}

function canvasPressed(){
    mySound.play();
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

function serialRead() {
    if (port.availableBytes() > 0) {
        let data = port.readUntil("\n");
        if (data) {
            data = data.trim();
            let values = data.split(",");
            if (values.length == 2) {
                microBitX = int(values[0]);
                microBitY = int(values[1]);
            }
        }
    }
}
```
mobile ``sketch.js``
```js
let socket;
let circleColor;

let sR, sG, sB;
let prevR = 0, prevG = 0, prevB = 0;
const threshold = 5;

function setup() {
    createCanvas(300, 400);
    background(220);
    socket = io();

    socket.on('connect', () => console.log('Connected to server'));
    socket.on('message', (data) => console.log('Received message:', data));
    socket.on('disconnect', () => console.log('Disconnected from server'));
    socket.on('connect_error', (error) => console.error('Socket.IO error:', error));

    sR = createSlider(0, 255, 0);
    sR.position(width / 3, 100);
    sR.size(150);

    sG = createSlider(0, 255, 0);
    sG.position(width / 3, 175);
    sG.size(150);

    sB = createSlider(0, 255, 0);
    sB.position(width / 3, 250);
    sB.size(150);
}

function draw() {
    background(220);
    fill(255, 128, 0);
    textAlign(CENTER, CENTER);
    textSize(24);
    text('Elige Color De los circulos', width / 2, 25);

    let r = sR.value();
    let g = sG.value();
    let b = sB.value();

    text("R: "+r, width / 3, 85);
    text("G: "+g, width / 3, 160);
    text("B: "+b, width / 3, 225);

    circleColor = color(r, g, b);
    fill(circleColor);
    ellipse(width/2, 325, 100, 100);

    // Emitir solo si hubo cambio significativo
    if (r != prevR || g != prevG || b != prevB) {
        socket.emit('message', { r, g, b });
        prevR = r;
        prevG = g;
        prevB = b;
    }
}
```



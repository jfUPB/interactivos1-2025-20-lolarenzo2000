# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](https://editor.p5js.org/generative-design/sketches/P_2_1_5_01)

Código a modificar:

``` js
var drawMode = 1;

function setup() {
  createCanvas(800, 800);
  noFill();
}

function draw() {
  background(255);

  translate(width / 2, height / 2);

  // first shape (fixed)
  strokeWeight(3);
  overlay();

  // second shape (dynamically translated/rotated and scaled)
  var x = map(mouseX, 0, width, -50, 50);
  var a = map(mouseX, 0, width, -0.5, 0.5);
  var s = map(mouseY, 0, height, 0.7, 1);

  if (drawMode == 1) rotate(a);
  if (drawMode == 2) translate(x, 0);
  scale(s);

  strokeWeight(2);
  overlay();
}

function overlay() {
  var w = width - 100;
  var h = height - 100;

  if (drawMode == 1) {
    for (var i = -w / 2; i < w / 2; i += 5) {
      line(i, -h / 2, i, h / 2);
    }
  } else if (drawMode == 2) {
    for (var i = 0; i < w; i += 10) {
      ellipse(0, 0, i);
    }
  }
}

function keyPressed() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');

  // change draw mode
  if (key == '1') drawMode = 1;
  if (key == '2') drawMode = 2;
}
```

[Enlace a la aplicación modificada](https://editor.p5js.org/lolarenzo2000/sketches/rcED4UQuc)

Código modificado:

``` js
let drawMode = 1;
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
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

let X = 0;
let Y = 0;


function setup() {
  createCanvas(600, 600);
  noFill();
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

function updateButtonStates(newAState, newBState) {
  if (newAState === true && prevmicroBitAState === false) {
    //print("A pressed");
    drawMode = 1;
  }
  //if(newAState === false && prevmicroBitAState === true){
  //  print("A released")
  //}
  if (newBState === true && prevmicroBitBState === false) {
    //print("B pressed");
    drawMode = 2;
  }
  //if (newBState === false && prevmicroBitBState === true){
  //   print("B released")
  //}

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

function draw() {
  background(255);
  //******************************************
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

    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]);
          microBitY = int(values[1]);
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
        } else {
          print("No se están recibiendo 4 datos del micro:bit");
        }
      }
    }
  }
  //*******************************************

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
        if (microBitY < -200 || microBitY > 200){
          Y += microBitY/200
        }
        if (microBitX > 400|| microBitX < 400){
          X += microBitX/400;
        }
        translate(width / 2, height / 2);

        // first shape (fixed)
        strokeWeight(3);
        overlay();
        
        var x = map(X, 0, width, -50, 50);
        var a = map(X, 0, width, -0.5, 0.5);
        var s = map(Y, 0, height, 0.7, 1);
        
        if (drawMode == 1) rotate(a);
        if (drawMode == 2) translate(x, 0);
        scale(s);

        strokeWeight(2);
        overlay()
      }
      break;
  }
}

function overlay() {
  var w = width - 100;
  var h = height - 100;

  if (drawMode == 1) {
    for (var i = -w / 2; i < w / 2; i += 5) {
      line(i, -h / 2, i, h / 2);
    }
  } else if (drawMode == 2) {
    for (var i = 0; i < w; i += 10) {
      ellipse(0, 0, i);
    }
  }
}
```

## Video

[Video demostratativo](https://upbeduco-my.sharepoint.com/:v:/g/personal/lorenzo_perezs_upb_edu_co/Ebev1BpznzhErSjcQT95O-kBPPDgqPuwjyh78AJm3tBBVw?e=tY8E5f&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D)




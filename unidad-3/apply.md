# Unidad 3


## 🛠 Fase: Apply

### Actividad 06
~~~ js
let state = 0;

let init = 0;
let config = 1;
let armed = 2;
let exploded = 3;

let starTime = 0;

let fuse = 20;

let defused = false;

//Set the password
let password = "+-+"


let passkey = ""
let keyindex = 0

function setup() {
  createCanvas(400, 400);
  
  let plusBtn = createButton('+');
  plusBtn.position(220, 300);
  plusBtn.style('font-size','25px')
  plusBtn.style('border-radius','85px')
  plusBtn.mousePressed(plusPressed);
  
  let minusBtn = createButton('-');
  minusBtn.position(150, 300);
  minusBtn.style('font-size','25px')
  minusBtn.style('border-radius','85px')
  minusBtn.mousePressed(minusPressed);
  
  let armBtn = createButton('Arm');
  armBtn.position(170, 50);
  armBtn.style('font-size','25px')
  armBtn.style('border-radius','85px')
  armBtn.mousePressed(armPressed);
  
  let resetBtn = createButton('Reset');
  resetBtn.position(160,350);
  resetBtn.style('font-size','25px')
  resetBtn.style('border-radius','85px')
  resetBtn.mousePressed(resetPressed);
  
}

function draw() {
  background(220); 
  if (state == init){
    state = config;
  }
  else if (state == config) {
    fuseDraw();    
    textSize(16);
    textAlign(CENTER,CENTER)
    text('Config',200,25)
  }
  else if (state == armed){
    fuseDraw();    
    textSize(16);
    textAlign(CENTER,CENTER)
    text('Armed',200,25)
    text(passkey,200,290)
    
    countdown();
    if (fuse == 0){
      state = exploded
    }
  }
  else if (state == exploded){
    background('#DA572E')
    textSize(80);
    textAlign(CENTER,CENTER)
    text('Exploded',200,200);
  }  
}



//Dibujar los numeros en pantalla-------------
function fuseDraw(){
    textSize(100);
    textAlign(CENTER,CENTER)
    text(fuse,200,200);
}


//Cuenta Regresiva----------------------------
function countdown(){
  if (millis()-starTime > 1000){
    fuse -= 1
    starTime = millis();
  }  
}

//Defuse-------------------------------------
function defuse(){
  if (passkey.length == password.length){
    if (password == passkey){
      state = config
      fuse = 20;
      passkey = ""
    }else{
      passkey = ""
    }
  }
}


//botones------------------------------------
//----------------------------Reset
function resetPressed(){
  if (state == exploded){
    state = config
    fuse = 20;
    passkey = ""
  }
}
//--------------------------ArmBomb
function armPressed(){
  if (state == config){
    state = armed
  }
}

//-----------------------------Plus
function plusPressed(){
  if (state == config && fuse+1 <= 60){
    fuse += 1
  }
  else if (state == armed){
    passkey += "+"
    defuse()
  }
}
//----------------------------minus
function minusPressed() {
  if (state == config && (fuse-1 >= 10)){
    fuse -= 1
  }
  else if (state == armed){
    passkey += "-"
    defuse()
  }
}
~~~

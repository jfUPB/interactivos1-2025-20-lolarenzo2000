# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01
#### Describe detalladamente cómo funciona este ejemplo.
Se crea una clase _Pixel_ con un estado, un tiepo de inicio, un intervalo, posicion _x_ y _y_ , y un estado inicial del pixel; y una funcion que actualiza el pixel. Luego se crean dos pixeles con intervalos distintos, luego corre el codigo update que hace que los pixeles titilen en un intervalo antes dado.
* #### ¿Cuáles son los estados en el programa?
  El estado inicial y el estado de espera
* #### ¿Cuáles son los eventos/inputs en el programa?
  Prender y apagar repetidamente un pixel en un intervalo dado en un espacio dado
* #### ¿Cuáles son las acciones en el programa?
  Prender y apagar repetidamente un pixel

### Actividad 02
Implementemos juntos un semáforo simple (rojo, amarillo, verde) utilizando una máquina de estados en Micropython. Representaremos cada color del semáforo con un LED del display del micro:bit.
1. #### Codigo:
  ```py
from microbit import *
import utime

STATE_GREEN = 0
STATE_YELLOW = 1
STATE_RED = 2

state = STATE_GREEN

GREEN_DELAY = 2000
YELLOW_DELAY = 1000
RED_DELAY = 1500

start_Time = 0

while True:
    if state == STATE_GREEN:
        display.set_pixel(2,0,9)
        if utime.ticks_diff(utime.ticks_ms(),start_Time)>GREEN_DELAY:
            start_Time = utime.ticks_ms()
            display.set_pixel(2,0,0)
            state = STATE_YELLOW
    elif state == STATE_YELLOW:
        display.set_pixel(2,2,9)
        if utime.ticks_diff(utime.ticks_ms(),start_Time)>YELLOW_DELAY:
            start_Time = utime.ticks_ms()
            display.set_pixel(2,2,0)
            state = STATE_RED
    elif state == STATE_RED:
        display.set_pixel(2,4,9)
        if utime.ticks_diff(utime.ticks_ms(),start_Time)>RED_DELAY:
            start_Time = utime.ticks_ms()
            display.set_pixel(2,4,0)
            state = STATE_GREEN
  ```
3. #### Identifica los estados, eventos y acciones en tu código.
   * ##### Estados:
     Estado Verde(inicial), estado amarillo y estado rojo
   * ##### Eventos:
     Esperar
   * ##### Acciones:
     El semaforo cambia de estado
### Actividad 03
1. #### Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.
   Porque de una funcion se pueden hacer varias acciones posibles
2. #### Identifica los estados, eventos y acciones en el programa.
   * ##### Estados:
     estado inicial, estado "happy", estado "smile" y estado "sad"
   * ##### Eventos:
     Precionar el boton o esperar
   * ##### Acciones:
     Cambio de la expresion en la pantalla     
3. Describe y Aplica aL menos 3 vectores de prueba
   1.Esperar


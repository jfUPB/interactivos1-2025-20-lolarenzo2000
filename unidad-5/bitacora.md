
# Evidencias de la unidad 5

## Actividad 02

* ### ¿Por qué se ve este resultado?
  <img width="996" height="248" alt="image" src="https://github.com/user-attachments/assets/1c1781b0-b1da-4eb9-a4ba-99d7240770c5" />
  Porque la informacion esta siendo mandada en binario, no en ascii.
* ### Ahora cambia la opción de Mostrar datos como a Todo en Hex y vuelve a capturar el resultado.
  <img width="986" height="239" alt="image" src="https://github.com/user-attachments/assets/9c74c974-0080-4d8c-b6e8-ad72ea3d535f" />
  ¿Cómo está relacionado con esta línea de código?
  
  ```py
  data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
  ```
  La funcion ``struct.pack()`` devuelve los bytes de los valores dados en un formato establecido.
  
* ### ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?
  En ventajas, se usa menos memoria, es mas facil de leer y escribir para la maquina, y en desventajas es que es dificil de leer por el humano y se requiere codigo o software que lo decifre.
* ### ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato ``'>2h2B'``? ¿Qué significa cada uno de los bytes que se envían?
  <img width="335" height="105" alt="image" src="https://github.com/user-attachments/assets/69a20744-6bad-4a4d-adaf-e5559bf6eda6" />
  
  * Se estan enviando 6 bytes por mensaje.
  * ``'>'`` significa **big-endian** que hace que los bytes se ordenen de que el primero es el que representa el valor mas grande, ``'2h'`` significa dos variables **short** las cuales se divide en dos bytes cada una, ``'2b'`` significa dos variables de **signed char** que ocupan un byte cada una.
  * Los 2 primeros bytes son ``xValue``, los suigientes 2 son ``yValue`` y los ultimos dos son ``aState`` y ``bState`` respectivamente.

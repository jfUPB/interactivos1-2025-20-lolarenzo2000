
# Evidencias de la unidad 5


## Investigacion
### Actividad 02

* #### ¿Por qué se ve este resultado?
  <img width="996" height="248" alt="image" src="https://github.com/user-attachments/assets/1c1781b0-b1da-4eb9-a4ba-99d7240770c5" />
  Porque la informacion esta siendo mandada en binario, no en ascii.
* #### Ahora cambia la opción de Mostrar datos como a Todo en Hex y vuelve a capturar el resultado.
  <img width="986" height="239" alt="image" src="https://github.com/user-attachments/assets/9c74c974-0080-4d8c-b6e8-ad72ea3d535f" />
  ¿Cómo está relacionado con esta línea de código?
  
  ```py
  data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
  ```
  La funcion ``struct.pack()`` devuelve los bytes de los valores dados en un formato establecido.
  
* #### ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?
  En ventajas, se usa menos memoria, es mas facil de leer y escribir para la maquina, y en desventajas es que es dificil de leer por el humano y se requiere codigo o software que lo decifre.
* #### ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato ``'>2h2B'``? ¿Qué significa cada uno de los bytes que se envían?
  <img width="335" height="105" alt="image" src="https://github.com/user-attachments/assets/69a20744-6bad-4a4d-adaf-e5559bf6eda6" />
  
  * Se estan enviando 6 bytes por mensaje.
  * ``'>'`` significa **big-endian** que hace que los bytes se ordenen de que el primero es el que representa el valor mas grande, ``'2h'`` significa dos variables **short** las cuales se divide en dos bytes cada una, ``'2b'`` significa dos variables de **signed char** que ocupan un byte cada una.
  * Los 2 primeros bytes son ``xValue``, los suigientes 2 son ``yValue`` y los ultimos dos son ``aState`` y ``bState`` respectivamente.
### Actividad 03
* #### Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.
  Porque antes el tamaño de lo que llegaba era variable, ahora siempre se mandan solo 6 bytes, donde cada dato siene sus propios bytes.
* #### Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas?
  La nueva funcion ``readSerialData()`` el cual se divide en 5 partes:  
  1. ##### Leer datos disponibles del puerto serial
     ``` js
     let available = port.availableBytes();
     if (available > 0) {
       let newData = port.readBytes(available);
       serialBuffer = serialBuffer.concat(newData);
     }
     ```
     * Se checkea si hay bytes en el puerto serial.
     * si si hay bytes, se le concatenaran al Serial Buffer.
  2. ##### Procesar el buffer de datos
     ``` js
     while (serialBuffer.length >= 8) {
       if (serialBuffer[0] !== 0xaa) {
           serialBuffer.shift();
           continue;
         }
     ```
     * El loop hace que el programa pueda siempre lea el bufer solo caundo hay minimo un paquete de datos.
     * Si el primer byte del buffer no es igual al header con ``serialBuffer.shift()`` se remueve el primer byte y luego se resetea el loop con ``continue``.
     
  3. ##### Procesamiento del packete
     ``` js
     if (serialBuffer.length < 8) break;
     ```
     * El loop se rompera si el serial buffer es menos de un paquete
     ``` js
     let packet = serialBuffer.slice(0, 8);
     serialBuffer.splice(0, 8);
     ```
     * Como si se encontro el buffer y hay minimo 8 bytes, el codigo extraera los 8 primeros bytes como un packete con la funcion ``slice()``.
     * Luego se remueven los mismos bytes del serial buffer.
  4. ##### Validacion checksum
     ``` js
     let dataBytes = packet.slice(1, 7);
     let receivedChecksum = packet[7];
     let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;
     ```
     * Se separan los datos del paquete, y se guarda el checksum del paquete.
     * Se genera un checksum diferente con los datos recividos.
     ``` js
     if (computedChecksum !== receivedChecksum) {
       console.log("Checksum error in packet");
       continue; 
     }
     ```
     * Si el checksum generado es diferente del checksum del packete, el codigo continuara a chekear el siguiente paquete.

  5. ##### Extraccion de datos del paquete
     ``` js
     let buffer = new Uint8Array(dataBytes).buffer;
     let view = new DataView(buffer);
     microBitX = view.getInt16(0) + windowWidth / 2;
     microBitY = view.getInt16(2) + windowHeight / 2;
     microBitAState = view.getUint8(4) === 1;
     microBitBState = view.getUint8(5) === 1;
     ```
     * Los datos se convierten en un array buffer usando ``Uint8Array(dataBytes).buffer``.
     * Se crea un ``DataView`` para leer los diferentes tipos de datos en el buffer:
     * ``getInt16()`` Lee los dos bytes desde la posicion pedida.
     * ``getUnit8`` Lee el byte de la posicion pedida.

## Reto
### Actividad 04
1. Remplazo el sistema ascii del viejo codigo con el nuevo sistema binario, usando el mismo codigo del ejemplo proporcionado, la aplicacion casi funciona como lo hacia la otra aplicacion pero con una sensibilidad diferente.
2. El problema de la sensibilidad era una operacion que faltaba, la aplicacion ya funciona igual que al codigo con el metodo ascii.
3. [Nuevo Codigo](https://editor.p5js.org/lolarenzo2000/full/4XhanlZmE)

## Rubrica
1. ### Profundidad de la Indagación ``Logrado 3.8``
   Me hiciste buenas preguntas y comparaciones, aunque me faltó profundizar un poco más en las implicaciones del diseño de los protocolos.

2. ### Calidad de la Experimentación ``Logrado 3.5``
   Describí bien mis pruebas y lo que observé, pero no llegué a proponer experimentos más creativos o diferentes a los esperados.

3. ### Análisis y Reflexión ``Logrado 4.0``
   Reflexioné con claridad sobre lo que pasó y lo conecté con la teoría, aunque me faltó generalizar más allá del ejercicio puntual.

4. ### Apropiación y Articulación de Conceptos ``Logrado 4.0``
   Entendí y expliqué los conceptos principales con mis palabras, aunque no los integré como un sistema completo.
### Nota final: ``3.8/5.0``


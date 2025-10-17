
# Evidencias de la unidad 7

## Actividad 01
- **¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de ``http://localhost:3000`` o la IP local de tu computador para que el celular se conecte?**  
  Obtuve la url ``https://366bl71v-3000.use2.devtunnels.ms/``, porque si usaramos la url local el celular no podria comunicarse con el computador.
- **Describe brevemente qué hace ``npm install`` y ``npm start``**
  - ``npm install``: Instala las dependencias del projecto y sus paquetes.
  - ``npm start``: Ejecuta un script predefinido. Su funcion principal es inicializar el programa o un servidor de developer.
- **¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?**  
  Aparece que se conecto un cliente, pero no especifica cual.
- **Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?**  
  La aplicacion funciono, pero tenia un poco de latencia.
## Actividad 02
- **¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?**  
  Porque queremos una conexion entre dos dispositivos que pueden no estar en el mismo wifi.
- **Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil**
  Funciona como un mouseDragged, donde detecta donde se esta presionando y moviendo. El thershold esta ahi para controlar el movimiento haciendo que el movimiento que se envia sea mayor a 5.
- **Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?**  
  Al usar ip local no hay problemas de latencia, ademas del riesgo que puede tener usar un devtunnel, ademas de que hay que recordar cerrarlo.
- **Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal)**  
  <img width="1918" height="1026" alt="image" src="https://github.com/user-attachments/assets/a1b56844-0384-47ae-8c99-a6f913dc90bb" />

## Actividad 03
- **¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?**  
  Con app.get() se decide una ruta manual, mientras que con expres.static() se automatiza la entrega de archivos definiendo una carpeta.
- **Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?**
- **Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?**  
  Solo el que es escritorio recibiria el mensaje, porque el movil solo envia.
- **¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?**  
  Menciona la informacion que se estan comunicando las aplicaciones entre si, y sirve para ver si hay errores.

## Actividad 05



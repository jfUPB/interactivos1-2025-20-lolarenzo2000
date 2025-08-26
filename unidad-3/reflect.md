# Unidad 3


## 🤔 Fase: Reflect

### Actividad 08 (Autoevaluacion)
---


#### Parte 1: recuperación de conocimiento (Retrieval Practice)  

1. ##### Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?  
    Evento inicial, evento disparador, evento final y acciones  
  
2. ##### Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender varios eventos y tareas “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit o en p5.js. ¿Qué problema soluciona en comparación con usar funciones como sleep()?  
    Hace que se puedan hacer varias cosas a la vez  
  
3. ##### Imagina que tienes que añadir una nueva funcionalidad a la bomba: si se recibe un evento especial (por ejemplo, una combinación de botones o un comando serial) mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?   
    Seria poner una accion que solo se entra despues de undir la combinacion o llega el comando, que hace que el temporizador de divida por 2  
  
4. ##### Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.  
    Sirve para ver si el programa funciona de forma logica  
  

  
#### Parte 2: reflexión sobre tu proceso (Metacognición)

1. ##### ¿Qué parte del diseño de la bomba te resultó más desafiante: crear el diagrama de estados o traducir ese diagrama a código? ¿Por qué?
   El diagrama de estados, soy mejor programando en el momento
   
3. ##### Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?
   La combinacion para desarmar la bomba no funcionaba en un punto porque estaba intentando usar un bucle
   
5. ##### El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?
   Traduci el codigo que ya habia hecho en micro:bit poco a poco
    
7. ##### Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?
   En  un videojuego donde la animacion pase dependiendo del estado del personaje

### Actividad 9 (FeedBack)
---
1. #### Continuar: ¿Qué actividad, explicación o ejemplo de esta unidad te ayudó más a entender el poder de las máquinas de estados? ¿Qué elemento consideras que es indispensable y debería mantener?  
   Todo
  
2. #### Dejar de hacer: ¿Hubo algún paso o actividad que te pareció confuso? ¿Qué cambiarías o eliminarías?  
   No
  
3. #### Empezar a hacer: ¿Qué te habría ayudado a entender mejor?  
   Entendi bien el tema
  
4. #### Ritmo y dificultad: En una escala del 1 (muy fácil) al 5 (muy difícil), ¿Cómo calificarías la dificultad de pasar del análisis de un programa a diseñar y programar uno complejo? ¿Por qué?  
   2 Me gusta hacer codigo no lo considero dificil pero aveces se me olvida programar con concurrencia
  
5. #### Comentario adicional: ¿Hay algo más que te gustaría compartir sobre tu proceso de aprendizaje en esta unidad? ¿Algún momento de frustración o de “¡Aha!” que quieras destacar?  
   Fue bastante interesante pasar de micro:bit a un lenguaje mas complejo como P5js

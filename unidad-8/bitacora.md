# Bitácora de aprendizaje de la unidad 8

## Actividad 01


<img width="1315" height="696" alt="image" src="https://github.com/user-attachments/assets/ed3146d1-271b-47c4-bf0f-37fefc81c97e" />

Este programa lo que hace es hacer que un circulo se mueva en la pantalla. Cuando se hace click el circulo se queda quieto por un rato y despues de eso se vuelve a mover con un tamaño diferente y en la consola aparece que se realizo un proceso matematico para calcular el nuevo tamaño del circulo.

Yo esperaba ver uin circulo que se moviera de manera normal, pero creo q  ue por este metodo

<img width="727" height="287" alt="image" src="https://github.com/user-attachments/assets/46e2f2a3-5660-4c63-bcb3-708696e69e00" />

la pc siempre se va a demorar un poquito para cambiar el tamaño del circulo.

ahora modificamos el codigo y pasa esto:

<img width="1493" height="784" alt="image" src="https://github.com/user-attachments/assets/2210ddd9-6939-47a6-8941-9dc81c3309d0" />

Ahora el circulo no se queda quieto, pero el resultado no sale de inmediato en la consola, se demora un poco mas. Creo que es porque eel programa ahora designa solo una parte de su capacidad para realizar el procedimieto, mientras que la otra parte sigue enfocada en hacer que el programa siga funcionando y el circulo se siga moviendo.

##### Diferencia entre paralelismo y concurrencia

Como lo vimos en clase, el paralalelismo es cuando mar, valencia, chepi y yo hacemos 4 acciones todo el tiempo a la misma vez, mientras que la concurrencia es cuano nat ella sola hace un poquito de cada tarea pero lo haace tan rapido que parece que estuviera haciendo todas al mismo tiempo


## Actividad 02



<img width="909" height="636" alt="image" src="https://github.com/user-attachments/assets/e1a5e370-8161-4ec3-a104-cc35fa40d543" />




### ¿en qué partes del código se está protegiendo el acceso a la variable circleSize?,
en el código anterior se está protegiendo el acceso a la variable circlesize en los lugares donde se usa lock y unlock esto pasa en la función draw cuando se dibuja el círculo y también en heavycomputation cuando se cambia el tamaño del círculo usando ofrandom esas partes del código son las que evitan que los dos hilos accedan a circlesize al mismo tiempo

### ¿qué ocurre con el paralelismo cuando se sincroniza el acceso a un recurso compartido?, ¿el rendimiento puede verse afectado por el uso de mutex?, ¿por qué?,
cuando se sincroniza el acceso a un recurso compartido el paralelismo se reduce un poco porque los hilos tienen que esperar a que el otro termine de usar el recurso antes de poder acceder a él esto hace que el programa sea más seguro pero también un poco más lento el rendimiento puede verse afectado porque los hilos pasan tiempo bloqueados esperando el turno del mutex aunque eso evita errores y hace que los datos sean correctos

### ¿qué ocurre si cambias el valor de la variable useLock?, ¿por qué crees que ocurre esto?,
cuando cambio el valor de uselock a verdadero el programa usa el mutex para proteger el contador y el resultado sale correcto o muy cercano al valor esperado pero si lo cambio a falso el contador termina con un número mucho menor al que debería tener porque los hilos se pisan entre sí al modificar la variable sin control eso pasa porque varios hilos están tratando de sumar al mismo tiempo y se pierden algunas actualizaciones

### ¿por qué ocurre la condición de carrera en este caso?,
la condición de carrera ocurre porque varios hilos están intentando modificar la misma variable counter al mismo tiempo y la operación de incremento no es atómica el procesador primero lee el valor lo guarda en un registro luego lo incrementa y después lo escribe en memoria si dos hilos hacen eso al mismo tiempo pueden leer el mismo valor y sobreescribir el resultado del otro haciendo que el contador no aumente bien

### ¿cómo puede presentarse la condición de carrera en este caso?, ¿qué es lo que está pasando?, te pido que propongas un ejemplo,
una condición de carrera puede pasar por ejemplo si el contador vale 5 y dos hilos lo van a aumentar el hilo a lee 5 y lo incrementa a 6 pero antes de escribirlo el hilo b también lee 5 los dos terminan escribiendo 6 en memoria y el resultado final queda mal porque debería ser 7 esto pasa porque los dos hilos hicieron la operación sin sincronizarse y uno sobreescribió el trabajo del otro


## Actividad 03

### ejecuta el código y observa el resultado

al ejecutar la versión secuencial se nota que el cálculo bloquea la interfaz y tarda mucho en completarse, la ventana puede quedar sin actualizar hasta que termina el bucle, en la versión paralelo el tiempo total de cálculo suele reducirse y la interfaz se mantiene más responsiva porque el trabajo se distribuye entre varios hilos, la textura final se carga cuando todos los hilos han terminado, a veces la mejora no es proporcional al número de hilos por el overhead de crear y sincronizar hilos y por limitaciones del hardware como el ancho de banda de memoria. el código paralelo divide la imagen por filas y crea un objeto mandelbrotthread para un rango de filas por hilo, cada hilo calcula sus píxeles y escribe directamente en el ofpixels compartido, no se usa un mutex porque cada hilo escribe en filas distintas evitando solapamiento de posiciones, el main thread controla el estado comprobando isthreadrunning y cuando todos los hilos han terminado actualiza la textura con texture.loaddata, esto evita leer pixels mientras los hilos escriben, además la versión paralelo detecta el número de hilos del hardware con hardware_concurrency y asigna rowsperthread para repartir la carga



Para experimentar, aumente el numero de hilos y ver como se relacionaba este con el tiempo dee carga. Mi hipotesis es que conforme vaya aumentando los hilos menor va a ser el tiempo, pues es lo mas logico y es precisamente por eso que la actividad anterior funciono


<img width="644" height="131" alt="image" src="https://github.com/user-attachments/assets/8ee7d3e8-146d-4436-90bc-624cd0f72f23" />


<img width="679" height="187" alt="image" src="https://github.com/user-attachments/assets/c3f09f2b-e796-4357-8db4-d6878cb6e4dc" />


<img width="656" height="149" alt="image" src="https://github.com/user-attachments/assets/83c20e95-9092-479a-9996-3a1a5634324b" />


Es charro, porque al principio, con dos hilos trabaja mas que con uno. Pero cuando dupplico la cifra a 4 hilos llega a ser incluso mas lento, esto muestra que el rendimiento mejora inicialmente al aumentar los hilos hasta cierto punto pero luego deja de mejorar e incluso empeora, esto puede deberse a que el tamaño de la imagen o la carga de trabajo no es tan grande, por lo tanto el costo de crear y manejar más hilos empieza a ser mayor que el beneficio, por ende mi hipotesis no era correcta :(

## Actividad 04


Sin hilos:

<img width="1031" height="823" alt="image" src="https://github.com/user-attachments/assets/887ad053-b9b1-45a5-93b5-19fa1ebd7ffd" />


Con hilos:

<img width="1007" height="737" alt="image" src="https://github.com/user-attachments/assets/cdbdda56-191a-47cd-ad5b-825e456a0276" />



### ¿Cuál es la estructura de datos principal que contiene la información de todos los boids y que es accedida por múltiples hilos?
la estructura principal es un vector llamado boids que pertenece a la clase flock, este vector guarda todos los objetos boid y es compartido entre el hilo principal que dibuja y el hilo secundario que actualiza el movimiento de los boids

### ¿Qué operaciones realizan sobre el vector de boids compartido en Flock::threadedFunction()?
en esta función el hilo trabajador recorre el vector boids y llama a la función run de cada boid, dentro de esa función se calculan las fuerzas de separación alineación y cohesión y se actualizan las posiciones y velocidades de cada boid, es decir que el hilo está modificando constantemente los valores del vector

### ¿Qué operación realiza ofApp::draw() sobre el vector compartido?
en la función draw se recorre el vector boids para dibujar cada boid en pantalla usando sus posiciones actuales, el hilo principal solo lee los datos del vector para representar la simulación visualmente

### ¿Qué operación realizan Flock::addBoid() y ofApp::mouseDragged()?
estas funciones añaden nuevos boids al vector compartido cuando se arrastra el mouse, básicamente modifican el tamaño del vector y agregan nuevos objetos boid al final

### Describe un escenario específico donde la falta de sincronización podría causar un problema
si el hilo trabajador está recorriendo el vector de boids para calcular la separación y al mismo tiempo el hilo principal o la función mouseDragged intenta añadir un nuevo boid al vector, podría cambiar el tamaño del vector mientras el otro hilo lo está leyendo, esto puede causar errores de memoria o que el programa se cierre porque el iterador pierde su referencia al cambiar el tamaño del vector

### Localiza todas las llamadas a lock() y unlock() dentro de la clase Flock
en la clase flock se usan lock y unlock en la función addBoid cuando se añade un nuevo boid, también en la función threadedFunction al principio y al final del ciclo donde se actualizan los boids, y en la función draw dentro de ofApp antes y después de recorrer el vector para dibujar los boids

Justificación: cómo las llamadas a lock()/unlock() evitan el problema anterior
las llamadas a lock y unlock bloquean el acceso al vector mientras un hilo lo está usando, esto hace que ningún otro hilo pueda modificar el vector hasta que se libere el bloqueo, de esa forma se evita que un hilo cambie el tamaño del vector mientras otro lo está leyendo o escribiendo, protegiendo la memoria y evitando errores

Aunque los locks aseguran la correctitud, por qué tener muchos hilos esperando para adquirir un lock podría limitar el rendimiento del paralelismo
porque cuando varios hilos quieren acceder al mismo recurso bloqueado, todos deben esperar a que se libere el lock, esto hace que los hilos se detengan temporalmente y no puedan trabajar en paralelo, causando cuellos de botella y reduciendo la ventaja del uso de varios hilos

En el ejemplo dado solo hay dos hilos, el principal y el trabajador, realmente se está explotando la idea de tener hilos
no completamente, porque solo se usa un hilo extra para calcular el movimiento de todos los boids, si se dividiera el trabajo en varios hilos que cada uno calcule un grupo diferente de boids se podría aprovechar mejor el paralelismo del procesador

### Qué pasaría si tuviéramos varios hilos que calculan el movimiento de los boids, cómo podrías implementarlo y qué problemas podrían surgir
se podría dividir el vector de boids en varias partes y asignar un hilo para cada grupo, así todos se actualizarían al mismo tiempo, pero habría problemas si varios hilos intentan acceder a los mismos datos de vecinos para calcular las fuerzas, eso podría causar condiciones de carrera o lecturas inconsistentes, para solucionarlo se podrían usar locks más específicos o dividir el cálculo en fases donde primero todos leen los datos y luego todos escriben los resultados

### Qué diferencias encuentras entre el Flocking sin hilos y el Flocking con hilos, y por qué es importante la sincronización en el segundo caso
en el flocking sin hilos todo se ejecuta en el mismo hilo por lo que no hay riesgo de conflictos de memoria, pero el rendimiento baja al aumentar los boids, en cambio en el flocking con hilos la simulación se actualiza aparte mientras se dibuja, lo que mejora la fluidez, pero como hay varios hilos accediendo al mismo vector se necesita sincronización para evitar errores y condiciones de carrera

### Por qué al añadir un nuevo boid la simulación se ralentiza, y qué ocurre si se añaden muchos boids
porque cada boid tiene que calcular su relación con los demás boids, así que cuando se añaden más el número de cálculos crece mucho, si se agregan demasiados boids el programa se vuelve más lento porque cada frame requiere más procesamiento

### Por qué la versión con hilos tiene un sleep(5) en el hilo trabajador, y qué pasaría si lo eliminamos
el sleep se usa para darle un pequeño descanso al hilo trabajador y evitar que consuma todos los recursos del procesador, si se elimina el hilo estaría corriendo sin pausa lo que aumentaría el uso de la cpu y podría volver más inestable la simulación o hacer que el dibujo no alcance a actualizarse correctamente

### Compara el rendimiento de ambos enfoques, cuál crees que es más eficiente y por qué
el enfoque con hilos es más eficiente porque permite que el cálculo y el dibujo se hagan al mismo tiempo, el hilo secundario actualiza las posiciones mientras el principal dibuja, así se aprovecha mejor el procesador y la simulación se siente más fluida especialmente con muchos boids

### Qué pasaría si no se usaran lock y unlock en la versión con hilos y cómo afectaría esto al comportamiento del programa
sin los locks los hilos podrían acceder al vector al mismo tiempo y modificarlo mientras otro lo está leyendo, esto causaría comportamientos impredecibles como boids que desaparecen o posiciones corruptas, incluso el programa podría cerrarse por errores de memoria difíciles de reproducir

## Actividad 05

parte clave de la función modificada que calcula el píxel para el conjunto de julia:

```javascript

int calculateJuliaPixel(float x, float y, glm::vec2 k, int maxIterations) {
    float zx = x;
    float zy = y;
    int iteration = 0;

    while (zx * zx + zy * zy < 4.0f && iteration < maxIterations) {
        float xtemp = zx * zx - zy * zy + k.x;
        zy = 2.0f * zx * zy + k.y;
        zx = xtemp;
        iteration++;
    }

    return iteration;
}
```

mapeo de la posición del mouse a la constante k
``` javascript
void ofApp::mouseMoved(int x, int y ){
    juliaK.x = ofMap(x, 0, ofGetWidth(), -1.5f, 1.5f);
    juliaK.y = ofMap(y, 0, ofGetHeight(), -1.5f, 1.5f);
    recalculate = true;
}
```

### cómo reutilicé la estructura de hilos de la versión mandelbrot

la estructura de hilos fue prácticamente la misma, cada hilo sigue procesando un rango de filas del framebuffer, lo único que cambió fue la función que se llama dentro del hilo, en lugar de calculateMandelbrotPixel ahora se usa calculateJuliaPixel, y también se pasa la constante k actual como parámetro, el resto de la lógica para crear, lanzar y sincronizar los hilos no necesitó modificaciones grandes, solo actualicé el nombre de la función y la variable que usa los datos del fractal

###cómo me aseguré de que la imagen se recalculara cuando el mouse se movía

cada vez que el mouse se mueve se actualiza la constante juliaK, y además se activa una bandera llamada recalculate, en la función update() se revisa esta bandera, y si está activa se vuelve a lanzar el cálculo completo del fractal con los hilos, de esa forma la imagen se refresca automáticamente cuando el mouse cambia de posición

### capturas de pantalla

<img width="1788" height="842" alt="image" src="https://github.com/user-attachments/assets/79450e96-f5a9-4533-89ff-29d94d125fcd" />

<img width="1797" height="819" alt="image" src="https://github.com/user-attachments/assets/0865f5d0-f8e3-47d9-9146-39b10068be0c" />

### desafíos encontrados 

uno de los principales desafíos fue ajustar el rango de mapeo del mouse para que los cambios en el fractal fueran suaves, al principio los valores variaban demasiado rápido y el fractal parpadeaba, también tuve que asegurarme de que la variable k se compartiera correctamente entre los hilos sin generar errores de sincronización, otro detalle fue optimizar el recalculo para que no se quedara congelado el programa cuando se movía el mouse muy rápido

## Autoevaluacion

Nota propuesta: 5.0

Considero que comprendi bastante claros los conceptos en la actividad #1, comprendo el porque al da click el circulo se quedaba quieto durante un rato, y lo explique con mis propias palabras con un ejemplo que vimos en clase, demostrando que si presto atención a los ejemplos y tengo una alta comprension de estos

<img width="1232" height="701" alt="image" src="https://github.com/user-attachments/assets/15218348-fe00-45df-8218-de454be33d43" />



Tambien segui el conducto regular a la hora de experimentar con el numero de hilos, planteando una hipotesis la cual a pesar al principio no estaba buena, supe como argumentar la razon por la que me equivoque


<img width="1225" height="688" alt="image" src="https://github.com/user-attachments/assets/ee8e0da2-ed14-4f8c-be29-d4f3ad54ea5d" />



con esta misma actividad  entendí cómo se puede medir el rendimiento y la eficiencia del código paralelo, aprendí a usar las funciones de tiempo para analizar cuánto se demora el cálculo completo y comprobé que usar varios hilos sí mejora el desempeño.

Por ultimo, para la actividad final aprendí a mapear la posición del mouse a los valores de esa constante para crear una visualización interactiva, logré que el cálculo se actualizara automáticamente al mover el mouse, y eso hizo que el programa fuera más dinámico y visualmente interesante

























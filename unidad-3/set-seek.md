# Unidad 3

## 🔎 Fase: Set + Seek

### ACTIVIDAD INTEGRADORA DE INVESTIGACIÓN

#### Predicción

##### ¿Cuál será la salida final en la consola de este programa?

La salida del programa en la consola mostraria varias lineas. Primero aparece el experimento con los parametros y ahi se ve que val_A empieza en 20 y dentro de la funcion sumaPorValor se muestra 30 pero al final sigue siendo 30 tambien. Luego con val_B empieza en 20, dentro de la funcion cambia a 30 y al final tambien queda en 30. Con val_C pasa lo mismo, arranca en 20, luego dentro de la funcion con el puntero sale 30 y al terminar vuelve a mostrarse 20 otra vez.

Despues viene la parte de las variables estaticas, ahi se ve que cada vez que se llama la funcion ejecutarContador el numero va aumentando, primero 1, luego 2 y por ultimo 3. En resumen el programa deberia imprimir algo como los valores iniciales y finales de las tres variables con las funciones, y al final las tres llamadas de la funcion estatica mostrando el contador que va creciendo.

##### Salida que espero

```

Valor inicial de val_A: 20
   Dentro de sumaPorValor, 'a' ahora es: 30
Valor final de val_A: 30

Valor inicial de val_B: 20
   Dentro de sumaPorReferencia, 'a' ahora es: 30
Valor final de val_B: 30

Valor inicial de val_C: 20
   Dentro de sumaPorPuntero, '*a' ahora es: 30
Valor final de val_C: 20

  Llamada a ejecutarContador. Valor de contador_estatico: 1
   Llamada a ejecutarContador. Valor de contador_estatico: 2
   Llamada a ejecutarContador. Valor de contador_estatico: 3
```


##### MAPA CONCEPTUAL
<img width="1920" height="1080" alt="CODIGO" src="https://github.com/user-attachments/assets/212dd117-4171-44e1-8bd3-1d8bc80656fc" />


#### Verificación y analisis

##### comparacion de salida con prediccion

<img width="1471" height="702" alt="image" src="https://github.com/user-attachments/assets/8697c96e-ee88-4cd6-8f1c-4ddebbd980b8" />



###### Diferencias y por que creo se dieron

Las diferencias principales entre la predicción y la salida real ocurrieron en el valor final de val_A y val_C. En la predicción se esperaba que val_A terminara en 30, pero en realidad quedó en 20 porque al pasarlo por valor la función recibe solo una copia, y cualquier cambio afecta únicamente a la variable local dentro de la función. En cambio, con val_C se predijo que quedaría en 20, pero realmente terminó en 30, ya que al pasarse por puntero la función accede directamente a la dirección de memoria de la variable original, modificándola de forma permanente.






##### Momentos clave en la  ejecucion del programa

se inicializan las variables

<img width="1881" height="862" alt="image" src="https://github.com/user-attachments/assets/fa6c8a34-40cb-484e-9d25-2929ea05e024" />



Esta imagen muestra que aunque dentro de la funcion sumaPorValor la variable llega a cambiar a 30, al volver a main sigue en 20. Esto demuestra que al pasar por valor solo se envia una copia, por eso el original no se modifica.

<img width="1412" height="587" alt="image" src="https://github.com/user-attachments/assets/03f1632a-3d55-413f-86b7-12f2e1e29611" />

En esta captura se ve que al llamar la funcion y modificar el valor, el cambio se mantiene al regresar a main. Esto evidencia que al pasar por referencia si se modifica la variable original porque se trabaja directamente sobre ella.

<img width="1362" height="814" alt="image" src="https://github.com/user-attachments/assets/a438f9ce-2698-4745-b258-a23a11b23dab" />

Aqui se nota que dentro de la funcion el valor cambia a 30, pero al final en main vuelve a 20. Esto demuestra que si no se usa correctamente la direccion o el contenido del puntero, el cambio no se mantiene en la variable original.

<img width="1487" height="804" alt="image" src="https://github.com/user-attachments/assets/d25b3310-691f-43c4-91a8-a40f2deb43ab" />

Esta captura muestra como en cada llamada el valor no vuelve a cero, sino que va aumentando de 1 en 1. Esto demuestra que las variables estaticas recuerdan su ultimo valor entre llamadas a la funcion.

<img width="1686" height="804" alt="image" src="https://github.com/user-attachments/assets/d625119c-509e-47a3-80da-3a278ac47b49" />

<img width="1875" height="716" alt="image" src="https://github.com/user-attachments/assets/1be3c300-4b1f-4f79-90e6-0085c7e31a43" />


##### Explica con tus propias palabras el comportamiento de contador_estatico. ¿Por qué “recuerda” su valor entre llamadas a la función ejecutarContador? ¿En qué se diferencia de una variable local normal?

el contador estatico es una variable que se crea solo una vez y no se borra cada vez que termina la funcion por eso siempre recuerda el ultimo valor que tenia cuando se vuelve a llamar a la funcion la diferencia con una variable local normal es que la local se borra y se vuelve a crear desde cero en cada llamada mientras que la estatica conserva su valor anterior
























# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

#### Ciclo fetch-decode-execute

El proposito de esta actividad es entender como funciona el ciclo fetch-decode-execute. ¿Que es el feetch?¿Que es el decode?¿Que es execute?

``` asm
@1
D=A
@2
D=D+A
@16
M=D
@END
(END)
0;JMP
```

##### Experiencia con CPU hack y su relacion con fetch-decode-execute

En la experimentacion de este codigo mediante la CPU hack, pude notar como la computadora realiza el proceso de buscar una instruccion, algo importante a resaltar es que las variables modificables de este sistema son A y D, mediante estas se hacen diferentes operaciones. La variable A es la mas importante, podemos ingresarle un valor por medio de un @1, u otro numero cualquiera, la decodificacion del codigo, a pesar de que lo vemos como un codigo facil de comprender, la maquina interpreta cada instruccion como ceros y unos y las ejecuta dandole valores a A o D y avanzando al siguiente numero, el cual  indica cual va a ser la siguiente instruccion a ejecutar.

###### fetch
La CPU busca las instrucciones por medio de el numero de la izquierda, analizando el digito mayor, es decir, el de a la izquierda del todo

###### decode

La computadora analiza la informacion o el contenido de la instruccion, y lo decodifica en ceros y unos

###### execute

La computadora ejecuta las instrucciones, realizando diferentes acciones según la instruccion, como saltar a una etiqueta, almacenar un dato en A o D, etc.

##### Etiqueas

Son una parte bastante importante, pues permite guardar la ubicacion de una instruccion dentro de la memoria, permitiendo asi realizar ciclos, volver a ejecutar una instruccion, y ayuda a mejorar la legibilidad y el mantenimiento de este tipo de codigos

#### Experiencia con el experimento de clase

Me di cuenta de algunas cosas que no me habian quedado claras, pensaba que M era otra variable, pero me di cuenta que era una referencia a la memoria RAM, si se quería decir que el resultado de la suma se guardara en 20, primero se debia poner @20 y despues M=D, pues si no haciamos esto, la suma se hubiera guardado en la memoria con el ultimo numero con el que quedo A

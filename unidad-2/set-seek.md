# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

El codigo es bastante sencillo, pienso que funciona guardando en el registro A el punto en pantalla 16384, la memoria de la pantalla define si un pixel esta encendido o apagado, y como le ponemos un 1, se apaga





<img width="1917" height="680" alt="image" src="https://github.com/user-attachments/assets/c7cde6dc-10d6-46aa-bbf5-d9ab9191af06" />



### Actividad 02



Ahora, si queremos hacer una linea en vez de un punto hay que cambiar un poco el codigo, asignando M: -1, haciendo que los primeros 16 bits de la pantalla se apaguen




<img width="1893" height="691" alt="image" src="https://github.com/user-attachments/assets/dc846584-e603-4ab3-95dc-3f98d5857f19" />





Tambien podemos interpretar la relacion entre el lenguaje ensamblador y lenguajes mas basicos como c++



<img width="1573" height="354" alt="image" src="https://github.com/user-attachments/assets/625a0611-23e6-45ef-93a7-ee042f0009e8" />




### Actividad 03

Ahora esta linea la vamos a mover con las teclas D y I, para esto hemos escrito el siguiente codigo

```asm

@SCREEN
M=-1
@CONTADOR
M=0

(LEER)

@KBD
D=M
@100
D=D-A
@DERECHA
D;JEQ


@KBD
D=M
@105
D=D-A
@IZQUIERDA
D;JEQ

@LEER
0;JMP

(DERECHA)
@CONTADOR
D=M
@SCREEN
A=D+A
M=0


@CONTADOR
M=M+1
D=M
@SCREEN
A=D+A

M=-1
@LEER
0;JMP

(IZQUIERDA)
@CONTADOR 
D=M
@SCREEN
A=D+A
M=0

@CONTADOR
M=M-1
D=M
@SCREEN
A=D+A

M=-1

@LEER
0;JMP
```
Antes de probar el programa, mi hipotesis es que teniendo en cuenta que el codigo  tiene varias lineas con saltos a la etiqueta leer, creo que la computadora va a estar en un bucle, leyendo constantemente las entradas del teclado y haciendo que se mueva a la derecha o a la izquierda.

Este programa permite mover los 16 pixeles hacia la derecha o la izquierda en la memoria de pantalla del computador Hack, Cuando el programa inicia, se enciende el primer píxel y se entra en un bucle que se repite constantemente, verificando si se ha presionado alguna tecla y no usa estructuras de alto nivel, todo se maneja mediante saltos condicionales y acceso directo a direcciones de memoria.



### Actividad 04

```asm

// Adds1+...+100.
 @i // i refers to some memory location.
 M=1 // i=1
 @sum // sum refers to some memory location.
 M=0 // sum=0
 (LOOP)
 @i
 D=M // D=i
 @100
 D=D-A // D=i-100
 @END
 D;JGT // If(i-100)>0 gotoEND
 @i
 D=M // D=i
 @sum
 M=D+M // sum=sum+i
 @i
 M=M+1 // i=i+1
 @LOOP
 0;JMP // GotoLOOP
 (END)
 @END
 0;JMP // Infinite loop
```

Tanto el programa que usa for como el que usa while realizan exactamente la misma operación, sumar los números del 1 al 100 e ir acumulando el resultado en una variable. La única diferencia está en la forma en que se estructura el código al traducir a ensamblador, no existe una instrucción especial para for o while, así que ambos deben implementarse usando saltos, etiquetas o comparaciones pero de resto es igual, en ambos casos se inicializan las variables, se comparan, etc.

### Actividad 05

#### Codigo 1
```asm
@10
D=A
@16
M=D
@16
D=A
@17
M=D
@20
D=A
@17
A=M
M=D
```
#### Codigo 2

```asm
@10
D=A
@16
M=D
@5
D=A
@17
M=D
@16
D=A
@18
M=D
@18
A=M
D=M
@17
M=D
```

En ambos programas se usa un termino recientemente visto en clase que son los punteros,  En el primer programa se asigna la dirección de a a p y luego se cambia el valor apuntado por p a 20 lo cual modifica directamente el valor de a, por otro lado en el segundo programa veo que se realiza algo mas o menos parecido, pero al reves, se copia el valor apuntado por p dentro de b.

En el lenguaje ensamblador como tal no existen los punteros, si no que hay direcciones de memoria manipuladas directamente.











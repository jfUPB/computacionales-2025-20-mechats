# Unidad 2


## 🛠 Fase: Apply

#### Actividad 06

```asm
@1
D=A
@16
M=D
@2
D=A
@17
M=D
@3
D=A
@18
M=D
@4
D=A
@19
M=D
@5
D=A
@20
M=D
@6
D=A
@21
M=D
@7
D=A
@22
M=D
@8
D=A
@23
M=D
@9
D=A
@24
M=D
@10
D=A
@25
M=D

@0
D=A
@26
M=D
@27
M=D

(LOOP)
@27
D=M
@10
D=D-A
@END
D;JGE

@27
D=M
@16
A=D+A
D=M

@26
M=D+M

@27
M=M+1

@LOOP
0;JMP

(END)
@END
0;JMP



```

<img width="1728" height="763" alt="image" src="https://github.com/user-attachments/assets/21d8a884-a6ba-4b7e-8a52-13e7633cb6bb" />








##### Construcción paso a paso del codigo

```asm
@1
D=A
@16
M=D
@2
D=A
@17
M=D
@3
D=A
@18
M=D

```
Aqui estoy guardando manualmente los valores del arreglo arr[] = {1, 2, 3} en las posiciones de memoria 16  17 y 18.

```asm
@0
D=A
@26
M=D   
@27
M=D   
```
Estoy creando dos variables: sum en la RAM[26] y j en RAM[27] Después de ejecutar, revisé que RAM[26] = 0 y  RAM[27] = 0, Asi supe que estaban bien inicializadas


```asm
@27
D=M
@10
D=D-A
@END
D;JGE
```
Aqui estaba  verificando si j es menor que 10. Si no lo es, se salta a (END), Corrí el programa y observé si el salto a (END) ocurre cuando j = 10. Para eso cambié manualmente RAM[27] a 10 y verifiqué que saltara a la etiqueta (END).

```asm
@27
D=M
@16
A=D+A
D=M
```
Aqui estaba accediendo al elemento arr[j], sumando la base del arreglo (16) con el valor de j, lo probe poniendo j = 2 (RAM[27] = 2), y verifiqué que D cargue el valor de RAM[18], que es 3.

#### Como paso final

para el final de la construccion del programa esperaba que al final del ciclo, sum  contubiera la suma de todos los elementos de arr[0] a arr[9]
( 1+2+3+...+10 = 55) y su observamos los resultados del programa ejecutado

<img width="1545" height="627" alt="image" src="https://github.com/user-attachments/assets/a13dbd72-d7bb-4760-8a2d-8cf2c613ee91" />













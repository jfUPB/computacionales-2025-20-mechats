# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**


###¿Que es el encapsulamiento para mi?

Si mal no estoy, es una manera de hacer que el codigo no sea accesible para todo el mundo, es como una forma de protegerlo. Como tal no me ha servido en ningun ejemplo practico, pero si se que es muy util en aplicaciones que piden contraseñas, porque la contraseña queda guardada en el programa pero no se puede ver en otras clases

###¿Que es la herencia?

La herencia es una forma de copiar los atributos y metodos de una clase para ponerlos en otra, existen varios tipos de herencia, hay uno en el que no se pueden modificar los metodos ni los atributos desde la clase que hereda, otra que si se pueden modificar.

La herencia es muy util a la hora de resumir codigo, y no solo eso, si no de simplificar el proceso de codificacion a la hora de hacer que una clase implemente varios metodos diferentes, por ejemplo tenemos la clase avión o medio de transporte aereo, esta cuenta con metodos como despegar, volar, aterrizar. Ahora tenemos otras clases diferentes (helicoptero, avioneta, globo aereostatico) lo logico seria que estas subclases heredaran los metodos de la clase medio de transporte aereo

###¿Que es el polimorfismo?

La verdad no tengo el concepto claro, a mi el polimorfismo me suena a un codigo que puede ser independiente por si solo y se puede ensamblar en otra parte y ademas es modificable, por ejemplo, tenemos un programa que administra un lavadero de carros, pasa el timepo y el lavadero ahora tiene una nueva sucursal. El codigo deberia ser posible modificarlo para que se le añadan nuevas clases o metodos en funcion a la nueva sede

### Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es.

Pienso que aqui hay un encapsulamiento
```csharp
  protected set { nombre = value; }
```
se esta protegiendo el private string  nombre, aunque no tengo muy claro para que sirve pienso que puede funcionar para que el nombre nos ea modificable en otra parte del codigo

### ¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?

Se evita que las clases hijas accedan directamente a nombre, y usando 

```csharp
 this.Nombre = nombre;
```

se hace que Nombre, que esta publico, adquiera ell valor de nombre que esta protegido por un get set (suposicion)

### ¿Cómo se evidencia la herencia en la clase Circulo?





## 2.  **La pregunta inicial**

## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación

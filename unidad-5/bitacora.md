# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**


#### ¿Que es el encapsulamiento para mi?

Si mal no estoy, es una manera de hacer que el codigo no sea accesible para todo el mundo, es como una forma de protegerlo. Como tal no me ha servido en ningun ejemplo practico, pero si se que es muy util en aplicaciones que piden contraseñas, porque la contraseña queda guardada en el programa pero no se puede ver en otras clases

#### ¿Que es la herencia?

La herencia es una forma de copiar los atributos y metodos de una clase para ponerlos en otra, existen varios tipos de herencia, hay uno en el que no se pueden modificar los metodos ni los atributos desde la clase que hereda, otra que si se pueden modificar.

La herencia es muy util a la hora de resumir codigo, y no solo eso, si no de simplificar el proceso de codificacion a la hora de hacer que una clase implemente varios metodos diferentes, por ejemplo tenemos la clase avión o medio de transporte aereo, esta cuenta con metodos como despegar, volar, aterrizar. Ahora tenemos otras clases diferentes (helicoptero, avioneta, globo aereostatico) lo logico seria que estas subclases heredaran los metodos de la clase medio de transporte aereo

#### ¿Que es el polimorfismo?

La verdad no tengo el concepto claro, a mi el polimorfismo me suena a un codigo que puede ser independiente por si solo y se puede ensamblar en otra parte y ademas es modificable, por ejemplo, tenemos un programa que administra un lavadero de carros, pasa el timepo y el lavadero ahora tiene una nueva sucursal. El codigo deberia ser posible modificarlo para que se le añadan nuevas clases o metodos en funcion a la nueva sede

#### Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es.

Pienso que aqui hay un encapsulamiento
```csharp
  protected set { nombre = value; }
```
se esta protegiendo el private string  nombre, aunque no tengo muy claro para que sirve pienso que puede funcionar para que el nombre nos ea modificable en otra parte del codigo

#### ¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?

Se evita que las clases hijas accedan directamente a nombre, y usando 

```csharp
 this.Nombre = nombre;
```

se hace que Nombre, que esta publico, adquiera ell valor de nombre que esta protegido por un get set (suposicion)

#### ¿Cómo se evidencia la herencia en la clase Circulo?

no lo tengo muy claro

#### Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?

el nombre

#### Observa el bucle foreach. La variable fig es de tipo Figura, pero a veces contiene un Circulo y otras un Rectangulo. Cuando se llama a fig.Dibujar(), el programa ejecuta la versión correcta. En tu opinión, ¿Cómo crees que funciona esto “por debajo”? No necesitas saber la respuesta correcta, solo quiero que intentes razonar cómo podría ser.

En el foreach fig está declarado como Figura, pero  puede guardar un Circulo o un Rectangulo, no se muy bien como funcione pero siento que cuando llamo a fig.Dibujar(), mágicamente se ejecuta la versión correcta
Yo me lo imagino como si el objeto tuviera una especie de “etiqueta oculta” que dice qué tipo real es

#### Memoria y herencia: cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?

Si creo un Rectangulo, en memoria se deberían guardar todos los datos juntos: primero la parte que corresponde a Figura (el Nombre), y después lo que es exclusivo de Rectangulo (Base y Altura) Me lo imagino como un bloque de memoria dividido en secciones, la primera guarda nombre y la otra los datos especificos de la figura


#### El mecanismo del polimorfismo: pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.

creo que el programa mantiene una especie de tabla de métodos que dice: si es Círculo, usa esta función; si es Rectángulo, usa esta otra. Entonces cuando escribo fig.Dibujar() el compilador no decide en ese momento, sino que en ejecución el objeto consulta su tabla y escoge la función correcta

#### La barrera del encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase? ¿Es algo que se revisa cuando escribes el código, o es una protección que existe mientras el programa se ejecuta? ¿Por qué piensas eso?

pienso que la restricción de private la revisa principalmente el compilador, o sea, cuando escribo código y trato de acceder a algo privado, el compilador me bloquea y me diceesto no es permitido. Ya en la ejecución, seguramente el objeto sí tiene esos datos en memoria, pero el compilador se asegura de que yo nunca pueda escribir código que los toque directamente

#### Autoevaluacion y primeras preguntas

Me di cuenta que los conceptos que mas claros tengo o mejor dicho que menos peor tengo aprendidos son la herencia y el encapsulamiento, por otro lado el polimorfismo es un tema que la verdad no manejo completamente, siento que tengo una idea base pero no esta del todo desarrollada ni mucho menos certera







## 2.  ¿Como funciona el polimorfismo durante la compilación y durante la ejecución?

## 3.  **Registro de exploración:** 

### Hipotesis

Mi hipotesis se mantiene en que cuando un objeto llama una metodo o funcion, el metodo se aplica según el tipo de objeto gracias a una lista, sin embargo creo que esto pasa es durante la ejecución. Durante la compilación el compilador deberia tener una forma de generar por asi decirlo varios tipos de metodos para que cada uno se aplique a un objeto diferente. Siento que cada metodo se guardaria en un lugar de la memoria diferente, pero no estoy seguro sin el tiempo de ejecución sigue siendo asi.

### Experimento


> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación

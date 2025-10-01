# Bitácora de aprendizaje de la unidad 6


## Actividad 02

### Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?

El patrón observer sirve para que un objeto pueda avisarle a varios otros cuando algo cambia, sin necesidad de estar directamente conectado con ellos. El problema que resuelve es el acoplamiento fuerte, pues en lugar de que el Sujeto conozca todos los detalles de cada observador , simplemente dispara una notificación y cada Observador decide cómo reaccionar. Esto hace que el sistema sea más flexible y fácil de ampliar

### Diagrama de la relación entre Subject, Observer, ofApp y Particle



<img width="850" height="594" alt="image" src="https://github.com/user-attachments/assets/292ffb29-a17d-4d40-8f36-74064886d467" />



### Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.



<img width="1059" height="580" alt="image" src="https://github.com/user-attachments/assets/9ee2abeb-e4e9-4b8a-abe8-b5db9db4911d" />

## Actividad 03

### Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?

es separar la creación de objetos del código que los usa. Esto significa que ofApp no necesita saber cómo se construye un objeto ni qué configuración específica debe tener, solo pide el objeto y la fábrica se encarga de devolverlo ya configurado. El problema que resuelve es el acoplamiento fuerte: evita que el código cliente dependa de clases concretas y de toda la lógica de inicialización

### ¿Qué ventajas aporta el uso de ParticleFactory en ofApp::setup en comparación con instanciar y configurar las partículas directamente allí? Piensa en términos de organización del código (SRP - Single Responsibility Principle), legibilidad y facilidad para añadir nuevos tipos de partículas en el futuro.

el uso de particlefactory en ofapp setup trae varias ventajas primero permite que el codigo este mas ordenado y facil de leer ya que la logica de crear particulas no queda mezclada con la configuracion de la aplicacion segundo sigue el principio de responsabilidad unica porque cada clase se enfoca en lo que debe hacer ofapp organiza la aplicacion y particlefactory crea las particulas tercero facilita mucho cuando se quieren agregar nuevos tipos de particulas porque solo se modifica la fabrica sin tener que tocar otras partes del codigo esto hace que el mantenimiento sea mas facil y el programa sea mas escalable en el futuro

### Imagina que quieres añadir un nuevo tipo de partícula llamada "black_hole" que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la ParticleFactory existente. ¿Tendrías que modificar ofApp::setup? ¿Por qué sí o por qué no?
Para añadir la partícula "black_hole" tendría que:

pues, para eso yo creo que habria que hacer una serie de pasos:

1 ir a la clase ParticleFactory.

2 en el método createParticle, agregar un nuevo caso para "black_hole".

3 crear un objeto Particle con las propiedades: tamaño grande, color negro y velocidad muy lenta.

4 devolver esa partícula como resultado.

### El método createParticle en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de ParticleFactory y un método de instancia createParticle()?

las ventajas son que el método estático hace que sea muy fácil de usar, porque no hay que crear objetos adicionales, solo se llama directamente desde la clase, esto reduce la cantidad de código repetido y hace que la lógica de creación esté toda en un mismo punto, también mejora el rendimiento en cierta medida porque no hay que manejar instancias extra, y ayuda a que el código cliente sea más limpio y directo, otra ventaja es que, al ser centralizado, es fácil mantener o cambiar las reglas de creación sin ir a buscar en muchas partes del programa

las desventajas son que, al ser estático, la factory no se puede extender tan fácilmente, por ejemplo, no puedes hacer subclases de la factory para crear variaciones distintas de partículas, tampoco puedes aprovechar patrones más avanzados como inyección de dependencias porque no tienes una instancia configurable, además, se pierde flexibilidad si en el futuro quieres tener varias factories con configuraciones diferentes, por ejemplo, una factory que cree partículas rápidas y otra de partículas lentas, no sería tan fácil con métodos estáticos, finalmente, si el proyecto crece demasiado, la dependencia en un método estático puede hacer el código menos modular y más difícil de probar en unit tests

## Actividad 04

### Explica con tus propias palabras el propósito del patrón State. ¿Cuándo es útil aplicarlo?

el patrón state sirve para que un objeto pueda cambiar su comportamiento dependiendo de su estado interno sin necesidad de llenar el código de condicionales gigantes lo que se hace es encapsular cada comportamiento en una clase separada y la clase principal delega la lógica al estado actual es muy útil cuando un objeto puede tener múltiples comportamientos y estos dependen de su estado por ejemplo una partícula que puede moverse normalmente ser atraída al mouse repelerse o detenerse


### Dibuja un diagrama de estados simple para la clase Particle. Muestra los diferentes estados (Normal, Attract, Repel, Stop) como nodos y las transiciones entre ellos como flechas etiquetadas con el evento que las causa (p. ej., la tecla presionada: ‘n’, ‘a’, ‘r’, ‘s’).


<img width="787" height="582" alt="image" src="https://github.com/user-attachments/assets/ec5118cc-ef98-4fbd-8d9b-d4012e28903a" />










### Describe las ventajas de usar el patrón State en Particle en lugar de tener un miembro std::string estadoActual y usar un gran if/else if/else o switch dentro de Particle::update() para cambiar el comportamiento. Piensa en cohesión, extensibilidad (añadir nuevos estados) y el Principio Abierto/Cerrado (Open/Closed Principle).

primero mejora la cohesión porque cada clase de estado tiene su lógica bien organizada y no se mezcla con las demás segundo hace que el código sea más fácil de mantener y extender porque si quiero agregar un nuevo estado solo creo una nueva clase sin tocar el código existente esto sigue el principio abierto cerrado tercero el código de particle queda más limpio porque no necesita saber qué hacer en cada estado solo delega la responsabilidad al objeto de estado actual

### Qué responsabilidad tienen los métodos onEnter y onExit en el patrón State? Proporciona un ejemplo de por qué podrían ser útiles (incluso si no se usan mucho en todos los estados de este caso de estudio). Por ejemplo, ¿Qué podrías hacer en onEnter para AttractState o en onExit para StopState?

los métodos onenter y onexit sirven para ejecutar acciones específicas al entrar o salir de un estado por ejemplo en este caso normalstate usa onenter para asignar una nueva velocidad aleatoria a la partícula podrían ser útiles en otros casos como en attractstate para inicializar una fuerza especial al entrar o en stopstate para reiniciar la velocidad a cero al salir así se asegura que cada transición se maneje correctamente sin dejar restos de un estado anterior










### ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.

 En primer lugar, reduce el acoplamiento entre las clases, ya que ofApp no necesita conocer los detalles internos de cada partícula ni recorrerlas una por una para cambiar su comportamiento, simplemente lanza una notificación y cada partícula decide qué hacer con ella. Esto también mejora la extensibilidad, porque si en el futuro quiero agregar nuevos tipos de objetos que reaccionen a los eventos, puedo hacerlo sin tener que modificar el código de ofApp. Además, el código resulta más limpio y fácil de mantener, pues cada clase se enfoca en su propia responsabilidad. Finalmente, el patrón facilita la escalabilidad, ya que un solo evento enviado desde el sujeto puede llegar automáticamente a todas las partículas, sin necesidad de escribir más lógica en el controlador principal.


